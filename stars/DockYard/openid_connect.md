---
project: openid_connect
stars: 95
description: Client library for consuming and working with OpenID Connect Providers
url: https://github.com/DockYard/openid_connect
---

OpenIDConnect
=============

Client library for consuming and working with OpenID Connect Providers

**OpenIDConnect is built and maintained by DockYard, contact us for expert Elixir and Phoenix consulting**.

Installation
------------

Available in Hex, the package can be installed as:

Add `openid_connect` to your list of dependencies in `mix.exs`:

def deps do
  \[{:openid\_connect, "~> 1.0.1"}\]
end

Getting Started
---------------

### Configuration

This library works with any OpenID Connect provider through a standard configuration map. You'll need to create a configuration map for each provider you want to work with:

google\_config \= %{
  discovery\_document\_uri: "https://accounts.google.com/.well-known/openid-configuration",
  client\_id: "CLIENT\_ID",
  client\_secret: "CLIENT\_SECRET",
  redirect\_uri: "https://example.com/session",
  response\_type: "code",
  scope: "openid email profile"
}

The configuration requires:

-   `discovery_document_uri`: URL to the OpenID Connect Discovery Document
-   `client_id`: OAuth 2.0 Client Identifier provided by your identity provider
-   `client_secret`: OAuth 2.0 Client Secret provided by your identity provider
-   `response_type`: OAuth 2.0 Response Type (typically "code" for authorization code flow)
-   `scope`: Space-separated list of scopes (must include "openid")

Additional optional configuration:

-   `leeway`: Number of seconds to allow for clock skew when verifying token expiration (default: 30)

Most major OAuth2 providers support OpenID Connect, including:

-   Google
-   Microsoft Azure AD
-   Auth0
-   Okta
-   AWS Cognito
-   Keycloak
-   OneLogin
-   Many others

For a full list, see major OpenID Connect providers.

### Usage

Implementing OpenID Connect authentication in your app involves these steps:

1.  Generate an authorization URI and redirect the user to it
2.  Handle the callback from the provider after successful authentication
3.  Exchange the authorization code for tokens
4.  Verify the ID token
5.  Use the claims to establish a user session

#### 1\. Generate the Authorization URI

Create a URL that will redirect the user to the provider's login page:

{:ok, uri} \= OpenIDConnect.authorization\_uri(
  google\_config,
  "https://example.com/auth/callback",
  %{state: state\_token}
)

You should:

-   Generate a secure state token for CSRF protection
-   Store this state token in your session
-   Include the state token in the authorization URI

#### 2\. Handle the Callback from the Provider

After the user logs in, the provider redirects back to your `redirect_uri` with an authorization code and the state token you provided:

\# In your callback controller/handler
def callback(conn, params) do
  \# First verify that the state parameter matches the one we stored
  stored\_state \= get\_session(conn, :state\_token)
  received\_state \= params\["state"\]
  
  if Plug.Crypto.secure\_compare(stored\_state, received\_state) do
    \# State is valid, proceed with code exchange
    handle\_valid\_callback(conn, params)
  else
    \# State token doesn't match, reject the request
    conn
    |> put\_status(401)
    |> render("error.html", error: "Invalid state parameter")
  end
end

#### 3\. Exchange the Authorization Code for Tokens

Exchange the code for ID and access tokens:

{:ok, tokens} \= OpenIDConnect.fetch\_tokens(google\_config, %{
  code: params\["code"\],
  redirect\_uri: "https://example.com/auth/callback"  \# Must match original redirect\_uri
})

\# tokens will contain:
\# %{
\#   "access\_token" => "ya29.a0AfB\_...",
\#   "id\_token" => "eyJhbGciOiJSUzI1...",
\#   "expires\_in" => 3599,
\#   "token\_type" => "Bearer",
\#   "refresh\_token" => "1//03s..." (if requested)
\# }

#### 4\. Verify the ID Token

The ID token is a JWT containing claims about the user. Always verify it before trusting its contents:

{:ok, claims} \= OpenIDConnect.verify(google\_config, tokens\["id\_token"\])

\# claims will contain user information like:
\# %{
\#   "sub" => "10865933565....",  # Unique user identifier
\#   "email" => "user@example.com",
\#   "email\_verified" => true,
\#   "name" => "User Name",
\#   "picture" => "https://...",
\#   "given\_name" => "User",
\#   "family\_name" => "Name",
\#   "locale" => "en",
\#   "iat" => 1585662674,  # Issued at timestamp
\#   "exp" => 1585666274,  # Expiration timestamp
\#   "aud" => "YOUR\_CLIENT\_ID",
\#   "iss" => "https://accounts.google.com"
\# }

#### 5\. Use the Claims to Establish a User Session

Use the verified claims to identify your user and establish a session:

\# The "sub" claim is the unique identifier for the user
user\_id \= claims\["sub"\]

\# Find or create a user in your system
user \= find\_or\_create\_user(user\_id, claims)

\# Establish a session for this user
conn
|> put\_session(:user\_id, user.id)
|> redirect(to: "/dashboard")

#### Optional: Fetch Additional User Information

Some providers allow you to fetch additional user information using the access token:

{:ok, userinfo} \= OpenIDConnect.fetch\_userinfo(google\_config, tokens\["access\_token"\])

#### Ending a User Session

Some providers support log out via an end session endpoint:

{:ok, logout\_uri} \= OpenIDConnect.end\_session\_uri(
  google\_config,
  %{id\_token\_hint: id\_token, post\_logout\_redirect\_uri: "https://example.com/logout/callback"}
)

\# Redirect the user to the logout\_uri
redirect(conn, external: logout\_uri)

**Key Security Considerations:**

1.  Always validate the state token
2.  Store secrets (client ID, client secret) in environment variables
3.  Verify the ID token before trusting its contents
4.  Use HTTPS for all redirect URIs
5.  Consider token storage carefully - sessions are usually appropriate
6.  Clear tokens when logging out

Authors
-------

-   Brian Cardarella

We are very thankful for the many contributors

Versioning
----------

This library follows Semantic Versioning

Looking for help with your Elixir project?
------------------------------------------

At DockYard we are ready to help you build your next Elixir project. We have a unique expertise in Elixir and Phoenix development that is unmatched. Get in touch!

At DockYard we love Elixir! You can read our Elixir blog posts or come visit us at The Boston Elixir Meetup that we organize.

Want to help?
-------------

Please do! We are always looking to improve this library. Please see our Contribution Guidelines on how to properly submit issues and pull requests.

Sponsors
--------

In addition to our contributors, this library receives support and maintenance from TV Labs

Legal
-----

DockYard, Inc. © 2018

@dockyard

Licensed under the MIT license
