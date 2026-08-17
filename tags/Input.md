# silk:Input
The **silk:Input** tag generates an input component to show and edit data columns.

This can be contained in a **silk:Form** component to edit a series of columns in a record, or be used standalone.

## Tag Definition
Used standalone:
```xml
<silk:Input
  id=""
  type=""
  name=""
  form=""
  label=""
  description=""
  descriptionPlace=""
  width=""
  height="200px"
  scrollHeight=""
  block="false"
  placeholder=""
  maxLength=""
  dataSource=""
  valueColumn=""
  labelColumn=""
  linkedColumns=""
  required="false"
  editable="true"
  visible="true"
  hideEmpty="false"
  scope="1"
  mask=""
  value=""
  mode="false"
  cssClass=""
  extraProperties=""
  htmlToolbar="/ckeditor-conf/bar-simple.js"
  htmlTheme="/ckeditor-conf/bar-simple.js"
  target=""
  prompt=""
  promptValue=""
  template=""
  direction=""
  itemsDirection=""
  filePreview="false"
  fileDownload="false"
  filePreviewLabel="Preview"
  fileDownloadLabel="Download"
  fileUploadLabel=""
  filePreviewClass="btn-primary"
  fileDownloadClass="btn-primary"
  filePreviewIcon="fas fa-file"
  fileDownloadIcon="fas fa-file-download"
  uploadURL=""
  fileTypeList=""
  fileSizeLimit=""
  renderIf=""
  targetPage=""
  timer=""
  toggleList=""
  autocomplete="false"
/>
```

