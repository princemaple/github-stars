---
project: signoz
stars: 25198
description: SigNoz is an open-source observability platform native to OpenTelemetry with logs, traces and metrics in a single application. An open-source alternative to DataDog, NewRelic, etc. 🔥 🖥.   👉  Open source Application Performance Monitoring (APM) & Observability tool
url: https://github.com/SigNoz/signoz
---

  
SigNoz
=========

All your logs, metrics, and traces in one place. Monitor your application, spot issues before they occur and troubleshoot downtime quickly with rich context. SigNoz is a cost-effective open-source alternative to Datadog and New Relic. Visit signoz.io for the full documentation, tutorials, and guide.

### **Documentation** • **ReadMe in Chinese** • **ReadMe in German** • **ReadMe in Portuguese** • **Slack Community** • **Twitter**

Features
--------

### Application Performance Monitoring

Use SigNoz APM to monitor your applications and services. It comes with out-of-box charts for key application metrics like p99 latency, error rate, Apdex and operations per second. You can also monitor the database and external calls made from your application. Read more.

You can instrument your application with OpenTelemetry to get started.

### Logs Management

SigNoz can be used as a centralized log management solution. We use ClickHouse (used by likes of Uber & Cloudflare) as a datastore, ⎯ an extremely fast and highly optimized storage for logs data. Instantly search through all your logs using quick filters and a powerful query builder.

You can also create charts on your logs and monitor them with customized dashboards. Read more.

### Distributed Tracing

Distributed Tracing is essential to troubleshoot issues in microservices applications. Powered by OpenTelemetry, distributed tracing in SigNoz can help you track user requests across services to help you identify performance bottlenecks.

See user requests in a detailed breakdown with the help of Flamegraphs and Gantt Charts. Click on any span to see the entire trace represented beautifully, which will help you make sense of where issues actually occurred in the flow of requests.

Read more.

### Metrics and Dashboards

Ingest metrics from your infrastructure or applications and create customized dashboards to monitor them. Create visualization that suits your needs with a variety of panel types like pie chart, time-series, bar chart, etc.

Create queries on your metrics data quickly with an easy-to-use metrics query builder. Add multiple queries and combine those queries with formulae to create really complex queries quickly.

Read more.

### Alerts

Use alerts in SigNoz to get notified when anything unusual happens in your application. You can set alerts on any type of telemetry signal (logs, metrics, traces), create thresholds and set up a notification channel to get notified. Advanced features like alert history and anomaly detection can help you create smarter alerts.

Alerts in SigNoz help you identify issues proactively so that you can address them before they reach your customers.

Read more.

### Exceptions Monitoring

Monitor exceptions automatically in Python, Java, Ruby, and Javascript. For other languages, just drop in a few lines of code and start monitoring exceptions.

See the detailed stack trace for all exceptions caught in your application. You can also log in custom attributes to add more context to your exceptions. For example, you can add attributes to identify users for which exceptions occurred.

Read more.

  
  

Why SigNoz?
-----------

SigNoz is a single tool for all your monitoring and observability needs. Here are a few reasons why you should choose SigNoz:

-   Single tool for observability(logs, metrics, and traces)
    
-   Built on top of OpenTelemetry, the open-source standard which frees you from any type of vendor lock-in
    
-   Correlated logs, metrics and traces for much richer context while debugging
    
-   Uses ClickHouse (used by likes of Uber & Cloudflare) as datastore - an extremely fast and highly optimized storage for observability data
    
-   DIY Query builder, PromQL, and ClickHouse queries to fulfill all your use-cases around querying observability data
    
-   Open-Source - you can use open-source, our cloud service or a mix of both based on your use case
    

Getting Started
---------------

### Create a SigNoz Cloud Account

SigNoz cloud is the easiest way to get started with SigNoz. Our cloud service is for those users who want to spend more time in getting insights for their application performance without worrying about maintenance.

Get started for free

### Deploy using Docker(self-hosted)

Please follow the steps listed here to install using docker

The troubleshooting instructions may be helpful if you face any issues.

### Deploy in Kubernetes using Helm(self-hosted)

Please follow the steps listed here to install using helm charts

  
  

We also offer managed services in your infra. Check our pricing plans for all details.

Join our Slack community
------------------------

Come say Hi to us on Slack 👋

  
  

### Languages supported:

SigNoz supports all major programming languages for monitoring. Any framework and language supported by OpenTelemetry is supported by SigNoz. Find instructions for instrumenting different languages below:

-   Java
-   Python
-   Node.js or Javascript
-   Go
-   PHP
-   .NET
-   Ruby
-   Elixir
-   Rust
-   Swift

You can find our entire documentation here.

  
  

Comparisons to Familiar Tools
-----------------------------

### SigNoz vs Prometheus

Prometheus is good if you want to do just metrics. But if you want to have a seamless experience between metrics, logs and traces, then current experience of stitching together Prometheus & other tools is not great.

SigNoz is a one-stop solution for metrics and other telemetry signals. And because you will use the same standard(OpenTelemetry) to collect all telemetry signals, you can also correlate these signals to troubleshoot quickly.

For example, if you see that there are issues with infrastructure metrics of your k8s cluster at a timestamp, you can jump to other signals like logs and traces to understand the issue quickly.

### SigNoz vs Jaeger

Jaeger only does distributed tracing. SigNoz supports metrics, traces and logs - all the 3 pillars of observability.

Moreover, SigNoz has few more advanced features wrt Jaeger:

-   Jaegar UI doesn’t show any metrics on traces or on filtered traces
-   Jaeger can’t get aggregates on filtered traces. For example, p99 latency of requests which have tag - customer\_type='premium'. This can be done easily on SigNoz
-   You can also go from traces to logs easily in SigNoz

### SigNoz vs Elastic

-   SigNoz Logs management are based on ClickHouse, a columnar OLAP datastore which makes aggregate log analytics queries much more efficient
-   50% lower resource requirement compared to Elastic during ingestion

We have published benchmarks comparing Elastic with SigNoz. Check it out here

### SigNoz vs Loki

-   SigNoz supports aggregations on high-cardinality data over a huge volume while loki doesn’t.
-   SigNoz supports indexes over high cardinality data and has no limitations on the number of indexes, while Loki reaches max streams with a few indexes added to it.
-   Searching over a huge volume of data is difficult and slow in Loki compared to SigNoz

We have published benchmarks comparing Loki with SigNoz. Check it out here

  
  

Contributing
------------

We ❤️ contributions big or small. Please read CONTRIBUTING.md to get started with making contributions to SigNoz.

Not sure how to get started? Just ping us on `#contributing` in our slack community

### Project maintainers

#### Backend

-   Ankit Nayan
-   Nityananda Gohain
-   Srikanth Chekuri
-   Vishal Sharma
-   Shivanshu Raj Shrivastava
-   Ekansh Gupta
-   Aniket Agarwal

#### Frontend

-   Yunus M
-   Vikrant Gupta
-   Sagar Rajput
-   Shaheer Kochai
-   Amlan Kumar Nandy
-   Sahil Khan
-   Aditya Singh
-   Abhi Kumar

#### DevOps

-   Prashant Shahi
-   Vibhu Pandey

  
  

Documentation
-------------

You can find docs at https://signoz.io/docs/. If you need any clarification or find something missing, feel free to raise a GitHub issue with the label `documentation` or reach out to us at the community slack channel.

  
  

Community
---------

Join the slack community to know more about distributed tracing, observability, or SigNoz and to connect with other users and contributors.

If you have any ideas, questions, or any feedback, please share on our Github Discussions

As always, thanks to our amazing contributors!
