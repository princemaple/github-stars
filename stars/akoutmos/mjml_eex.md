---
project: mjml_eex
stars: 122
description: Create emails that WOW your customers using MJML and EEx
url: https://github.com/akoutmos/mjml_eex
---

Easily create beautiful emails using MJML right from Elixir!

  

Contents
========

-   Installation
-   Supporting MJML EEx
-   Using MJML EEx
-   Configuration
-   Attribution

Installation
------------

Available in Hex, the package can be installed by adding `mjml_eex` to your list of dependencies in `mix.exs`:

def deps do
  \[
    {:mjml\_eex, "~> 0.13.0"}
  \]
end

Documentation can be found at https://hexdocs.pm/mjml\_eex.

Supporting MJML EEx
-------------------

If you rely on this library to generate awesome looking emails for your application, it would much appreciated if you can give back to the project in order to help ensure its continued development.

Checkout my GitHub Sponsorship page if you want to help out!

### Gold Sponsors

### Silver Sponsors

### Bronze Sponsors

Using MJML EEx
--------------

### Basic Usage

defmodule BasicTemplate do
  use MjmlEEx, mjml\_template: "basic\_template.mjml.eex"
end

And the accompanying MJML EEx template `basic_template.mjml.eex` (note that the path is relative to the calling module path):

<mjml\>
  <mj-body\>
    <mj-section\>
      <mj-column\>
        <mj-divider border-color\="#F45E43"\></mj-divider\>
        <mj-text font-size\="20px" color\="#F45E43"\>
          Hello <%= @first\_name %\> <%= @last\_name %\>!
        </mj-text\>
      </mj-column\>
    </mj-section\>
  </mj-body\>
</mjml\>

With those two in place, you can now run `BasicTemplate.render(first_name: "Alex", last_name: "Koutmos")` and you will get back an HTML document that can be emailed to users.

### Using Functions from Template Module

You can also call functions from your template module if they exist in your MJML EEx template using the following module declaration:

defmodule FunctionTemplate do
  use MjmlEEx, mjml\_template: "function\_template.mjml.eex"

  defp generate\_full\_name(first\_name, last\_name) do
    "#{first\_name} #{last\_name}"
  end
end

In conjunction with the following template:

<mjml\>
  <mj-body\>
    <mj-section\>
      <mj-column\>
        <mj-divider border-color\="#F45E43"\></mj-divider\>
        <mj-text font-size\="20px" color\="#F45E43"\>
          Hello <%= generate\_full\_name(@first\_name, @last\_name) %\>!
        </mj-text\>
      </mj-column\>
    </mj-section\>
  </mj-body\>
</mjml\>

In order to render the email you would then call: `FunctionTemplate.render(first_name: "Alex", last_name: "Koutmos")`

### Using Components

**Static components**

In addition to compiling single MJML EEx templates, you can also create MJML partials and include them in other MJML templates AND components using the special `render_static_component` function. With the following modules:

defmodule FunctionTemplate do
  use MjmlEEx, mjml\_template: "component\_template.mjml.eex"
end

defmodule HeadBlock do
  use MjmlEEx.Component

  @impl true
  def render(\_opts) do
    """
    <mj-head>
      <mj-title>Hello world!</mj-title>
      <mj-font name="Roboto" href="https://fonts.googleapis.com/css?family=Montserrat:300,400,500"></mj-font>
    </mj-head>
    """
  end
end

And the following template:

<mjml\>
  <%= render\_static\_component HeadBlock %\>

  <mj-body\>
    <mj-section\>
      <mj-column\>
        <mj-divider border-color\="#F45E43"\></mj-divider\>
        <mj-text font-size\="20px" color\="#F45E43"\>
          Hello <%= generate\_full\_name(@first\_name, @last\_name) %\>!
        </mj-text\>
      </mj-column\>
    </mj-section\>
  </mj-body\>
</mjml\>

Be sure to look at the `MjmlEEx.Component` module for additional usage information as you can also pass options to your template and use them when generating the partial string. One thing to note is that when using `render_static_component`, the data that is passed to the component must be defined at compile time. This means that you cannot use any assigns that would be evaluated at runtime. For example, this would raise an error:

<mj\-text\>
  <%\= render\_static\_component MyTextComponent, some\_data: @some\_data %\>
</mj\-text\>

**Dynamic components**

