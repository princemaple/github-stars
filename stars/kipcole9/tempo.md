---
project: tempo
stars: 177
description: Date/Time library for Elixir based upon intervals not instants
url: https://github.com/kipcole9/tempo
---

Tempo
=====

> “Time has no divisions to mark its passage, there is never a thunderstorm or blare of trumpets to announce the beginning of a new month or year. Even when a new century begins it is only we mortals who ring bells and fire off pistols.” Thomas Mann, The Magic Mountain, ch. 5, “Whims of Mercurius,” (1924), trans. by Helen T. Lowe-Porter (1928).

A Time library based upon conceptualizing time as intervals rather than instants. A blog of the ideas behind this library is at https://kipcole9.github.io/tempo/.

> #### I'm back to work on Tempo {: .info}
> 
> As of August 2023 I'm actively back at work on Tempo with the aim of a first Hex release by the end of September.

ElixirConf 22 Video on Time Algebra
-----------------------------------

A talk that introduces a unified time type and builds on the idea of time as intervals is now on Youtube.

Project status
--------------

As of August 2023, development is now more active again with an intent to publish on Hex an intial release by the end of September.

Parsing and inspection of almost the entirity of ISO8601 Parts 1 and 2 is now complete including repeat rules (added in August 2023). The main omissions are uncertainty and approximation of time units.

The key items to complete by then are:

1.  Shift math in order to be able to calculate intervals and repeating rules
2.  Tempo comparison using Allens Interval Algebra. Since the conceptual model is all intervals - not instants - comparison is a more complex algebra.
3.  Enumerate Intervals
4.  Implement selections
5.  Implement repeat rules
6.  Add support for the proposed timezone extension - parsing, inspecting and added to structs. Timezone manipulation and conversion may not make it in the initial release.
7.  Documentation. Lots of documentation.

Installation
------------

Tempo is not yet available for installation from `hex.pm`. And since it has basically no functional utility at the moment, installing it would only be for experimentation and amusement.

def deps do
  \[
    {:tempo, "~> 0.1.0", github: "kipcole9/tempo"}
  \]
end

The docs will be found at https://hexdocs.pm/tempo.

Links
-----

-   Computerphile on Timezones
-   RFC3339 and ISO8601 formats
-   Allen's Interval Algebra
