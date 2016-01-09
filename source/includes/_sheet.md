# Sheet

A Dtab spreadsheet or sheet is basically a spreadsheet that allows users to write javascripts and apply them to target cells or ranges.
It has two (2) most important sections upon opening a sheet:

* Grid - sheet cell data.
* Notebook - sheet notes.

## Grid

A grid contains many columns and rows. Each column can have labels from A to Z, and each row has a numeric index number.
Within the grid are the cells. Each cell can contain either text, number, formula, or function. 
A formula or a function within the cell starts with *=* sign. 

A javascript function call is possible within this app. 

If the following method is defined, a cell with the content *= foo()* will have the value *Hello World*.

```javascript
function foo(){
  return 'Hello World';
}
````

## Notebook

A notebook consists of multiple notes. 
Upon loading a sheet, all notes will be loaded based on the notes' orders.

### Note

A note has 3 different sections:

* Tag - usually hidden for normal mode, and shown when a note is in hidden mode.
* Content - javascript code, mardown code, or html code.
* Result - charts and related info for javascript note; html code for html/markdown note.

Besides the above sections, a note has 2 other buttons resided top right corner: note type and options

*Note type* defines the note type. It has one of the following types:

* Javascript - javascript code.
* Mardown - mardown code.
* Html - HTML code.

Markdown and HTML translated code will be updated live while typing.

*Options* button provide additional note options as followed:

* Move up - move note order 1 level up.
* Move down - move note order 1 level down.
* Add before - add a blank note before the current note.
* Add after - add a blank note after the current note.
* Run - play/re-play the current note.
* Hide - hide note. A hidden note will only have its tag shown, its content will be hidden.
* Delete - remove note permanently. A prompt will appear if a note has more than 3 lines.

Current note is the note that is being focused. Clicking away from the current note will replay its content.

### Shortcuts

Shortcuts are recommended to use while editing notes since it provides great flexibility for moving between different notes. 

* Cmd + Enter - execute code (Windows' users can use Alt key instead)
* Ctrl + Enter - execute current note and move down the next one. If the next one does not exist, this will create a new note after the the current one.
* Ctrl + Shift + Enter - execute current note and move up the previous note. If it reaches the top, it will stay with the current note

## Charting

Charting is a unique and important feature in this app. There's a built-in wrapper on top of Highcharts that make charting quick and easy.
The following charts are supported:

* Line, multi-line (Charts.Line)
* Bar, multi-bar (Charts.Bar)
* Area, multi-area (Charts.Area)
* Stacked-area (Charts.StackedArea)
* Pie (Charts.Pie)

A detailed example can be accessed 
<a href="https://dtab.io/sheets/568f61ac6e8ca271338363eb" target="_blank"> here </a>.

### Syntax & Usage

Syntax: Charts.ChartType( dataRange, options )

All charts are part of *Charts* class. A chart call requires a data range string and an optional options.
Multiple ranges can be specified within the same string using commas. For example:

*dataRange* can be one of the following formats:

* 'A1:C10' - single data range presents the data block from top left cell A1 and bottom right cell C10. 
* 'A1:C10,A3:C7,B7:E11' - multiple data ranges present data from multiple blocks. Blocks can overlap or repeat itself for multiple datasets. 

*options* object variable contains has following optional attributes:

* el - target element for drawing, this can be a floating element on grid. Without defining this, chart will be drawn below the note.
* label - array of label strings for top, left, and bottom. A single label string is used as top label
* name - array of strings for dataset series. If a string is specified, the same name will be applied for all series.
* xAxis - array of strings for xAxises' column names. If a string is specified, the name will be applied for all datasets' xAxises.
* yAxis - a string or array of string contains name of yAxis column name. If a single string is specified, the name will be applied for all datasets' yAxises.
* showLegend - boolean value for showing or hiding chart legend. By default, it is false for single dataset, and is true for multiple datasets.

xAxis & yAxis must contain the exact column strings. Any extra spaces in the name will be consider as different column. 
If xAxis and yAxis are not spicified, the 1st column and 2nd column will be chosen fir the axises accordingly .

For Pie chart, xAxis is used as 'Categories' column and yAxis is used as 'Values' column. A pie chart only takes a single dataset.

Example of a simple chart call:

```javascript
Charts.Bar('A1:H7');
````

### Drawing multi-dataset charts

Drawing multi-dataset charts is possible by specifying mutiple data ranges or axises. 
If all datasets share the same data range block, a single data range can used concurrently with multiple xAxises and yAxises.

### Drawing on grid

A chart can be drawn directly on the sheet grid. 
A GridView element needs to be first initialized using *Dtab.GridView* class constructor. It has the following optional attributes:

* id - charting element (div) id (without '#').
* pos - x and y position object relative to the grid for the element, *{x:0, y:0}* as default.
* css - the element styles. An element has a default 500px width and 250px height.
* className - additional class names for the element.
* draggable - allow dragging, *true* as default.
* clear - clear element on play, *true* as default.

### Full example

The following is a full example of multi-bar chart extracted from the example above:

```javascript
el = new Dtab.GridView({
  id: 'chart', 
  className: 'bar-chart',
  pos: {x: 20, y: 200}, 
  css: {width: 510, height: 280},
  draggable: false,
  clear: true
});

options = {
  el: el,
  name: ["< 5", "5-13","14-17","18-24","25-44","45-64","65+"],
  label: ["Multi-bar chart", "xAxis label", 'yAxis label'],
  xAxis: "State",
  yAxis: ["Under 5 Years","14 to 17 Years","18 to 24 Years","25 to 44 Years","45 to 64 Years","65 Years and Over"],
  showLegend: false
};

Charts.Bar('A1:H7', options);
```

## Util functions

This app doesn't limit one's ability to perform any further complex charting functions. 
Users can use any external chart libraries instead of the above charting wrapper. 
The following functions can be useful for this purpose:

* dtab.getRange( dataRangeString, callback ) - get data ranges in JSON format. This can be multiple comma separated ranges.
* dtab.getNoteView() - the note chart view element. This element is placed right below the note.
* Dtab.GridView() - the constructore for initializing an element on the grid.

## Settings

Sheet settings are important to a particular sheet. All settings are placed under *Settings* tab.
This tab allow users to control external libraries, tags, privacy, and more.

### External Libraries

This gives the ability to load external javascript libraries before loading the sheet grid data. 
External function calls can be used directly in the grid cells or within the javascript notes. 

### Privacy 

A sheet can have the following type of privacy:

* Private - completely private to owner and shared users only
* Unlisted - publically available but hidden from search
* Public - publically available and shown from search

### Tags

Tags are useful feature that allows users to find related sheets within similar categories. A publically shared sheet should have tags.

### Description

This describes the sheet data and anything related to the sheet. 
It's a good idea to provide sheet description for any publically exposed sheets. This would help the search engine to find the best fit sheet within the system.