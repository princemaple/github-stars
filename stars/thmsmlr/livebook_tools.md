---
project: livebook_tools
stars: 110
description: Powertools for livebook.dev — AI Code Editing, MCP Servers, and Running Livebooks from the CLI
url: https://github.com/thmsmlr/livebook_tools
---

LivebookTools
=============

Livebook Tools is a CLI tool to give you superpowers while working with `.livemd` files.  
Its primary features are:

-   **BYOE (Bring Your Own Editor)** - Sync your `.livemd` files to an open Livebook session so you can edit them in your AI powered code editor, like Cursor.
-   **MCP Server** - A simple model context protocol server for connecting AI coding agents to your Livebook sessions. More on this below.
-   **Run Livebooks from the CLI** - Convert your `.livemd` files to Elixir scripts and run them top to bottom as if they were a `.exs` script. Useful if you want to turn a livebook into a cron job.

Installation
------------

Livebook Tools is an Elixir escript.  
To install it, you can use the `mix escript.install` command.

mix escript.install github thmsmlr/livebook\_tools

Once installed, ensure that the escript directory is on your path.

# for normal elixir users
export PATH="$HOME/.mix/escripts:$PATH"

# for asdf elixir users
for escripts\_dir in $(find "${ASDF\_DATA\_DIR:-$HOME/.asdf}/installs/elixir" -type d -name "escripts" 2>/dev/null); do
  export PATH="$escripts\_dir:$PATH"
done

Running Livebook
----------------

In order for Livebook tools to work properly, it needs to be able to connect to a running Livebook server using distributed Elixir.  
To do this will depend on how you are running Livebook.  
In its simplest form, all you need to do is add the two environment variables to your `~/.bashrc` or `~/.zshrc` file.

export LIVEBOOK\_NODE="livebook@127.0.0.1"
export LIVEBOOK\_COOKIE="secret"

Then when you run the Livebook tools or Livebook, both programs will discover these values and make sure that they can connect to each other. If you're running using Livebook Desktop, then you may need to add these values to the `~/.livebookdesktop.sh` file as well. For more information on Livebook Desktop, check out the Livebook HexDocs.

Setting up MCP Server
---------------------

The MCP Server is a simple model context protocol server that allows you to connect AI coding agents to your Livebook sessions.  
I have personally tested the implementation with Cursor, though it should work with any AI code editor that supports the MCP protocol. The MCP server runs via STDIO, so all you have to do is tell Cursor to connect via the command and it'll auto discover the tools and connect them to it's coding agent. For more information on MCP works with Cursor, check out the Cursor MCP docs.

Useful Tips
-----------

Sometimes you want to customize how the code runs, whether it's running in Livebook or via the command line using `livebook_tools run <file>`. There are some easy code snippets that you can use to detect whether you're running in a live book or on the command line,

\# Detect if we're running in a livebook
is\_livebook \= !String.ends\_with?(\_\_ENV\_\_.file, ".exs")

\# If we're running in a livebook, argv doesn't really make sense, so we'll just return an empty list
argv \= if is\_livebook, do: \[\], else: System.argv()

\# Parse command line arguments
\# We'll use OptionParser to handle both flags and positional arguments
{parsed\_opts, positional\_args, invalid\_opts} \=
  OptionParser.parse(
    argv,
    strict: \[
      dry\_run: :boolean,
      limit: :integer
    \],
    aliases: \[
      d: :dry\_run,
      l: :limit
    \]
  )

\# Extract options with default values, in livebook it'll just use the default values
dry\_run \= Keyword.get(parsed\_opts, :dry\_run, false)
limit \= Keyword.get(parsed\_opts, :limit, 10)
