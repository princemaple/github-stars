---
project: elixir-hl7
stars: 125
description: An Elixir library for working with HL7 v2.x healthcare data 
url: https://github.com/HCA-Healthcare/elixir-hl7
---

Elixir HL7
==========

An Elixir library for working with HL7 v2.x healthcare data.

Elixir HL7 provides functions to parse, query and modify healthcare data that conforms to the HL7 v2.x standards. It should be able to reconstruct any HL7 message without data loss or corruption.

It also provides basic support for reading HL7 file streams with configurable delimiters (MLLP included).

This library has been tested on a wide variety of real-world HL7 messages to ensure correctness and flexibility.

Since many HL7 messages do not strictly conform to the standards specified for each version, the library does not attempt to enforce limits such as character counts or structural expectations.

In fact, HL7 uses implicit hierarchies within segments (by leaving out certain separators) and to group segments (via expected patterns only known to the consuming application).

The majority of the API currently resides in the eponymous `HL7` module.

You can learn more about HL7 here:

-   Wikipedia's HL7 article
-   The official HL7 website (hl7.org)

Full documentation is available at hex.pm.

Please report an issue if something appears to be handled incorrectly.

License
=======

Elixir HL7 source code is released under Apache 2 License. Check the LICENSE file for more information.
