# Box
 Wraps the HTML element produced by the [silk:Box](silk:Box) tag (`#id`)
 and re-renders its inner HTML from an HTML template plus the
 currently selected data-source item.

 Lifecycle:
 1. `new Box(id, options)`
 2. `initBox()` — binds `$box` to the DOM node
 3. `load()` — fills the node from the data source

 Depends on framework helpers: `ifUndefined`, `getTemplateData`, `callFunction`. 

Example
 ```
 var box = new Box("detailPanel", {
   template: "<h2>{{title}}</h2><p>{{body}}</p>",
   dataSource: myTable
 });
 initBox();
 load();
 ```

**Kind**: global class  


## Constructor
 <a name="_new"></a>

### new Box(id, [options])
Box UI component bound to a SilkBuilder data source.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| id | <code>string</code> |  | Unique DOM id of the box element (without `#`). |
| [options] | <code>Object</code> |  | Construction options. |
| [options.template] | <code>string</code> | <code>&quot;\&quot;\&quot;&quot;</code> | HTML template with data-binding fields. |
| [options.dataSource] | <code>Object</code> | <code></code> | Table / DataProvider instance   exposing `getSelectedItem()`. |

## Methods
 <a name="+getTemplate"></a>

### getTemplate() ⇒ <code>string</code>
HTML template used to render the box contents.

**Kind**: instance method of [<code>Box</code>](#Box)  
<a name="Box+hide"></a>

### hide()
Hide the  Equivalent to `toggle(false)`.
Requires [initBox](#Box+initBox).

**Kind**: instance method of [<code>Box</code>](#Box)  
<a name="Box+initBox"></a>

### initBox()
Bind `$box` to `$("#" + id)`. Call once after the element exists in the DOM.

**Kind**: instance method of [<code>Box</code>](#Box)  
<a name="Box+load"></a>

### load()
Render the box from the current data-source selection.

Uses `getTemplateData(template, 0, dataSource.getSelectedItem())`
and writes the result into `$box`. No-op if `dataSource` is null.
Requires [initBox](#Box+initBox).

**Kind**: instance method of [<code>Box</code>](#Box)  
<a name="Box+setTemplate"></a>

### setTemplate(newTemplate)
Replace the HTML template used on the next [load](#Box+load).
Does not re-render until `load()` is called.

**Kind**: instance method of [<code>Box</code>](#Box)  

| Param | Type | Description |
| --- | --- | --- |
| newTemplate | <code>string</code> | New template markup. |

<a name="Box+show"></a>

### show()
Show the  Equivalent to `toggle(true)`.
Requires [initBox](#Box+initBox).

**Kind**: instance method of [<code>Box</code>](#Box)  
<a name="Box+toggle"></a>

### toggle([status])
Show, hide, or flip visibility of the 

- No argument: jQuery `.toggle()` (flip current state).
- `boolean`: show if `true`, hide if `false`.
- Other value: evaluated with `callFunction(status)` and passed to
  jQuery `.toggle()`.

Requires [initBox](#Box+initBox) first.

**Kind**: instance method of [<code>Box</code>](#Box)  

| Param | Type | Description |
| --- | --- | --- |
| [status] | <code>boolean</code> \| <code>\*</code> | Visibility flag or callable specifier. |