If you need to render your components dynamically, use `render_dynamic_component` instead and be sure to configure your template module like below to generate the email HTML at runtime. First, you create your component, for example, `MyTemplate.CtaComponent.ex`:

def MyTemplate.CtaComponent do
  use MjmlEEx.Component, mode: :runtime

  @impl MjmlEEx.Component
  def render(assigns) do
    """
    <mj-column>
      <mj-text font-size="20px" color="#F45E43">
        #{assigns\[:call\_to\_action\_text\]}
      </mj-text>
      <mj-button align="center" inner-padding="12px 20px">
        #{assigns\[:call\_to\_action\_link\]}
      </mj-button>
    </mj-column>
    """
  end
end

then, in your MJML template, insert it using the `render_dynamic_template_component` function:

<mjml\>
  <mj-body\>
    <mj-section\>
      <mj-column\>
        <mj-divider border-color\="#F45E43"\></mj-divider\>
        <%= render\_dynamic\_component MyTemplate.CtaComponent %{call\_to\_action\_text: "Call to action text",
        call\_to\_action\_link: "#{@cta\_link}"} %\>
      </mj-column\>
    </mj-section\>
  </mj-body\>
</mjml\>

In your `UserNotifier` module, or equivalent, you render your template, passing any assigns/data it expects:

WelcomeEmail.render(call\_to\_action\_text: call\_to\_action\_text, call\_to\_action\_link: call\_to\_action\_link)

### Using Layouts

Often times, you'll want to create an Email skeleton or layout using MJML, and then inject your template into that layout. MJML EEx supports this functionality which makes it really easy to have business branded emails application wide without having to copy and paste the same boilerplate in every template.

To create a layout, define a layout module like so:

defmodule BaseLayout do
  use MjmlEEx.Layout, mjml\_layout: "base\_layout.mjml.eex"
end

And an accompanying layout like so:

<mjml\>
  <mj-head\>
    <mj-title\>Say hello to card</mj-title\>
    <mj-font name\="Roboto" href\="https://fonts.googleapis.com/css?family=Montserrat:300,400,500"\></mj-font\>
    <mj-attributes\>
      <mj-all font-family\="Montserrat, Helvetica, Arial, sans-serif"\></mj-all\>
      <mj-text font-weight\="400" font-size\="16px" color\="#000000" line-height\="24px"\></mj-text\>
      <mj-section padding\="<%= @padding %>"\></mj-section\>
    </mj-attributes\>
  </mj-head\>

  <%= @inner\_content %\>
</mjml\>

As you can see, you can include assigns in your layout template (like `@padding`), but you also need to include a mandatory `@inner_content` expression. That way, MJML EEx knowns where to inject your template into the layout. With that in place, you just need to tell your template module what layout to use (if you are using a layout that is):

defmodule MyTemplate do
  use MjmlEEx,
    mjml\_template: "my\_template.mjml.eex",
    layout: BaseLayout
end

And your template file can contain merely the parts that you need for that particular template:

<mj-body\> ... </mj-body\>

Using with Gettext
------------------

Similarly to Phoenix live/dead views, you can leverage Gettext to produce translated emails. To use Gettext, you will need to have a Gettext module defined in your project (this should be created automatically for you when you create your Phoenix project via `mix phx.new MyApp`). Then your MjmlEEx module will look something like this:

defmodule MyApp.GettextTemplate do
    import MyApp.Gettext

    use MjmlEEx,
      mjml\_template: "gettext\_template.mjml.eex",
      mode: :compile
  end

Make sure that you have the `import MyApp.Gettext` statement before the `use MjmlEEx` statement as you will get a compiler error that the `gettext` function that is being called in the `gettext_template.mjml.eex` has not been defined.

Configuration
-------------

MJML EEx has support for both the 1st party NodeJS compiler and the 3rd party Rust compiler. By default, MJML EEx uses the Rust compiler as there is an Elixir NIF built with Rustler that packages the Rust library for easy use: mjml\_nif. By default the Rust compiler is used as it does not require you to have NodeJS available.

In order to use the NodeJS compiler, you can provide the following configuration in your `config.exs` file:

config :mjml\_eex, compiler: MjmlEEx.Compilers.Node

Be sure to check out the documentation for the `MjmlEEx.Compilers.Node` module as it also requires some additional set up.

Attribution
-----------

-   The logo for the project is an edited version of an SVG image from the unDraw project
-   The Elixir MJML library that this library builds on top of MJML
-   The Rust MRML library that provides the MJML compilation functionality MRML
