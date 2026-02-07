---
project: cldr
stars: 470
description: Elixir implementation of CLDR/ICU
url: https://github.com/elixir-cldr/cldr
---

Getting Started with Cldr
=========================

> #### Change to :json\_library configuration {: .warning}
> 
> As of `ex_cldr` version 2.37.2 the configuration parameter `:json_library` does not attempt to read the configuration of either Phoenix or Ecto.

> #### Automatic configuration of :json\_library {: .info}
> 
> OTP 27 and Elixir 1.18 both include native JSON libraries. Therefore if running on either (or both) of these platforms, no `:json_library` configuration is required or recommended.

Introduction
------------

`ex_cldr` is an Elixir library for the Unicode Consortium's Common Locale Data Repository (CLDR). The intentions of CLDR, and this library, is to simplify the locale specific formatting and parsing of numbers, lists, currencies, calendars, units of measure and dates/times. As of August 16th 2024 and `ex_cldr` Version 2.40.1, `ex_cldr` is based upon CLDR version 45.0.

The first step is to define a module that will host the desired `ex_cldr` configuration and the functions that serve as the public API. This module is referred to in this documentation as a `backend` module. For example:

defmodule MyApp.Cldr do
  @moduledoc """
  Define a backend module that will host our
  Cldr configuration and public API.
  Most function calls in Cldr will be calls
  to functions on this module.
  """
  use Cldr,
    locales: \["en", "fr", "zh", "th"\],
    default\_locale: "en"

end

This strategy means that different configurations can be defined and it also means that one `ex_cldr` implementation won't interfere with implementations in another, potentially dependent, applications.

The functions you are mostly likely to use are:

-   `MyApp.Cldr.default_locale/0`
-   `MyApp.Cldr.put_locale/1`
-   `MyApp.Cldr.get_locale/0`
-   `MyApp.Cldr.known_locale_names/0`
-   `MyApp.Cldr.Locale.new/1`
-   `MyApp.Cldr.validate_locale/1`

Use Case
--------

Use this library if you need to:

-   Support multiple languages and locales in your application
    
-   Support formatting numbers, dates, times, date-times, units and lists in one language or many
    
-   Need to access the data maintained in the CLDR repository in a functional manner
    
-   Parse an Accept-Language HTTP header or a language tag
    

**It is highly likely that you will also want to install one or more of the dependent packages that provide localization and formatting for a particular data domain. See Additional Cldr Packages below**.

Elixir Version Requirements
---------------------------

-   ex\_cldr requires Elixir 1.12 or later.

Installation
------------

Add `ex_cldr` and the JSON library of your choice as a dependency to your `mix` project. If running on OTP 27 or later, this step is not required since `ex_cldr` will detect and use the built-in `:json` module.

defp deps do
  \[
    {:ex\_cldr, "~> 2.37"},
    \# Poison or any other compatible json library
    \# that implements \`encode!/1\` and \`decode!/1\`
    \# :jason is recommended
    {:jason, "~> 1.0"}
    \# {:poison, "~> 2.1 or ~> 3.0"}
  \]
end

then retrieve `ex_cldr` and the JSON library from hex:

mix deps.get
mix deps.compile

Additional Cldr Packages
------------------------

`ex_cldr` includes only basic functions to maintain the CLDR data repository in an accessible manner and to manage locale definitions. Additional functionality is available by adding additional packages:

-   Plugs for setting the locale from an HTTP request: ex\_cldr\_plugs
-   Number formatting: ex\_cldr\_numbers
-   List formatting: ex\_cldr\_lists
-   Unit or measure formatting: ex\_cldr\_units
-   Date/Time/DateTime formatting: ex\_cldr\_dates\_times
-   Route localization for Phoenix: ex\_cldr\_routes
-   Locale name localisation: ex\_cldr\_locale\_display
-   HTML select helpers: ex\_cldr\_html
-   Calendars: ex\_cldr\_calendars
-   Calendar formatting: ex\_cldr\_calendars\_format
-   Printf-like formatting: ex\_cldr\_print
-   Collation: ex\_cldr\_collation
-   ICU Message formatting: ex\_cldr\_messages
-   Person name formatting: ex\_cldr\_person\_names
-   Territories localization and information: ex\_cldr\_territories by @Schultzer
-   Languages localization: ex\_cldr\_languages by @lostkobrakai

