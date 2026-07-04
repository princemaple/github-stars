---
project: signoz
stars: 27691
description: SigNoz is an open-source observability platform native to OpenTelemetry with logs, traces and metrics in a single application. An open-source alternative to DataDog, NewRelic, etc. 🔥 🖥.   👉  Open source Application Performance Monitoring (APM) & Observability tool
url: https://github.com/SigNoz/signoz
---

中文 · Deutsch · Português

SigNoz is an open-source observability platform built on OpenTelemetry. We’re building an enterprise-grade alternative to fragmented monitoring stacks, with logs, metrics, traces, alerts, and dashboards in one place.

### Choose how to run SigNoz

#### SigNoz Cloud (Recommended)

Fully managed SigNoz with a 30-day free trial, no credit card required, usage-based pricing that starts at $49, and regional data hosting.

**Start free →**

#### Enterprise

Enterprise Cloud, BYOC, or Enterprise Self-Hosted with compliance, support, custom retention, RBAC, ingestion controls, data residency, and region selection.

**Explore Enterprise →**

#### Community

Free open-source SigNoz that runs in your own infrastructure. Deploy with Docker, Kubernetes, or Linux and keep full control of your data plane.

**Install SigNoz →**

### What can you monitor?

SigNoz helps teams debug production issues faster by connecting logs, metrics, traces, alerts, dashboards, exceptions, and agent-native workflows in one place.

#### APM Overview

Monitor service latency, error rate, throughput, Apdex, top endpoints, database calls, and external calls.

Learn more: APM documentation

#### Log Management

Ingest, search, aggregate, and correlate logs with traces and metrics using a visual query builder.

Learn more: Log management documentation

#### Metrics and Dashboards

Build dashboards for application, infrastructure, and custom metrics using Query Builder, PromQL, or ClickHouse SQL.

Learn more: Metrics documentation

#### Infrastructure Monitoring

Monitor Kubernetes clusters, pods, nodes, workloads, and host-level CPU, memory, disk, network, logs, and traces.

Learn more: Infrastructure monitoring documentation

#### LLM and AI Observability

Trace LLM apps, RAG pipelines, prompts, tool calls, tokens, latency, and costs alongside application and infrastructure telemetry.

Learn more: LLM observability documentation

#### Agent-Native Observability and MCP

Use the SigNoz MCP server to bring telemetry into coding agents, or use Noz inside SigNoz to investigate incidents, tune alerts, and build dashboards with production context. Noz is available only on SigNoz Cloud.

Learn more: SigNoz MCP server docs · Agent skills docs

#### Distributed Tracing

Follow requests across services with flamegraphs, waterfalls, span events, filters, and trace analytics.

Learn more: Distributed tracing documentation

#### Trace Funnels

Create funnels from traces to understand request-flow drop-offs, failed transitions, and systemic workflow issues.

Learn more: Trace funnels documentation

Also monitor: **exceptions**, **alerts**, **external APIs**, and **integrations** for OpenTelemetry, Prometheus, Kubernetes, cloud providers, language SDKs, application frameworks, databases, and LLM tools.

### Why teams use SigNoz

1.  **OpenTelemetry-native**  
    Instrument once with open standards and keep ownership of your telemetry.
2.  **Correlated signals**  
    Move from service charts to traces, logs, infra metrics, and exceptions without switching tools.
3.  **Single columnar database**  
    Built for high-cardinality, high-volume observability workloads.
4.  **Predictable pricing**  
    No per-host pricing, no user-seat pricing, and no special pricing for custom metrics.
5.  **Enterprise ready**  
    SOC 2 Type II and HIPAA compliance, RBAC, ingestion controls, custom retention, support, BYOC, and self-hosting.

### Getting started

#### Start on Cloud

Create a managed SigNoz workspace and get your first dashboard without running observability infrastructure.

**Start free on SigNoz Cloud**

#### Self-host SigNoz

Run SigNoz in your own infrastructure with Foundry, Docker, Kubernetes, or Linux.

**Foundry** · **Docker** · **Kubernetes** · **Linux**

#### Send data

Instrument applications and infrastructure with OpenTelemetry, Prometheus, language SDKs, and integrations.

**Instrumentation** · **Integrations**

### Comparisons to familiar tools

SigNoz is often adopted by teams moving from a stack of single-purpose tools or commercial platforms with unpredictable pricing.

**Prometheus**  
Good if you just need metrics. SigNoz keeps metrics, logs, traces, dashboards, and alerts together so teams can debug with correlated context.

**Jaeger**  
Jaeger only does distributed tracing. SigNoz adds metrics, logs, trace analytics, dashboards, alerts, exceptions, and trace-to-log workflows.

**Elastic**  
SigNoz uses columnar database for efficient observability analytics and high-cardinality log workloads, with 50% lower resource requirement compared to Elastic during ingestion. Check the detailed study.

**Loki**  
In the linked benchmark, SigNoz indexed all keys in the test setup, while Loki hit max stream errors when more labels were added. Check the detailed study.

Contributing
------------

We ❤️ contributions big or small. Please read CONTRIBUTING.md to get started with making contributions to SigNoz.

Not sure how to get started? **Just ping us on `#contributing` in our slack community.**

As always, thanks to our amazing contributors!
