---
project: volt
stars: 139
description: Elixir-native frontend build tool — dev server, HMR, and production builds for JavaScript, TypeScript, Vue SFCs, and CSS. No Node.js required.
url: https://github.com/elixir-volt/volt
---

Volt ⚡
======

Vite-level frontend tooling that runs inside the BEAM. One dep replaces esbuild, the Tailwind CLI, and Node.js with Rust NIFs powered by OXC and LightningCSS.

mix igniter.install volt
mix phx.server

The installer configures everything. No binaries to download, no extra processes to manage.

Volt's npm integration uses `npm_ex`, which ignores package lifecycle hooks by default. Runtime package installs do not execute `preinstall`, `install`, or `postinstall` scripts, mitigating install-time credential stealers.

Why Volt
--------

Phoenix ships with esbuild and a Tailwind CLI as separate binaries downloaded at compile time. They can't coordinate HMR or share work, and anything beyond vanilla JS requires Node.js.

Volt replaces both with a single Elixir dep. `mix phx.server` starts the frontend toolchain automatically, rebuilding Tailwind in ~40ms on template changes and hot-swapping JS modules via HMR. Compilation errors show as a browser overlay. Production builds finish in under 100ms.

You also get features you'd expect from Vite: code splitting, CSS Modules, `import.meta.glob()`, dynamic import variables, `.env` variables, static asset imports, import aliases, and `import.meta.hot` with state preservation.

The pieces integrate because they run in one toolchain: template edits can trigger incremental Tailwind rebuilds, browser console output can flow back to your Elixir terminal, and project-specific JS/TS lint rules can be written as Elixir modules. See the Features guide for the full list.

Installation
------------

mix igniter.install volt

Or add the dep manually:

def deps do
  \[{:volt, "~> 0.10"}\]
end

See the Getting Started guide for manual configuration.

Configuration
-------------

Standard `config/*.exs`. No `vite.config.js`, no `tailwind.config.js`:

config :volt,
  entry: "assets/js/app.ts",
  target: :es2020,
  sourcemap: :hidden,
  tailwind: \[
    css: "assets/css/app.css",
    sources: \[
      %{base: "lib/", pattern: "\*\*/\*.{ex,heex}"},
      %{base: "assets/", pattern: "\*\*/\*.{js,ts,jsx,tsx}"}
    \]
  \]

`Volt.static_path/2` resolves Volt-managed assets to source files in dev and content-hashed paths in production:

<link phx-track-static rel\="stylesheet" href\={Volt.static\_path(@endpoint, "/assets/css/app.css")} />
<script defer phx-track-static type\="module" src\={Volt.static\_path(@endpoint, "/assets/js/app.js")}\></script\>

Production builds
-----------------

```
$ mix volt.build

Building Tailwind CSS...
  app-1a2b3c4d.css  23.9 KB
Built Tailwind in 43ms
Building "assets/js/app.ts"...
  app-5e6f7a8b.js  128.4 KB  (gzip: 38.2 KB)
  manifest.json  2 entries
Built in 15ms
```

Tree-shaking, minification, code splitting, configurable env prefixes and asset URL prefixes, source maps, content-hashed JavaScript/CSS/assets, and manifest output. Ready for `mix phx.digest`.

Framework support
-----------------

Vue SFCs with scoped CSS, React JSX with the automatic runtime, Svelte 5 with runes, and Solid JSX all compile without Node.js installed. Plain TypeScript with LiveView hooks works too.

See the examples for complete Phoenix projects with each framework.

Developer tools
---------------

JS/TS formatting and linting run as Rust NIFs. `mix format` handles Elixir and JavaScript together:

\# .formatter.exs
\[plugins: \[Volt.Formatter\], inputs: \["assets/\*\*/\*.{js,ts,jsx,tsx}"\]\]

mix format           # Elixir + JS/TS
mix volt.lint        # 650+ oxlint rules
mix volt.js.check    # format + lint for CI
mix volt.js.check --type-aware --type-check

Project-specific lint rules can be written in Elixir with `OXC.Lint.Rule`. Type-aware TypeScript rules can run through `tsgolint` with `--type-aware`.

Plugins
-------

Extend the build pipeline with the `Volt.Plugin` behaviour. Plugins can resolve imports, load custom file types, transform ASTs, render chunks, or call JS tooling through an embedded runtime:

defmodule MyApp.MarkdownPlugin do
  @behaviour Volt.Plugin

  def name, do: "markdown"

  def load(path) do
    if String.ends\_with?(path, ".md") do
      html \= path |> File.read!() |> Earmark.as\_html!()
      {:ok, "export default #{Jason.encode!(html)};\\n"}
    end
  end
end

config :volt, plugins: \[MyApp.MarkdownPlugin\]

See the Plugins guide for the full hook API.

Documentation
-------------

Full documentation, guides, and cheatsheets on HexDocs.

License
-------

MIT © 2026 Danila Poyarkov
