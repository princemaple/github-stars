---
project: stripity-stripe
stars: 1061
description: An Elixir Library for Stripe
url: https://github.com/beam-community/stripity-stripe
---

Stripe for Elixir
=================

An Elixir library for working with Stripe.

2.x.x status
------------

Which version should I use?
===========================

Below is a list of which Stripe API version recent releases of Stripe Elixir. It only indicates the API version being called, not necessarily its compatibility. See the Stripe API Upgrades page for more details.

Starting with stripity\_stripe version 2.5.0, you can specify the Stripe API Version to use for a specific request by including the `:api_version` option. Note that while this will use a specific Stripe API Version to make the request, the library will still expect a response matching its corresponding default Stripe API Version. See the Shared Options documentation for more details.

`:stripity_stripe`

Stripe API Version

`2.0.x`

`2018-02-28`

`2.1.0 - 2.2.0`

`2018-05-21`

`2.2.2`

`2018-08-23`

`2.2.3 - 2.3.0`

`2018-11-08`

`2.4.0 - 2.7.0`

`2019-05-16`

`master`

`2019-10-17`

Documentation
=============

-   Latest HexDocs

Installation
------------

Install the dependency by version:

{:stripity\_stripe, "~> 2.0"}

Or by commit reference:

{:stripity\_stripe, git: "https://github.com/beam-community/stripity\_stripe", ref: "017d7ecdb5aeadccc03986c02396791079178ba2"}

Next, add to your applications:

_Not necessary if using elixir >= 1.4_

defp application do
  \[applications: \[:stripity\_stripe\]\]
end

Configuration
-------------

To make API calls, it is necessary to configure your Stripe secret key.

import Config

config :stripity\_stripe, api\_key: System.get\_env("STRIPE\_SECRET")
\# OR
config :stripity\_stripe, api\_key: "YOUR SECRET KEY"

It's possible to use a function or a tuple to resolve the secret:

config :stripity\_stripe, api\_key: {MyApp.Secrets, :stripe\_secret, \[\]}
\# OR
config :stripity\_stripe, api\_key: fn \-> System.get\_env("STRIPE\_SECRET") end

Moreover, if you are using Poison instead of Jason, you can configure the library to use Poison like so:

config :stripity\_stripe, json\_library: Poison

### Timeout

To set timeouts, pass opts for the http client. The default one is Hackney.

config :stripity\_stripe, hackney\_opts: \[{:connect\_timeout, 1000}, {:recv\_timeout, 5000}\]

### Request Retries

To set retries, you can pass the number of attempts and range of backoff (time between attempting the request again) in milliseconds.

config :stripity\_stripe, :retries, \[max\_attempts: 3, base\_backoff: 500, max\_backoff: 2\_000\]

Examples
--------

Stripe supports a token based, and intent based approach for processing payments. The token based approach is simpler, but it is not supported in Europe. The intents API is the way forward, and should be used for new development.

### Intents

Create a new `SetupIntent` object in Stripe. The created intent ID will be passed to the frontend to use with Stripe elements so the end user can enter their payment details. SetupIntents are ephemeral. It is best to create a new one each time the user reaches your payment page.

{:ok, setup\_intent} \= Stripe.SetupIntent.create(%{})

\# Return the ID to your frontend, and pass it to the confirmCardSetup method from Stripe elements
{:ok, setup\_intent.id}

On the frontend, use the setup intent ID you created in conjunction with Stripe elements `confirmCardSetup` method.

stripe.confirmCardSetup(setupIntentId, {
  payment\_method: {
    ...
  }
})
.then(result \=> {
  const setupIntentId \= result.setupIntent.id
  const paymentMethodId \= result.setupIntent.payment\_method

  // send the paymentMethodId and optionally (if needed) the setupIntentId
})

With the new payment method ID, you can associate the payment method with a Stripe customer.

Get an existing customer.

{:ok, stripe\_customer} \= Stripe.Customer.retrieve(stripe\_customer\_id)

Or create a new one.

new\_customer \= %{
  email: email,
}

{:ok, stripe\_customer} \= Stripe.Customer.create(new\_customer)