Each of these packages includes `ex_cldr` as a dependency so configuring any of these additional packages will automatically install `ex_cldr`.

Configuration
-------------

`ex_cldr` attempts to maximise runtime performance at the expense of additional compile time. Where possible `ex_cldr` will create functions to encapsulate data at compile time. To perform these optimizations for all 541 locales known to Cldr wouldn't be an effective use of your time or your computer's. Therefore `ex_cldr` requires that you configure the locales you want to use.

`ex_cldr` is configured in your backend module. This removes any dependency on your `mix.exs` and therefore simplifies deployment as a release.

### Backend Module Configuration

> #### `use Cldr` {: .info}
> 
> When you `use Cldr`, a number of functions are generated that encapsulate CLDR data. A module that invokes `use Cldr` is referred to as a Cldr backend module.
> 
> The functions in a Cldr backend module form the primary recommended API for `ex_cldr`.
> 
> In addition, a number of additional modules may be generated with names that are prefixed by the name of the module in which `use Cldr` is invoked. The number and names of these additional modules is determined by the modules configured under the `:providers` option to `use Cldr`.
> 
> It is not recommended that a module that invokes `use Cldr` define any other functions.

defmodule MyApp.Cldr do
  use Cldr,
    default\_locale: "en",
    locales: \["fr", "en", "bs", "si", "ak", "th"\],
    add\_fallback\_locales: false,
    gettext: MyApp.Gettext,
    data\_dir: "./priv/cldr",
    otp\_app: :my\_app,
    precompile\_number\_formats: \["¤¤#,##0.##"\],
    precompile\_transliterations: \[{:latn, :arab}, {:thai, :latn}\],
    providers: \[Cldr.Number\],
    generate\_docs: true,
    force\_locale\_download: false
end

### Otp App Configuration

In the backend configuration example above the `:otp_app` key has been defined. This means that `ex_cldr` will look for additional configuration, defined under the key `:my_app` with the sub-key `MyApp.Cldr`. For example:

\# cldr.ex
defmodule MyApp.Cldr do
  use Cldr,
    otp\_app: :my\_app,
    default\_locale: "en",
    gettext: MyApp.Gettext,
    json\_library: Jason,
    data\_dir: "./priv/cldr",
    precompile\_number\_formats: \["¤¤#,##0.##"\],
    providers: \[Cldr.Number\]
end

\# config/config.exs
config :my\_app, MyApp.Cldr,
  \# a single locale, for fast compilation in dev / test
  locales: \["en"\]

\# config/production.exs
config :my\_app, MyApp.Cldr,
  \# these will take a while to compile
  locales: \["fr", "en", "bs", "si", "ak", "th"\],
  precompile\_transliterations: \[{:latn, :arab}, {:thai, :latn}\]

Multiple backends can be configured under a single `:otp_app` if required.

### Global configuration.

In `config.exs` a global configuration can be defined under the `:ex_cldr` key. Although any valid configuration keys can be used here, only the keys `:json_library`, `:default_locale`, `:default_backend`, `:cacertfile`, `:data_dir`, `:force_locale_download` are considered valid. Other configuration keys may be used to aid migration from `ex_cldr` version 1.x but a deprecation message will be printed during compilation. Here's an example of global configuration:

config :ex\_cldr,
  default\_locale: "en",
  default\_backend: MyApp.Cldr,
  json\_library: Jason,
  cacertfile: "path/to/cacertfile"

