---
project: exceljs
stars: 14868
description: Excel Workbook Manager
url: https://github.com/exceljs/exceljs
---

ExcelJS
=======

Read, manipulate and write spreadsheet data and styles to XLSX and JSON.

Reverse engineered from Excel spreadsheet files as a project.

Translations
============

-   中文文档

Installation
============

npm install exceljs

New Features!
=============

-   Merged Add pivot table with limitations #2551.  
    Many thanks to Protobi and Michael for this contribution!
-   Merged fix: styles rendering in case when "numFmt" is present in conditional formatting rules (resolves #1814) #1815.  
    Many thanks to @andreykrupskii for this contribution!
-   Merged inlineStr cell type support #1575 #1576.  
    Many thanks to @drdmitry for this contribution!
-   Merged Fix parsing of boolean attributes #1849.  
    Many thanks to @bno1 for this contribution!
-   Merged add optional custom auto-filter to table #1670.  
    Many thanks to @thambley for this contribution!
-   Merged Deep copy inherited style #1850.  
    Many thanks to @ikzhr for this contribution!
-   Merged Upgrade actions/cache and actions/setup-node #1846.  
    Many thanks to @cclauss for this contribution!
-   Merged Check object keys in isEqual #1831.  
    Many thanks to @bno1 for this contribution!
-   Merged Add v17 to testing workflow #1856.  
    Many thanks to @Siemienik for this contribution!
-   Merged Upgrade jszip to its latest version to date. This version does not have any vulnerability found by Snyk so far #1895.  
    Many thanks to @ValerioSevilla for this contribution!
-   Merged Update README.md #1677.  
    Many thanks to @xjrcode for this contribution!
-   Merged (docs): set prototype of RegExp correctly. #1700.  
    Many thanks to @joeldenning for this contribution!
-   Merged Added timeouts to github actions #1733.  
    Many thanks to @alexbjorlig for this contribution!
-   Merged fix issue 1676 #1701.  
    Many thanks to @skypesky for this contribution!
-   Merged ExcelJS/ExcelJS#2237 : Update CI Tests, Drop support for Node v8 #2242.  
    Many thanks to @Siemienik for this contribution!
-   Merged Fix types for getWorksheet() #2223.  
    Many thanks to @hfhchan-plb for this contribution!
-   Merged add characters cannot be used for worksheet name #2126.  
    Many thanks to @tkm-kj for this contribution!
-   Merged Fix issue #1753 Reject promise when workbook reader is writing to temporary file stream and error occurs #1756.  
    Many thanks to @pauliusg for this contribution!
-   Merged README.md to have correct link for Streaming XLSX #2186.  
    Many thanks to @wulfsolter for this contribution!
-   Merged Added a polyfill of promise.finally to support lower versions of Firefox. #1982.  
    Many thanks to @DemoJj for this contribution!
-   Merged Fix read this.worksheet before assign it #1934.  
    Many thanks to @ZyqGitHub1 for this contribution!
-   Merged chore: upgrade jszip to ^3.10.1 #2211.  
    Many thanks to @jarrod-cocoon for this contribution!
-   Merged fixed spelling error in README.md file #2208.  
    Many thanks to @HugoP27 for this contribution!
-   Merged fix: Fix xlsx.writeFile() not catching error when error occurs #2244.  
    Many thanks to @zurmokeeper for this contribution!
-   Merged Improve worksheets' naming validation logic. #2257.  
    Many thanks to @Siemienik for this contribution!
-   Merged fix issue 2125 - spliceRows remove last row #2140.  
    Many thanks to @babu-ch for this contribution!
-   Merged fix: fix the loss of column attributes due to incorrect column order #2222.  
    Many thanks to @cpaiyueyue for this contribution!
-   Merged Fix: Sheet Properties Types #2327.  
    Many thanks to @albeniraouf for this contribution!
-   Merged Use node 18 LTS for tsc, and benchmark. Add node 20. to test matrix. … #2354.  
    Many thanks to @Siemienik for this contribution!
-   Merged Add missing tooltip attribute to CellHyperlinkValue index.d.ts #2350.  
    Many thanks to @NiklasPor for this contribution!
-   Merged Increase resilience to generating large workbooks #2320.  
    Many thanks to @hfhchan-plb for this contribution!
-   Merged repair all 'c2fo.io' links ('c2fo.github.io') #2324.  
    Many thanks to @justintunev7 for this contribution!
-   Merged fix: fix type definitions about last column, formula values and protection #2309.  
    Many thanks to @gltjk for this contribution!
-   Merged fix: add spinCount field for WorksheetProtection type #2284.  
    Many thanks to @damingerdai for this contribution!
-   Merged Add type definition for WorksheetModel.merges #2281.  
    Many thanks to @ytjmt for this contribution!

Contributions
=============

Contributions are very welcome! It helps me know what features are desired or what bugs are causing the most pain.

I have just one request; If you submit a pull request for a bugfix, please add a unit-test or integration-test (in the spec folder) that catches the problem. Even a PR that just has a failing test is fine - I can analyse what the test is doing and fix the code from that.

Note: Please try to avoid modifying the package version in a PR. Versions are updated on release and any change will most likely result in merge collisions.

To be clear, all contributions added to this library will be included in the library's MIT licence.

### Let's chat together:

Contents
========

-   Importing
-   Interface
    -   Create a Workbook
    -   Set Workbook Properties
    -   Workbook Views
    -   Add a Worksheet
    -   Remove a Worksheet
    -   Access Worksheets
    -   Worksheet State
    -   Worksheet Properties
    -   Page Setup
    -   Headers and Footers
    -   Worksheet Views
        -   Frozen Views
        -   Split Views
    -   Auto Filters
    -   Columns
    -   Rows
        -   Add Rows
        -   Handling Individual Cells
        -   Merged Cells
        -   Insert Rows
        -   Splice
        -   Duplicate Row
    -   Defined Names
    -   Data Validations
    -   Cell Comments
    -   Tables
    -   Styles
        -   Number Formats
        -   Fonts
        -   Alignment
        -   Borders
        -   Fills
        -   Rich Text
    -   Conditional Formatting
    -   Outline Levels
    -   Images
    -   Sheet Protection
    -   File I/O
        -   XLSX
            -   Reading XLSX
            -   Writing XLSX
        -   CSV
            -   Reading CSV
            -   Writing CSV
        -   Streaming I/O
            -   Streaming XLSX
-   Browser
-   Value Types
    -   Null Value
    -   Merge Cell
    -   Number Value
    -   String Value
    -   Date Value
    -   Hyperlink Value
    -   Formula Value
        -   Shared Formula
        -   Formula Type
        -   Array Formula
    -   Rich Text Value
    -   Boolean Value
    -   Error Value
-   Config
-   Known Issues
-   Release History

Importing⬆
==========

const ExcelJS \= require('exceljs');

ES5 Imports⬆
------------

To use the ES5 transpiled code, for example for node.js versions older than 10, use the dist/es5 path.

const ExcelJS \= require('exceljs/dist/es5');

**Note:** The ES5 build has an implicit dependency on a number of polyfills which are no longer explicitly added by exceljs. You will need to add "core-js" and "regenerator-runtime" to your dependencies and include the following requires in your code before the exceljs import:

// polyfills required by exceljs
require('core-js/modules/es.promise');
require('core-js/modules/es.string.includes');
require('core-js/modules/es.object.assign');
require('core-js/modules/es.object.keys');
require('core-js/modules/es.symbol');
require('core-js/modules/es.symbol.async-iterator');
require('regenerator-runtime/runtime');

const ExcelJS \= require('exceljs/dist/es5');

For IE 11, you'll also need a polyfill to support unicode regex patterns. For example,

const rewritePattern \= require('regexpu-core');
const {generateRegexpuOptions} \= require('@babel/helper-create-regexp-features-plugin/lib/util');

const {RegExp} \= global;
try {
  new RegExp('a', 'u');
} catch (err) {
  global.RegExp \= function(pattern, flags) {
    if (flags && flags.includes('u')) {
      return new RegExp(rewritePattern(pattern, flags, generateRegexpuOptions({flags, pattern})));
    }
    return new RegExp(pattern, flags);
  };
  global.RegExp.prototype \= RegExp.prototype;
}

Browserify⬆
-----------

ExcelJS publishes two browserified bundles inside the dist/ folder:

One with implicit dependencies on core-js polyfills...

<script src\="https://cdnjs.cloudflare.com/ajax/libs/babel-polyfill/6.26.0/polyfill.js"\></script\>
<script src\="exceljs.js"\></script\>

And one without...

<script src\="\--your-project's-pollyfills-here--"\></script\>
<script src\="exceljs.bare.js"\></script\>

Interface⬆
==========

Create a Workbook⬆
------------------

const workbook \= new ExcelJS.Workbook();

Set Workbook Properties⬆
------------------------

workbook.creator \= 'Me';
workbook.lastModifiedBy \= 'Her';
workbook.created \= new Date(1985, 8, 30);
workbook.modified \= new Date();
workbook.lastPrinted \= new Date(2016, 9, 27);

// Set workbook dates to 1904 date system
workbook.properties.date1904 \= true;

Set Calculation Properties⬆
---------------------------

// Force workbook calculation on load
workbook.calcProperties.fullCalcOnLoad \= true;

Workbook Views⬆
---------------

The Workbook views controls how many separate windows Excel will open when viewing the workbook.

workbook.views \= \[
  {
    x: 0, y: 0, width: 10000, height: 20000,
    firstSheet: 0, activeTab: 1, visibility: 'visible'
  }
\]

Add a Worksheet⬆
----------------

const sheet \= workbook.addWorksheet('My Sheet');

Use the second parameter of the addWorksheet function to specify options for the worksheet.

For Example:

// create a sheet with red tab colour
const sheet \= workbook.addWorksheet('My Sheet', {properties:{tabColor:{argb:'FFC0000'}}});

// create a sheet where the grid lines are hidden
const sheet \= workbook.addWorksheet('My Sheet', {views: \[{showGridLines: false}\]});

// create a sheet with the first row and column frozen
const sheet \= workbook.addWorksheet('My Sheet', {views:\[{state: 'frozen', xSplit: 1, ySplit:1}\]});

// Create worksheets with headers and footers
const sheet \= workbook.addWorksheet('My Sheet', {
  headerFooter:{firstHeader: "Hello Exceljs", firstFooter: "Hello World"}
});

// create new sheet with pageSetup settings for A4 - landscape
const worksheet \=  workbook.addWorksheet('My Sheet', {
  pageSetup:{paperSize: 9, orientation:'landscape'}
});

Remove a Worksheet⬆
-------------------

Use the worksheet `id` to remove the sheet from workbook.

For Example:

// Create a worksheet
const sheet \= workbook.addWorksheet('My Sheet');

// Remove the worksheet using worksheet id
workbook.removeWorksheet(sheet.id)

Access Worksheets⬆
------------------

// Iterate over all sheets
// Note: workbook.worksheets.forEach will still work but this is better
workbook.eachSheet(function(worksheet, sheetId) {
  // ...
});

// fetch sheet by name
const worksheet \= workbook.getWorksheet('My Sheet');

// fetch sheet by id
// INFO: Be careful when using it!
// It tries to access to \`worksheet.id\` field. Sometimes (really very often) workbook has worksheets with id not starting from 1.
// For instance It happens when any worksheet has been deleted.
// It's much more safety when you assume that ids are random. And stop to use this function.
// If you need to access all worksheets in a loop please look to the next example.
const worksheet \= workbook.getWorksheet(1);

// access by \`worksheets\` array:
workbook.worksheets\[0\]; //the first one;

It's important to know that `workbook.getWorksheet(1) != Workbook.worksheets[0]` and `workbook.getWorksheet(1) != Workbook.worksheets[1]`, because `workbook.worksheets[0].id` may have any value.

Worksheet State⬆
----------------

// make worksheet visible
worksheet.state \= 'visible';

// make worksheet hidden
worksheet.state \= 'hidden';

// make worksheet hidden from 'hide/unhide' dialog
worksheet.state \= 'veryHidden';

Worksheet Properties⬆
---------------------

Worksheets support a property bucket to allow control over some features of the worksheet.

// create new sheet with properties
const worksheet \= workbook.addWorksheet('sheet', {properties:{tabColor:{argb:'FF00FF00'}}});

// create a new sheet writer with properties
const worksheetWriter \= workbookWriter.addWorksheet('sheet', {properties:{outlineLevelCol:1}});

// adjust properties afterwards (not supported by worksheet-writer)
worksheet.properties.outlineLevelCol \= 2;
worksheet.properties.defaultRowHeight \= 15;

**Supported Properties**

Name

Default

Description

tabColor

undefined

Color of the tabs

outlineLevelCol

0

The worksheet column outline level

outlineLevelRow

0

The worksheet row outline level

defaultRowHeight

15

Default row height

defaultColWidth

(optional)

Default column width

dyDescent

55

TBD

### Worksheet Metrics⬆

Some new metrics have been added to Worksheet...

Name

Description

rowCount

The total row size of the document. Equal to the row number of the last row that has values.

actualRowCount

A count of the number of rows that have values. If a mid-document row is empty, it will not be included in the count.

columnCount

The total column size of the document. Equal to the maximum cell count from all of the rows

actualColumnCount

A count of the number of columns that have values.

Page Setup⬆
-----------

All properties that can affect the printing of a sheet are held in a pageSetup object on the sheet.

// create new sheet with pageSetup settings for A4 - landscape
const worksheet \=  workbook.addWorksheet('sheet', {
  pageSetup:{paperSize: 9, orientation:'landscape'}
});

// create a new sheet writer with pageSetup settings for fit-to-page
const worksheetWriter \= workbookWriter.addWorksheet('sheet', {
  pageSetup:{fitToPage: true, fitToHeight: 5, fitToWidth: 7}
});

// adjust pageSetup settings afterwards
worksheet.pageSetup.margins \= {
  left: 0.7, right: 0.7,
  top: 0.75, bottom: 0.75,
  header: 0.3, footer: 0.3
};

// Set Print Area for a sheet
worksheet.pageSetup.printArea \= 'A1:G20';

// Set multiple Print Areas by separating print areas with '&&'
worksheet.pageSetup.printArea \= 'A1:G10&&A11:G20';

// Repeat specific rows on every printed page
worksheet.pageSetup.printTitlesRow \= '1:3';

// Repeat specific columns on every printed page
worksheet.pageSetup.printTitlesColumn \= 'A:C';

**Supported pageSetup settings**

Name

Default

Description

margins

Whitespace on the borders of the page. Units are inches.

orientation

'portrait'

Orientation of the page - i.e. taller (portrait) or wider (landscape)

horizontalDpi

4294967295

Horizontal Dots per Inch. Default value is -1

verticalDpi

4294967295

Vertical Dots per Inch. Default value is -1

fitToPage

Whether to use fitToWidth and fitToHeight or scale settings. Default is based on presence of these settings in the pageSetup object - if both are present, scale wins (i.e. default will be false)

pageOrder

'downThenOver'

Which order to print the pages - one of \['downThenOver', 'overThenDown'\]

blackAndWhite

false

Print without colour

draft

false

Print with less quality (and ink)

cellComments

'None'

Where to place comments - one of \['atEnd', 'asDisplayed', 'None'\]

errors

'displayed'

Where to show errors - one of \['dash', 'blank', 'NA', 'displayed'\]

scale

100

Percentage value to increase or reduce the size of the print. Active when fitToPage is false

fitToWidth

1

How many pages wide the sheet should print on to. Active when fitToPage is true

fitToHeight

1

How many pages high the sheet should print on to. Active when fitToPage is true

paperSize

What paper size to use (see below)

showRowColHeaders

false

Whether to show the row numbers and column letters

showGridLines

false

Whether to show grid lines

firstPageNumber

Which number to use for the first page

horizontalCentered

false

Whether to center the sheet data horizontally

verticalCentered

false

Whether to center the sheet data vertically

**Example Paper Sizes**

Name

Value

Letter

undefined

Legal

5

Executive

7

A3

8

A4

9

A5

11

B5 (JIS)

13

Envelope #10

20

Envelope DL

27

Envelope C5

28

Envelope B5

34

Envelope Monarch

37

Double Japan Postcard Rotated

82

16K 197x273 mm

119

Headers and Footers⬆
--------------------

Here's how to add headers and footers. The added content is mainly text, such as time, introduction, file information, etc., and you can set the style of the text. In addition, you can set different texts for the first page and even page.

Note: Images are not currently supported.

// Create worksheets with headers and footers
var sheet \= workbook.addWorksheet('sheet', {
  headerFooter:{firstHeader: "Hello Exceljs", firstFooter: "Hello World"}
});
// Create worksheets with headers and footers
var worksheetWriter \= workbookWriter.addWorksheet('sheet', {
  headerFooter:{firstHeader: "Hello Exceljs", firstFooter: "Hello World"}
});
// Set footer (default centered), result: "Page 2 of 16"
worksheet.headerFooter.oddFooter \= "Page &P of &N";

// Set the footer (default centered) to bold, resulting in: "Page 2 of 16"
worksheet.headerFooter.oddFooter \= "Page &P of &N";

// Set the left footer to 18px and italicize. Result: "Page 2 of 16"
worksheet.headerFooter.oddFooter \= "&LPage &P of &N";

// Set the middle header to gray Aril, the result: "52 exceljs"
worksheet.headerFooter.oddHeader \= "&C&KCCCCCC&\\"Aril\\"52 exceljs";

// Set the left, center, and right text of the footer. Result: “Exceljs” in the footer left. “demo.xlsx” in the footer center. “Page 2” in the footer right
worksheet.headerFooter.oddFooter \= "&Lexceljs&C&F&RPage &P";

// Add different header & footer for the first page
worksheet.headerFooter.differentFirst \= true;
worksheet.headerFooter.firstHeader \= "Hello Exceljs";
worksheet.headerFooter.firstFooter \= "Hello World"

**Supported headerFooter settings**

Name

Default

Description

differentFirst

false

Set the value of differentFirst as true, which indicates that headers/footers for first page are different from the other pages

differentOddEven

false

Set the value of differentOddEven as true, which indicates that headers/footers for odd and even pages are different

oddHeader

null

Set header string for odd(default) pages, could format the string

oddFooter

null

Set footer string for odd(default) pages, could format the string

evenHeader

null

Set header string for even pages, could format the string

evenFooter

null

Set footer string for even pages, could format the string

firstHeader

null

Set header string for the first page, could format the string

firstFooter

null

Set footer string for the first page, could format the string

**Script Commands**

Commands

Description

&L

Set position to the left

&C

Set position to the center

&R

Set position to the right

&P

The current page number

&N

The total number of pages

&D

The current date

&T

The current time

&G

A picture

&A

The worksheet name

&F

The file name

&B

Make text bold

&I

Italicize text

&U

Underline text

&"font name"

font name, for example &"Aril"

&font size

font size, for example 12

&KHEXCode

font color, for example &KCCCCCC

Worksheet Views⬆
----------------

Worksheets now support a list of views, that control how Excel presents the sheet:

-   frozen - where a number of rows and columns to the top and left are frozen in place. Only the bottom right section will scroll
-   split - where the view is split into 4 sections, each semi-independently scrollable.

Each view also supports various properties:

Name

Default

Description

state

'normal'

Controls the view state - one of normal, frozen or split

rightToLeft

false

Sets the worksheet view's orientation to right-to-left

activeCell

undefined

The currently selected cell

showRuler

true

Shows or hides the ruler in Page Layout

showRowColHeaders

true

Shows or hides the row and column headers (e.g. A1, B1 at the top and 1,2,3 on the left

showGridLines

true

Shows or hides the gridlines (shown for cells where borders have not been defined)

zoomScale

100

Percentage zoom to use for the view

zoomScaleNormal

100

Normal zoom for the view

style

undefined

Presentation style - one of pageBreakPreview or pageLayout. Note pageLayout is not compatible with frozen views

### Frozen Views⬆

Frozen views support the following extra properties:

Name

Default

Description

xSplit

0

How many columns to freeze. To freeze rows only, set this to 0 or undefined

ySplit

0

How many rows to freeze. To freeze columns only, set this to 0 or undefined

topLeftCell

special

Which cell will be top-left in the bottom-right pane. Note: cannot be a frozen cell. Defaults to first unfrozen cell

worksheet.views \= \[
  {state: 'frozen', xSplit: 2, ySplit: 3, topLeftCell: 'G10', activeCell: 'A1'}
\];

### Split Views⬆

Split views support the following extra properties:

Name

Default

Description

xSplit

0

How many points from the left to place the splitter. To split vertically, set this to 0 or undefined

ySplit

0

How many points from the top to place the splitter. To split horizontally, set this to 0 or undefined

topLeftCell

undefined

Which cell will be top-left in the bottom-right pane.

activePane

undefined

Which pane will be active - one of topLeft, topRight, bottomLeft and bottomRight

worksheet.views \= \[
  {state: 'split', xSplit: 2000, ySplit: 3000, topLeftCell: 'G10', activeCell: 'A1'}
\];

Auto filters⬆
-------------

It is possible to apply an auto filter to your worksheet.

worksheet.autoFilter \= 'A1:C1';

While the range string is the standard form of the autoFilter, the worksheet will also support the following values:

// Set an auto filter from A1 to C1
worksheet.autoFilter \= {
  from: 'A1',
  to: 'C1',
}

// Set an auto filter from the cell in row 3 and column 1
// to the cell in row 5 and column 12
worksheet.autoFilter \= {
  from: {
    row: 3,
    column: 1
  },
  to: {
    row: 5,
    column: 12
  }
}

// Set an auto filter from D3 to the
// cell in row 7 and column 5
worksheet.autoFilter \= {
  from: 'D3',
  to: {
    row: 7,
    column: 5
  }
}

Columns⬆
--------

// Add column headers and define column keys and widths
// Note: these column structures are a workbook-building convenience only,
// apart from the column width, they will not be fully persisted.
worksheet.columns \= \[
  { header: 'Id', key: 'id', width: 10 },
  { header: 'Name', key: 'name', width: 32 },
  { header: 'D.O.B.', key: 'DOB', width: 10, outlineLevel: 1 }
\];

// Access an individual columns by key, letter and 1-based column number
const idCol \= worksheet.getColumn('id');
const nameCol \= worksheet.getColumn('B');
const dobCol \= worksheet.getColumn(3);

// set column properties

// Note: will overwrite cell value C1
dobCol.header \= 'Date of Birth';

// Note: this will overwrite cell values C1:C2
dobCol.header \= \['Date of Birth', 'A.K.A. D.O.B.'\];

// from this point on, this column will be indexed by 'dob' and not 'DOB'
dobCol.key \= 'dob';

dobCol.width \= 15;

// Hide the column if you'd like
dobCol.hidden \= true;

// set an outline level for columns
worksheet.getColumn(4).outlineLevel \= 0;
worksheet.getColumn(5).outlineLevel \= 1;

// columns support a readonly field to indicate the collapsed state based on outlineLevel
expect(worksheet.getColumn(4).collapsed).to.equal(false);
expect(worksheet.getColumn(5).collapsed).to.equal(true);

// iterate over all current cells in this column
dobCol.eachCell(function(cell, rowNumber) {
  // ...
});

// iterate over all current cells in this column including empty cells
dobCol.eachCell({ includeEmpty: true }, function(cell, rowNumber) {
  // ...
});

// add a column of new values
worksheet.getColumn(6).values \= \[1,2,3,4,5\];

// add a sparse column of values
worksheet.getColumn(7).values \= \[,,2,3,,5,,7,,,,11\];

// cut one or more columns (columns to the right are shifted left)
// If column properties have been defined, they will be cut or moved accordingly
// Known Issue: If a splice causes any merged cells to move, the results may be unpredictable
worksheet.spliceColumns(3,2);

// remove one column and insert two more.
// Note: columns 4 and above will be shifted right by 1 column.
// Also: If the worksheet has more rows than values in the column inserts,
//  the rows will still be shifted as if the values existed
const newCol3Values \= \[1,2,3,4,5\];
const newCol4Values \= \['one', 'two', 'three', 'four', 'five'\];
worksheet.spliceColumns(3, 1, newCol3Values, newCol4Values);

Rows⬆
-----

// Get a row object. If it doesn't already exist, a new empty one will be returned
const row \= worksheet.getRow(5);

// Get multiple row objects. If it doesn't already exist, new empty ones will be returned
const rows \= worksheet.getRows(5, 2); // start, length (>0, else undefined is returned)

// Get the last editable row in a worksheet (or undefined if there are none)
const row \= worksheet.lastRow;

// Set a specific row height
row.height \= 42.5;

// make row hidden
row.hidden \= true;

// set an outline level for rows
worksheet.getRow(4).outlineLevel \= 0;
worksheet.getRow(5).outlineLevel \= 1;

// rows support a readonly field to indicate the collapsed state based on outlineLevel
expect(worksheet.getRow(4).collapsed).to.equal(false);
expect(worksheet.getRow(5).collapsed).to.equal(true);

row.getCell(1).value \= 5; // A5's value set to 5
row.getCell('name').value \= 'Zeb'; // B5's value set to 'Zeb' - assuming column 2 is still keyed by name
row.getCell('C').value \= new Date(); // C5's value set to now

// Get a row as a sparse array
// Note: interface change: worksheet.getRow(4) ==> worksheet.getRow(4).values
row \= worksheet.getRow(4).values;
expect(row\[5\]).toEqual('Kyle');

// assign row values by contiguous array (where array element 0 has a value)
row.values \= \[1,2,3\];
expect(row.getCell(1).value).toEqual(1);
expect(row.getCell(2).value).toEqual(2);
expect(row.getCell(3).value).toEqual(3);

// assign row values by sparse array  (where array element 0 is undefined)
const values \= \[\]
values\[5\] \= 7;
values\[10\] \= 'Hello, World!';
row.values \= values;
expect(row.getCell(1).value).toBeNull();
expect(row.getCell(5).value).toEqual(7);
expect(row.getCell(10).value).toEqual('Hello, World!');

// assign row values by object, using column keys
row.values \= {
  id: 13,
  name: 'Thing 1',
  dob: new Date()
};

// Insert a page break below the row
row.addPageBreak();

// Iterate over all rows that have values in a worksheet
worksheet.eachRow(function(row, rowNumber) {
  console.log('Row ' + rowNumber + ' = ' + JSON.stringify(row.values));
});

// Iterate over all rows (including empty rows) in a worksheet
worksheet.eachRow({ includeEmpty: true }, function(row, rowNumber) {
  console.log('Row ' + rowNumber + ' = ' + JSON.stringify(row.values));
});

// Iterate over all non-null cells in a row
row.eachCell(function(cell, colNumber) {
  console.log('Cell ' + colNumber + ' = ' + cell.value);
});

// Iterate over all cells in a row (including empty cells)
row.eachCell({ includeEmpty: true }, function(cell, colNumber) {
  console.log('Cell ' + colNumber + ' = ' + cell.value);
});

// Commit a completed row to stream
row.commit();

// row metrics
const rowSize \= row.cellCount;
const numValues \= row.actualCellCount;

Add Rows⬆
---------

// Add a couple of Rows by key-value, after the last current row, using the column keys
worksheet.addRow({id: 1, name: 'John Doe', dob: new Date(1970,1,1)});
worksheet.addRow({id: 2, name: 'Jane Doe', dob: new Date(1965,1,7)});

// Add a row by contiguous Array (assign to columns A, B & C)
worksheet.addRow(\[3, 'Sam', new Date()\]);

// Add a row by sparse Array (assign to columns A, E & I)
const rowValues \= \[\];
rowValues\[1\] \= 4;
rowValues\[5\] \= 'Kyle';
rowValues\[9\] \= new Date();
worksheet.addRow(rowValues);

// Add a row with inherited style
// This new row will have same style as last row
// And return as row object
const newRow \= worksheet.addRow(rowValues, 'i');

// Add an array of rows
const rows \= \[
  \[5,'Bob',new Date()\], // row by array
  {id:6, name: 'Barbara', dob: new Date()}
\];
// add new rows and return them as array of row objects
const newRows \= worksheet.addRows(rows);

// Add an array of rows with inherited style
// These new rows will have same styles as last row
// and return them as array of row objects
const newRowsStyled \= worksheet.addRows(rows, 'i');

Parameter

Description

Default Value

value/s

The new row/s values

style

'i' for inherit from row above, 'i+' to include empty cells, 'n' for none

_'n'_

Handling Individual Cells⬆
--------------------------

const cell \= worksheet.getCell('C3');

// Modify/Add individual cell
cell.value \= new Date(1968, 5, 1);

// query a cell's type
expect(cell.type).toEqual(Excel.ValueType.Date);

// use string value of cell
myInput.value \= cell.text;

// use html-safe string for rendering...
const html \= '<div>' + cell.html + '</div>';

Merged Cells⬆
-------------

// merge a range of cells
worksheet.mergeCells('A4:B5');

// ... merged cells are linked
worksheet.getCell('B5').value \= 'Hello, World!';
expect(worksheet.getCell('B5').value).toBe(worksheet.getCell('A4').value);
expect(worksheet.getCell('B5').master).toBe(worksheet.getCell('A4'));

// ... merged cells share the same style object
expect(worksheet.getCell('B5').style).toBe(worksheet.getCell('A4').style);
worksheet.getCell('B5').style.font \= myFonts.arial;
expect(worksheet.getCell('A4').style.font).toBe(myFonts.arial);

// unmerging the cells breaks the style links
worksheet.unMergeCells('A4');
expect(worksheet.getCell('B5').style).not.toBe(worksheet.getCell('A4').style);
expect(worksheet.getCell('B5').style.font).not.toBe(myFonts.arial);

// merge by top-left, bottom-right
worksheet.mergeCells('K10', 'M12');

// merge by start row, start column, end row, end column (equivalent to K10:M12)
worksheet.mergeCells(10,11,12,13);

Insert Rows⬆
------------

insertRow(pos, value, style \= 'n')
insertRows(pos, values, style \= 'n')

// Insert a couple of Rows by key-value, shifting down rows every time
worksheet.insertRow(1, {id: 1, name: 'John Doe', dob: new Date(1970,1,1)});
worksheet.insertRow(1, {id: 2, name: 'Jane Doe', dob: new Date(1965,1,7)});

// Insert a row by contiguous Array (assign to columns A, B & C)
worksheet.insertRow(1, \[3, 'Sam', new Date()\]);

// Insert a row by sparse Array (assign to columns A, E & I)
var rowValues \= \[\];
rowValues\[1\] \= 4;
rowValues\[5\] \= 'Kyle';
rowValues\[9\] \= new Date();
// insert new row and return as row object
const insertedRow \= worksheet.insertRow(1, rowValues);

// Insert a row, with inherited style
// This new row will have same style as row on top of it
// And return as row object
const insertedRowInherited \= worksheet.insertRow(1, rowValues, 'i');

// Insert a row, keeping original style
// This new row will have same style as it was previously
// And return as row object
const insertedRowOriginal \= worksheet.insertRow(1, rowValues, 'o');

// Insert an array of rows, in position 1, shifting down current position 1 and later rows by 2 rows
var rows \= \[
  \[5,'Bob',new Date()\], // row by array
  {id:6, name: 'Barbara', dob: new Date()}
\];
// insert new rows and return them as array of row objects
const insertedRows \= worksheet.insertRows(1, rows);

// Insert an array of rows, with inherited style
// These new rows will have same style as row on top of it
// And return them as array of row objects
const insertedRowsInherited \= worksheet.insertRows(1, rows, 'i');

// Insert an array of rows, keeping original style
// These new rows will have same style as it was previously in 'pos' position
const insertedRowsOriginal \= worksheet.insertRows(1, rows, 'o');

Parameter

Description

Default Value

pos

Row number where you want to insert, pushing down all rows from there

value/s

The new row/s values

style

'i' for inherit from row above, , 'i+' to include empty cells, 'o' for original style, 'o+' to include empty cells, 'n' for none

_'n'_

Splice⬆
-------

// Cut one or more rows (rows below are shifted up)
// Known Issue: If a splice causes any merged cells to move, the results may be unpredictable
worksheet.spliceRows(4, 3);

// remove one row and insert two more.
// Note: rows 4 and below will be shifted down by 1 row.
const newRow3Values \= \[1, 2, 3, 4, 5\];
const newRow4Values \= \['one', 'two', 'three', 'four', 'five'\];
worksheet.spliceRows(3, 1, newRow3Values, newRow4Values);

// Cut one or more cells (cells to the right are shifted left)
// Note: this operation will not affect other rows
row.splice(3, 2);

// remove one cell and insert two more (cells to the right of the cut cell will be shifted right)
row.splice(4, 1, 'new value 1', 'new value 2');

Parameter

Description

Default Value

start

Starting point to splice from

count

Number of rows/cells to remove

...inserts

New row/cell values to insert

Duplicate a Row⬆
----------------

duplicateRow(start, amount \= 1, insert \= true)

const wb \= new ExcelJS.Workbook();
const ws \= wb.addWorksheet('duplicateTest');
ws.getCell('A1').value \= 'One';
ws.getCell('A2').value \= 'Two';
ws.getCell('A3').value \= 'Three';
ws.getCell('A4').value \= 'Four';

// This line will duplicate the row 'One' twice but it will replace rows 'Two' and 'Three'
// if third param was true so it would insert 2 new rows with the values and styles of row 'One'
ws.duplicateRow(1,2,false);

Parameter

Description

Default Value

start

Row number you want to duplicate (first in excel is 1)

amount

The times you want to duplicate the row

1

insert

_true_ if you want to insert new rows for the duplicates, or _false_ if you want to replace them

_true_

Defined Names⬆
--------------

Individual cells (or multiple groups of cells) can have names assigned to them. The names can be used in formulas and data validation (and probably more).

// assign (or get) a name for a cell (will overwrite any other names that cell had)
worksheet.getCell('A1').name \= 'PI';
expect(worksheet.getCell('A1').name).to.equal('PI');

// assign (or get) an array of names for a cell (cells can have more than one name)
worksheet.getCell('A1').names \= \['thing1', 'thing2'\];
expect(worksheet.getCell('A1').names).to.have.members(\['thing1', 'thing2'\]);

// remove a name from a cell
worksheet.getCell('A1').removeName('thing1');
expect(worksheet.getCell('A1').names).to.have.members(\['thing2'\]);

Data Validations⬆
-----------------

Cells can define what values are valid or not and provide prompting to the user to help guide them.

Validation types can be one of the following:

Type

Description

list

Define a discrete set of valid values. Excel will offer these in a dropdown for easy entry

whole

The value must be a whole number

decimal

The value must be a decimal number

textLength

The value may be text but the length is controlled

custom

A custom formula controls the valid values

For types other than list or custom, the following operators affect the validation:

Operator

Description

between

Values must lie between formula results

notBetween

Values must not lie between formula results

equal

Value must equal formula result

notEqual

Value must not equal formula result

greaterThan

Value must be greater than formula result

lessThan

Value must be less than formula result

greaterThanOrEqual

Value must be greater than or equal to formula result

lessThanOrEqual

Value must be less than or equal to formula result

// Specify list of valid values (One, Two, Three, Four).
// Excel will provide a dropdown with these values.
worksheet.getCell('A1').dataValidation \= {
  type: 'list',
  allowBlank: true,
  formulae: \['"One,Two,Three,Four"'\]
};

// Specify list of valid values from a range.
// Excel will provide a dropdown with these values.
worksheet.getCell('A1').dataValidation \= {
  type: 'list',
  allowBlank: true,
  formulae: \['$D$5:$F$5'\]
};

// Specify Cell must be a whole number that is not 5.
// Show the user an appropriate error message if they get it wrong
worksheet.getCell('A1').dataValidation \= {
  type: 'whole',
  operator: 'notEqual',
  showErrorMessage: true,
  formulae: \[5\],
  errorStyle: 'error',
  errorTitle: 'Five',
  error: 'The value must not be Five'
};

// Specify Cell must be a decimal number between 1.5 and 7.
// Add 'tooltip' to help guid the user
worksheet.getCell('A1').dataValidation \= {
  type: 'decimal',
  operator: 'between',
  allowBlank: true,
  showInputMessage: true,
  formulae: \[1.5, 7\],
  promptTitle: 'Decimal',
  prompt: 'The value must between 1.5 and 7'
};

// Specify Cell must be have a text length less than 15
worksheet.getCell('A1').dataValidation \= {
  type: 'textLength',
  operator: 'lessThan',
  showErrorMessage: true,
  allowBlank: true,
  formulae: \[15\]
};

// Specify Cell must be have be a date before 1st Jan 2016
worksheet.getCell('A1').dataValidation \= {
  type: 'date',
  operator: 'lessThan',
  showErrorMessage: true,
  allowBlank: true,
  formulae: \[new Date(2016,0,1)\]
};

Cell Comments⬆
--------------

Add old style comment to a cell

// plain text note
worksheet.getCell('A1').note \= 'Hello, ExcelJS!';

// colourful formatted note
ws.getCell('B1').note \= {
  texts: \[
    {'font': {'size': 12, 'color': {'theme': 0}, 'name': 'Calibri', 'family': 2, 'scheme': 'minor'}, 'text': 'This is '},
    {'font': {'italic': true, 'size': 12, 'color': {'theme': 0}, 'name': 'Calibri', 'scheme': 'minor'}, 'text': 'a'},
    {'font': {'size': 12, 'color': {'theme': 1}, 'name': 'Calibri', 'family': 2, 'scheme': 'minor'}, 'text': ' '},
    {'font': {'size': 12, 'color': {'argb': 'FFFF6600'}, 'name': 'Calibri', 'scheme': 'minor'}, 'text': 'colorful'},
    {'font': {'size': 12, 'color': {'theme': 1}, 'name': 'Calibri', 'family': 2, 'scheme': 'minor'}, 'text': ' text '},
    {'font': {'size': 12, 'color': {'argb': 'FFCCFFCC'}, 'name': 'Calibri', 'scheme': 'minor'}, 'text': 'with'},
    {'font': {'size': 12, 'color': {'theme': 1}, 'name': 'Calibri', 'family': 2, 'scheme': 'minor'}, 'text': ' in-cell '},
    {'font': {'bold': true, 'size': 12, 'color': {'theme': 1}, 'name': 'Calibri', 'family': 2, 'scheme': 'minor'}, 'text': 'format'},
  \],
  margins: {
    insetmode: 'custom',
    inset: \[0.25, 0.25, 0.35, 0.35\]
  },
  protection: {
    locked: True,
    lockText: False
  },
  editAs: 'twoCells',
};

### Cell Comments Properties⬆

The following table defines the properties supported by cell comments.

Field

Required

Default Value

Description

texts

Y

The text of the comment

margins

N

{}

Determines the value of margins for automatic or custom cell comments

protection

N

{}

Specifying the lock status of objects and object text using protection attributes

editAs

N

'absolute'

Use the 'editAs' attribute to specify how the annotation is anchored to the cell

### Cell Comments Margins

Determine the page margin setting mode of the cell annotation, automatic or custom mode.

ws.getCell('B1').note.margins \= {
  insetmode: 'custom',
  inset: \[0.25, 0.25, 0.35, 0.35\]
}

### Supported Margins Properties⬆

Property

Required

Default Value

Description

insetmode

N

'auto'

Determines whether comment margins are set automatically and the value is 'auto' or 'custom'

inset

N

\[0.13, 0.13, 0.25, 0.25\]

Whitespace on the borders of the comment. Units are centimeter. Direction is left, top, right, bottom

Note: This `inset` setting takes effect only when the value of `insetmode` is 'custom'.

### Cell Comments Protection

Specifying the lock status of objects and object text using protection attributes.

ws.getCell('B1').note.protection \= {
  locked: 'False',
  lockText: 'False',
};

### Supported Protection Properties⬆

Property

Required

Default Value

Description

locked

N

'True'

This element specifies that the object is locked when the sheet is protected

lockText

N

'True'

This element specifies that the text of the object is locked

Note: Locked objects are valid only when the worksheet is protected.

### Cell Comments EditAs⬆

The cell comments can also have the property 'editAs' which will control how the comments is anchored to the cell(s). It can have one of the following values:

ws.getCell('B1').note.editAs \= 'twoCells';

Value

Description

twoCells

It specifies that the size and position of the note varies with cells

oneCells

It specifies that the size of the note is fixed and the position changes with the cell

absolute

This is the default. Comments will not be moved or sized with cells

Tables⬆
-------

Tables allow for in-sheet manipulation of tabular data.

To add a table to a worksheet, define a table model and call addTable:

// add a table to a sheet
ws.addTable({
  name: 'MyTable',
  ref: 'A1',
  headerRow: true,
  totalsRow: true,
  style: {
    theme: 'TableStyleDark3',
    showRowStripes: true,
  },
  columns: \[
    {name: 'Date', totalsRowLabel: 'Totals:', filterButton: true},
    {name: 'Amount', totalsRowFunction: 'sum', filterButton: false},
  \],
  rows: \[
    \[new Date('2019-07-20'), 70.10\],
    \[new Date('2019-07-21'), 70.60\],
    \[new Date('2019-07-22'), 70.10\],
  \],
});

Note: Adding a table to a worksheet will modify the sheet by placing headers and row data to the sheet. Any data on the sheet covered by the resulting table (including headers and totals) will be overwritten.

### Table Properties⬆

The following table defines the properties supported by tables.

Table Property

Description

Required

Default Value

name

The name of the table

Y

displayName

The display name of the table

N

name

ref

Top left cell of the table

Y

headerRow

Show headers at top of table

N

true

totalsRow

Show totals at bottom of table

N

false

style

Extra style properties

N

{}

columns

Column definitions

Y

rows

Rows of data

Y

### Table Style Properties⬆

The following table defines the properties supported within the table style property.

Style Property

Description

Required

Default Value

theme

The colour theme of the table

N

'TableStyleMedium2'

showFirstColumn

Highlight the first column (bold)

N

false

showLastColumn

Highlight the last column (bold)

N

false

showRowStripes

Alternate rows shown with background colour

N

false

showColumnStripes

Alternate rows shown with background colour

N

false

### Table Column Properties⬆

The following table defines the properties supported within each table column.

Column Property

Description

Required

Default Value

name

The name of the column, also used in the header

Y

filterButton

Switches the filter control in the header

N

false

totalsRowLabel

Label to describe the totals row (first column)

N

'Total'

totalsRowFunction

Name of the totals function

N

'none'

totalsRowFormula

Optional formula for custom functions

N

### Totals Functions⬆

The following table list the valid values for the totalsRowFunction property defined by columns. If any value other than 'custom' is used, it is not necessary to include the associated formula as this will be inserted by the table.

Totals Functions

Description

none

No totals function for this column

average

Compute average for the column

countNums

Count the entries that are numbers

count

Count of entries

max

The maximum value in this column

min

The minimum value in this column

stdDev

The standard deviation for this column

var

The variance for this column

sum

The sum of entries for this column

custom

A custom formula. Requires an associated totalsRowFormula value.

### Table Style Themes⬆

Valid theme names follow the following pattern:

-   "TableStyle\[Shade\]\[Number\]"

Shades, Numbers can be one of:

-   Light, 1-21
-   Medium, 1-28
-   Dark, 1-11

For no theme, use the value null.

Note: custom table themes are not supported by exceljs yet.

### Modifying Tables⬆

Tables support a set of manipulation functions that allow data to be added or removed and some properties to be changed. Since many of these operations may have on-sheet effects, the changes must be committed once complete.

All index values in the table are zero based, so the first row number and first column number is 0.

**Adding or Removing Headers and Totals**

const table \= ws.getTable('MyTable');

// turn header row on
table.headerRow \= true;

// turn totals row off
table.totalsRow \= false;

// commit the table changes into the sheet
table.commit();

**Relocating a Table**

const table \= ws.getTable('MyTable');

// table top-left move to D4
table.ref \= 'D4';

// commit the table changes into the sheet
table.commit();

**Adding and Removing Rows**

const table \= ws.getTable('MyTable');

// remove first two rows
table.removeRows(0, 2);

// insert new rows at index 5
table.addRow(\[new Date('2019-08-05'), 5, 'Mid'\], 5);

// append new row to bottom of table
table.addRow(\[new Date('2019-08-10'), 10, 'End'\]);

// commit the table changes into the sheet
table.commit();

**Adding and Removing Columns**

const table \= ws.getTable('MyTable');

// remove second column
table.removeColumns(1, 1);

// insert new column (with data) at index 1
table.addColumn(
  {name: 'Letter', totalsRowFunction: 'custom', totalsRowFormula: 'ROW()', totalsRowResult: 6, filterButton: true},
  \['a', 'b', 'c', 'd'\],
  2
);

// commit the table changes into the sheet
table.commit();

**Change Column Properties**

const table \= ws.getTable('MyTable');

// Get Column Wrapper for second column
const column \= table.getColumn(1);

// set some properties
column.name \= 'Code';
column.filterButton \= true;
column.style \= {font:{bold: true, name: 'Comic Sans MS'}};
column.totalsRowLabel \= 'Totals';
column.totalsRowFunction \= 'custom';
column.totalsRowFormula \= 'ROW()';
column.totalsRowResult \= 10;

// commit the table changes into the sheet
table.commit();

Styles⬆
-------

Cells, Rows and Columns each support a rich set of styles and formats that affect how the cells are displayed.

Styles are set by assigning the following properties:

-   numFmt
-   font
-   alignment
-   border
-   fill

// assign a style to a cell
ws.getCell('A1').numFmt \= '0.00%';

// Apply styles to worksheet columns
ws.columns \= \[
  { header: 'Id', key: 'id', width: 10 },
  { header: 'Name', key: 'name', width: 32, style: { font: { name: 'Arial Black' } } },
  { header: 'D.O.B.', key: 'DOB', width: 10, style: { numFmt: 'dd/mm/yyyy' } }
\];

// Set Column 3 to Currency Format
ws.getColumn(3).numFmt \= '"£"#,##0.00;\[Red\]\\-"£"#,##0.00';

// Set Row 2 to Comic Sans.
ws.getRow(2).font \= { name: 'Comic Sans MS', family: 4, size: 16, underline: 'double', bold: true };

When a style is applied to a row or column, it will be applied to all currently existing cells in that row or column. Also, any new cell that is created will inherit its initial styles from the row and column it belongs to.

If a cell's row and column both define a specific style (e.g. font), the cell will use the row style over the column style. However if the row and column define different styles (e.g. column.numFmt and row.font), the cell will inherit the font from the row and the numFmt from the column.

Caveat: All the above properties (with the exception of numFmt, which is a string), are JS object structures. If the same style object is assigned to more than one spreadsheet entity, then each entity will share the same style object. If the style object is later modified before the spreadsheet is serialized, then all entities referencing that style object will be modified too. This behaviour is intended to prioritize performance by reducing the number of JS objects created. If you want the style objects to be independent, you will need to clone them before assigning them. Also, by default, when a document is read from file (or stream) if spreadsheet entities share similar styles, then they will reference the same style object too.

### Number Formats⬆

// display value as '1 3/5'
ws.getCell('A1').value \= 1.6;
ws.getCell('A1').numFmt \= '# ?/?';

// display value as '1.60%'
ws.getCell('B1').value \= 0.016;
ws.getCell('B1').numFmt \= '0.00%';

### Fonts⬆

// for the wannabe graphic designers out there
ws.getCell('A1').font \= {
  name: 'Comic Sans MS',
  family: 4,
  size: 16,
  underline: true,
  bold: true
};

// for the graduate graphic designers...
ws.getCell('A2').font \= {
  name: 'Arial Black',
  color: { argb: 'FF00FF00' },
  family: 2,
  size: 14,
  italic: true
};

// for the vertical align
ws.getCell('A3').font \= {
  vertAlign: 'superscript'
};

// note: the cell will store a reference to the font object assigned.
// If the font object is changed afterwards, the cell font will change also...
const font \= { name: 'Arial', size: 12 };
ws.getCell('A3').font \= font;
font.size \= 20; // Cell A3 now has font size 20!

// Cells that share similar fonts may reference the same font object after
// the workbook is read from file or stream

Font Property

Description

Example Value(s)

name

Font name.

'Arial', 'Calibri', etc.

family

Font family for fallback. An integer value.

1 - Serif, 2 - Sans Serif, 3 - Mono, Others - unknown

scheme

Font scheme.

'minor', 'major', 'none'

charset

Font charset. An integer value.

1, 2, etc.

size

Font size. An integer value.

9, 10, 12, 16, etc.

color

Colour description, an object containing an ARGB value.

{ argb: 'FFFF0000'}

bold

Font **weight**

true, false

italic

Font _slope_

true, false

underline

Font underline style

true, false, 'none', 'single', 'double', 'singleAccounting', 'doubleAccounting'

strike

Font strikethrough

true, false

outline

Font outline

true, false

vertAlign

Vertical align

'superscript', 'subscript'

### Alignment⬆

// set cell alignment to top-left, middle-center, bottom-right
ws.getCell('A1').alignment \= { vertical: 'top', horizontal: 'left' };
ws.getCell('B1').alignment \= { vertical: 'middle', horizontal: 'center' };
ws.getCell('C1').alignment \= { vertical: 'bottom', horizontal: 'right' };

// set cell to wrap-text
ws.getCell('D1').alignment \= { wrapText: true };

// set cell indent to 1
ws.getCell('E1').alignment \= { indent: 1 };

// set cell text rotation to 30deg upwards, 45deg downwards and vertical text
ws.getCell('F1').alignment \= { textRotation: 30 };
ws.getCell('G1').alignment \= { textRotation: \-45 };
ws.getCell('H1').alignment \= { textRotation: 'vertical' };

**Valid Alignment Property Values**

horizontal

vertical

wrapText

shrinkToFit

indent

readingOrder

textRotation

left

top

true

true

integer

rtl

0 to 90

center

middle

false

false

ltr

\-1 to -90

right

bottom

vertical

fill

distributed

justify

justify

centerContinuous

distributed

### Borders⬆

// set single thin border around A1
ws.getCell('A1').border \= {
  top: {style:'thin'},
  left: {style:'thin'},
  bottom: {style:'thin'},
  right: {style:'thin'}
};

// set double thin green border around A3
ws.getCell('A3').border \= {
  top: {style:'double', color: {argb:'FF00FF00'}},
  left: {style:'double', color: {argb:'FF00FF00'}},
  bottom: {style:'double', color: {argb:'FF00FF00'}},
  right: {style:'double', color: {argb:'FF00FF00'}}
};

// set thick red cross in A5
ws.getCell('A5').border \= {
  diagonal: {up: true, down: true, style:'thick', color: {argb:'FFFF0000'}}
};

**Valid Border Styles**

-   thin
-   dotted
-   dashDot
-   hair
-   dashDotDot
-   slantDashDot
-   mediumDashed
-   mediumDashDotDot
-   mediumDashDot
-   medium
-   double
-   thick

### Fills⬆

// fill A1 with red darkVertical stripes
ws.getCell('A1').fill \= {
  type: 'pattern',
  pattern:'darkVertical',
  fgColor:{argb:'FFFF0000'}
};

// fill A2 with yellow dark trellis and blue behind
ws.getCell('A2').fill \= {
  type: 'pattern',
  pattern:'darkTrellis',
  fgColor:{argb:'FFFFFF00'},
  bgColor:{argb:'FF0000FF'}
};

// fill A3 with solid coral
ws.getCell('A3').fill \= {
  type: 'pattern',
  pattern:'solid',
  fgColor:{argb:'F08080'},
};

// fill A4 with blue-white-blue gradient from left to right
ws.getCell('A4').fill \= {
  type: 'gradient',
  gradient: 'angle',
  degree: 0,
  stops: \[
    {position:0, color:{argb:'FF0000FF'}},
    {position:0.5, color:{argb:'FFFFFFFF'}},
    {position:1, color:{argb:'FF0000FF'}}
  \]
};

// fill A5 with red-green gradient from center
ws.getCell('A5').fill \= {
  type: 'gradient',
  gradient: 'path',
  center:{left:0.5,top:0.5},
  stops: \[
    {position:0, color:{argb:'FFFF0000'}},
    {position:1, color:{argb:'FF00FF00'}}
  \]
};

#### Pattern Fills⬆

Property

Required

Description

type

Y

Value: 'pattern'  
Specifies this fill uses patterns

pattern

Y

Specifies type of pattern (see Valid Pattern Types below)

fgColor

N

Specifies the pattern foreground color. Default is black.

bgColor

N

Specifies the pattern background color. Default is white.

Note: If you want to fill a cell using the `solid` pattern, then you don't need to specify `bgColor`. See example above for cell `A3` with a `solid` pattern and a coral `fgColor`.

**Valid Pattern Types**

-   none
-   solid
-   darkGray
-   mediumGray
-   lightGray
-   gray125
-   gray0625
-   darkHorizontal
-   darkVertical
-   darkDown
-   darkUp
-   darkGrid
-   darkTrellis
-   lightHorizontal
-   lightVertical
-   lightDown
-   lightUp
-   lightGrid
-   lightTrellis

#### Gradient Fills⬆

Property

Required

Description

type

Y

Value: 'gradient'  
Specifies this fill uses gradients

gradient

Y

Specifies gradient type. One of \['angle', 'path'\]

degree

angle

For 'angle' gradient, specifies the direction of the gradient. 0 is from the left to the right. Values from 1 - 359 rotates the direction clockwise

center

path

For 'path' gradient. Specifies the relative coordinates for the start of the path. 'left' and 'top' values range from 0 to 1

stops

Y

Specifies the gradient colour sequence. Is an array of objects containing position and color starting with position 0 and ending with position 1. Intermediary positions may be used to specify other colours on the path.

**Caveats**

Using the interface above it may be possible to create gradient fill effects not possible using the XLSX editor program. For example, Excel only supports angle gradients of 0, 45, 90 and 135. Similarly the sequence of stops may also be limited by the UI with positions \[0,1\] or \[0,0.5,1\] as the only options. Take care with this fill to be sure it is supported by the target XLSX viewers.

### Rich Text⬆

Individual cells now support rich text or in-cell formatting. Rich text values can control the font properties of any number of sub-strings within the text value. See Fonts for a complete list of details on what font properties are supported.

ws.getCell('A1').value \= {
  'richText': \[
    {'font': {'size': 12,'color': {'theme': 0},'name': 'Calibri','family': 2,'scheme': 'minor'},'text': 'This is '},
    {'font': {'italic': true,'size': 12,'color': {'theme': 0},'name': 'Calibri','scheme': 'minor'},'text': 'a'},
    {'font': {'size': 12,'color': {'theme': 1},'name': 'Calibri','family': 2,'scheme': 'minor'},'text': ' '},
    {'font': {'size': 12,'color': {'argb': 'FFFF6600'},'name': 'Calibri','scheme': 'minor'},'text': 'colorful'},
    {'font': {'size': 12,'color': {'theme': 1},'name': 'Calibri','family': 2,'scheme': 'minor'},'text': ' text '},
    {'font': {'size': 12,'color': {'argb': 'FFCCFFCC'},'name': 'Calibri','scheme': 'minor'},'text': 'with'},
    {'font': {'size': 12,'color': {'theme': 1},'name': 'Calibri','family': 2,'scheme': 'minor'},'text': ' in-cell '},
    {'font': {'bold': true,'size': 12,'color': {'theme': 1},'name': 'Calibri','family': 2,'scheme': 'minor'},'text': 'format'}
  \]
};

expect(ws.getCell('A1').text).to.equal('This is a colorful text with in-cell format');
expect(ws.getCell('A1').type).to.equal(Excel.ValueType.RichText);

### Cell Protection⬆

Cell level protection can be modified using the protection property.

ws.getCell('A1').protection \= {
  locked: false,
  hidden: true,
};

**Supported Protection Properties**

Property

Default

Description

locked

true

Specifies whether a cell will be locked if the sheet is protected.

hidden

false

Specifies whether a cell's formula will be visible if the sheet is protected.

Conditional Formatting⬆
-----------------------

Conditional formatting allows a sheet to show specific styles, icons, etc depending on cell values or any arbitrary formula.

Conditional formatting rules are added at the sheet level and will typically cover a range of cells.

Multiple rules can be applied to a given cell range and each rule will apply its own style.

If multiple rules affect a given cell, the rule priority value will determine which rule wins out if competing styles collide. The rule with the lower priority value wins. If priority values are not specified for a given rule, ExcelJS will assign them in ascending order.

Note: at present, only a subset of conditional formatting rules are supported. Specifically, only the formatting rules that do not require XML rendering inside an <extLst> element. This means that datasets and three specific icon sets (3Triangles, 3Stars, 5Boxes) are not supported.

// add a checkerboard pattern to A1:E7 based on row + col being even or odd
worksheet.addConditionalFormatting({
  ref: 'A1:E7',
  rules: \[
    {
      type: 'expression',
      formulae: \['MOD(ROW()+COLUMN(),2)=0'\],
      style: {fill: {type: 'pattern', pattern: 'solid', bgColor: {argb: 'FF00FF00'}}},
    }
  \]
})

**Supported Conditional Formatting Rule Types**

Type

Description

expression

Any custom function may be used to activate the rule.

cellIs

Compares cell value with supplied formula using specified operator

top10

Applies formatting to cells with values in top (or bottom) ranges

aboveAverage

Applies formatting to cells with values above (or below) average

colorScale

Applies a coloured background to cells based on where their values lie in the range

iconSet

Adds one of a range of icons to cells based on value

containsText

Applies formatting based on whether cell a specific text

timePeriod

Applies formatting based on whether cell datetime value lies within a specified range

### Expression⬆

Field

Optional

Default

Description

type

'expression'

priority

Y

<auto>

determines priority ordering of styles

formulae

array of 1 formula string that returns a true/false value. To reference the cell value, use the top-left cell address

style

style structure to apply if the formula returns true

### Cell Is⬆

Field

Optional

Default

Description

type

'cellIs'

priority

Y

<auto>

determines priority ordering of styles

operator

how to compare cell value with formula result

formulae

array of 1 formula string that returns the value to compare against each cell

style

style structure to apply if the comparison returns true

**Cell Is Operators**

Operator

Description

equal

Apply format if cell value equals formula value

greaterThan

Apply format if cell value is greater than formula value

lessThan

Apply format if cell value is less than formula value

between

Apply format if cell value is between two formula values (inclusive)

### Top 10⬆

Field

Optional

Default

Description

type

'top10'

priority

Y

<auto>

determines priority ordering of styles

rank

Y

10

specifies how many top (or bottom) values are included in the formatting

percent

Y

false

if true, the rank field is a percentage, not an absolute

bottom

Y

false

if true, the bottom values are included instead of the top

style

style structure to apply if the comparison returns true

### Above Average⬆

Field

Optional

Default

Description

type

'aboveAverage'

priority

Y

<auto>

determines priority ordering of styles

aboveAverage

Y

false

if true, the rank field is a percentage, not an absolute

style

style structure to apply if the comparison returns true

### Color Scale⬆

Field

Optional

Default

Description

type

'colorScale'

priority

Y

<auto>

determines priority ordering of styles

cfvo

array of 2 to 5 Conditional Formatting Value Objects specifying way-points in the value range

color

corresponding array of colours to use at given way points

style

style structure to apply if the comparison returns true

### Icon Set⬆

Field

Optional

Default

Description

type

'iconSet'

priority

Y

<auto>

determines priority ordering of styles

iconSet

Y

3TrafficLights

name of icon set to use

showValue

true

Specifies whether the cells in the applied range display the icon and cell value, or the icon only

reverse

false

Specifies whether the icons in the icon set specified in iconSet are show in reserve order. If custom equals "true" this value must be ignored

custom

false

Specifies whether a custom set of icons is used

cfvo

array of 2 to 5 Conditional Formatting Value Objects specifying way-points in the value range

style

style structure to apply if the comparison returns true

### Data Bar⬆

Field

Optional

Default

Description

type

'dataBar'

priority

Y

<auto>

determines priority ordering of styles

minLength

0

Specifies the length of the shortest data bar in this conditional formatting range

maxLength

100

Specifies the length of the longest data bar in this conditional formatting range

showValue

true

Specifies whether the cells in the conditional formatting range display both the data bar and the numeric value or the data bar

gradient

true

Specifies whether the data bar has a gradient fill

border

true

Specifies whether the data bar has a border

negativeBarColorSameAsPositive

true

Specifies whether the data bar has a negative bar color that is different from the positive bar color

negativeBarBorderColorSameAsPositive

true

Specifies whether the data bar has a negative border color that is different from the positive border color

axisPosition

'auto'

Specifies the axis position for the data bar

direction

'leftToRight'

Specifies the direction of the data bar

cfvo

array of 2 to 5 Conditional Formatting Value Objects specifying way-points in the value range

style

style structure to apply if the comparison returns true

### Contains Text⬆

Field

Optional

Default

Description

type

'containsText'

priority

Y

<auto>

determines priority ordering of styles

operator

type of text comparison

text

text to search for

style

style structure to apply if the comparison returns true

**Contains Text Operators**

Operator

Description

containsText

Apply format if cell value contains the value specified in the 'text' field

containsBlanks

Apply format if cell value contains blanks

notContainsBlanks

Apply format if cell value does not contain blanks

containsErrors

Apply format if cell value contains errors

notContainsErrors

Apply format if cell value does not contain errors

### Time Period⬆

Field

Optional

Default

Description

type

'timePeriod'

priority

Y

<auto>

determines priority ordering of styles

timePeriod

what time period to compare cell value to

style

style structure to apply if the comparison returns true

**Time Periods**

Time Period

Description

lastWeek

Apply format if cell value falls within the last week

thisWeek

Apply format if cell value falls in this week

nextWeek

Apply format if cell value falls in the next week

yesterday

Apply format if cell value is equal to yesterday

today

Apply format if cell value is equal to today

tomorrow

Apply format if cell value is equal to tomorrow

last7Days

Apply format if cell value falls within the last 7 days

lastMonth

Apply format if cell value falls in last month

thisMonth

Apply format if cell value falls in this month

nextMonth

Apply format if cell value falls in next month

Outline Levels⬆
---------------

Excel supports outlining; where rows or columns can be expanded or collapsed depending on what level of detail the user wishes to view.

Outline levels can be defined in column setup:

worksheet.columns \= \[
  { header: 'Id', key: 'id', width: 10 },
  { header: 'Name', key: 'name', width: 32 },
  { header: 'D.O.B.', key: 'DOB', width: 10, outlineLevel: 1 }
\];

Or directly on the row or column

worksheet.getColumn(3).outlineLevel \= 1;
worksheet.getRow(3).outlineLevel \= 1;

The sheet outline levels can be set on the worksheet

// set column outline level
worksheet.properties.outlineLevelCol \= 1;

// set row outline level
worksheet.properties.outlineLevelRow \= 1;

Note: adjusting outline levels on rows or columns or the outline levels on the worksheet will incur a side effect of also modifying the collapsed property of all rows or columns affected by the property change. E.g.:

worksheet.properties.outlineLevelCol \= 1;

worksheet.getColumn(3).outlineLevel \= 1;
expect(worksheet.getColumn(3).collapsed).to.be.true;

worksheet.properties.outlineLevelCol \= 2;
expect(worksheet.getColumn(3).collapsed).to.be.false;

The outline properties can be set on the worksheet

worksheet.properties.outlineProperties \= {
  summaryBelow: false,
  summaryRight: false,
};

Images⬆
-------

Adding images to a worksheet is a two-step process. First, the image is added to the workbook via the addImage() function which will also return an imageId value. Then, using the imageId, the image can be added to the worksheet either as a tiled background or covering a cell range.

Note: As of this version, adjusting or transforming the image is not supported and images are not supported in streaming mode.

### Add Image to Workbook⬆

The Workbook.addImage function supports adding images by filename or by Buffer. Note that in both cases, the extension must be specified. Valid extension values include 'jpeg', 'png', 'gif'.

// add image to workbook by filename
const imageId1 \= workbook.addImage({
  filename: 'path/to/image.jpg',
  extension: 'jpeg',
});

// add image to workbook by buffer
const imageId2 \= workbook.addImage({
  buffer: fs.readFileSync('path/to.image.png'),
  extension: 'png',
});

// add image to workbook by base64
const myBase64Image \= "data:image/png;base64,iVBORw0KG...";
const imageId2 \= workbook.addImage({
  base64: myBase64Image,
  extension: 'png',
});

### Add image background to worksheet⬆

Using the image id from Workbook.addImage, the background to a worksheet can be set using the addBackgroundImage function

// set background
worksheet.addBackgroundImage(imageId1);

### Add image over a range⬆

Using the image id from Workbook.addImage, an image can be embedded within the worksheet to cover a range. The coordinates calculated from the range will cover from the top-left of the first cell to the bottom right of the second.

// insert an image over B2:D6
worksheet.addImage(imageId2, 'B2:D6');

Using a structure instead of a range string, it is possible to partially cover cells.

Note that the coordinate system used for this is zero based, so the top-left of A1 will be { col: 0, row: 0 }. Fractions of cells can be specified by using floating point numbers, e.g. the midpoint of A1 is { col: 0.5, row: 0.5 }.

// insert an image over part of B2:D6
worksheet.addImage(imageId2, {
  tl: { col: 1.5, row: 1.5 },
  br: { col: 3.5, row: 5.5 }
});

The cell range can also have the property 'editAs' which will control how the image is anchored to the cell(s) It can have one of the following values:

Value

Description

undefined

It specifies the image will be moved and sized with cells

oneCell

This is the default. Image will be moved with cells but not sized

absolute

Image will not be moved or sized with cells

ws.addImage(imageId, {
  tl: { col: 0.1125, row: 0.4 },
  br: { col: 2.101046875, row: 3.4 },
  editAs: 'oneCell'
});

### Add image to a cell⬆

You can add an image to a cell and then define its width and height in pixels at 96dpi.

worksheet.addImage(imageId2, {
  tl: { col: 0, row: 0 },
  ext: { width: 500, height: 200 }
});

### Add image with hyperlinks⬆

You can add an image with hyperlinks to a cell, and defines the hyperlinks in image range.

worksheet.addImage(imageId2, {
  tl: { col: 0, row: 0 },
  ext: { width: 500, height: 200 },
  hyperlinks: {
    hyperlink: 'http://www.somewhere.com',
    tooltip: 'http://www.somewhere.com'
  }
});

Sheet Protection⬆
-----------------

Worksheets can be protected from modification by adding a password.

await worksheet.protect('the-password', options);

Worksheet protection can also be removed:

worksheet.unprotect();

See Cell Protection for details on how to modify individual cell protection.

**Note:** While the protect() function returns a Promise indicating that it is async, the current implementation runs on the main thread and will use approx 600ms on an average CPU. This can be adjusted by setting the spinCount, which can be used to make the process either faster or more resilient.

### Sheet Protection Options⬆

Field

Default

Description

selectLockedCells

true

Lets the user select locked cells

selectUnlockedCells

true

Lets the user select unlocked cells

formatCells

false

Lets the user format cells

formatColumns

false

Lets the user format columns

formatRows

false

Lets the user format rows

insertRows

false

Lets the user insert rows

insertColumns

false

Lets the user insert columns

insertHyperlinks

false

Lets the user insert hyperlinks

deleteRows

false

Lets the user delete rows

deleteColumns

false

Lets the user delete columns

sort

false

Lets the user sort data

autoFilter

false

Lets the user filter data in tables

pivotTables

false

Lets the user use pivot tables

spinCount

100000

The number of hash iterations performed when protecting or unprotecting

File I/O⬆
---------

### XLSX⬆

#### Reading XLSX⬆

Options supported when reading XLSX files.

Field

Required

Type

Description

ignoreNodes

N

Array

A list of node names to ignore while loading the XLSX document. Improves performance in some situations.  
Available: `sheetPr`, `dimension`, `sheetViews` , `sheetFormatPr`, `cols` , `sheetData`, `autoFilter` , `mergeCells` , `rowBreaks`, `hyperlinks` , `pageMargins`, `dataValidations`, `pageSetup`, `headerFooter` , `printOptions` , `picture`, `drawing`, `sheetProtection`, `tableParts` , `conditionalFormatting`, `extLst`,

// read from a file
const workbook \= new Excel.Workbook();
await workbook.xlsx.readFile(filename);
// ... use workbook

// read from a stream
const workbook \= new Excel.Workbook();
await workbook.xlsx.read(stream);
// ... use workbook

// load from buffer
const workbook \= new Excel.Workbook();
await workbook.xlsx.load(data);
// ... use workbook

// using additional options
const workbook \= new Excel.Workbook();
await workbook.xlsx.load(data, {
  ignoreNodes: \[
    'dataValidations' // ignores the workbook's Data Validations
  \],
});
// ... use workbook

#### Writing XLSX⬆

// write to a file
const workbook \= createAndFillWorkbook();
await workbook.xlsx.writeFile(filename);

// write to a stream
await workbook.xlsx.write(stream);

// write to a new buffer
const buffer \= await workbook.xlsx.writeBuffer();

### CSV⬆

#### Reading CSV⬆

Options supported when reading CSV files.

Field

Required

Type

Description

dateFormats

N

Array

Specify the date encoding format of dayjs.

map

N

Function

Custom Array.prototype.map() callback function for processing data.

sheetName

N

String

Specify worksheet name.

parserOptions

N

Object

parseOptions options @fast-csv/format module to write csv data.

// read from a file
const workbook \= new Excel.Workbook();
const worksheet \= await workbook.csv.readFile(filename);
// ... use workbook or worksheet

// read from a stream
const workbook \= new Excel.Workbook();
const worksheet \= await workbook.csv.read(stream);
// ... use workbook or worksheet

// read from a file with European Dates
const workbook \= new Excel.Workbook();
const options \= {
  dateFormats: \['DD/MM/YYYY'\]
};
const worksheet \= await workbook.csv.readFile(filename, options);
// ... use workbook or worksheet

// read from a file with custom value parsing
const workbook \= new Excel.Workbook();
const options \= {
  map(value, index) {
    switch(index) {
      case 0:
        // column 1 is string
        return value;
      case 1:
        // column 2 is a date
        return new Date(value);
      case 2:
        // column 3 is JSON of a formula value
        return JSON.parse(value);
      default:
        // the rest are numbers
        return parseFloat(value);
    }
  },
  // https://c2fo.github.io/fast-csv/docs/parsing/options
  parserOptions: {
    delimiter: '\\t',
    quote: false,
  },
};
const worksheet \= await workbook.csv.readFile(filename, options);
// ... use workbook or worksheet

The CSV parser uses fast-csv to read the CSV file. The formatterOptions in the options passed to the above write function will be passed to the @fast-csv/format module to write csv data. Please refer to the fast-csv README.md for details.

Dates are parsed using the npm module dayjs. If a dateFormats array is not supplied, the following dateFormats are used:

-   'YYYY-MM-DD\[T\]HH:mm:ss'
-   'MM-DD-YYYY'
-   'YYYY-MM-DD'

Please refer to the dayjs CustomParseFormat plugin for details on how to structure a dateFormat.

#### Writing CSV⬆

Options supported when writing to a CSV file.

Field

Required

Type

Description

dateFormat

N

String

Specify the date encoding format of dayjs.

dateUTC

N

Boolean

Specify whether ExcelJS uses `dayjs.utc ()` to convert time zone for parsing dates.

encoding

N

String

Specify file encoding format. (Only applies to `.writeFile`.)

includeEmptyRows

N

Boolean

Specifies whether empty rows can be written.

map

N

Function

Custom Array.prototype.map() callback function for processing row values.

sheetName

N

String

Specify worksheet name.

sheetId

N

Number

Specify worksheet ID.

formatterOptions

N

Object

formatterOptions options @fast-csv/format module to write csv data.

// write to a file
const workbook \= createAndFillWorkbook();
await workbook.csv.writeFile(filename);

// write to a stream
// Be careful that you need to provide sheetName or
// sheetId for correct import to csv.
await workbook.csv.write(stream, { sheetName: 'Page name' });

// write to a file with European Date-Times
const workbook \= new Excel.Workbook();
const options \= {
  dateFormat: 'DD/MM/YYYY HH:mm:ss',
  dateUTC: true, // use utc when rendering dates
};
await workbook.csv.writeFile(filename, options);

// write to a file with custom value formatting
const workbook \= new Excel.Workbook();
const options \= {
  map(value, index) {
    switch(index) {
      case 0:
        // column 1 is string
        return value;
      case 1:
        // column 2 is a date
        return dayjs(value).format('YYYY-MM-DD');
      case 2:
        // column 3 is a formula, write just the result
        return value.result;
      default:
        // the rest are numbers
        return value;
    }
  },
  // https://c2fo.github.io/fast-csv/docs/formatting/options
  formatterOptions: {
    delimiter: '\\t',
    quote: false,
  },
};
await workbook.csv.writeFile(filename, options);

// write to a new buffer
const buffer \= await workbook.csv.writeBuffer();

The CSV parser uses fast-csv to write the CSV file. The formatterOptions in the options passed to the above write function will be passed to the @fast-csv/format module to write csv data. Please refer to the fast-csv README.md for details.

Dates are formatted using the npm module dayjs. If no dateFormat is supplied, dayjs.ISO\_8601 is used. When writing a CSV you can supply the boolean dateUTC as true to have ExcelJS parse the date without automatically converting the timezone using `dayjs.utc()`.

### Streaming I/O⬆

The File I/O documented above requires that an entire workbook is built up in memory before the file can be written. While convenient, it can limit the size of the document due to the amount of memory required.

A streaming writer (or reader) processes the workbook or worksheet data as it is generated, converting it into file form as it goes. Typically this is much more efficient on memory as the final memory footprint and even intermediate memory footprints are much more compact than with the document version, especially when you consider that the row and cell objects are disposed once they are committed.

The interface to the streaming workbook and worksheet is almost the same as the document versions with a few minor practical differences:

-   Once a worksheet is added to a workbook, it cannot be removed.
-   Once a row is committed, it is no longer accessible since it will have been dropped from the worksheet.
-   unMergeCells() is not supported.

Note that it is possible to build the entire workbook without committing any rows. When the workbook is committed, all added worksheets (including all uncommitted rows) will be automatically committed. However in this case, little will have been gained over the Document version.

#### Streaming XLSX⬆

##### Streaming XLSX Writer(#contents)

The streaming XLSX workbook writer is available in the ExcelJS.stream.xlsx namespace.

The constructor takes an optional options object with the following fields:

Field

Description

stream

Specifies a writable stream to write the XLSX workbook to.

filename

If stream not specified, this field specifies the path to a file to write the XLSX workbook to.

useSharedStrings

Specifies whether to use shared strings in the workbook. Default is `false`.

useStyles

Specifies whether to add style information to the workbook. Styles can add some performance overhead. Default is `false`.

zip

Zip options that ExcelJS internally passes to Archiver. Default is `undefined`.

If neither stream nor filename is specified in the options, the workbook writer will create a StreamBuf object that will store the contents of the XLSX workbook in memory. This StreamBuf object, which can be accessed via the property workbook.stream, can be used to either access the bytes directly by stream.read() or to pipe the contents to another stream.

// construct a streaming XLSX workbook writer with styles and shared strings
const options \= {
  filename: './streamed-workbook.xlsx',
  useStyles: true,
  useSharedStrings: true
};
const workbook \= new Excel.stream.xlsx.WorkbookWriter(options);

In general, the interface to the streaming XLSX writer is the same as the Document workbook (and worksheets) described above, in fact the row, cell and style objects are the same.

However there are some differences...

**Construction**

As seen above, the WorkbookWriter will typically require the output stream or file to be specified in the constructor.

**Committing Data**

When a worksheet row is ready, it should be committed so that the row object and contents can be freed. Typically this would be done as each row is added...

worksheet.addRow({
   id: i,
   name: theName,
   etc: someOtherDetail
}).commit();

The reason the WorksheetWriter does not commit rows as they are added is to allow cells to be merged across rows:

worksheet.mergeCells('A1:B2');
worksheet.getCell('A1').value \= 'I am merged';
worksheet.getCell('C1').value \= 'I am not';
worksheet.getCell('C2').value \= 'Neither am I';
worksheet.getRow(2).commit(); // now rows 1 and two are committed.

As each worksheet is completed, it must also be committed:

// Finished adding data. Commit the worksheet
worksheet.commit();

To complete the XLSX document, the workbook must be committed. If any worksheet in a workbook are uncommitted, they will be committed automatically as part of the workbook commit.

// Finished the workbook.
await workbook.commit();
// ... the stream has been written

##### Streaming XLSX Reader(#contents)

The streaming XLSX workbook reader is available in the ExcelJS.stream.xlsx namespace.

The constructor takes a required input argument and an optional options argument:

Argument

Description

input (required)

Specifies the name of the file or the readable stream from which to read the XLSX workbook.

options (optional)

Specifies how to handle the event types occuring during the read parsing.

options.entries

Specifies whether to emit entries (`'emit'`) or not (`'ignore'`). Default is `'emit'`.

options.sharedStrings

Specifies whether to cache shared strings (`'cache'`), which inserts them into the respective cell values, or whether to emit them (`'emit'`) or ignore them (`'ignore'`), in both of which case the cell value will be a reference to the shared string's index. Default is `'cache'`.

options.hyperlinks

Specifies whether to cache hyperlinks (`'cache'`), which inserts them into their respective cells, whether to emit them (`'emit'`) or whether to ignore them (`'ignore'`). Default is `'cache'`.

options.styles

Specifies whether to cache styles (`'cache'`), which inserts them into their respective rows and cells, or whether to ignore them (`'ignore'`). Default is `'cache'`.

options.worksheets

Specifies whether to emit worksheets (`'emit'`) or not (`'ignore'`). Default is `'emit'`.

const workbookReader \= new ExcelJS.stream.xlsx.WorkbookReader('./file.xlsx');
for await (const worksheetReader of workbookReader) {
  for await (const row of worksheetReader) {
    // ...
  }
}

Please note that `worksheetReader` returns an array of rows rather than each row individually for performance reasons: nodejs/node#31979

###### Iterating over all events(#contents)

Events on workbook are 'worksheet', 'shared-strings' and 'hyperlinks'. Events on worksheet are 'row' and 'hyperlinks'.

const options \= {
  sharedStrings: 'emit',
  hyperlinks: 'emit',
  worksheets: 'emit',
};
const workbook \= new ExcelJS.stream.xlsx.WorkbookReader('./file.xlsx', options);
for await (const {eventType, value} of workbook.parse()) {
  switch (eventType) {
    case 'shared-strings':
      // value is the shared string
    case 'worksheet':
      // value is the worksheetReader
    case 'hyperlinks':
      // value is the hyperlinksReader
  }
}

###### Readable stream(#contents)

While we strongly encourage to use async iteration, we also expose a streaming interface for backwards compatibility.

const options \= {
  sharedStrings: 'emit',
  hyperlinks: 'emit',
  worksheets: 'emit',
};
const workbookReader \= new ExcelJS.stream.xlsx.WorkbookReader('./file.xlsx', options);
workbookReader.read();

workbookReader.on('worksheet', worksheet \=> {
  worksheet.on('row', row \=> {
  });
});

workbookReader.on('shared-strings', sharedString \=> {
  // ...
});

workbookReader.on('hyperlinks', hyperlinksReader \=> {
  // ...
});

workbookReader.on('end', () \=> {
  // ...
});
workbookReader.on('error', (err) \=> {
  // ...
});

Browser⬆
========

A portion of this library has been isolated and tested for use within a browser environment.

Due to the streaming nature of the workbook reader and workbook writer, these have not been included. Only the document based workbook may be used (see Create a Workbook for details).

For example code using ExcelJS in the browser take a look at the spec/browser folder in the github repo.

Prebundled⬆
-----------

The following files are pre-bundled and included inside the dist folder.

-   exceljs.js
-   exceljs.min.js

Value Types⬆
============

The following value types are supported.

Null Value⬆
-----------

Enum: Excel.ValueType.Null

A null value indicates an absence of value and will typically not be stored when written to file (except for merged cells). It can be used to remove the value from a cell.

E.g.

worksheet.getCell('A1').value \= null;

Merge Cell⬆
-----------

Enum: Excel.ValueType.Merge

A merge cell is one that has its value bound to another 'master' cell. Assigning to a merge cell will cause the master's cell to be modified.

Number Value⬆
-------------

Enum: Excel.ValueType.Number

A numeric value.

E.g.

worksheet.getCell('A1').value \= 5;
worksheet.getCell('A2').value \= 3.14159;

String Value⬆
-------------

Enum: Excel.ValueType.String

A simple text string.

E.g.

worksheet.getCell('A1').value \= 'Hello, World!';

Date Value⬆
-----------

Enum: Excel.ValueType.Date

A date value, represented by the JavaScript Date type.

E.g.

worksheet.getCell('A1').value \= new Date(2017, 2, 15);

Hyperlink Value⬆
----------------

Enum: Excel.ValueType.Hyperlink

A URL with both text and link value.

E.g.

// link to web
worksheet.getCell('A1').value \= {
  text: 'www.mylink.com',
  hyperlink: 'http://www.mylink.com',
  tooltip: 'www.mylink.com'
};

// internal link
worksheet.getCell('A1').value \= { text: 'Sheet2', hyperlink: '#\\'Sheet2\\'!A1' };

Formula Value⬆
--------------

Enum: Excel.ValueType.Formula

An Excel formula for calculating values on the fly. Note that while the cell type will be Formula, the cell may have an effectiveType value that will be derived from the result value.

Note that ExcelJS cannot process the formula to generate a result, it must be supplied.

Note that function semantic names must be in English and the separator must be a comma.

E.g.

worksheet.getCell('A3').value \= { formula: 'A1+A2', result: 7 };
worksheet.getCell('A3').value \= { formula: 'SUM(A1,A2)', result: 7 };

Cells also support convenience getters to access the formula and result:

worksheet.getCell('A3').formula \=== 'A1+A2';
worksheet.getCell('A3').result \=== 7;

### Shared Formula⬆

Shared formulae enhance the compression of the xlsx document by decreasing the repetition of text within the worksheet xml. The top-left cell in a range is the designated master and will hold the formula that all the other cells in the range will derive from. The other 'slave' cells can then refer to this master cell instead of redefining the whole formula again. Note that the master formula will be translated to the slave cells in the usual Excel fashion so that references to other cells will be shifted down and to the right depending on the slave's offset to the master. For example: if the master cell A2 has a formula referencing A1 then if cell B2 shares A2's formula, then it will reference B1.

A master formula can be assigned to a cell along with the slave cells in its range

worksheet.getCell('A2').value \= {
  formula: 'A1',
  result: 10,
  shareType: 'shared',
  ref: 'A2:B3'
};

A shared formula can be assigned to a cell using a new value form:

worksheet.getCell('B2').value \= { sharedFormula: 'A2', result: 10 };

This specifies that the cell B2 is a formula that will be derived from the formula in A2 and its result is 10.

The formula convenience getter will translate the formula in A2 to what it should be in B2:

expect(worksheet.getCell('B2').formula).to.equal('B1');

Shared formulae can be assigned into a sheet using the 'fillFormula' function:

// set A1 to starting number
worksheet.getCell('A1').value \= 1;

// fill A2 to A10 with ascending count starting from A1
worksheet.fillFormula('A2:A10', 'A1+1', \[2,3,4,5,6,7,8,9,10\]);

fillFormula can also use a callback function to calculate the value at each cell

// fill A2 to A100 with ascending count starting from A1
worksheet.fillFormula('A2:A100', 'A1+1', (row, col) \=> row);

### Formula Type⬆

To distinguish between real and translated formula cells, use the formulaType getter:

worksheet.getCell('A3').formulaType \=== Enums.FormulaType.Master;
worksheet.getCell('B3').formulaType \=== Enums.FormulaType.Shared;

Formula type has the following values:

Name

Value

Enums.FormulaType.None

0

Enums.FormulaType.Master

1

Enums.FormulaType.Shared

2

### Array Formula⬆

A new way of expressing shared formulae in Excel is the array formula. In this form, the master cell is the only cell that contains any information relating to a formula. It contains the shareType 'array' along with the range of cells it applies to and the formula that will be copied. The rest of the cells are regular cells with regular values.

Note: array formulae are not translated in the way shared formulae are. So if master cell A2 refers to A1, then slave cell B2 will also refer to A1.

E.g.

// assign array formula to A2:B3
worksheet.getCell('A2').value \= {
  formula: 'A1',
  result: 10,
  shareType: 'array',
  ref: 'A2:B3'
};

// it may not be necessary to fill the rest of the values in the sheet

The fillFormula function can also be used to fill an array formula

// fill A2:B3 with array formula "A1"
worksheet.fillFormula('A2:B3', 'A1', \[1,1,1,1\], 'array');

Rich Text Value⬆
----------------

Enum: Excel.ValueType.RichText

Rich, styled text.

E.g.

worksheet.getCell('A1').value \= {
  richText: \[
    { text: 'This is '},
    {font: {italic: true}, text: 'italic'},
  \]
};

Boolean Value⬆
--------------

Enum: Excel.ValueType.Boolean

E.g.

worksheet.getCell('A1').value \= true;
worksheet.getCell('A2').value \= false;

Error Value⬆
------------

Enum: Excel.ValueType.Error

E.g.

worksheet.getCell('A1').value \= { error: '#N/A' };
worksheet.getCell('A2').value \= { error: '#VALUE!' };

The current valid Error text values are:

Name

Value

Excel.ErrorValue.NotApplicable

#N/A

Excel.ErrorValue.Ref

#REF!

Excel.ErrorValue.Name

#NAME?

Excel.ErrorValue.DivZero

#DIV/0!

Excel.ErrorValue.Null

#NULL!

Excel.ErrorValue.Value

#VALUE!

Excel.ErrorValue.Num

#NUM!

Interface Changes⬆
==================

Every effort is made to make a good consistent interface that doesn't break through the versions but regrettably, now and then some things have to change for the greater good.

0.1.0⬆
------

### Worksheet.eachRow⬆

The arguments in the callback function to Worksheet.eachRow have been swapped and changed; it was function(rowNumber,rowValues), now it is function(row, rowNumber) which gives it a look and feel more like the underscore (\_.each) function and priorities the row object over the row number.

### Worksheet.getRow⬆

This function has changed from returning a sparse array of cell values to returning a Row object. This enables accessing row properties and will facilitate managing row styles and so on.

The sparse array of cell values is still available via Worksheet.getRow(rowNumber).values;

0.1.1⬆
------

### cell.model⬆

cell.styles renamed to cell.style

0.2.44⬆
-------

Promises returned from functions switched from Bluebird to native node Promise which can break calling code if they rely on Bluebird's extra features.

To mitigate this the following two changes were added to 0.3.0:

-   A more fully featured and still browser compatible promise lib is used by default. This lib supports many of the features of Bluebird but with a much lower footprint.
-   An option to inject a different Promise implementation. See Config section for more details.

Config⬆
=======

ExcelJS now supports dependency injection for the promise library. You can restore Bluebird promises by including the following code in your module...

ExcelJS.config.setValue('promise', require('bluebird'));

Please note: I have tested ExcelJS with bluebird specifically (since up until recently this was the library it used). From the tests I have done it will not work with Q.

Caveats⬆
========

Dist Folder⬆
------------

Before publishing this module, the source code is transpiled and otherwise processed before being placed in a dist/ folder. This README identifies two files - a browserified bundle and minified version. No other contents of the dist/ folder are guaranteed in any way other than the file specified as "main" in the package.json

Known Issues⬆
=============

Testing with Puppeteer⬆
-----------------------

The test suite included in this lib includes a small script executed in a headless browser to validate the bundled packages. At the time of this writing, it appears that this test does not play nicely in the Windows Linux subsystem.

For this reason, the browser test can be disabled by the existence of a file named .disable-test-browser

sudo apt-get install libfontconfig

Splice vs Merge⬆
----------------

If any splice operation affects a merged cell, the merge group will not be moved correctly

Release History⬆
================

Version

Changes

0.0.9

-   Number Formats

0.1.0

-   Bug Fixes
    -   "<" and ">" text characters properly rendered in xlsx
-   Better Column control
-   Better Row control

0.1.1

-   Bug Fixes
    -   More textual data written properly to xml (including text, hyperlinks, formula results and format codes)
    -   Better date format code recognition
-   Cell Font Style

0.1.2

-   Fixed potential race condition on zip write

0.1.3

-   Cell Alignment Style
-   Row Height
-   Some Internal Restructuring

0.1.5

-   Bug Fixes
    -   Now handles 10 or more worksheets in one workbook
    -   theme1.xml file properly added and referenced
-   Cell Borders

0.1.6

-   Bug Fixes
    -   More compatible theme1.xml included in XLSX file
-   Cell Fills

0.1.8

-   Bug Fixes
    -   More compatible theme1.xml included in XLSX file
    -   Fixed filename case issue
-   Cell Fills

0.1.9

-   Bug Fixes
    -   Added docProps files to satisfy Mac Excel users
    -   Fixed filename case issue
    -   Fixed worksheet id issue
-   Core Workbook Properties

0.1.10

-   Bug Fixes
    -   Handles File Not Found error
-   CSV Files

0.1.11

-   Bug Fixes
    -   Fixed Vertical Middle Alignment Issue
-   Row and Column Styles
-   Worksheet.eachRow supports options
-   Row.eachCell supports options
-   New function Column.eachCell

0.2.0

-   Streaming XLSX Writer
    -   At long last ExcelJS can support writing massive XLSX files in a scalable memory efficient manner. Performance has been optimised and even smaller spreadsheets can be faster to write than the document writer. Options have been added to control the use of shared strings and styles as these can both have a considerable effect on performance
-   Worksheet.lastRow
    -   Access the last editable row in a worksheet.
-   Row.commit()
    -   For streaming writers, this method commits the row (and any previous rows) to the stream. Committed rows will no longer be editable (and are typically deleted from the worksheet object). For Document type workbooks, this method has no effect.

0.2.2

-   One Billion Cells
    -   Achievement Unlocked: A simple test using ExcelJS has created a spreadsheet with 1,000,000,000 cells. Made using random data with 100,000,000 rows of 10 cells per row. I cannot validate the file yet as Excel will not open it and I have yet to implement the streaming reader but I have every confidence that it is good since 1,000,000 rows loads ok.

0.2.3

-   Bug Fixes
    -   Merge Cell Styles
        -   Merged cells now persist (and parse) their styles.
-   Streaming XLSX Writer
    -   At long last ExcelJS can support writing massive XLSX files in a scalable memory efficient manner. Performance has been optimised and even smaller spreadsheets can be faster to write than the document writer. Options have been added to control the use of shared strings and styles as these can both have a considerable effect on performance
-   Worksheet.lastRow
    -   Access the last editable row in a worksheet.
-   Row.commit()
    -   For streaming writers, this method commits the row (and any previous rows) to the stream. Committed rows will no longer be editable (and are typically deleted from the worksheet object). For Document type workbooks, this method has no effect.

0.2.4

-   Bug Fixes
    -   Worksheets with Ampersand Names
        -   Worksheet names are now xml-encoded and should work with all xml compatible characters
-   Row.hidden & Column.hidden
    -   Rows and Columns now support the hidden attribute.
-   Worksheet.addRows
    -   New function to add an array of rows (either array or object form) to the end of a worksheet.

0.2.6

-   Bug Fixes
    -   invalid signature: 0x80014: Thanks to hasanlussa for the PR
-   Defined Names
    -   Cells can now have assigned names which may then be used in formulas.
-   Converted Bluebird.defer() to new Bluebird(function(resolve, reject){}). Thanks to user Nishchit for the Pull Request

0.2.7

-   Data Validations
    -   Cells can now define validations that controls the valid values the cell can have

0.2.8

-   Rich Text Value
    -   Cells now support **_in-cell_** formatting - Thanks to Peter ADAM
-   Fixed typo in README - Thanks to MRdNk
-   Fixing emit in worksheet-reader - Thanks to Alan Gunning
-   Clearer Docs - Thanks to miensol

0.2.9

-   Fixed "read property 'richText' of undefined error. Thanks to james075

0.2.10

-   Refactoring Complete. All unit and integration tests pass.

0.2.11

-   Outline Levels. Thanks to cricri for the contribution.
-   Worksheet Properties
-   Further refactoring of worksheet writer.

0.2.12

-   Sheet Views. Thanks to cricri again for the contribution.

0.2.13

-   Fix for exceljs might be vulnerable for regular expression denial of service. Kudos to yonjah and Josh Emerson for the resolution.
-   Fix for Multiple Sheets opens in 'Group' mode in Excel. My bad - overzealous sheet view code.
-   Also fix for empty sheet generating invalid xlsx.

0.2.14

-   Fix for exceljs might be vulnerable for regular expression denial of service. Kudos to yonjah and Josh Emerson for the resolution.
-   Fixed Multiple Sheets opens in 'Group' mode in Excel again. Added Workbook views.
-   Also fix for empty sheet generating invalid xlsx.

0.2.15

-   Added Page Setup Properties. Thanks to Jackkum for the PR

0.2.16

-   New Page Setup Property: Print Area

0.2.17

-   Merged Fix a bug on phonetic characters. This fixes an issue related to reading workbooks with phonetic text in. Note phonetic text is not properly supported yet - just properly ignored. Thanks to zephyrrider and gen6033 for the contribution.

0.2.18

-   Merged Fix regression #150: Stream API fails to write XLSX files. Apologies for the regression! Thanks to danieleds for the fix.
-   Merged Fix a bug on phonetic characters. This fixes an issue related to reading workbooks with phonetic text in. Note phonetic text is not properly supported yet - just properly ignored. Thanks to zephyrrider and gen6033 for the contribution.

0.2.19

-   Merged Update xlsx.js #119. This should make parsing more resilient to open-office documents. Thanks to nvitaterna for the contribution.

0.2.20

-   Merged Changes from exceljs/exceljs#127 applied to latest version #179. Fixes parsing of defined name values. Thanks to agdevbridge and priitliivak for the contribution.

0.2.21

-   Merged color tabs for worksheet-writer #135. Modified the behaviour to print deprecation warning as tabColor has moved into options.properties. Thanks to ethanlook for the contribution.

0.2.22

-   Merged Throw legible error when failing Value.getType() #136. Thanks to wulfsolter for the contribution.
-   Honourable mention to contributors whose PRs were fixed before I saw them:
    -   haoliangyu
    -   wulfsolter

0.2.23

-   Merged Fall back to JSON.stringify() if unknown Cell.Type #137 with some modification. If a cell value is assigned to an unrecognisable javascript object, the stored value in xlsx and csv files will be JSON stringified. Note that if the file is read again, no attempt will be made to parse the stringified JSON text. Thanks to wulfsolter for the contribution.

0.2.24

-   Merged Protect cell fix #166. This does not mean full support for protected cells merely that the parser is not confused by the extra xml. Thanks to jayflo for the contribution.

0.2.25

-   Added functions to delete cells, rows and columns from a worksheet. Modelled after the Array splice method, the functions allow cells, rows and columns to be deleted (and optionally inserted). See Columns and Rows for details.  
    Note: Not compatible with cell merges

0.2.26

-   Merged Update border-xform.js #184Border edges without style will be parsed and rendered as no-border. Thanks to skumarnk2 for the contribution.

0.2.27

-   Merged Pass views to worksheet-writer #187. Now also passes views to worksheet-writer. Thanks to Temetz for the contribution.
-   Merged Do not escape xml characters when using shared strings #189. Fixing bug in shared strings. Thanks to tkirda for the contribution.

0.2.28

-   Merged Fix tiny bug \[Update hyperlink-map.js\] #190Thanks to lszlkss for the contribution.
-   Merged fix typo on sheet view showGridLines option #196 "showGridlines" should have been "showGridLines". Thanks to gadiaz1 for the contribution.

0.2.29

-   Merged Fire finish event instead of end event on write stream #199 and Listen for finish event on zip stream instead of middle stream #200. Fixes issues with stream completion events. Thanks to junajan for the contribution.

0.2.30

-   Merged Fix issue #178 #201. Adds the following properties to workbook:
    
    -   title
    -   subject
    -   keywords
    -   category
    -   description
    -   company
    -   manager
    
    Thanks to stavenko for the contribution.

0.2.31

-   Merged Fix issue #163: the "spans" attribute of the row element is optional #203. Now xlsx parsing will handle documents without row spans. Thanks to arturas-vitkauskas for the contribution.

0.2.32

-   Merged Fix issue 206 #208. Fixes issue reading xlsx files that have been printed. Also adds "lastPrinted" property to Workbook. Thanks to arturas-vitkauskas for the contribution.

0.2.33

-   Merged Allow styling of cells with no value. #210. Includes Null type cells with style in the rendering parsing. Thanks to oferns for the contribution.

0.2.34

-   Merged Fix "Unexpected xml node in parseOpen" bug in LibreOffice documents for attributes dc:language and cp:revision #212. Thanks to jessica-jordan for the contribution.

0.2.35

-   Fixed Getting a column/row count #74. Worksheet now has rowCount and columnCount properties (and actual variants), Row has cellCount.

0.2.36

-   Merged Stream reader fixes #217. Thanks to kturney for the contribution.

0.2.37

-   Merged Fix output order of Sheet Properties #225. Thanks to keeneym for the contribution.
-   Merged remove empty worksheet\[0\] from \_worksheets #231. Thanks to pookong for the contribution.
-   Merged do not skip empty string in shared strings so that indexes match #232. Thanks again to pookong for the contribution.
-   Merged use shared strings for streamed writes #233. Thanks again to pookong for the contribution.

0.2.38

-   Merged Add a comment for issue #216 #236. Thanks to jsalwen for the contribution.
-   Merged Start on support for 1904 based dates #237. Fixed date handling in documents with the 1904 flag set. Thanks to holm for the contribution.

0.2.39

-   Merged Stops Bluebird warning about unreturned promise #245. Thanks to robinbullocks4rb for the contribution.
-   Merged Added missing dependency: col-cache.js #247. Thanks to Manish2005 for the contribution.

0.2.42

-   Browser Compatible!
    -   Well mostly. I have added a browser sub-folder that contains a browserified bundle and an index.js that can be used to generate another. See Browser section for details.
-   Fixed corrupted theme.xml. Apologies for letting that through.
-   Merged \[BUGFIX\] data validation formulae undefined #253. Thanks to jayflo for the contribution.

0.2.43

-   Merged added a (maybe partial) solution to issue 99. i wasn't able to create an appropriate test #255. This fixes Too few data or empty worksheet generate malformed excel file #99. Thanks to mminuti for the contribution.

0.2.44

-   Reduced Dependencies.
    -   Goodbye lodash, goodbye bluebird. Minified bundle is now just over half what it was in the first version.

0.2.45

-   Merged Sheets with hyperlinks and data validations are corrupted #256. Thanks to simon-stoic for the contribution.

0.2.46

-   Merged Exclude character controls from XML output. Fixes #234 #262. Thanks to holm for the contribution.
-   Merged Add support for identifier #259. This fixes Broken XLSX because of "vertical tab" ascii character in a cell #234. Thanks to NOtherDev for the contribution.

0.3.0

-   Addressed Breaking change removing bluebird #266. Appologies for any inconvenience.
-   Added Promise library dependency injection. See Config section for more details.

0.3.1

-   Merged Update dependencies #279. Thanks to holm for the contribution.
-   Merged Minor fixes for stream handling #267. Thanks to holm for the contribution.
-   Added automated tests in phantomjs for the browserified code.

0.4.0

-   Fixed issue Boolean cell with value ="true" is returned as 1 #278. The fix involved adding two new Call Value types:
    
    -   Boolean Value
    -   Error Value
    
    Note: Minor version has been bumped up to 4 as this release introduces a couple of interface changes:
    -   Boolean cells previously will have returned 1 or 0 will now return true or false
    -   Error cells that previously returned a string value will now return an error structure
-   Fixed issue Code correctness - setters don't return a value #280.
-   Addressed issue v0.3.1 breaks meteor build #288.

0.4.1

-   Merged Add support for cp:contentStatus #285. Thanks to holm for the contribution.
-   Merged Fix Valid characters in XML (allow \\n and \\r when saving) #286. Thanks to Rycochet for the contribution.
-   Fixed hyperlink with query arguments corrupts workbook #275. The hyperlink target is not escaped before serialising in the xml.

0.4.2

-   Addressed the following issues:
    
    -   White text and borders being changed to black #290
    -   Losing formatting/pivot table from loaded file #261
    -   Solid fill become black #272
    
    These issues are potentially caused by a bug that caused colours with zero themes, tints or indexes to be rendered and parsed incorrectly.
    
    Regarding themes: the theme files stored inside the xlsx container hold important information regarding colours, styles etc and if the theme information from a loaded xlsx file is lost, the results can be unpredictable and undesirable. To address this, when an ExcelJS Workbook parses an XLSX file, it will preserve any theme files it finds and include them when writing to a new XLSX. If this behaviour is not desired, the Workbook class exposes a clearThemes() function which will drop the theme content. Note that this behaviour is only implemented in the document based Workbook class, not the streamed Reader and Writer.
    

0.4.3

-   Merged Support error references in cell ranges #294. Thanks to holm for the contribution.

0.4.4

-   Merged Issue with copied cells #297. This merge adds support for shared formulas. Thanks to muscapades for the contribution.

0.4.6

-   Merged Correct spelling #304. Thanks to toanalien for the contribution.
-   Merged Added support for auto filters #306. This adds Auto Filters to the Worksheet. Thanks to C4rmond4i for the contribution.
-   Restored NodeJS 4.0.0 compatability by removing the destructuring code. My apologies for any inconvenience.

0.4.9

-   Switching to transpiled code for distribution. This will ensure compatability with 4.0.0 and above from here on. And it will also allow use of much more expressive JS code in the lib folder!
-   Basic Image Support!Images can now be added to worksheets either as a tiled background or stretched over a range. Note: other features like rotation, etc. are not supported yet and will reqeuire further work.

0.4.10

-   Merged Add missing Office Rels #319. Thanks goes to mauriciovillalobos for the contribution.
-   Merged Add printTitlesRow Support #320 Thanks goes to psellers89 for the contribution.

0.4.11

-   Merged Avoid error on anchor with no media #327. Thanks goes to holm for the contribution.
-   Merged Assortment of fixes for streaming read #332. Thanks goes to holm for the contribution.

0.4.12

-   Merged Don’t set address if hyperlink r:id is undefined #334. Thanks goes to holm for the contribution.

0.4.13

-   Merged Issue 296 #343. This fixes Issue with writing newlines #296. Thanks goes to holly-weisser for the contribution.

0.4.14

-   Merged Syntax highlighting added ✨ #350. Thanks goes to rmariuzzo for the contribution.

0.5.0

-   Merged Fix right to left issues #356. Fixes Add option to RTL file #72 and Adding an option to set RTL worksheet #126. Big thank you to alitaheri for this contribution.

0.5.1

-   Merged Fix #345 TypeError: Cannot read property 'date1904' of undefined #364. This fixes TypeError: Cannot read property 'date1904' of undefined #345. Thanks to Diluka for this contribution.

0.6.0

-   Merged Add rowBreaks feature. #389. Thanks to brucejo75 for this contribution.

0.6.1

-   Merged Guard null model fields - fix and tests #403. Thanks to thecjharries for this contribution. Also thanks to Ryc O'Chet for help with reviewing.

0.6.2

-   Merged Add some comments in readme according csv importing #396. Thanks to Michael Lelyakin for this contribution. Also thanks to planemar for help with reviewing. This also closes csv to stream doesn't work #395.

0.7.0

-   Merged Impl <xdr:twoCellAnchor editAs=oneCell> #407. Thanks to Ocke Janssen and Kay Ramme for this contribution. This change allows control on how images are anchored to cells.

0.7.1

-   Merged Don't break when attempting to import a zip file that's not an Excel file (eg. .numbers) #423. Thanks to Andreas Lind for this contribution. This change makes exceljs more reslilient when opening non-excel files.
-   Merged Fixes #419 : Updates readme. #434. Thanks to Vishnu Kyatannawar for this contribution.
-   Merged Don't break when docProps/core.xml contains a <cp:version> tag #436. Thanks to Andreas Lind for this contribution. This change handles core.xml files with empty version tags.

0.8.0

-   Merged Add Base64 Image support for the .addImage() method #442. Thanks to James W Mann for this contribution.
-   Merged update moment to 2.19.3 #453. Thanks to Markan Patel for this contribution.

0.8.1

-   Merged Additional information about font family property #457. Thanks to kayakyakr for this contribution.
-   Merged Fixes #458 #459. This fixes Add style to column causes it to be hidden #458. Thanks to Alexander James Phillips for this contribution.

0.8.2

-   Merged Don't break when loading an Excel file containing a chartsheet #466. Thanks to Andreas Lind for this contribution.
-   Merged Hotfix/sheet order#257 #471. This fixes Sheet Order #257. Thanks to Robbi for this contribution.

0.8.3

-   Assimilated fix #79 outdated dependencies in unzip2. Thanks to Jules Sam. Randolph for starting this fix and a really big thanks to Alexander Kachkaev for finding the final solution.

0.8.4

-   Merged Round Excel date to nearest millisecond when converting to javascript date #479. Thanks to Benoit Jean for this contribution.

0.8.5

-   Merged Bug fix: wb.worksheets/wb.eachSheet caused getWorksheet(0) to return sheet #485. Thanks to mah110020 for this contribution.

0.9.0

-   Merged Feature/issue 424 #489. This fixes No way to control summaryBelow or summaryRight #424. Many thanks to Sarah for this contribution.

0.9.1

-   Merged add type definition #490. This adds type definitions to ExcelJS! Many thanks to taoqf for this contribution.

1.0.0

-   Merged Add Node 8 and Node 9 to continuous integration testing #494. Many thanks to Markan Patel for this contribution.
-   Merged Small README fix #508. Many thanks to Guilherme Bernal for this contribution.
-   Merged Add support for inlineStr, including rich text #501. Many thanks to linguamatics-pdenes and Rob Scott for their efforts towards this contribution. Since this change is technically a breaking change (the rendered XML for inline strings will change) I'm making this a major release!

1.0.1

-   Fixed spliceColumns problem when the number of columns are important #520.

1.0.2

-   Merged Loosen exceljs's dependency requirements for moment #524. Many thanks to nicoladefranceschi for this contribution. This change addresses Ability to use external "moment" package #517.

1.1.0

-   Addressed Is there a way inserting values in columns. #514. Added a new getter/setter property to Column to get and set column values (see Columns for details).

1.1.1

-   Merged Include index.d.ts in published packages #532. To fix TypeScript definitions missing from npm package #525. Many thanks to Kagami Sascha Rosylight for this contribution.

1.1.2

-   Merged Don't break when docProps/core.xml contains <cp:contentType /> #536. Many thanks to Andreas Lind (and reviewers) for this contribution.

1.1.3

-   Merged Try to handle the case where a <c> element is missing an r attribute #537. Many thanks to Andreas Lind for this contribution.

1.2.0

-   Merged Add dateUTC flag to CSV Writing #544. Many thanks to Zackery Griesinger for this contribution.

1.2.1

-   Merged worksheet name is writable #547. Many thanks to xzper for this contribution.

1.3.0

-   Merged Add CSV write buffer support #549. Many thanks to Jarom Loveridge for this contribution.

1.4.2

-   Merged Discussion: Customizable row/cell limit #541. Many thanks to Andreas Lind for this contribution.

1.4.3

-   Merged Get the right text out of hyperlinked formula cells #552. Many thanks to Andreas Lind and Christian Holm for this contribution.

1.4.5

-   Merged Add test case with a huge file #556. Many thanks to Andreas Lind and Christian Holm for this contribution.

1.4.6

-   Merged Update README.md to reflect correct functionality of row.addPageBreak() #557. Many thanks to RajDesai for this contribution.
-   Merged fix index.d.ts #558. Many thanks to Diluka for this contribution.

1.4.7

-   Merged List /xl/sharedStrings.xml in \[Content\_Types\].xml only if one of the … #562. Many thanks to Priidik Vaikla for this contribution.

1.4.8

-   Merged List /xl/sharedStrings.xml in \[Content\_Types\].xml only if one of the … #562. Many thanks to Priidik Vaikla for this contribution.
-   Fixed issue with above where shared strings were used but the content type was not added.

1.4.9

-   Merged List /xl/sharedStrings.xml in \[Content\_Types\].xml only if one of the … #562. Many thanks to Priidik Vaikla for this contribution.
-   Fixed issue with above where shared strings were used but the content type was not added.
-   Fixed issue 1.4.8 broke writing Excel files with useSharedStrings:true #581.

1.4.10

-   Merged core-xform: Tolerate a missing cp: namespace for the coreProperties element #564. Many thanks to Andreas Lind for this contribution.

1.4.12

-   Merged Avoid error on malformed address #567. Many thanks to Andreas Lind for this contribution.
-   Merged Added a missing Promise<void> in index.d.ts #571. Many thanks to Gabriel Fournier for this contribution. This release should fix Is workbook.commit() still a promise or not #548

1.4.13

-   Merged Issue #488 #574. Many thanks to dljenkins for this contribution. This release should fix Invalid time value Exception #488.

1.5.0

-   Merged Sheet add state for hidden or show #577. Many thanks to Freddie Hsinfu Huang for this contribution. This release should fix hide worksheet and reorder sheets #226.

1.5.1

-   Merged Update index.d.ts #582. Many thanks to hankolsen for this contribution.
-   Merged Decode the _x<4 hex chars>_ escape notation in shared strings #584. Many thanks to Andreas Lind for this contribution.

1.6.0

-   Added .html property to Cells to facilitate html-safe rendering. See Handling Individual Cells for details.

1.6.1

-   Merged Fix Issue #488 where dt is an invalid date format. #587 to fix Invalid time value Exception #488. Many thanks to Iliya Zubakin for this contribution.

1.6.2

-   Merged Fix Issue #488 where dt is an invalid date format. #587 to fix Invalid time value Exception #488. Many thanks to Iliya Zubakin for this contribution.
-   Merged drawing element must be below rowBreaks according to spec or corrupt worksheet #590 Many thanks to Liam Neville for this contribution.

1.6.3

-   Merged set type optional #595 Many thanks to taoqf for this contribution.
-   Merged Fix some xlsx stream read xlsx not in guaranteed order problem #578 Many thanks to KMethod for this contribution.
-   Merged Fix formatting issue in README #599 Many thanks to Vishnu Kyatannawar for this contribution.

1.7.0

-   Merged Ability to set tooltip for hyperlink #602 Many thanks to Kuznetsov Aleksey for this contribution.

1.8.0

-   Merged Fix misinterpreted ranges from <definedName> #636 Many thanks to Andreas Lind for this contribution.
-   Merged Add LGTM code quality badges #640 Many thanks to Xavier RENE-CORAIL for this contribution.
-   Merged Add type definition for Column.values #646 Many thanks to Emil Laine for this contribution. This fixes Column.values is missing TypeScript definitions #645.
-   Merged Update README.md with load() option #663 Many thanks to Joanna Walker for this contribution.
-   Merged fixed packages according to npm audit #677 Many thanks to Manuel Minuti for this contribution.
-   Merged Update index.d.ts #699 Many thanks to Ray Yen for this contribution.
-   Merged Replaced node-unzip-2 to unzipper package which is more robust #708 Many thanks to johnmalkovich100 for this contribution.
-   Merged Read worksheet hidden state #728 Many thanks to Dishu(Lester) Lyu for this contribution.
-   Merged add Worksheet.state typescript definition fix #714 #736 Many thanks to Ilyes Kechidi for this contribution. This fixes Worksheet State does not exist in index.d.ts #714.

1.9.0

-   Merged Improvements for images (correct reading/writing possitions) #702. This fixes Image location don't respect Column width #650 and Image position - stretching image #467. Many thanks to Siemienik Paweł for this contribution.

1.9.1

-   Merged Add Typescript support for formulas without results #619. Many thanks to Loursin for this contribution.
-   Merged Fix existing row styles when using spliceRows #737. Many thanks to cxam for this contribution.
-   Merged Consistent code quality #774. Many thanks to Andreas Lubbe for this contribution.

1.10.0

-   Fixed effect of splicing rows and columns on defined names
-   Merged Add support for adding images anchored to one cell #746. Many thanks to Karl von Randow for this contribution.
-   Merged Add vertical align property #758. Many thanks to MikeZyatkov for this contribution.
-   Merged Replace the temp lib to tmp #775. Many thanks to Ivan Sotnikov for this contribution.
-   Merged Replace the temp lib to tmp #775. Many thanks to Andreas Lubbe for this contribution.
-   Merged Update Worksheet.dimensions return type #793. Many thanks to Siemienik Paweł for this contribution.
-   Merged One more types fix #795. Many thanks to Siemienik Paweł for this contribution.

1.11.0

-   Merged Add the ability to bail out of parsing if the number of columns exceeds a given limit #776. Many thanks to Andreas Lind for this contribution.
-   Merged Add support for repeated columns on every page when printing. #799. Many thanks to Jasmin Auger for this contribution.
-   Merged Do not use a promise polyfill on modern setups #815. Many thanks to Andreas Lubbe for this contribution.
-   Merged copy LICENSE to the dist folder #807. Many thanks to Yuping Zuo for this contribution.
-   Merged Avoid unhandled rejection on XML parse error #813. Many thanks to Andreas Lind for this contribution.

1.12.0

-   Merged (chore) increment unzipper to 0.9.12 to address npm advisory 886 #819. Many thanks to Kreig Zimmerman for this contribution.
-   Merged docs(README): improve docs #817. Many thanks to Yuping Zuo for this contribution.
-   Merged add comment support #529 #823. Many thanks to ilimei for this contribution.
    
    This fixes the following issues:
    
    -   Is it possible to add comment on a cell? #202
    -   Add comment to cell #451
    -   Excel add comment on cell #503
    -   How to add Cell comment #529
    -   Please add example to how I can insert comments for a cell #707

1.12.1

-   Merged fix issue with print area defined name corrupting file #822. Many thanks to Julia Donaldson for this contribution. This fixes issue Defined Names Break/Corrupt Excel File into Repair Mode #664.
-   Merged Only keep at most 31 characters for sheetname #831. Many thanks to Xuebin He for this contribution. This fixes issue Limit worksheet name length to 31 characters #398.

1.12.2

-   Merged add cn doc #834 and update cn doc #852. Many thanks to flydragon for this contribution.
-   Merged fix minor spelling mistake in readme #853. Many thanks to John Varga for this contribution.
-   Merged Fix defaultRowHeight not working #855. Many thanks to autukill for this contribution. This should fix row height doesn't apply to row #422, The worksheet.properties.defaultRowHeight can't work!! How to set the rows height, help!! #634 and Default row height doesn't work ? #696.
-   Merged Always keep first font #854. Many thanks to Dmitriy Gusev for this contribution. This should fix document scale (width only) is different after read & write #816, Default font from source document can not be parsed. #833 and Wrong base font: hardcoded Calibri instead of font from the document #849.

1.13.0

-   Merged zip: allow tuning compression for performance or size #862. Many thanks to myfreeer for this contribution.
-   Merged Feat configure headers and footers #863. Many thanks to autukill for this contribution.
-   Fixed an issue with defaultRowHeight where the default value resulted in 'customHeight' property being set.

1.14.0

-   Merged Fix header and footer text format error in README.md #874. Many thanks to autukill for this contribution.
-   Added Tables. See Tables for details.
-   Merged fix: #877 and #880. Many thanks to Alexander Heinrich for this contribution. This fixes bug: Hyperlink without text crashes write #877 and bug: malformed comment crashes on write #880

1.15.0

-   Merged Add Compression level option to WorkbookWriterOptions for streaming #889. Many thanks to Alfredo Benassi for this contribution.
-   Merged Feature/Cell Protection #903 and Feature/Sheet Protection #907. Many thanks to karabaesh for these contributions.

2.0.1

Major Version Change
--------------------

Introducing async/await to ExcelJS!

The new async and await features of JavaScript can help a lot to make code more readable and maintainable. To avoid confusion, particularly with returned promises from async functions, we have had to remove the Promise class configuration option and from v2 onwards ExcelJS will use native Promises. Since this is potentially a breaking change we're bumping the major version for this release.

Changes
-------

-   Merged Introduce async/await #829. Many thanks to Andreas Lubbe for this contribution.
-   Merged Update index.d.ts #930. Many thanks to cosmonovallc for this contributions.
-   Merged TS: Add types for addTable function #940. Many thanks to egmen for this contributions.
-   Merged added explicit return types to the type definitions of Worksheet.protect() and Worksheet.unprotect() #926. Many thanks to Tamas Czinege for this contributions.
-   Dropped dependencies on Promise libraries.

3.0.0

Another Major Version Change
----------------------------

Javascript has changed a lot over the years, and so have the modules and technologies surrounding it. To this end, this major version of ExcelJS changes the structure of the publish artefacts:

### Main Export is now the Original Javascript Source

Prior to this release, the transpiled ES5 code was exported as the package main. From now on, the package main comes directly from the lib/ folder. This means a number of dependencies have been removed, including the polyfills.

### ES5 and Browserify are Still Included

In order to support those that still require ES5 ready code (e.g. as dependencies in web apps) the source code will still be transpiled and available in dist/es5.

The ES5 code is also browserified and available as dist/exceljs.js or dist/exceljs.min.js

_See the section Importing for details_

3.1.0

-   Merged Uprev fast-csv to latest version which does not use unsafe eval #873. Many thanks to Mike Townsend for this contribution.
-   Merged Exclude Infinity on createInputStream #906. Many thanks to Sophie Kwon for this contribution.
-   Merged Feature/Add comments/notes to stream writer #911. Many thanks to brunoargolo for this contribution. This fixes Can't add cell comment using streaming WorkbookWriter #868
-   Fixed an issue with reading .xlsx files containing notes. This should resolve the following issues:
    -   Reading comment/note from xlsx #941
    -   Excel.js doesn't parse comments/notes. #944

3.2.0

-   Merged Add document for zip options of streaming WorkbookWriter #923. Many thanks to Soichi Takamura for this contribution.
-   Merged array formula #933. Many thanks to yoann-antoviaque for this contribution. This fixes broken array formula #932 and adds Array Formulae to ExcelJS.

3.3.0

-   Merged Fix anchor.js #892. Many thanks to Wojciech Wojtkowski for this contribution.
-   Merged add xml:space="preserve" for all whitespaces #896. Many thanks to Sebastian Keller for this contribution.
-   Merged Add `shrinkToFit` to document and typing #959. Many thanks to ('3') for this contribution. This fixes shrinkToFit property not on documentation #943.
-   Merged #951: Force formula re-calculation on file open from Excel #980. Many thanks to zymon for this contribution. This fixes Force formula re-calculation on file open from Excel #951.
-   Fixed Lib contains class syntax, not compatible with IE11 #989.

3.3.1

-   Merged Add headerFooter to worksheet model when importing from file #1000. Many thanks to Kaiichiro Ota for this contribution.
-   Merged Update eslint plugins and configs #1005, Drop grunt-lib-phantomjs #1006 and Rename .browserslintrc.txt to .browserslistrc #1007. Many thanks to Takeshi Kurosawa for this contribution.
-   Merged Fix issue #988 #1012. This fixes Can not read excel file #988. Many thanks to Todd Hambley for this contribution.

3.4.0

-   Merged Feature/stream writer add background images #1016. Many thanks to brunoargolo for this contribution.
-   Merged Fix issue # 991 #1019. This fixes read csv file issue #991. Many thanks to Nathaniel J. Liberty for this contribution.
-   Merged Large excels - optimize performance of writing file by excelJS + optimize generated file (MS excel opens it much faster) #1018. Many thanks to Piotr for this contribution.

3.5.0

-   Conditional Formatting A subset of Excel Conditional formatting has been implemented! Specifically the formatting rules that do not require XML to be rendered inside an <extLst> node, or in other words everything except databar and three icon sets (3Triangles, 3Stars, 5Boxes). These will be implemented in due course
-   Merged remove core-js/ import #1030. Many thanks to jeffrey n. carre for this contribution. This change is used to create a new browserified bundle artefact that does not include any polyfills. See Browserify for details.

3.6.0

-   Merged 1041 multiple print areas #1042. Many thanks to Alexander Pruss for this contribution.
-   Merged fix typings for cell.note #1058. Many thanks to xydens for this contribution.
-   Conditional Formatting has been completed. The <extLst> conditional formattings including dataBar and the three iconSet types (3Triangles, 3Stars, 5Boxes) are now available.

3.6.1

-   Merged Clarify merging cells by row/column numbers #1047. Many thanks to Kendall Roth for this contribution.
-   Merged Fix README mistakes concerning freezing views #1048. Many thanks to overlookmotel for this contribution.
-   Merged:
    
    -   fix issue #1045 horizontalCentered & verticalCentered in page not working #1073
    -   Fix the problem of anchor failure of readme\_zh.md file #1082
    -   Fix problems caused by case of worksheet names #1065
    
    Many thanks to Alan Wang for this contribution.

3.7.0

-   Merged Fix Issue #1075: Unable to read/write defaultColWidth attribute in <sheetFormatPr> node #1076. Many thanks to Kaiichiro Ota for this contribution.
-   Merged function duplicateRows added #1078 and Duplicate rows #1088. Many thanks to cbeltrangomez84 for this contribution.
-   Merged Prevent from unhandled promise rejection durning workbook load #1087. Many thanks to Wojtek for this contribution.
-   Merged fix issue #899 Support for inserting pictures with hyperlinks #1071. Many thanks to Alan Wang for this contribution.
-   Merged Update TS definition to reference proper internal libraries #1089. Many thanks to Jesse Kawell for this contribution.

3.8.0

-   Merged Issue/Corrupt workbook using stream writer with background image #1090. Many thanks to brunoargolo for this contribution.
-   Merged Fix index.d.ts #1092. Many thanks to Siemienik Paweł for this contribution.
-   Merged Wait for writing to tmp fiels before handling zip stream close #1093. Many thanks to Wojtek for this contribution.
-   Merged Support ArrayBuffer as an xlsx.load argument #1095. Many thanks to Wojtek for this contribution.
-   Merged Export shared strings with RichText #1099. Many thanks to Kaiichiro Ota for this contribution.
-   Merged Keep borders of merged cells after rewriting an Excel workbook #1102. Many thanks to Kaiichiro Ota for this contribution.
-   Merged Fix #1103: `editAs` not working #1104. Many thanks to Alan Wang for this contribution.
-   Merged Fix to issue #1101 #1105. Many thanks to Carlos Andres Beltran Gomez for this contribution.
-   Merged fix some errors and typos in readme #1107. Many thanks to Alan Wang for this contribution.
-   Merged Update issue templates #1112. Many thanks to Siemienik Paweł for this contribution.

3.8.1

-   Merged Update issue templates #1112. Many thanks to Siemienik Paweł for this contribution.
-   Merged Typo: Replace 'allways' with 'always' #1124. Many thanks to Siemienik Paweł for this contribution.
-   Merged Replace uglify with terser #1125. Many thanks to Andreas Lubbe for this contribution.
-   Merged Apply codestyles on each commit and run lint:fix #1126. Many thanks to Andreas Lubbe for this contribution.
-   Merged \[WIP\] Replace sax with saxes #1127. Many thanks to Andreas Lubbe for this contribution.
-   Merged Add PR, Feature Request and Question github templates #1128. Many thanks to Andreas Lubbe for this contribution.
-   Merged fix issue #749 Fix internal link example errors in readme #1137. Many thanks to Alan Wang for this contribution.

3.8.2

-   Merged Update @types/node version to latest lts #1133. Many thanks to Siemienik Paweł for this contribution.
-   Merged fix issue #1118 Adding Data Validation and Conditional Formatting to the same sheet causes corrupt workbook #1134. Many thanks to Alan Wang for this contribution.
-   Merged Add benchmarking #1139. Many thanks to Andreas Lubbe for this contribution.
-   Merged fix issue #731 image extensions not be case sensitive #1148. Many thanks to Alan Wang for this contribution.
-   Merged fix issue #1165 and update index.d.ts #1169. Many thanks to Alan Wang for this contribution.

3.9.0

-   Merged Optimize SAXStream #1140. Many thanks to Andreas Lubbe for this contribution.
-   Merged fix issue #1057 Fix addConditionalFormatting is not a function error when using Streaming XLSX Writer #1143. Many thanks to Alan Wang for this contribution.
-   Merged fix issue #204 sets default column width #1160. Many thanks to Alan Wang for this contribution.
-   Merged Include cell address for Shared Formula master must exist.. error #1164. Many thanks to Brad Reed for this contribution.
-   Merged Typo in DataValidation examples #1166. Many thanks to Matthieu Ravey for this contribution.
-   Merged fixes #1175 #1176. Many thanks to Siemienik Paweł for this contribution.
-   Merged fix issue #1178 and update index.d.ts #1179. Many thanks to Alan Wang for this contribution.
-   Merged Simple test if typescript is able to compile #1182. Many thanks to Siemienik Paweł for this contribution.
-   Merged More improvements #1190. Many thanks to Andreas Lubbe for this contribution.
-   Merged Ensure all node\_modules are compatible with IE11 #1193. Many thanks to Andreas Lubbe for this contribution.
-   Merged fix issue #1194 and update index.d.ts #1199. Many thanks to Alan Wang for this contribution. This fixes \[BUG\] TypeScript version doesn't have definition for Worksheet.addConditionalFormatting #1194.
Merged fix issue #1157 marked Cannot set property #1204. Many thanks to Alan Wang for this contribution. This fixes \[BUG\] Cannot set property 'marked' of undefined #1157.-   Merged Deprecate createInputStream #1209. Many thanks to Andreas Lubbe for this contribution.
Merged fix issue #1206 #1205 Abnormality of and attributes #1210. Many thanks to Alan Wang for this contribution. This fixes \[BUG\] Unlocked cells do not maintain their unlocked status after reading and writing a workbook. #1205 and \[BUG\] Unlocked cells lose their vertical and horizontal alignment after a read and write. #1206.

3.10.0

-   Merged \[Chore\] Upgrade dependencies #1233. Many thanks to Andreas Lubbe for this contribution.
Merged Fix issue #1198 Absolute path and relative path need to be compatible #1220. Many thanks to Alan Wang for this contribution. This fixes \[BUG\] Loading OpenPyXL workbooks #1198. Merged Upgrade tmp #1234. Many thanks to Andreas Lubbe for this contribution. This fixes Process doesn't exit < 8.12.0 #882.-   Merged New version of dayjs requires explicit `Z` in the date formats #1270. Many thanks to Andreas Lubbe for this contribution.
Merged Fixed #1276 #1280. Many thanks to Subhajit Das for this contribution. This fixes \[BUG\] Invalid regular expression: /^\[ -íŸ¿î€€-ï¿½ð�€€-ô�¿¿\]$/: Range out of order in character class #1276. Merged \[bugfix\] Fix special cell values causing invalid files produced #1278. Many thanks to Alan Wang for this contribution. This fixes Special cell value results invalid file #703.-   Merged Re-translation of simplified Chinese documents (zh-cn) #1208. Many thanks to 不如怀念 for this contribution.
-   Merged data-validations-xform: keep formulae if type not exists #1229. Many thanks to myfreeer for this contribution.
Merged WorkbookWriter support rowBreaks #1257. Many thanks to Alan Wang for this contribution. This fixes \[BUG\] WorkbookWriter doesn't support headerFooter and rowBreaks. #1248.-   Merged Fixed ascii only #1289. Many thanks to Subhajit Das for this contribution.
-   Merged Supports setting cell comment properties #1159. Many thanks to Alan Wang for this contribution.
-   Merged docs: add links to top with jump2header #1215. Many thanks to Dragoș Străinu for this contribution.
-   Merged Fix cell.text return an empty object when cell is empty #1310. Many thanks to Alan Wang for this contribution.
-   Merged Use rest args instead of slicing arguments #1303. Many thanks to Andreas Lubbe for this contribution.

4.0.1

-   A Major Version Change - The main ExcelJS interface has been migrated from streams based API to Async Iterators making for much cleaner code. While technically a breaking change, most of the API is unchanged For details see UPGRADE-4.0.md.
-   This upgrade has come from the following merges:
    
    -   \[MAJOR VERSION\] Async iterators #1135
    -   \[MAJOR VERSION\] Move node v8 support to ES5 imports #1142
    
    A lot of work from the team went into this - in particular Andreas Lubbe and Siemienik Paweł.

4.1.0

-   Merged Remove const enum and add ErrorValue in index.d.ts #1317 Many thanks to Alex Plumley for this contribution.
-   Merged update README.md and READEME\_zh.md #1319 Many thanks to Alan Wang for this contribution.
-   Merged Added insert rows functionality with new style inherit options #1324 Many thanks to Subhajit Das for this contribution.
-   Merged Updated readme for insert rows #1327 Many thanks to Subhajit Das for this contribution.
-   Merged Fix: Async iterators definition #1338 Many thanks to Julien - JuH for this contribution.
-   Merged \[bugfix\] Fix special cell values causing invalid files produced(#1339) #1344. This fixes \[BUG\] hasOwnProperty, constructor special words not serialized correctly with stream.xlsx.WorkbookWriter #1339. Many thanks to Alan Wang for this contribution.
-   Merged Fix the error that comment does not delete at spliceColumn #1334. Many thanks to sdg9670 for this contribution.
-   Merged bug fix can not read property date1904 of undefined #1328. Many thanks to 1328 for this contribution.

4.1.1

-   Merged update index.d.ts #1356 Many thanks to Siemienik Paweł for this contribution.
-   Merged Fix styleOption error in index.ts #1358. This fixes \[BUG\] 4.1.0 causes TypeScript compilation errors - addRows styleOption should be optional? #1357. Many thanks to sdg9670 for this contribution.
-   Merged Improved documentation #1354 Many thanks to Subhajit Das for this contribution.

4.2.0

-   Merged Fix issue #1431 Streaming WorkbookReader \_parseSharedStrings doesn't handle rich text within shared string nodes #1432. Many thanks to Reza Heidari for this contribution.
-   Merged Change typing for colorScale colour to array of colours #1442. Many thanks to Leondro Lio for this contribution.
-   Merged AddRow/s and InsertRow/s now returning the newly added rows #1443. Many thanks to Subhajit Das for this contribution.
-   Merged fix docs #1475. Many thanks to Dmytro Kyba for this contribution.
-   Merged \[bugfix\]Fix Issue #1254 and update index.d.ts #1360. This should fix \[BUG\] getSheetValues() typescript definition is incorrect #1254. Many thanks to Alan Wang for this contribution.
-   Merged Fix issue #1261 WorkbookWriter sheet.protect() function doesn't exist #1262. This should fix \[BUG\] WorkbookWriter sheet.protect() function doesn't exist #1261. Many thanks to Reza Heidari for this contribution.
-   Merged README: images not supported in streaming mode #1405. Many thanks to Christian d'Heureuse for this contribution.
-   Merged Run linter with prettier 2 #1477. Many thanks to Andreas Lubbe for this contribution.
-   Merged Increase the performance of some xml and html helpers #1476. Many thanks to Andreas Lubbe for this contribution.
-   Merged Performance improvement in col-cache #1482. Many thanks to Kevin Kwok for this contribution.
-   Merged Fix type definition for DefinedNamesRanges #1481. Many thanks to Kevin Kwok for this contribution.
-   Merged Fixed undefined ref error when setting a data validation that is a range of cells at the worksheet level #1480. Many thanks to Bene-Graham for this contribution.
-   Merged add A3 paperSize number #1485. This should fix \[F\] The printing size can be set to A3 #1406. Many thanks to skypesky for this contribution.
-   Merged Fix #1364 Incorrect Worksheet Name on Streaming XLSX Reader #1478. This should fix \[BUG\] Incorrect Worksheet Name on Streaming XLSX Reader #1364. Many thanks to Kevin Kwok for this contribution.
-   Merged grunt: skip babel transpile for core-js #1466. Many thanks to myfreeer for this contribution.
-   Merged xlsx: use TextDecoder and TextEncoder in browser #1486. Many thanks to myfreeer for this contribution.
-   Merged Refine typing for Column #1488. This should fix \[BUG\] Typescript error from getColumn.eachCell #1120. Many thanks to Selwyn Yeow for this contribution.
-   Merged col-cache: optimize for performance #1489. Many thanks to myfreeer for this contribution.
-   Merged Add lastColumn property (fixes #1453) #1487. This should fix property of worsheet.lastcolumn #1453. Many thanks to FliegendeWurst for this contribution.
-   Merged Add a test for CSV writeFile encoding #1495. This should close \[BUG\] Export CSV garbled characters #1473. and Can't get hebrew to display correctly in a generted CSV file #995. Many thanks to Joseph Dykstra for this contribution.
-   Merged Clarify `encoding` option is just for `.writeFile` #1496. Many thanks to Joseph Dykstra for this contribution.
-   Merged Merge cells after row insert #1377. Many thanks to Curt Commander for this contribution.
-   Merged Fix issue 1474 (to check invalid sheet name) #1484. This should fix \[BUG\] Incorrectly handles '/', ':' characters in sheet name #1474. Many thanks to skypesky for this contribution.

4.2.1

-   Merged Typing FillPattern fgColor should be optional #1550. Many thanks to Andries Smit for this contribution.
-   Merged Fixed return type on getRows #1564. Many thanks to Paul Mcilwaine for this contribution.
-   Merged fix #1598 lint violations #1599. Fixes \[BUG\] npm run lint reports multiple violations #1598. Many thanks to Ilya I for this contribution.
-   Merged Fix fullAddress row and col types #1606. Many thanks to Adam Eisenreich for this contribution.

4.3.0

-   Merged Add TS declarations of Workbook properties #1656. Many thanks to Tanawit Kritwongwiman for this contribution.
-   Merged Fix issue #178 #201. Many thanks to Vasiliy Stavenko for this contribution.
-   Merged doc: add example for solid pattern usage #1649. Many thanks to fpaupier for this contribution.
-   Merged Add type definition for lastColumn property (fixes #1453) #1629. Fixes Add type for property of worsheet.lastcolumn #1453. Many thanks to Daniel Gonçalves for this contribution.
-   Merged fix #1598 lint violations #1599. Fixes \[BUG\] npm run lint reports multiple violations #1598. Many thanks to Ilya I for this contribution.
-   Merged Update @types/node version to latest lts #1133. Fixes ERROR in node\_modules/exceljs/index.d.ts(1648,34): error TS2503: Cannot find namespace 'NodeJS'. #971 and ERROR in node\_modules/exceljs/index.d.ts(1661,34): error TS2503: Cannot find namespace 'NodeJS'. #997. Many thanks to Siemienik Pawel for this contribution.
-   Merged Added Node v16 to the test suite #1731. Many thanks to Alex Bjørlig for this contribution.
-   Merged Readme moment to dayjs #1708. Many thanks to Jerebtw for this contribution.
-   Merged Ability to set tooltip for hyperlink #602. Many thanks to Aleksey Kuznetsov for this contribution.
-   Merged Fixed conditional format corrupting sheet #1305 #1574. Fixes \[BUG\] Errors when opening file in Excel after saving a file with conditional formatting #1305. Many thanks to Rolando Romero for this contribution.
-   Merged Improvements for images (correct reading/writing possitions) #702. Many thanks to Siemienik Pawel for this contribution.
