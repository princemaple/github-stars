---
project: broadway
stars: 2594
description: Concurrent and multi-stage data ingestion and data processing with Elixir
url: https://github.com/dashbitco/broadway
---

Broadway
========

Build concurrent and multi-stage data ingestion and data processing pipelines with Elixir. Broadway allows developers to consume data efficiently from different sources, known as producers, such as Amazon SQS, Apache Kafka, Google Cloud PubSub, RabbitMQ, and others. Broadway pipelines are long-lived, concurrent, and robust, thanks to the Erlang VM and its actors.

Broadway takes its name from the famous Broadway street in New York City, renowned for its stages, actors, and producers.

To learn more and get started, check out our official website and our guides and docs.

Built-in features
-----------------

Broadway takes the burden of defining concurrent GenStage topologies and provides a simple configuration API that automatically defines concurrent producers, concurrent processing, batch handling, and more, leading to both time and cost efficient ingestion and processing of data. It features:

-   Back-pressure
-   Automatic acknowledgements at the end of the pipeline
-   Batching
-   Fault tolerance
-   Graceful shutdown
-   Built-in testing
-   Custom failure handling
-   Ordering and partitioning
-   Rate-limiting
-   Metrics

### Producers

There are several producers that you can use to integrate with existing services and technologies. See the docs for detailed how-tos and supported producers.

Installation
------------

Add `:broadway` to the list of dependencies in `mix.exs`:

def deps do
  \[
    {:broadway, "~> 1.0"}
  \]
end

A quick example: SQS integration
--------------------------------

Assuming you have added `broadway_sqs` as a dependency and configured your SQS credentials accordingly, you can consume Amazon SQS events in only 20 LOCs:

defmodule MyBroadway do
  use Broadway

  alias Broadway.Message

  def start\_link(\_opts) do
    Broadway.start\_link(\_\_MODULE\_\_,
      name: \_\_MODULE\_\_,
      producer: \[
        module: {BroadwaySQS.Producer, queue\_url: "https://us-east-2.queue.amazonaws.com/100000000001/my\_queue"}
      \],
      processors: \[
        default: \[concurrency: 50\]
      \],
      batchers: \[
        s3: \[concurrency: 5, batch\_size: 10, batch\_timeout: 1000\]
      \]
    )
  end

  def handle\_message(\_processor\_name, message, \_context) do
    message
    |> Message.update\_data(&process\_data/1)
    |> Message.put\_batcher(:s3)
  end

  def handle\_batch(:s3, messages, \_batch\_info, \_context) do
    \# Send batch of messages to S3
  end

  defp process\_data(data) do
    \# Do some calculations, generate a JSON representation, process images.
  end
end

Once your Broadway module is defined, you just need to add it as a child of your application supervision tree as `{MyBroadway, []}`.

Comparison to Flow
------------------

You may also be interested in Flow by Dashbit. Both Broadway and Flow are built on top of GenStage. Flow is a more general abstraction than Broadway that focuses on data as a whole, providing features like aggregation, joins, windows, etc. Broadway focuses on events and on operational features, such as metrics, automatic acknowledgements, failure handling, and so on. Broadway is recommended for continuous, long-running pipelines. Flow works with short- and long-lived data processing.

License
-------

Copyright 2019 Plataformatec  
Copyright 2020 Dashbit

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

```
http://www.apache.org/licenses/LICENSE-2.0
```

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