Note that the `:json_library` key can only be defined at the global level since it is required during compilation before any backend module is compiled.

> #### Automatic configuration of :json\_library {: .info}
> 
> OTP 27 and Elixir 1.18 both include native JSON libraries. Therefore if running on either (or both) of these platforms, no `:json_library` configuration is required or recommended.

On most platforms other than Windows the `:cacertfile` will be automatically detected. Any configured `:cacertfile` will take precedence on all platforms.

**If configuration beyond the keys `:default_locale`, `:cacertfile` or `:json_library` are defined a deprecation warning is printed at compile time noting that configuration should be moved to a backend module.**

### Configuration Priority

When building the consolidated configuration the following priority applies:

-   Consider the global configuration
-   Merge the otp\_app configuration over the top of the global configuration
-   Merge the backend module configuration over the top

### Backend Configuration Keys

The configuration keys available for `ex_cldr` are:

-   `default_locale` specifies the default locale to be used for this backend. The default locale in case no other locale has been set is `"en-001"`. The default locale is calculated as follows:
    
    -   If set by the `:default_locale` key, then this is the priority
    -   If no `:default_locale` key, then a configured `Gettext` default locale for this backend is chosen.
    -   If no `:default_locale` key is specified and no `Gettext` module is configured, or is configured but has no default set, use `Cldr.default_locale/0` which returns either the default locale configurated in `mix.exs` under the `ex_cldr` key or then the system default locale will is currently `en-001`.
-   `locales`: Defines what locales will be configured in `ex_cldr`. Only these locales will be available and an exception `Cldr.UnknownLocaleError` will be raised if there is an attempt to use an unknown locale. This is the same behaviour as `Gettext`. Locales are configured as a list of binaries (strings). For convenience it is possible to use wildcard matching of locales which is particularly helpful when there are many regional variances of a single language locale. For example, there are over 100 regional variants of the "en" locale in CLDR. A wildcard locale is detected by the presence of `.`, `[`, `*` and `+` in the locale string. This locale is then matched using the pattern as a `regex` to match against all available locales. The example below will configure all locales that start with `en-` and the locale `fr`.
    

use Cldr,
  default\_locale: "en",
  locales: \["en-\*", "fr"\]

-   There is one additional setting which is `:all` which will configure all ~700 locales. **This is highly discouraged** since it will take many minutes to compile your project and will consume more memory than you really want. This setting is there to aid in running the test suite. Really, don't use this setting.
    
-   `:add_fallback_locales` is a boolean key which when `true` results in the fallback locales being added for each of the configured locales. The default is `false`. The reason to set this option to `true` is that some data such as rules based number formats and subdivision data are inherited from their language roots. For example, the locale `en-001` is inherited from the locale `en`. Locale `en-001` does not have any rules-based number formats or subdivision data defined for it. However locale `en` does. Including the fallback locales maximises the opportunity to resolve localised data.
    
-   `:gettext`: specifies the name of a Gettext module that informs `ex_cldr` to use that module as an additional source of locales you want to configure. Since `Gettext` uses the POSIX locale name format (locales with an '\_' in them) and `ex_cldr` uses the Unicode format (a '-' as the subtag separator), `ex_cldr` will transliterate locale names from `Gettext` into the `ex_cldr` canonical form. For example:
    

use Cldr,
  default\_locale: "en",
  gettext: MyApp.Gettext,
  locales: \["en-\*", "fr"\]

-   `:data_dir`: indicates where downloaded locale files will be stored. The default is `:code.priv_dir(otp_app)` where `otp_app` is the app defined under the `:otp_app` configuration key. If that key is not specified then the `:ex_cldr` app is used. It is recommended that an `:otp_app` key is specified in your backend module configuration.
    
-   `:precompile_number_formats`: provides a means to have user-defined format strings precompiled at application compile time. This has a performance benefit since precompiled formats execute approximately twice as fast as formats that are not precompiled.
    
