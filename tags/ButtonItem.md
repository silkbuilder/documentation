# silk:ButtonItem
The *silk:ButtonItem* defines the sub-buttons for a "Drop-down Button". Adding a *silk:ButtonItem* to a *silk:Button* converts it into a "Drop-down Button".

This is a standalone component.

## Tag Definition
Used standalone:
```xml
<silk:ButtonItem
  id=""
  label=""
  icon=""
  confirmTitle=""
  confirmMessage=""
  confirmLabel=""
  confirmIcon=""
  toggleList=""
  logicGrid=""
  criteria=""
  renderIf=""
  targetPage=""
/>
```

## Properties 
### id
The button's unique identifier.<br>If the button's events are not going to be used, the id is not required.<br>Default Value: *Empty*.
### label
The label is used as the button's label. It is not required if the button only shows an icon.<br>Default Value: *Empty*.
### icon
The icon class is from a Font Awesome icon.<br>Default Value: *Empty*.
### confirmTitle
Sets the title of the confirmation dialog.<br>Default Value: *Empty*.
### confirmMessage
Sets the message to show in the confirmation dialog.<br>Default Value: *Empty*.
### confirmLabel
Sets the label for the accept button in the confirmation dialog.<br>Default Value: *Empty*.
### confirmIcon
Sets the confirmation dialog icon.<br>Default Value: *Empty*.
### toggleList
The list of comma-separated elements that will be toggled together with the component.<br>The value "parent" toggles the immediate parent element.<br>The value "grandpa" toggles the grandparent element.<br>Default Value: *Empty*.
### logicGrid
Default Value: *Empty*.
### criteria
Default Value: *Empty*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
### targetPage
The ID of the page to be shown when the button is clicked. This also works with *silk:Modal*.<br>If opening a page/modal is the only button's functionality, then an ID is not necessary.<br>Default Value: *Empty*.
