---
project: yugo
stars: 53
description: Yugo is an easy and high-level IMAP client library for Elixir.
url: https://github.com/Flying-Toast/yugo
---

Yugo
====

Yugo is an easy and high-level IMAP client library for Elixir.

To begin, start a `Yugo.Client` as part of your application's supervision tree:

defmodule MyApp.Application do
  use Application

  @impl true
  def start(\_type, \_args) do
    children \= \[
      {Yugo.Client,
       name: :example\_client,
       server: "imap.example.com",
       username: "me@example.com",
       password: "pa55w0rd"}
    \]

    Supervisor.start\_link(children, strategy: :one\_for\_one)
  end
end

Now you can call `Yugo.subscribe/2` to have your process receive messages whenever a new email arrives that matches the provided `Yugo.Filter`:

\# filter to only notify us about messages containing "hello" or "goodbye" in the subject:
my\_filter \=
  Yugo.Filter.all()
  |> Yugo.Filter.subject\_matches(~r/(hello|goodbye)/)

\# By subscribing, our process will be notified about all future emails that match the filter.
Yugo.subscribe(:example\_client, my\_filter)

receive do
  {:email, \_client, message} \->
    IO.puts("Received an email with subject \`#{message.subject}\`:")
    IO.inspect(message)
end
