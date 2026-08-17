# silk:Group
The *silk:Group* component is used to group elements under a title.

## Tag Definition
Used standalone:
```xml
<silk:Group
  id=""
  title=""
  renderIf=""
  negation=""
  cssClass=""
  cssStyle=""
/>
```
Used as a container:
```xml
<silk:Group
  id=""
  title=""
  renderIf=""
  negation=""
  cssClass=""
  cssStyle=""
>
   Contains: Other HTML and/or Silk components.
</silk:Group>
```

## Properties 
### id
An optional group's unique identifier.<br>Default Value: *Empty*.
### title
Defines the group title.<br>Default Value: *Empty*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
### negation
If set to true, the logic statement result from the *renderIf* property will be negated. This is like saying "not renderIf".<br>Default Value: *Empty*.
### cssClass
The CSS classes to stylize the group wrapper".<br>Default Value: *Empty*.
### cssStyle
To add extra styling using CSS styling elements.<br>Default Value: *Empty*.
