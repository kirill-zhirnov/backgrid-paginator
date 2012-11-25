<link rel="stylesheet" href="lib/backgrid.css" />
<link rel="stylesheet" href="lib/extensions/paginator/backgrid-paginator.css" />

# Backgrid.js

Backgrid.js is a set of components for building semantic and easily stylable
data grid widgets. It offers a simple, intuitive programming interface that
makes easy things easy, but hard things possible when dealing with tabular data.

## Features

The goal of Backgrid.js is to produce a set of core Backbone UI elements that
offer you all the basic displaying, sorting and editing functionalities you'd
expect, and to create an elegant API that makes extending Backgrid.js with extra
functionalities easy.

## Advantages

- No Hungarian notations.
- Solid foundation. Based on Backbone.js.
- Semantic and easily stylable. Just style with plain CSS like you would a normal HTML table.
- Low learning curve. Works with plain old Backbone models and collections. Easy things are easy, hards things possible.
- Highly modular and customizable. Componenets are just simple Backbone View classes, customization is easy if you already know Backbone.
- Lightweight. Extra features are separated into extensions, which keeps the bloat away.
- Good documentation.

## Supported browsers:

- Internet Explorer 8+ [[1]](#note-1)
- Chrome 4+
- Safari 4+
- Firefox 4+
- Opera 9+ [[2]](#note-2)

### Notes:

<span id="note-1">[1]</span>: Both the desktop and mobile versions of the above browsers are supported.

<span id="note-2">[2]</span>: Currently needs to double click on a cell to gain focus.

## Examples

```javascript
var Territory = Backbone.Model.extend({});

// Get a pageable collection of territories.
var PageableTerritories = Backbone.Paginator.clientPager.extend({
  model: Territory,
  
  // Params for $.ajax.
  paginator_core: {
    dataType: "json",
    url: "examples/territories.json"
  },
  
  // Paging info.
  paginator_ui: {
    firstPage: 1, // page indices start at 1.
    currentPage: 1,
    perPage: 15,
    totalPages: 17
  },
  
  // No need for server query, Backbone.Paginator supports loading the
  // whole thing and paging just inside the browser.
  server_api: {},
  
  // How the Pager should parse the response.
  parse: function (resp) {
    return resp;
  }
});

// Fetch all the territories and go to the page when done
var pageableTerritories = new PageableTerritories();
pageableTerritories.fetch().done(function () {
  pageableTerritories.goTo(1);
});

// Column definitions
var columns = [{
  name: "id", // The key of the model attribute
  label: "ID", // The name to display in the header
  editable: false, // By default every cell in a column is editable, but *ID* shouldn't be
  // Defines a cell type, and ID is displayed as an integer without the ',' separating 1000s.
  cell: Backgrid.IntegerCell.extend({
    orderSeparator: ''
  })
}, {
  name: "name",
  label: "Name",
  // The cell type can be a reference of a Backgrid.Cell subclass, any Backgrid.Cell subclass instances like *id* above, or a string
  cell: "string" // This is converted to "StringCell" and a corresponding class in the Backgrid package namespace is looked up
}, {
  name: "pop",
  label: "Population",
  cell: "integer" // An integer cell is a number cell that displays humanized integers
}, {
  name: "percentage",
  label: "% of World Population",
  cell: "number" // A cell type for floating point value, defaults to have a precision 2 decimal numbers
}, {
  name: "date",
  label: "Date",
  cell: "date",
}, {
  name: "url",
  label: "URL",
  cell: "uri" // Renders the value in an HTML <a> element
}];

// Initialize a new Grid instance
var grid = new Backgrid.Grid({
  columns: columns,
  collection: pageableTerritories,
  footer: Backgrid.Paginator
});

// Render the grid and attach the root to your HTML document
$("#example-1-result").append(grid.render().$el);
```

## Result

<div id="example-1-result" class="backgrid-container" style="height: 523px"></div>


## More Examples

Are you kidding me? This is a README file. Go to the [documentation](index.html
"Backbone.js Documentation") to find out more :)


## Release History

### 0.1

- Initial Release

## License
Copyright (c) 2012 Jimmy Yuen Ho Wong  
Source code licensed under the [MIT license](LICENSE-MIT "MIT License").

Documentation licenses under [GPLv3](http://www.gnu.org/licenses/gpl-3.0.html "GPLv3")

<script src="assets/js/jquery.js"></script>
<script src="assets/js/underscore.js"></script>
<script src="assets/js/backbone.js"></script>
<script src="assets/js/backbone.paginator.js"></script>
<script src="lib/backgrid.js"></script>
<script src="lib/extensions/paginator/backgrid-paginator.js"></script>
<script>
$(document).ready(function () {
    eval($("code").text());
});
</script>

