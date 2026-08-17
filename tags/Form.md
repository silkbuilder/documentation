# silk:Form
The **silk:Form** component serves as a data visualizer and adds the typical form to manipulate the information. It provides the interface for the user to perform tasks like adding, editing, and deleting records, connecting to the **silk:Table** and the **silk:DataProvider**.

The information collected by the Form is sent to the server using the **silk:DataProvider** component.

## Tag Definition
Used standalone:
```xml
<silk:Form
  id=""
  dataSource=""
  parentForm=""
  dialog="true"
  dialogTitle=""
  dialogPosition=""
  insertBt=""
  updateBt=""
  deleteBt=""
  cancelBt=""
  submitBt=""
  mode="false"
  buttonTarget=""
  buttonTest=""
  autoFocus=""
  insertTitle="Adding"
  updateTitle="Editing"
  deleteTitle="Deleting"
  insertMessage="Created"
  updateMessage="Edited"
  deleteMessage="Deleted"
  renderIf=""
  init="true"
  cssClass=""
  toggleList=""
  toggleEdit=""
  confirmTitle=""
  confirmMessage=""
  confirmLabel=""
  confirmIcon=""
  confirmTarget=""
  action=""
  target=""
  method=""
/>
```
Used as a container:
```xml
<silk:Form
  id=""
  dataSource=""
  parentForm=""
  dialog="true"
  dialogTitle=""
  dialogPosition=""
  insertBt=""
  updateBt=""
  deleteBt=""
  cancelBt=""
  submitBt=""
  mode="false"
  buttonTarget=""
  buttonTest=""
  autoFocus=""
  insertTitle="Adding"
  updateTitle="Editing"
  deleteTitle="Deleting"
  insertMessage="Created"
  updateMessage="Edited"
  deleteMessage="Deleted"
  renderIf=""
  init="true"
  cssClass=""
  toggleList=""
  toggleEdit=""
  confirmTitle=""
  confirmMessage=""
  confirmLabel=""
  confirmIcon=""
  confirmTarget=""
  action=""
  target=""
  method=""
>
   Contains: silk:Input and HTML components.
</silk:Form>
```

## Properties 
<sup>*</sup>Required property.
### id<sup>*</sup>
The Form's unique identifier.<br>Default Value: *Empty*.
### dataSource
The component's identifier provides the record's columns used by the form's inputs. This can be a **silk:Table** or a **silk:DataProvider**.<br>In the case of **silk:Table** the Form will use the selected row record.<br>In the case of a **silk:DataProvider** the form will use the the first record.<br>If not provided, it is expected for the form's inputs to be initialize programmatically.<br>Default Value: *Empty*.
### parentForm
The identifier of a Form to connect to its dataSource will be used to initialize its children's input.<br>Default Value: *Empty*.
### dialog
Defines if the form's dialog bar containing the Submit and Cancel buttons should be displayed in editing mode.<br>Default Value: *true*.
### dialogTitle
Sets a title for the editing dialog when the form is editable.<br>Default Value: *Empty*.
### dialogPosition
Defines if the dialog will be placed at the page header, top or the bottom of the form.<br>If not provided the dialog is placed in the page's header by default.<br>Default Value: *Empty*.
### insertBt
The name of the button that will be used to trigger an insert action.<br>Default Value: *Empty*.
### updateBt
The name of the button that will be used to trigger an update action.<br>Default Value: *Empty*.
### deleteBt
The name of the button that will be used to trigger a delete action.<br>Default Value: *Empty*.
### cancelBt
The name of the button that will be used to trigger a cancel action.<br>Default Value: *Empty*.
### submitBt
The name of the button that will be used to trigger a submit action.<br>Default Value: *Empty*.
### mode
Defines the initial status of the Form. If *true,* it will initialize as editable. It also supports the values "read" or "write."<br>Default Value: *false*.
### buttonTarget
A comma-separated list of pages used to place the auto-generated action buttons. These buttons will be placed in the page's header.<br>The order is the page for the insert button, the page for the edit button, and the page for the delete button.<br>Only including the insert page will default this page for the other buttons.<br>Including the insert and edit page will default the edit page as the target for the delete button.<br>Sending the value *none* or *null* for any page will not generate that button.<br>This example will only generate the edit button: *buttonTarget="none,formPage,none"*.<br>Default Value: *Empty*.
### buttonTest
Receives the logical sentences defining whether the action buttons will be added at render time. The explanation on how to use the logic statement is found in <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>This follows the same order as the *buttonTarget* property but separated by a pipe symbol: "|".<br>Default Value: *Empty*.
### autoFocus
Enables or disables the first input auto focus. True by default.<br>Default Value: *Empty*.
### insertTitle
The text to show in the dialog bar when performing an update.<br>Default Value: *Adding*.
### updateTitle
The text to show in the dialog bar when operating an update.<br>Default Value: *Editing*.
### deleteTitle
The text to show in the dialog bar when operating a delete.<br>Default Value: *Deleting*.
### insertMessage
The message to show after operating an insert.<br>Default Value: *Created*.
### updateMessage
The message to show after operating an update.<br>Default Value: *Edited*.
### deleteMessage
The message to show after operating a delete.<br>Default Value: *Deleted*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
### init
Defines if the component will be initialized after being created.<br>Default Value: *true*.
### cssClass
The CSS class or classes to be added to the Form.<br>Default Value: *Empty*.
### toggleList
The list of comma-separated elements that will be toggled together with the component.<br>The value "parent" toggles the immediate parent element.<br>The value "grandpa" toggles the grandparent element.<br>Default Value: *Empty*.
### toggleEdit
The list of comma-separated elements that will be inversely toggled when the form is in editing mode. This is used to hide elements when the form changes to editable mode.<br>Default Value: *Empty*.
### confirmTitle
Sets the title of the confirmation dialog.<br>Default Value: *Empty*.
### confirmMessage
Sets the message to show in the confirmation dialog.<br>Default Value: *Empty*.
### confirmLabel
Sets the label for the accept button in the confirmation dialog.<br>Default Value: *Empty*.
### confirmIcon
Sets the confirmation dialog icon.<br>Default Value: *Empty*.
### confirmTarget
Sets which actions will trigger the confirmation dialog.<br>Default Value: *Empty*.
### action
Set the action property. If used the form will use the tag FORM instead of a DIV.<br>Default Value: *Empty*.
### target
Sets the form's target.<br>Default Value: *Empty*.
### method
Sets the form's method.<br>Default Value: *Empty*.
