# Sheet

A Dtab spreadsheet or sheet is basically a spreadsheet that allows users to write pseudo javascripts and apply them to target cells or ranges.

## Grid

A sheet grid contains columns and rows. Each column can have labels from A to Z, and each row can 

## Notebook

A Dtab notebook consists of multiple notes. A note can be a javascript, mardown, or html note. Upon loading sheet, all notes will be loaded based on note orders.

### Note view

A note has 3 different sections:

* Tag - is usually hidden and only shown when note is in hidden mode
* Content - contains content for edit that includes javascript code, mardown code, or html code
* Result - contains charts for a javascript note; contains html note view for markdown and html codes

Besides the above sections, a note has 2 other button options: 

* Note type - allows changing note type
* Options - allows moving a note within the notebook, add before/after, execute or remove a note

### Shortcuts

Shortcuts are recommended to use while editing notes since it gives users a great flexibility moving around different block notes. 

* Cmd + Enter - execute code
* Ctrl + Enter - execute current note and move down the next one. If the next one does not exist, create a new one
* Ctrl + Shift + Enter - execute current note and move up the previous note. If it reaches the top, it will stay with the current note

## Charting

This app has a chart wrapper built on top of Highcharts to make charts easier to use with the grid data. The following charts are supported

* Line, multi-line
* Bar, multi-bar
* Area, multi-area
* Stacked-area
* Pie

### Usage

All charts are part of Charts class. A chart call requires at least one or multiple data range(s) string, and an optional options.

Data range has the format 'Cell0:Cell1'. Mutiple data ranges are separated using commas. For example:

* 'A1:C5' - single data range presents the data block from top left cell A1 and bottom right cell C5. 
* 'A1:C5,A3:C7,B7:E11' - multiple data ranges present data from multiple blocks. Blocks can overlap or repeat itself for multiple datasets. 

'options' variable contains the following attributes:

* el - target element for drawing, this can be a floating element on grid. Without defining this, chart will be drawn below the javascript note.
* labels - a string or array of string contains labels for top, left, bottom labels accordingly. A single string is used as top label
* names - a string or array of string contains names for dataset series. A single string is used as the name for all datasets.
* xAxis - a string or array of string contains name of xAxis column name. A single string is used as the name for all dataset xAxis.
* yAxis - a string or array of string contains name of yAxis column name. A single string is used as the name for all dataset yAxis.
* showLegend - boolean value for showing or hiding chart legend. By default, it is false for single dataset, and is true for multiple datasets.

For Pie chart, xAxis is used as 'Categories' column and yAxis is used as 'Values' column. A pie chart only takes a single dataset.

A complete example with multiple data ranges and options:

options = {  
  
}

Charts.Bar('')

### Drawing on grid

A chart can be drawn directly on the sheet grid. Use first initialize a chart block element on the grid and then use this element for charting. For example:


## Util functions

* dtab.getRange(rangeString, callback)

## Settings

A sheet can have different settings.

### External Libraries

This allows loading external javascript libraries before loading the sheet grid data.

### Privacy 

A sheet can have the following type of privacy:

* Private - completely private to owner and shared users only
* Unlisted - publically available but hidden from search
* Public - publically available and shown from search

### Tags

Tags are useful feature that allows users to find related sheets. A publically shared sheet should have tags.

### Description

This describes the sheet data and anything related to the sheet.