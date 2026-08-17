# Form Input File

Each upload file is a particular case. This document explains how the silk:Input component operates with files when set to type "file."

## The Table Setup

The table connected to the file has to contain a column to store the file's name. In the example below, the column *profileImage* will keep the file's name.

```sql
create table person (
	personID int,
  fullName varchar(100),
  profileImage varchar(20) -- Column to store the file's name.
)
```

## The ORM

When configuring the ORM, set the column storing the file's name to data type *String*. The SQL select should contain the particular column.

## The Input

In the application, add the silk:Input tag to handle the column storing the file's name. Set the property type to "file". The property uploadURL should contain the URL to the service operating the uploading process.

```xml
<silk:Input id="profileImage" type="file" label="Profile Image"
  uploadURL="{contextPath}/service/Person/Profile/UploadImage"
/>
```

The *silk:Input* tag has other properties related to the uploading files. The property **fileTypeList** receives a comma-separated list of accepted extensions. The property **fileSizeLimit** contains the number of maximum MB allowed to be uploaded. The navigator will process these restrictions on the client side. For precaution, these validations should also be done in the uploading service if necessary.

```xml
<silk:Input id="profileImage" type="file" label="Profile Image"
  uploadURL="{contextPath}/service/Person/Profile/UploadImage"
  fileTypeList="jpg,png"
  fileSizeLimit="5"
/>
```

In the application, the input will show in this way.

![Form Input File](../.gitbook/assets/form_file_empty.png)

The user could drag a file into the drop area or click the drop area to open the file browser to select a file.

### Auto file upload Issue

The file is automatically uploaded after it is dragged into the drop area or after being selected. Suppose a file is uploaded when the form operates an insert action, and the process gets canceled. In that case, the application will not create the record hosting the file's name, **but the already uploaded file will remain in the storage folder.** This becomes critical if the upload process changes the file's name using the newly created record's data. 

To avoid the above situation, set the file input to be visible only during "update" operations. Use the property "**editable"** to implement this functionality.

```xml
<silk:Form id="personForm" >
		<silk:Input id="fullName" type="text" label="Full Name" />
		<silk:Input id="profileImage" type="file" label="Profile Image"
			editable="personForm.getAction()=='update'"
			uploadURL="{contextPath}/service/Person/Profile/UploadImage"
			fileTypeList="jpg"
			fileSizeLimit="5"
		/>
		<silk:Input id="personID" type="hidden" />
</silk:Form>
```

SilkBuilder does not submit the form's inputs using the regular POST or GET method. These are processed differently by the framework. During the submission process, the file input will only send the file's name. This is because the file has already been uploaded and processed, as defined in the uploadURL property.

## The Upload Service

The service to process the upload is defined using the **uploadURL** property. The developer can program the service in any way that fits the processing goals. However, to facilitate the file processing SilkBuilder provides the Java classes [Uploaded](https://javadoc.silkbuilder.com/com/oopsclick/silk/file/Uploaded.html) and [FormField](https://javadoc.silkbuilder.com/com/oopsclick/silk/file/FormField.html). The following examples use these classes to execute the uploading process. 

The code below is a service that gets the file and saves it in a folder with no data return.

```java
<%@ page import="com.oopsclick.silk.utils.Form" %>
<%
  /*
   * Load the request into the an Form object.
   */
	Form form = new Form(request);

	/*
	 * Saves the document data stream in the provided folder.
	 */
	boolean result = form.saveFile("document","/files/data/");

%>
```

## Submit Extra Data

Use the input method *beforeUpload* to add extra data into the upload submission process. This method receives the parameters: input, the JavaScript **DataForm** object, the file's name, and the file's size. Use the DataForm's ***append\*** method to add extra information.

The example below shows how to add the data "fullName" to the DataForm before submission. All this process is necessary only if the upload service will use the fullName information during the uploading process.

```javascript
personForm.profileImage.on("beforeUpload", function(input,dataForm, fileName, fileSize){
	dataForm.append("fullName", personDP.getSelectedItem().fullName);
});
```
## Service with Extra Processing

The upload service receives the fulName in the request. This is added to the file's name before saving it. The event getSavedFileName() returns the name used to save the file. The service returns a JSON structure containing the new name in the property fileName.

```java
<%@ page import="com.oopsclick.silk.utils.Form" %>
<%
  /*
   * Load the request into the an Form object.
   */
	Form form = new Form(request);

	/*
	 * Gets the fullName value and replaces spaces with underscore.
	 */
	String fullName = form.getValue("file-input");
	fullName = fullName.toLowerCase().replaceAll(" ","_");

	/*
	 * Extract the 'profileImage' object from 'uploaded' into a FormField object.
	 */
	FormField profileImageField = uploaded.get("profileImage");

	/*
	 * Combines the fullName and profileImage value (the files's name) into 
	 */
	String newFileName = fullName+"_"+profileImageField.getValue();

	/*
	 * Saves the profileImageField stream into the selected folder
   * using the 'newFileName' value as the file's name.
	 */
	int result = profileImageField.saveFile(newFileName, "/folder/goes/here/");

	/*
	 * Builds a JSON structure to return the new file name.
	 * Uses the FormField's property 'getSavedFileName()' to retrieved the
	 * name used when saving the file.
	 * Using the 'newFileName' value will also work.
	 */
%>
{
	"fileName":"<%= profileImage.getSavedFileName() %>"
}
```

In the client, if SilkBuilder received the property *fileName* it automatically applies it to the input's value.

### Receiving Upload Service Data

If the upload service returns other data, these can be accessed and operated using the afterUpload event. This event receives the parameters: the input field, the operation's result: "true" if successful or "false" if failure, and the data object containing the parsed JSON data. 

```javascript
personForm.profileImage.on("afterUpload", function(input,result,data){
	if( result ){
		console.log( data.fileName );
	}
});
```