Attach the payment method to the customer.

{:ok, \_result} \= Stripe.PaymentMethod.attach(%{customer: stripe\_customer.id, payment\_method: payment\_method\_id})

Now you can charge the customer using a `PaymentIntent` from Stripe. Since we used a setup intent initially, the payment intent will be authorized to make payments off session, for example to charge for a recurring subscription.

{:ok, charge} \= Stripe.PaymentIntent.create(%{
  amount: cents\_int,
  currency: "USD",
  customer: stripe\_customer.id,
  payment\_method: payment\_method\_id,
  off\_session: true,
  confirm: true
})

Note: Object Expansion
----------------------

Some Stripe API endpoints support returning related objects via the object expansion query parameter. To take advantage of this feature, stripity\_stripe accepts a list of strings to be passed into `opts` under the `:expand` key indicating which objects should be expanded.

For example, calling `Charge.retrieve("ch_123")` would return a charge without expanding any objects.

%Charge{
  id: "ch\_123",
  balance\_transaction: "txn\_123",
  ...
}

However if we now include an expansion on the `balance_transaction` field using

Charge.retrieve("ch\_123", expand: \["balance\_transaction"\])

We will get the full object back as well.

%Charge{
  id: "ch\_123",
  balance\_transaction: %BalanceTransaction{
    id: "txn\_123",
    fee: 125,
    ...
  },
  ...
}

For details on which objects can be expanded check out the stripe object expansion docs.

Testing
=======

Starting stripe-mock
--------------------

To run the tests you'll need to install `stripe-mock`. It is a mock HTTP server that responds like the real Stripe API. It's powered by the Stripe OpenAPI specification, which is generated from within Stripe's API.

The stripe-mock instructions have more details, but if you have docker installed already you can quickly and easily start an instance to test against:

docker run --rm -it -p 12111-12112:12111-12112 stripe/stripe-mock:latest

Running the tests
-----------------

By default, `mix test` will start `stripe-mock` by finding and invoking the `stripe-mock` executable. If you would prefer to start it yourself, do so and add an env var `SKIP_STRIPE_MOCK_RUN` to skip starting stripe-mock. Any value will do. Example:

SKIP\_STRIPE\_MOCK\_RUN=1 mix test

To configure your test environment to use the local stripe-mock server, you may need to set the `api_base_url` field in your config:

```
config :stripity_stripe,
  api_key: "sk_test_thisisaboguskey",
  api_base_url: "http://localhost:12111"
```

Documentation for 1.x.x
=======================

Click to expand

Stripe API
----------

Works with API version 2015-10-16

Installation
------------

Install the dependency:

{:stripity\_stripe, "~> 1.6"}

Next, add to your applications:

defp application do
  \[applications: \[:stripity\_stripe\]\]
end

Configuration
-------------

To make API calls, it is necessary to configure your Stripe secret key (and optional platform client id if you are using Stripe Connect):

import Config

config :stripity\_stripe, secret\_key: "YOUR SECRET KEY"
config :stripity\_stripe, platform\_client\_id: "YOUR CONNECT PLATFORM CLIENT ID"

Testing
-------

If you start contributing and you want to run mix test, first you need to export STRIPE\_SECRET\_KEY environment variable in the same shell as the one you will be running mix test in. All tests have the @tag disabled: false and the test runner is configured to ignore disabled: true. This helps to turn tests on/off when working in them. Most of the tests depends on the order of execution (test random seed = 0) to minimize runtime. I've tried having each tests isolated but this made it take ~10 times longer.

```
export STRIPE_SECRET_KEY="yourkey"
mix test
```

The API
-------

I've tried to make the API somewhat comprehensive and intuitive. If you'd like to see things in detail be sure to have a look at the tests - they show (generally) the way the API goes together.

In general, if Stripe requires some information for a given API call, you'll find that as part of the arity of the given function. For instance if you want to delete a Customer, you'll find that you _must_ pass the id along:

{:ok, result} \= Stripe.Customers.delete "some\_id"