-   `:precompile_transliterations`: defines those transliterations between the digits of two different number systems that will be precompiled. The is a list of 2-tuples where each tuple is of the form `{from_number_system, to_number_system}` where each number system is expressed as an atom. The available number systems are returned by `Cldr.Number.System.systems_with_digits/0`. The default is the empty list `[]`.
    
-   `:precompile_date_time_formats`: provides a means to have user-defined date, time and date time format strings precompiled at application compile time. This has a performance benefit since precompiled formats execute approximately twice as fast as formats that are not precompiled. These formats are used by ex\_cldr\_date\_times.
    
-   `:precompile_interval_formats`: provides a means to have user-defined interval format strings precompiled at application compile time. This has a performance benefit since precompiled formats execute approximately twice as fast as formats that are not precompiled. These formats are used by ex\_cldr\_date\_times.
    
-   `:default_currency_format` determines whether `Cldr.Number.to_string/2` will use `:currency` or `:accounting` if no format is specified but a currency is. The default is `nil` which means that the format will be derived from the locale.
    
-   `:providers`: a list of modules that provide `ex_cldr` functionality to be compiled into the backend module. See the providers section below.
    
-   `:generate_docs` defines whether or not to generate documentation for the modules built as part of the backend. Since these modules represent the public API for `ex_cldr`, the default is `true`. Setting this key to `false` (the atom `false`, not a _falsy_ value) will prevent the generation of docs for this backend.
    
-   `:suppress_warnings` defines whether warnings are logged when a provider module is configured but not available. It also controls whether warnings are logged when a number format is compiled at runtime. Its purpose is to help identify those formats that might best be added to the `:precompile_number_formats` configuration. The default is `false`. Warnings are not logged when set to `true`.
    
-   `:force_locale_download` determines whether to always download locale files during compilation. Locale data is `ex_cldr` version dependent. When a new version of `ex_cldr` is installed, no locales are installed and therefore locales are downloaded at compilation time as required. This ensures that the right version of the locale data is always associated with the right version of `ex_cldr`. However, if locale data is being cached in CI/CD there is some possibility that there can be a version mismatch. Since reproducible builds are important, setting the `force_locale_download: true` in a backend or in global configuration adds additional certainty. The default setting is `false` thereby retaining compatibility with existing behaviour. The configuration can also be made dependent on `mix` environment as shown in this example:
    

defmodule MyApp.Cldr do
  use Cldr,
    locales: \["en", "fr"\],
    default\_locale: "en",
    force\_locale\_download: Mix.env() \== :prod
end

-   `:https_proxy` is the URL of a proxy host that will be used when downloading locales to be installed. When downloading, this configuration key has priority, followed by the environment variables `HTTPS_PROXY` and `https_proxy`. The default is `nil`.

### Providers

The data maintained by CLDR is quite large and not all capabilities are required by all applications. Hence `ex_cldr` has additional optional functionality that can be provided through additional `hex` packages. In order to support compile-time additions to a configured `backend`, any package can define a provider that will be called at compile time.

The currently known providers and their `hex` package names are:

Hex Package

Provider Module

Comment

ex\_cldr\_numbers

Cldr.Number

Formatting of numbers, currencies

ex\_cldr\_lists

Cldr.List

Formatting of lists

ex\_cldr\_units

Cldr.Unit

Formatting of SI and Imperial units

ex\_cldr\_person\_names

Cldr.PersonName

Formatting person names

ex\_cldr\_currencies

Cldr.Currency

Currency definitions and localizations

ex\_cldr\_territories

Cldr.Territory

Formatting of territory (country) data

ex\_cldr\_languages

Cldr.Language

Formatting of language information

ex\_cldr\_dates\_times

Cldr.DateTime

Formatting of dates, times & datetimes

ex\_cldr\_locale\_display

Cldr.LocaleDisplay

Localising locale names

ex\_cldr\_routes

Cldr.Route

Localized routes and route helpers

