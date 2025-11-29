---
project: gringotts
stars: 496
description: A complete payment library for Elixir and Phoenix Framework
url: https://github.com/aviabird/gringotts
---

Gringotts is a payment processing library in Elixir integrating various payment gateways, drawing motivation from Shopify's `activemerchant` gem and `commerce_billing`. Checkout the demo here.

Gringotts offers a **simple and unified API** to access dozens of different payment gateways with very different APIs, response schemas, documentation and jargon.

The project started out **as a fork of `commerce_billing`** and the notable differences are:

1.  No `GenServer` process to act as a "payment worker".
2.  Consistent docs and good amount of tests.
3.  Support many more payment gateways.

Installation
------------

### From `hex.pm`

Add `gringotts` to the list of dependencies of your application.

\# your mix.exs

def deps do
  \[
    {:gringotts, "~> 1.1"},
    \# ex\_money provides an excellent Money library, and integrates
    \# out-of-the-box with Gringotts
    {:ex\_money, ">= 2.6.0"}
  \]
end

Usage
-----

This simple example demonstrates how a `purchase` can be made using a sample credit card using the MONEI gateway.

One must "register" their account with `gringotts` ie, put all the authentication details in the Application config. Usually via `config/config.exs`

\# config/config.exs

config :gringotts, Gringotts.Gateways.Monei,
    userId: "your\_secret\_user\_id",
    password: "your\_secret\_password",
    entityId: "your\_secret\_channel\_id"

Copy and paste this code in a module or an `IEx` session, or use this handy `.iex.exs` for all the bindings.

alias Gringotts.Gateways.Monei
alias Gringotts.CreditCard

\# a fake sample card that will work now because the Gateway is by default
\# in "test" mode.

card \= %CreditCard{
  first\_name: "Harry",
  last\_name: "Potter",
  number: "4200000000000000",
  year: 2099, month: 12,
  verification\_code:  "123",
  brand: "VISA"
}

\# a sum of $42
amount \= Money.new(42, :USD)

case Gringotts.purchase(Monei, amount, card) do
  {:ok,    %{id: id}} \->
    IO.puts("Payment authorized, reference token: '#{id}'")

  {:error, %{status\_code: error, raw: raw\_response}} \->
    IO.puts("Error: #{error}\\nRaw:\\n#{raw\_response}")
end

On the `Gringotts.Money` protocol and money representation
----------------------------------------------------------

All financial applications must take proper care when representing money in their system. Using simple `float`ing values might lead to losses in the real world due to various reasons.

Most payment gateways are strict about the formatting of the `amount` in the request, hence we cannot render arbitrary floating amounts like `$4.99999`. Moreover, such amounts might mean something to your application but they don't have any value in the real world (since you can't charge someone for a fraction of a US cent).

Your application **must round** such amounts before invoking Gringotts **and manage any remainders sensibly** yourself.

> Gringotts may perform rounding using the `half-even` strategy, but it will discard remainders if any.

### Supported "Money" libraries

Gringotts does not ship with any library to work with monies. You are free to choose any monie library you wish, as long as they implement the `Gringotts.Money` for their type!

That said, we recommend \[`ex_money`\]\[ex\_money\] (above `v2.6.0`) to represent monies. You just have to add it in your `deps()`.

Supported Gateways
------------------

Gateway

PCI compliance

`purchase`

`authorize`

`capture`

`void`

`refund`

(card) `store`

(card) `unstore`

Authorize.Net

mandatory

✅

✅

✅

✅

✅

✅

✅

CAMS

mandatory

✅

✅

✅

✅

✅

❌

❌

MONEI

mandatory

✅

✅

✅

✅

✅

✅

❌

PAYMILL

optional

✅

✅

✅

✅

✅

❌

❌

Stripe

optional

✅

✅

✅

✅

✅

✅

✅

TREXLE

mandatory

✅

✅

✅

❌

✅

✅

❌

Road Map
--------

Apart from supporting more and more gateways, we also keep a somewhat detailed plan for the future on our wiki.

FAQ
---

#### 1\. What's with the name? "Gringotts"?

Gringotts has a nice ring to it. Also this.

License
-------

MIT
