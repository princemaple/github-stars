---
project: entrace_live_dashboard
stars: 36
description: Tracing experiments with live dashboard
url: https://github.com/underjord/entrace_live_dashboard
---

Entrace Live Dashboard
======================

Puts function tracing right into your Phoenix Live Dashboard.

Early version
-------------

The UI is still kind of rough. Should be plenty useful though. Contributions are very welcome.

Installation
------------

Add it to your deps in `mix.exs`:

\# ..
{:entrace\_live\_dashboard, "~> 0.1"}
\# ..

Then add the page to your live\_dashboard route in `router.ex`:

  live\_dashboard "/dashboard",
    metrics: SampleWeb.Telemetry,
    additional\_pages: \[
      trace\_calls:
        {EntraceLiveDashboard.PhoenixLiveDashboard.TraceCallPage, tracer: Sample.Tracer}
    \]

Visit your dashboard path and visit the "Trace Calls" menu item.