ex\_cldr\_messages

Cldr.Message

Formatting of ICU-formatted messages

ex\_money

Money

Operations on and formatting of a money type

Any library author can create a provider module by exposing a function called `cldr_backend_provider/1` that takes a `Cldr.Config` struct as a single parameter. The function should return an AST that is inserted into the `backend` module being compiled.

Providers are configured on each backend module under the `:providers` key. It must be a list of provider modules. For example:

defmodule MyApp.Cldr do
  use Cldr,
    locales: \["en", "zh"\],
    default\_locale: "en",
    providers: \[Cldr.Number, Cldr.List\]
end

**If :providers is `nil` (the default), `ex_cldr` will attempt to configure all of the providers described above if they have been installed as `deps`. If you don't wish to invoke any providers, use the empty list `[]`.**

Migrating from Cldr 1.x
-----------------------

1.  Create a `backend` module by following the configuration instructions
2.  Delete any duplicated global configuration in any `config.exs` files. Only the keys `:default_locale` and `:json_library` are supported in the global configuration
3.  Update any plugs to configure the desired backend
4.  Adjust any API calls from `Cldr.some_function` to `MyApp.Cldr.some_function`. Or better still, alias your backend module where required. ie. `alias MyApp.Cldr, as: Cldr`

Downloading Locales
-------------------

`ex_cldr` can be installed from either github or from hex.

-   If installed from GitHub then all 571 locales are installed when the repo is cloned into your application deps.
    
-   If installed from hex then only the locales "en", "en-001" and "und" are installed. When you configure additional locales these will be downloaded during application compilation.
    

Localizing Numbers
------------------

The `Cldr.Number` module implemented in the ex\_cldr\_numbers package provides number formatting. The public API for number formatting is `MyApp.Cldr.Number.to_string/2`. Some examples:

iex\> MyApp.Cldr.Number.to\_string 12345
"12,345"

iex\> MyApp.Cldr.Number.to\_string 12345, locale: "fr"
"12 345"

iex\> MyApp.Cldr.Number.to\_string 12345, locale: "fr", currency: "USD"
"12 345,00 $US"

iex\> MyApp.Cldr.Number.to\_string 12345, format: "#E0"
"1.2345E4"

