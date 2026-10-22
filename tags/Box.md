# silk:Box
The <silk:Box> component generates an DIV element supporting templates.

## Tag Definition
Used standalone:
```xml
<silk:Box
  id=""
  dataSource=""
  tag="div"
  cssClass="btn-primary"
  cssStyle=""
  renderIf=""
/>
```

## Properties 
<sup>*</sup>Required property.
### id<sup>*</sup>
The Column's unique identifier.<br>Default Value: *Empty*.
### dataSource
The component's identifier provides the record's columns used by the form's inputs. This can be a **silk:Table** or a **silk:DataProvider**.<br>In the case of **silk:Table** the Form will use the selected row record.<br>In the case of a **silk:DataProvider** the form will use the the first record.<br>If not provided, it is expected for the form's inputs to be initialize programmatically.<br>Default Value: *Empty*.
### tag
The HTML tag used as the Tail wrapper. If not provided, it uses "div".<br>Default Value: *div*.
### cssClass
The classes to stylize the button. It expects Bootstrap classes. The button already has the "btn" class and is initialized with "btn-primary".<br>Default Value: *btn-primary*.
### cssStyle
To add extra styling using CSS styling elements.<br>Default Value: *Empty*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
