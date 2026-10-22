# silk:Table
The component silk:Table visualizes data from a silk:DataProvider in a tabular format with columns and rows.

## Tag Definition
Used as a container:
```xml
<silk:Table
  id=""
  title=""
  cssClass=""
  containerClass=""
  dataSource=""
  autoSelect="true"
  selectable="true"
  targetPage=""
  header="fixed"
  treeData="undefined"
  rootLabel=""
  noRoot="false"
  multiRoot="false"
  deleteBranch="false"
  iconOpen="far fa-folder-open fa-lg"
  iconClose="far fa-folder  fa-lg"
  iconEmpty="far fa-file fa-lg"
  collapsable="true"
  collapsedLevel="100"
  parentList=""
  searchable="false"
  dpSearch="false"
  input="false"
  renderIf=""
  init="true"
  toggleList=""
  pill=""
>
   Contains: silk:Column, silk:Header, and silk:Body components.
</silk:Table>
```
### Basic Configuration

For a basic configuration, a table only needs an ID, the name of the **silk:DataProvider** working as the *dataSource*, and contain the definition of the columns to be displayed. The columns are defined with the **silk:Columns** component.

```xml
<silk:Table id="dataList" dataSource="dataDP" >
<silk:Columns title="Name" />{name}<silk:columns/>
  <silk:Columns title="Address" />{address}<silk:columns/>
</silk:Table>
```

### With a Title

If it is necessary to differentiate the information the table is showing from other components, a title can be added using the *title* property. This will add a header showing the provided text.

```xml
<silk:Table id="dataList" dataSource="dataDP" title="People List" >
<silk:Columns title="Name" />{name}<silk:columns/>
  <silk:Columns title="Phone" />{phoneNumber}<silk:columns/>
</silk:Table>
```

### Searchable

With a large number of rows, it becomes necessary to be able to filter the rows based on a search text criterion. Setting the property *searchable* to *"true"* will add a search input to the header. Using this input, the user can enter a text that will be used to filter the rows.

```xml
<silk:Table id="dataList" dataSource="dataDP" title="People List" searchable="true" >
<silk:Columns title="Name" />{name}<silk:columns/>
  <silk:Columns title="Phone" />{phoneNumber}<silk:columns/>
</silk:Table>
```

### Header with elements

The component **silk:TableHeader** is used to add extra elements to the table's header. This works in conjunction with the **silk:TableBody** component to group the table's columns.

```xml
<silk:Table id="dataList" dataSource="dataDP" title="People List" >
  <silk:TableHeader>
    <silk:Button id="" label="" />
  </silk:TableHeader>
  <silk:TableBody>
<silk:Columns title="Name" />{name}<silk:columns/>
  <silk:Columns title="Phone" />{phoneNumber}<silk:columns/>
  </silk:TableBody>
</silk:Table>
```

### Empty Message

The component **silk:TableEmpty** is used to define a message, or other elements, to indicate that the table does not have rows to display.

```xml
<silk:Table id="dataList" dataSource="dataDP" title="People List" >
  <silk:TableBody>
<silk:Columns title="Name" />{name}<silk:columns/>
  <silk:Columns title="Phone" />{phoneNumber}<silk:columns/>
  </silk:TableBody>
  <silk:TableEmpty>
  No records return.
  </silk:TableEmpty>
</silk:Table>
```

With the use of other properties, the **silk:Table** component can be configured to be used in multiple scenarios.

## Properties 
<sup>*</sup>Required property.
### id<sup>*</sup>
The component's unique identifier.<br>Default Value: *Empty*.
### title
The table's title. This is not a required attribute.<br>Default Value: *Empty*.
### cssClass
A list of extra CSS classes styling the table.<br>Default Value: *Empty*.
### containerClass
A list of extra CSS classes styling the table's container.<br>Default Value: *Empty*.
### dataSource
The ID of the *silk:DataProvider* used to fill the table content.<br>Default Value: *Empty*.
### autoSelect
Defines if the first row will be auto-selected. This is set to *true* by default.<br>Default Value: *true*.
### selectable
Determines if the rows will change their background when selected. The values are true, false.<br>By default, a table row is not visually selected; change the row color if the host page is the only one visible. If the desire is to have the chosen row always marked selected, then the values should be set to "always."<br>Default Value: *true*.
### targetPage
This indicates how the header will be placed. The values are:<br>- fixed: Attaches the top header and table header to the page's top.<br>- inline: Attaches the header and table header to the top of the table's location.<br>- none: No top header or table header.<br>- top-fixed: Attached top header to the page's top, no table header.<br>Default Value: *Empty*.
### header
This indicates how the header will be placed. The values are:<br><br>- fixed: Attaches the top header and table header to the page's top.<br><br>- inline: Attaches top header and table header to the top of the table's location.<br><br>- none: No top header or table header.<br>- top-fixed: Attached top header to the page's top, no table header.<br>Default Value: *fixed*.
### treeData
Defines if the table should process the data as a data tree. This value is usually inherited from the DataProvider but can be overwritten with this property if necessary.<br>Default Value: *undefined*.
### rootLabel
Set the label/name of the tree's root. This only works if *dataProvider* is set to *treeData="true"*.<br>Default Value: *Empty*.
### noRoot
Sets the root to be treated like a "regular row". Only works in data tree mode.<br>Default Value: *false*.
### multiRoot
Sets the tree to support multiple root branches. Only works in data tree mode and when noRoot is true.<br>Default Value: *false*.
### deleteBranch
Defines whether the tree allows a branch to be deleted. By default, only leaves are to be deleted.<br>It is the developer's responsibility to program the child branches or leaves deletion.<br>Default Value: *false*.
### iconOpen
The Font Awesome classes defining the open branch icon. Only works in data tree mode.<br>Default Value: *far fa-folder-open fa-lg*.
### iconClose
The Font Awesome classes defining the close branch icon. Only works in data tree mode.<br>Default Value: *far fa-folder  fa-lg*.
### iconEmpty
The Font Awesome classes defining the empty branch icon. Only works in data tree mode.<br>Default Value: *far fa-file fa-lg*.
### collapsable
Sets the branch to be able to collapse or unfold. Only works in data tree mode.<br>Default Value: *true*.
### collapsedLevel
Indicates which level the branch will initially be displayed collapsed. Only works in data tree mode.<br>Default Value: *100*.
### parentList
The ID of another *silk:Table* component, whose click row event will trigger a *load* event in this component.<br>Default Value: *Empty*.
### searchable
Opens a text input to filter the table data based on the entered text. By default, it searches and filters the data that has been loaded. When *dpSearch="true"* it will search and filter based on conditions set in the ORM.<br>Default Value: *false*.
### dpSearch
If set to *true,* a search action will trigger the event *select* in the selected dataSource. The developer should send the search text to the ORM using the *beforeSelect* event in the **silk:DataProvider**.<br>Default Value: *false*.
### input
Defines if the table will be initialized in "data entry" mode.<br>Default Value: *false*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
### init
Indicates if the table should initialize at creation time. This property should be set to *true* if it will be initialized programmatically.<br>Default Value: *true*.
### toggleList
The list of comma-separated elements that will be toggled together with the component.<br>The value "parent" toggles the immediate parent element.<br>The value "grandpa" toggles the grandparent element.<br><br>Default Value: *Empty*.
### pill
Defines if the table will use rows or table styled as pills.<br>The accepted values are true, row, or table.<br>This will inject the classes table-pill or row-pill to the table structure.<br>Default Value: *Empty*.