iex(\> MyApp.Cldr.Number.to\_string 1234, format: :roman
"MCCXXXIV"

iex\> MyApp.Cldr.Number.to\_string 1234, format: :ordinal
"1,234th"

iex\> MyApp.Cldr.Number.to\_string 1234, format: :spellout
"one thousand two hundred thirty-four"

See `h MyApp.Cldr.Number` and `h MyApp.Cldr.Number.to_string` in `iex` for further information.

Localizing Lists
----------------

The `Cldr.List` module provides list formatting and is implemented in the ex\_cldr\_lists package. The public API for list formatting is `Cldr.List.to_string/2`. Some examples:

iex\> MyApp.Cldr.List.to\_string(\["a", "b", "c"\], locale: "en")
"a, b, and c"

iex\> MyApp.Cldr.List.to\_string(\["a", "b", "c"\], locale: "en", format: :unit\_narrow)
"a b c"

iex\> MyApp.Cldr.List.to\_string(\["a", "b", "c"\], locale: "fr")
"a, b et c"

See `h MyApp.Cldr.List` and `h MyApp.Cldr.List.to_string` in `iex` for further information.

Localizing Units
----------------

The `Cldr.Unit` module provides unit localization and is implemented in the ex\_cldr\_units package. The public API for unit localization is `Cldr.Unit.to_string/3`. Some examples:

iex\> MyApp.Cldr.Unit.to\_string 123, :gallon
"123 gallons"

iex\> MyApp.Cldr.Unit.to\_string 1234, :gallon, format: :long
"1 thousand gallons"

iex\> MyApp.Cldr.Unit.to\_string 1234, :gallon, format: :short
"1K gallons"

iex\> MyApp.Cldr.Unit.to\_string 1234, :megahertz
"1,234 megahertz"

iex\> MyApp.Cldr.Unit.available\_units
\[:acre, :acre\_foot, :ampere, :arc\_minute, :arc\_second, :astronomical\_unit, :bit,
 :bushel, :byte, :calorie, :carat, :celsius, :centiliter, :centimeter, :century,
 :cubic\_centimeter, :cubic\_foot, :cubic\_inch, :cubic\_kilometer, :cubic\_meter,
 :cubic\_mile, :cubic\_yard, :cup, :cup\_metric, :day, :deciliter, :decimeter,
 :degree, :fahrenheit, :fathom, :fluid\_ounce, :foodcalorie, :foot, :furlong,
 :g\_force, :gallon, :gallon\_imperial, :generic, :gigabit, :gigabyte, :gigahertz,
 :gigawatt, :gram, :hectare, :hectoliter, :hectopascal, :hertz, :horsepower,
 :hour, :inch, ...\]

See `h MyApp.Cldr.Unit` and `h MyApp.Cldr.Unit.to_string` in `iex` for further information.

Localizing Dates
----------------

Formatting of relative dates and date times is supported in the `Cldr.DateTime.Relative` module implemented in the ex\_cldr\_dates\_times package. The public API is `MyApp.Cldr.DateTime.to_string/2` and `MyApp.Cldr.DateTime.Relative.to_string/2`. Some examples:

iex\> MyApp.Cldr.Date.to\_string Date.utc\_today()
{:ok, "Aug 18, 2017"}

iex\> MyApp.Cldr.Time.to\_string Time.utc\_now
{:ok, "11:38:55 AM"}

iex\> MyApp.Cldr.DateTime.to\_string DateTime.utc\_now
{:ok, "Aug 18, 2017, 11:39:08 AM"}

iex\> MyApp.Cldr.DateTime.Relative.to\_string 1, unit: :day, format: :narrow
{:ok, "tomorrow"}

iex\> MyApp.Cldr.DateTime.Relative.to\_string(1, unit: :day, locale: "fr")
"demain"

iex\> MyApp.Cldr.DateTime.Relative.to\_string(1, unit: :day, format: :narrow)
"tomorrow"

iex\> MyApp.Cldr.DateTime.Relative.to\_string(1234, unit: :year)
"in 1,234 years"

iex\> MyApp.Cldr.DateTime.Relative.to\_string(1234, unit: :year, locale: "fr")
"dans 1 234 ans"

Gettext Pluralization
---------------------

gettext allows for user-defined plural forms modules to be configured for a gettext backend.

To define a plural forms module that uses CLDR plural rules create a new module and then `use Cldr.Gettext.Plural`. For example:

```
defmodule MyApp.Gettext.Plural do
  use Cldr.Gettext.Plural, cldr_backend: MyApp.Cldr
end
```

This module can then be used in the configuration of a `gettext` backend. For example:

```
defmodule MyApp.Gettext do
  use Gettext, plural_forms: MyApp.Gettext.Plural
end
```

Note that `MyApp.Gettext.Plural` does not guarantee to return the same `plural index` as `Gettext`'s own pluralization engine which can introduce some compatibility issues if you plan to mix plural engines. See `Cldr.Gettext.Plural` for more information.

About Language Tags
-------------------

Note that `ex_cldr` defines locale strings according to the IETF standard as defined in RFC5646. `ex_cldr` also implements the `u` extension as defined in RFC6067 and the `t` extension defined in RFC6497. This is also the standard used by W3C.

The IETF standard is slightly different from the ISO/IEC 15897 standard used by Posix-based systems; primarily in that ISO 15897 uses a "\_" separator whereas IETF and W3C use "-".

Locale strings are case insensitive but there are common conventions:

-   Language codes are lower-cased
-   Territory codes are upper-cased
-   Script names are capital-cased
-   All other subtags are lower-cased

### `Sigil_l`

As of `ex_cldr` version 2.23.0, a sigil is available to simplify creating `t:Cldr.LanguageTag` structs. Usage is:

iex\> import Cldr.LanguageTag.Sigil
Cldr.LanguageTag.Sigil

\# Returns a locale that is valid and known to
\# the default backend module
iex\> ~l(en-US)
#Cldr.LanguageTag<en-US \[validated\]>

\# Same, but specifying the backend module
\# MyApp.Cldr specifically
iex\> ~l(en-US|MyApp.Cldr)
#Cldr.LanguageTag<en-US \[validated\]>

\# The \`u\` flag will parse and validate
\# the language tag but it may not be known
\# as a configured locale
iex\> ~l(zh)u
#Cldr.LanguageTag<zh \[canonical\]>

\# Language tags can convey a lot more information
\# than might be initially expected!
iex\> ~l(en-u-ca-ethiopic-cu-aud-sd-gbsct-t-d0-lower-k0-extended-m0-ungegn-x-ux)
#Cldr.LanguageTag<en-t-d0-lower-k0-extended-m0-ungegn-u-ca-ethiopic-cu-aud-sd-gbsct-x-ux \[validated\]>

### Locale extensions

Unicode defines the U extension which support defining the requested treatment of CLDR data formats. For example, a locale name can configure the requested:

-   calendar to be used for dates
-   collation
-   currency
-   currency format
-   number system
-   first day of the week
-   12-hour or 24-hour time
-   time zone
-   and many other items

For example, the following locale name will request the use of the timezone `Australia/Sydney`, and request the use of `accounting` format when formatting currencies:

iex\> MyApp.Cldr.validate\_locale "en-AU-u-tz-ausyd-cf-account"
{:ok,
 %Cldr.LanguageTag{
   canonical\_locale\_name: "en-Latn-AU",
   cldr\_locale\_name: "en-AU",
   extensions: %{},
   gettext\_locale\_name: "en",
   language: "en",
   language\_subtags: \[\],
   language\_variants: nil,
   locale: %Cldr.LanguageTag.U{cf: :account, timezone: "Australia/Sydney"},
   private\_use: \[\],
   rbnf\_locale\_name: "en",
   requested\_locale\_name: "en-AU",
   script: :Latn,
   territory: :AU,
   transform: %{}
 }}

The implementation of these extensions is governed by each library in the `ex_cldr` family. As of January 2020, ex\_cldr\_numbers version 2.10 implements the following `U` extension keys:

-   `cf` (currency format)
-   `cu` (currency)
-   `nu` (number system)

Other libraries in the family will progressively implement other extension keys.

### Notes

-   A language code is an ISO-3166 language code.
-   Potentially one or more modifiers separated by `-` (dash), not a `_`. (underscore). If you configure a `Gettext` module then `ex_cldr` will transliterate `Gettext`'s `_` into `-` for compatibility.
-   Typically the modifier is a territory code. This is commonly a two-letter uppercase combination. For example `pt-PT` is the locale referring to Portuguese as used in Portugal.
-   In `ex_cldr` a locale name is always a `binary` and never an `atom`. Internally a locale is parsed and stored as a `t:Cldr.LanguageTag` struct.
-   The locales known to `ex_cldr` can be retrieved by `Cldr.known_locale_names/1` to get the locales known to this configuration of `ex_cldr` and `Cldr.all_locale_names/0` to get the locales available in the CLDR data repository.

Developing ex\_cldr
-------------------

See the file `DEVELOPMENT.md` in the GitHub repository.

### Testing

Tests cover the full ~700 locales defined in CLDR. Since `ex_cldr` attempts to maximize the work done at compile time in order to minimize runtime execution, the compilation phase for tests is several minutes.

Tests are run on Elixir 1.11 and later. `ex_cldr` is not supported on Elixir versions before 1.11.
