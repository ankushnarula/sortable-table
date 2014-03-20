&lt;sortable-table&gt;
================

Polymer Web Component that generates a sortable &lt;table&gt; from JSON.

Maintained by [Steven Skelton](https://github.com/stevenrskelton)

[Additional Documentation on Table Sorting](http://stevenskelton.ca/sortable-table-with-polymer-web-components/)

[Additional Documentation on Templates](http://stevenskelton.ca/advanced-uses-polymer-templates/)

## Live Demos
 
> [Auto-Generated Columns](http://files.stevenskelton.ca/sortable-table/examples/autogenerated-columns.html)

> [Cell, Header, and Footer Templates](http://files.stevenskelton.ca/sortable-table/examples/columns-with-templates.html)

> [Complex Templates](http://files.stevenskelton.ca/sortable-table/examples/columns-with-templates-that-are-templates.html)

> [Dynamically Changing Columns and Templates](http://files.stevenskelton.ca/sortable-table/examples/dynamic-columns.html)

> [Larger Datasets](http://files.stevenskelton.ca/sortable-table/examples/large-dataset.html)

> [Nesting Tables in Cells](http://files.stevenskelton.ca/sortable-table/examples/nested-tables.html)

> [Refreshing Data](http://files.stevenskelton.ca/sortable-table/examples/refreshing-data.html)

> [Selectable Row](http://files.stevenskelton.ca/sortable-table/examples/selectable-row.html)

> [Themes](http://files.stevenskelton.ca/sortable-table/examples/themes.html)

## Usage

1. Import Web Components' polyfill:

	```html
	<script src="//cdnjs.cloudflare.com/ajax/libs/polymer/0.2.1/platform.js"></script>
	<script src="//cdnjs.cloudflare.com/ajax/libs/polymer/0.2.1/polymer.js"></script>
	```

2. Import Custom Element:

	```html
	<link rel="import" href="src/sortable-table.html">
	```

3. Start using it!

	```html
	<sortable-table></sortable-table>
	```

## Options

Attribute				| Options		| Default									| Description
---						| ---			| ---										| ---
`data`	 				| *array*		| `[]`										| Data rows
`columns`				| *array*		| `null`									| Columns to display, with options. If null, columns will be computed from `data`
`sortColumn`			| *string*		| `null`									| Current sorted `column.name`
`sortDescending`		| *boolean*		| `false`									| Current sorted column sort direction
`enableRowSelection`	| *boolean*		| `false`									| Enable user interactive row selection
`selected`				| *object*		| `null`									| Element in `data`
`selectedRowStyle`		| *string*		| `background-color:` `rgba(0,96,200,0.2);`	| CSS style to apply to `selected` row
`cellTemplate`   		| *string*		| `null`									| Renderer for entire `<td></td>` cell. Access to `{{column}}`, cell `{{value}}` and original `{{row}}` object from `data`.  Will be overwritten if specified in `columns`.
`headerTemplate`		| *string*		| `null`									| Renderer for entire `<th></th>` cell. Access to `{{column}}`.  Will be overwritten if specified in `columns`.


### Data

Input format for `data` rows is an array of objects, where data for each column is a property of the row object.

### Columns

Attribute  			| Options		| Default		| Description
---					| ---			| ---			| ---
`name`	  			| *string*		| _required_	| Name of row property
`title`	  			| *string*	   	| `name`		| Text to display in column header
`formula`			| *function*	| `null`		| Single parameter `row`, return will override any value for property in `data`, as well as be used for sorting
`cellTemplate`   	| *string*		| `null`		| Renderer for entire `<td></td>` cell. Access to `{{column}}`, cell `{{value}}` and original `{{row}}` object from `data`
`headerTemplate`	| *string*		| `null`		| Renderer for entire `<th></th>` cell. Access to `{{column}}`
`footerTemplate`	| *string*		| `null`		| Renderer for entire `<td></td>` cell. Access to `{{column}}`, array of all `{{values}}` of cells in the column, and array of all original `{{rowValues}}` object from `data` _(if they are defined)_

Example of a `cellTemplate` that displays an image beside the column value:

```html
<template id="myCellTemplate">
	<td>
		<img src="{{row.img}}" alt="{{row.title}}"/>{{value}}
	</td>
</template>
```
__Note:__  Normally `row[column.name] == value`, but `value` can be manually set by specifying a `formula`. This is useful if `value` won't sort correctly but you need access to the original value.

Example of a `headerTemplate` using images to indicate sorting:

```html
<template id="myHeaderTemplate">
	<th>
		{{!(column.title) ? column.name : column.title}}
		<img hidden?="{{!(sortColumn==column.name && sortDescending)}}" alt="up" />
		<img hidden?="{{!(sortColumn==column.name && !sortDescending)}}" alt="down" />
	</th>
</template>
```

Example of a `footerTemplate` that computes the sum of a column using a filter named `sum`:

```html
<template id="sumTemplate">
	<td class="sortable-table-header" style="text-align:right">
		{{values | sum}}
	</td>
</template>
```
__Note:__  Any filter used (eg: `sum` in above example) must be a member of `PolymerExpressions.prototype`

__Note:__  `cellTemplate`, `headerTemplate` and `footerTemplate` are limited to a subset of Javascript within `{{ }}` expressions. See the [Polymer documentation](http://www.polymer-project.org/docs/polymer/expressions.html) on Expression syntax.

## Todo

- Benchmark performance
- use proper Shadow DOM host style, support theming
- Test for correct sort on mixed alpha+numeric data
- Test cell templates are accessible in all use cases
- max sizing / scrolling
- paging
- cell selection
- maybe: multi-select
- maybe: column grouping
- maybe: reload data if individual row fields change
- __Internet Explorer is completely broken__

## History

For detailed changelog, check [Releases](https://github.com/stevenrskelton/sortable-table/releases).

## License

[MIT License](http://opensource.org/licenses/MIT) © Steven Skelton