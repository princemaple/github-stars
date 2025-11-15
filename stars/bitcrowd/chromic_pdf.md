---
project: chromic_pdf
stars: 468
description: Convenient HTML to PDF/A rendering library for Elixir based on Chrome & Ghostscript
url: https://github.com/bitcrowd/chromic_pdf
---

ChromicPDF is a HTML-to-PDF renderer for Elixir, based on headless Chrome.

Features
--------

-   **Node-free**: In contrast to many other packages, it does not use puppeteer, and hence does not require Node.js. It communicates directly with Chrome's DevTools API over pipes, offering the same performance as puppeteer, if not better.
-   **Header/Footer**: Using the DevTools API allows to apply the full set of options of the `printToPDF` function. Most notably, it supports header and footer HTML templates.
-   **PDF/A**: It can convert printed files to PDF/A using Ghostscript. Converted files pass the verapdf validator.

Requirements
------------

-   Chromium or Chrome
-   Ghostscript (optional, for PDF/A support and concatenation of multiple sources)

ChromicPDF is tested in the following configurations:

Elixir

Erlang/OTP

Distribution

Chromium

Ghostscript

1.15.7

26.2

Alpine 3.18

119.0.6045.159

10.02.0

1.14.5

25.3.1

Alpine 3.17

112.0.5615.165

10.01.1

1.14.0

25.1

Debian Buster

90.0.4430.212-1

9.27

1.11.4

22.3.4.26

Debian Buster

90.0.4430.212-1

9.27

Installation
------------

ChromicPDF is a supervision tree (rather than an application). You will need to inject it into the supervision tree of your application. First, add ChromicPDF to your runtime dependencies:

def deps do
  \[
    {:chromic\_pdf, "~> 1.17"}
  \]
end

Next, start ChromicPDF as part of your application:

\# lib/my\_app/application.ex
def MyApp.Application do
  def start(\_type, \_args) do
    children \= \[
      \# other apps...
      ChromicPDF
    \]

    Supervisor.start\_link(children, strategy: :one\_for\_one, name: MyApp.Supervisor)
  end
end

Usage
-----

### Main API

Here's how you generate a PDF from an external URL and store it in the local filesystem.

\# Prints a local HTML file to PDF.
ChromicPDF.print\_to\_pdf({:url, "https://example.net"}, output: "example.pdf")

The next example shows how to print a local HTML file to PDF/A, as well as the use of a callback function that receives the generated PDF as path to a temporary file.

ChromicPDF.print\_to\_pdfa({:url, "file:///example.html"}, output: fn pdf \->
  \# Send pdf via mail, upload to S3, ...
end)

### Template API

ChromicPDF.Template contains additional functionality for controlling page dimensions of your PDF.

\[content: "<p>Hello Template</p>", size: :a4\]
|> ChromicPDF.Template.source\_and\_options()
|> ChromicPDF.print\_to\_pdf()

### Multiple sources

Multiple sources can be automatically concatenated using Ghostscript.

ChromicPDF.print\_to\_pdf(\[{:html, "page 1"}, {:html, "page 2"}\], output: "joined.pdf")

### Examples

-   There is an outdated example of how to integrate ChromicPDF in a Phoenix application, see examples/phoenix.

Development
-----------

This should get you started:

```
mix deps.get
mix test
```

For running the full suite of integration tests, please install and have in your `$PATH`:

-   `verapdf`
-   For `pdfinfo` and `pdftotext`, you need `poppler-utils` (most Linux distributions) or Xpdf (OSX)
-   For the odd ZUGFeRD test in `zugferd_test.exs`, you need to download ZUV and set the `$ZUV_JAR` environment variable.

Acknowledgements
----------------

-   The PDF/A conversion is inspired by the `pdf2archive` script originally created by @matteosecli and later enhanced by @JaimeChavarriaga.

Copyright and License
---------------------

Copyright (c) 2019–2023 Bitcrowd GmbH

Licensed under the Apache License 2.0. See LICENSE file for details.