## Properties 
<sup>*</sup>Required property.
### id<sup>*</sup>
If used with a *silk:Form* the unique identifier is the name of the data column to be viewed or edited.<br>The unique identifier is any name if used as a standalone component.<br>Default Value: *Empty*.
### type<sup>*</sup>
The input type: text, textarea, code, sql, xml, js, xhtml, css html, date, time, datetime, select, numeric, integer, decimal, checkbox, button, options, radio, password, file, email, hidden, external.<br>Default Value: *Empty*.
### name
Defines the "name" of the input when used as a regular form HTML tag.<br>Default Value: *Empty*.
### form
The *silk:Form* the input will operate with.<br>Default Value: *Empty*.
### label
The text used as input's label.<br>Default Value: *Empty*.
### description
The input's description only shows in editing mode.<br>Default Value: *Empty*.
### descriptionPlace
The input's description's placement. This could be "top" or "bottom."<br>Default Value: *Empty*.
### width
Sets the width of the component in pixels or percentage.<br>Default Value: *Empty*.
### height
The height of the component in editing mode in the case of the types: textarea, code, sql, xml, js, xhtml, and html.<br>Default Value: *200px*.
### scrollHeight
The height of the component in read mode before the content needs scrolling.<br>Default Value: *Empty*.
### block
If the component is at the end of a block. The Following Inputs will start in a new line. A "block" is only available when using the *width* property.<br>Default Value: *false*.
### placeholder
If supported, the input's placeholder or helping text is shown inside the input.<br>Default Value: *Empty*.
### maxLength
The number of characters the input will allow.<br>Default Value: *Empty*.
### dataSource
The name of the *silk:DataProvider* providing the label and value list for the inputs "select", "options", and "radio".<br>Default Value: *Empty*.
### valueColumn
Defines the column name from the *DataSource* to be used to retrieve the item's value.<br>Only necessary if different than the input's id if used under the *Silk:Form* component. Use in select, options, and radio.<br>Default Value: *Empty*.
### labelColumn
Defines the column name from the *DataSource* that will be used as the item's label. If the column name is "label," it does not need to be included.<br>Default Value: *Empty*.
### linkedColumns
Indicates the dataProvider's columns that will be updated in the dataSource after the form data is accepted. To use in select, options, and radio.<br>Default Value: *Empty*.
### required
The logic value or JavaScript expression to determine if the component should be required before data submission.<br>Default Value: *false*.
### editable
The logic value or JavaScript expression to determine if the component should be editable.<br>Default Value: *true*.
### visible
The logic value or JavaScript expression to determine if the component should be visible.<br>Default Value: *true*.
### hideEmpty
Sets the input to be hidden if the value is empty while in read mode.<br>Default Value: *false*.
### scope
The component end target. The values can be.<br>  0 or "always" : Force send even if not changed.<br>  1 or "database" : If changed go to DataProvider and DB (default).<br>  2 or "dataprovider" : If changed go to DataProvider only.<br>  3 or "form": Stay only in the input/Form.<br>Default Value: *1*.
### mask
The input's entry mask or character filter. Mask values can be found [here](http://igorescobar.github.io/jQuery-Mask-Plugin/).<br>Default Value: *Empty*.
### value
To set the input value at initialization time.<br>Default Value: *Empty*.
### mode
To set the input mode at initialization time. If "write" or *true,* it starts in data entry mode. If "read" or *false*, it starts in view mode. Only valid if operating alone. The *silk:Form* overwrites this setting.<br>Default Value: *false*.
### cssClass
The extra CSS classes to use with the input element.<br>Default Value: *Empty*.
### extraProperties
Used to add extra HTML properties to the unavailable using the *silk:Input* properties.<br>Default Value: *Empty*.
### htmlToolbar
The JavaScript array to fill the Quill toolbar. To be used with type "html".<br>Default Value: */ckeditor-conf/bar-simple.js*.
### htmlTheme
The JavaScript file containing the custom configuration for CKEditor. To be used with type "html".<br>Default Value: */ckeditor-conf/bar-simple.js*.
### target
To indicate the HTML element in which inputs will be rendered. Not necessary if used with *silk:Form*.<br>Default Value: *Empty*.
### prompt
Adds an extra options to the select usually use to request a value selection.<br>Default Value: *Empty*.
### promptValue
The value returned by the select "prompt" if the user selects it.<br>Default Value: *Empty*.
### template
An HTML schema defining the component read view. Contains data columns encapsulated in {} and also HTML elements.<br>Default Value: *Empty*.
### direction
Defines the distribution direction of input items. This is used for the types 'options' and 'ratio'. The accepted values are "vertical" and "horizontal."<br>Default Value: *Empty*.
### itemsDirection
Defines the distribution direction input items. This is use for the type 'options' and 'ratio'.<br>Default Value: *Empty*.
### filePreview
Defines if the component shows a button to preview an uploaded file. Available then type is "file."<br>Default Value: *false*.
### fileDownload
If the component shows a button to download an uploaded file. Available then type is "file."<br>Default Value: *false*.
### filePreviewLabel
The label of the preview button. To use with a type "file."<br>Default Value: *Preview*.
### fileDownloadLabel
The label of the download button. To use with a type "file."<br>Default Value: *Download*.
### fileUploadLabel
The label of the download button. To use with a type "file."<br>Default Value: *Drag and drop a file here, or click to select a file.*<br>Default Value: *Empty*.
### filePreviewClass
The preview button Bootstrap class. To use with a type "file."<br>Default Value: *btn-primary*.
### fileDownloadClass
The download button Bootstrap class. To use with a type "file."<br>Default Value: *btn-primary*.
### filePreviewIcon
The preview button from the Font Awesome icon classes. To use with a type "file."<br>Default Value: *fas fa-file*.
### fileDownloadIcon
The download button from the Font Awesome icon classes. To use with a type "file."<br>Default Value: *fas fa-file-download*.
### uploadURL
The URL of the service uploading the file. To use with a type "file."<br>Default Value: *Empty*.
### fileTypeList
String containing the comma-separated list of accepted file extensions to be uploaded. To use with a type "file."<br>Default Value: *Empty*.
### fileSizeLimit
The number of MB allowed to be uploaded. To use with a type "file."<br>Default Value: *Empty*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the  <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
### targetPage
Defines the *silk:Page* that will be selected/shown when the input is clicked.  To use with a type "button."<br>Default Value: *Empty*.
### timer
If set to "true," the keyboard typing is monitored and the event "timer" is triggered when the user stops typing after 400 milliseconds has passed. The expected milliseconds can also be provided as a value.<br>Default Value: *Empty*.
### toggleList
The list of comma-separated elements that will be toggled together with the component.<br>The value "parent" toggles the immediate parent element.<br>The value "grandpa" toggles the grandparent element.<br>Default Value: *Empty*.
### autocomplete
Sets the input to be hidden if the value is empty while in read mode.<br>Default Value: *false*.
