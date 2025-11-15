---
project: borb
stars: 3543
description: borb is a library for reading, creating and manipulating PDF files in python.
url: https://github.com/borb-pdf/borb
---

borb
====

`borb` is a powerful and flexible Python library for creating and manipulating PDF files.

📖 Overview
-----------

`borb` provides a pure Python solution for PDF document management, allowing users to read, write, and manipulate PDFs. It models PDF files in a JSON-like structure, using nested lists, dictionaries, and primitives (numbers, strings, booleans, etc.). Created and maintained as a solo project, `borb` prioritizes common PDF use cases for practical and straightforward usage.

✨ Features
----------

Explore `borb`’s capabilities in the examples repository for practical, real-world applications, including:

-   PDF Metadata Management (reading, editing)
-   Text and Image Extraction
-   Adding Annotations (notes, links)
-   Content Manipulation (adding text, images, tables, lists)
-   Page Layout Management with `PageLayout`

…and much more!

🚀 Installation
---------------

Install `borb` directly via `pip`:

pip install borb

To ensure you have the latest version, consider the following commands:

pip uninstall borb
pip install --no-cache borb

👋 Getting Started: Hello World
-------------------------------

Create your first PDF in just a few lines of code with `borb`:

from pathlib import Path
from borb.pdf import Document, Page, PageLayout, SingleColumnLayout, Paragraph, PDF

\# Create an empty Document
d: Document \= Document()

\# Create an empty Page
p: Page \= Page()
d.append\_page(p)

\# Create a PageLayout
l: PageLayout \= SingleColumnLayout(p)

\# Add a Paragraph
l.append\_layout\_element(Paragraph('Hello World!'))

\# Write the PDF
PDF.write(what\=d, where\_to\="assets/output.pdf")

🛠 License
----------

`borb` is dual-licensed under AGPL and a commercial license.

The AGPL (Affero General Public License) is an open-source license, but commercial use cases require a paid license, especially if you intend to:

-   Offer paid PDF services (e.g., PDF generation in cloud applications)
-   Use `borb` in closed-source projects
-   Distribute `borb` in any closed-source product

For more information, contact our sales team.

🙏 Acknowledgements
-------------------

Special thanks to:

-   Aleksander Banasik
-   Benoît Lagae
-   Michael Klink

Your contributions and guidance have been invaluable to `borb`'s development.
