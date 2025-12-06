---
project: ex_ray
stars: 57
description: An Elixir OpenTracing library based on Otter
url: https://github.com/derailed/ex_ray
---

ExRay
=====

Motivation
----------

ExRay defines an annotation construct that wraps regular functions and enable them to be traced using a simple affordance **@trace** to interact with an OpenTracing compliant collector.

OpenTracing defines the concept of spans that track the call stack and record timing information and various call artifacts that can be used for application runtime inspection. This is a really cool piece of technology that compliments your monitoring solution as you now have x-ray vision of your application at runtime once a monitoring metric gets off the chart.

However in practice, your code gets quickly cluttered by your tracing efforts. ExRay alleviates the clutter by injecting cross-cutting tracing concern into your application code. By using @trace annotation, you can trap the essence of the calls without introducing tracing code mixed-in with your business logic.

ExRay leverages Otter Erlang OpenTracing lib from the fine folks of BlueHouse Technology.

Documentation
-------------

ExRay

Installation
------------

Tracing information needs to be collected by a tracing backend of your choice. You can run ExRay using any trace collector that Otter supports. In the following example we will use Jaeger from the self-driven folks at Uber!

1.  Start Jaeger
    
    Providing you have docker running on you box, you can use the all-in-one Jaeger image to get you started. If you are a Kubernetes fan, you can use the Jaeger chart
    
    docker run -d -e COLLECTOR\_ZIPKIN\_HTTP\_PORT=9411 -p5775:5775/udp -p6831:6831/udp -p6832:6832/udp \\
    -p5778:5778 -p16686:16686 -p14268:14268 -p9411:9411 jaegertracing/all-in-one:latest
    
    Alternatively, you could use the echo server otter\_srv for testing your installation but I find it more fun to have a cool UI to look at your tracing outcomes.
    
2.  Setup Dependencies
    
    Add the following dependencies to your project (Elixir or Phoenix)
    
    > NOTE: You can use Httpc(default), Hackney or IBrowse for your http client. We opt for Ibrowse here.
    
    def deps do
      \[
        ...
        {:ex\_ray , "~> 0.1.2"},
        {:ibrowse, "~> 4.4.0"}
      \]
    end
    
3.  Configure Otter
    
    In your config file, you need to tell Otter where to find your Zipkin collector.
    
      config :otter,
        zipkin\_collector\_uri:    'http://127.0.0.1:9411/api/v1/spans',
        zipkin\_tag\_host\_service: "TraceMe",
        http\_client:             :ibrowse
    
    > Note: This thru me for a loop! The uri is indeed a char list and not a string!
    
4.  Configure Your Application
    
    ExRay uses ETS to track the span chains. Each request will create a new chain that will grow and collapse with your function call stack. As such you will need to track a unique call ID either by generating a custom ID for each request. If you are using Phoenix, the framework does this for you by using the request\_id in the response headers. The ETS table is used to locate the parent span for which to attach to when navigating the call stack.
    
    > NOTE: One cool aspect of OpenTracing is the tracing does not stop at the process boundaries as you can continue the chain to other processes and external services. Please see the examples directory for further info.
    
    In your application initialization, you need to make sure the ExRay ETS table is created by calling
    
    \# application.ex
    ...
    ExRay.Store.create()
    ...
    
5.  Let's Trace!
    
    Here is a simples tracing example. Please take a look at the examples in the Repo and ExRay Tracers for Phoenix sample use cases.
    
      defmodule TraceMe do
        use ExRay, pre: :before\_fun, post: :after\_fun
    
        alias ExRay.Span
    
        \# Generates a request id
        @req\_id :os.system\_time(:milli\_seconds) |> Integer.to\_string |> IO.inspect
    
        @trace kind: :critical
        def fred(a, b), do: a+b
    
        defp before\_fun(ctx) do
          ctx.target
          |> Span.open(@req\_id)
          |> :otter.tag(:kind, ctx.meta\[:kind\])
          |> :otter.log(">>> #{ctx.target} with #{ctx.args |> inspect}")
        end
    
        defp after\_fun(ctx, span, res) do
          span
          |> :otter.log("<<< #{ctx.target} returned #{res}")
          |> Span.close(@req\_id)
        end
      end
    
6.  See it!
    
    That's great, but how do you see the tracing information?
    
    open http://localhost:16686
    
    Under _Service_ open up our _TraceMe_ service, click **Find Traces** and you should now see your span in all its glory ie timing, tag and log info
    

* * *

### Thank you for playing!

* * *

© 2017 Imhotep Software LLC. All materials licensed under Apache v2.0
