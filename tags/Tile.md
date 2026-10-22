# silk:Tile
The component **silk:Tile** distributes the data in a grid layout. The data is provided by a **silk:DataProvider** component.

## Tag Definition
Used as a container:
```xml
<silk:Tile
  id=""
  tag="div"
  align="center"
  dataSource=""
  parentList=""
  cssClass=""
  columns="0"
  rowClass=""
  selectedClass=""
  renderer=""
  targetPage=""
  autoSelect="true"
>
   Contains: HTML template.
</silk:Tile>
```

## Properties 
<sup>*</sup>Required property.
### id<sup>*</sup>
The tile's unique identifier.<br>Default Value: *Empty*.
### tag
The HTML tag used as the Tail wrapper. If not provided, it uses "div".<br>Default Value: *div*.
### align
The tile elements alignment. The accepted values are:<br>- start<br>- end<br>- center<br>- between<br>- around<br>- evenly<br>Default Value: *center*.
### dataSource
Set the name of the **silk:DataProvider** providing the data to render the tail's content.<br>Default Value: *Empty*.
### parentList
The list which will be used to trigger data loading.<br>Default Value: *Empty*.
### cssClass
Set the CSS Class used to stylize the tail container.<br>Default Value: *Empty*.
### columns
Set the number of columns a row could have to simulate a <div> table. This is optional<br>Default Value: *0*.
### rowClass
Set the CSS Class used to stylize the generated row if columns are more than 0.<br>Default Value: *Empty*.
### selectedClass
Set the CSS Class use to mark the selected cell.<br>Default Value: *Empty*.
### renderer
The name of the JavaScript function that will process the cell data.<br>Default Value: *Empty*.
### targetPage
This indicates how the header will be placed. The values are:<br>- fixed: Attaches the top header and table header to the page's top.<br>- inline: Attaches the header and table header to the top of the table's location.<br>- none: No top header or table header.<br>- top-fixed: Attached top header to the page's top, no table header.<br>Default Value: *Empty*.
### autoSelect
Defines if the first row will be auto-selected. This is set to *true* by default.<br>Default Value: *true*.