For optional arguments, you can send in a Keyword list that will get translated to parameters. So if you want to update a Subscription, for instance, you must send in the `customer_id` and `subscription_id` with the list of changes:

\# Change customer to the Premium subscription
{:ok, result} \= Stripe.Customers.change\_subscription "customer\_id", "sub\_id", \[plan: "premium"\]

Metadata (metadata:) key is supported on most object type and allow the storage of extra information on the stripe platform. See test for an example.

That's the rule of thumb with this library. If there are any errors with your call, they will bubble up to you in the `{:error, message}` match.

\# Example of paging through events
{:ok, events} \= Stripe.Events.list(key, "", 100) \# second arg is a marker for paging

case events\[:has\_more\] do
  true \->
    \# retrieve marker
    last \= List.last( events\[:data\] )
    case Stripe.Events.list key, last\["id"\], 100 do
      {:ok, events} \-> events\[:data\]
      \# ...
    end
  false \-> events\[:data\]
end

Connect
=======

Stripe Connect allows you to provide your customers with an easy onboarding to their own Stripe account. This is useful when you run an e-commerce as a service platform. Each merchant can transact using their own account using your platform. Then your platform uses Stripe's API with their own API key obtained in the onboarding process.

First, you need to register your platform on Stripe Connect to obtain a `client_id`. In your account settings, there's a "Connect" tab, select it. Then fill the information to activate your connect platform settings. The select he `client_id` (notice there's one for dev and one for prod), stash this `client_id` in the config file under

config :stripity\_stripe, platform\_client\_id: "ac\_???"

or in an env var named `STRIPE_PLATFORM_CLIENT_ID`.

Then you send your users to sign up for the stripe account using a link.

Here's an example of a button to start the workflow: Connect with Stripe

You can generate this URL using:

url \= Stripe.Connect.generate\_button\_url csrf\_token

When the user gets back to your platform, the following url (`redirect_uri` form item on your "Connect" settings) will be used:

```
//yoursvr/your_endpoint?scope=read_write&code=AUTHORIZATION_CODE
```

or

```
//yoursvr/your_endpoint?error=access_denied&error_description=The%20user%20denied%20your%20request
```

Using the code request parameter, you make the following call:

{:ok, resp} \-\> Stripe.Connect.oauth\_token\_callback code
resp\[:access\_token\]

`resp` will look like this:

%{
  token\_type: "bearer",
  stripe\_publishable\_key: PUBLISHABLE\_KEY,
  scope: "read\_write",
  livemode: false,
  stripe\_user\_id: USER\_ID,
  refresh\_token: REFRESH\_TOKEN,
  access\_token: ACCESS\_TOKEN
}

You can then pass the `access_token` to the other API modules to act on their behalf.

See a demo using the Phoenix framework with the bare minimum to get this working.

Testing Connect
---------------

The tests are currently manual as they require a unique OAuth authorization code per test. You need to obtain this code manually using the stripe connect workflow (that your user would go through using the above url).

First, log in your account. Then go to the following url: https://dashboard.stripe.com/account/applications/settings

Create a connect standalone account. Grab your development `client_id`. Put it in your config file. Enter a redirect url to your endpoint. Capture the "code" request parameter. Pass it to `Stripe.Connect.oauth_token_callback` or `Stripe.Connect.get_token`.

Contributing
============

Feedback, feature requests, and fixes are welcomed and encouraged. Please make appropriate use of Issues and Pull Requests. All code should have accompanying tests.

License
=======

Please see LICENSE.md for licensing details.

History
=======

Statement from original author
------------------------------

Why another Stripe Library? Currently there are a number of them in the Elixir world that are, well just not "done" yet. I started to fork/help but soon it became clear to me that what I wanted was

-   an existing/better test story
-   an API that didn't just mimic a REST interaction
-   a library that was up to date with Elixir > 1.0 and would, you know, actually _compile_.
-   function calls that returned a standard `{:ok, result}` or `{:error, message}` response

As I began digging things up with these other libraries it became rather apparent that I was not only tweaking the API, but also ripping out a lot of the existing code... and that usually means I should probably do my own thing. So I did.
