# DataProvider
 The DataProvider Class provides properties, methods, and events to interface with JSON data returned by data Outlet services. The [silk:DataProvider](..\tags\DataProvider.md) component creates the DataProvider object with a name as the component's ID.

```xml
<silk:DataProvider id="dataDP" servicePath="..." autoSelect="false" />
<silk:JQcode>
	dataDP.select();
</silk:JQcode>
```

**Kind**: global class  


## Constructor
 <a name="_new"></a>

### new DataProvider(id, options)
Returns a DataProvider instance.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| id | <code>String</code> |  | Unique identifier. |
| options | <code>Object</code> |  | Object containing the DataProvider configuration options. |
| [options.servicePath] | <code>String</code> |  | The URL to the Outlet Service providing the data. |
| [options.selectName] | <code>String</code> |  | The ORM's selectName used to extract the data. |
| [options.treeData] | <code>Boolean</code> | <code>false</code> | Indicates if the data will be treated as a hierarchical structure. |
| [options.markDeleted] | <code>Boolean</code> | <code>false</code> | Indicated that records will display like a deletion, but marked deleted in the database. |
| [options.isPublic] | <code>Integer</code> | <code>0</code> | Indicates if the service is publicly available. Use when accessing public Outlets from a private environment. |
| [options.debugLevel] | <code>Integer</code> | <code>0</code> | Defines the debugging level. |
| [options.pkColumn] | <code>String</code> |  | The primary key column of the table accessed. |
| [option.linkedDP] | <code>String</code> |  | The name of a related DataProvider that will be loaded after the local loading process ends. This could be a list of DataProvider’s names separated by commas. |
| [option.recordSync] | <code>Boolan</code> |  | The SELECT name used during the record sync process. If provided, it indicates that the DataProvider will automatically trigger the record sync method when a row is selected in a table component. |
| [option.dpSort] | <code>Boolean</code> | <code>false</code> | Indicates if the sorting will happen in the data provider. |

## Methods
 <a name="+addComponent"></a>

### addComponent(component)
Adds a component to the list of components that will be notified of changes in the DataProvider.<br>
The component must have a load() function.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| component | <code>Object</code> | The name of the component to be added |

<a name="DataProvider+batch"></a>

### batch()
Submits multiple operations loaded into the *operationsObject,* performing a batch request.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+clean"></a>

### clean()
Cleans the data from the *selectObject*.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+cleanOperations"></a>

### cleanOperations(init)
Cleans the loaded operation action in the *operationObject* before adding operations programmatically. If the provided parameter is *true,* it will initialize an empty select action, which is used to initialize the request object as a select. Submitting an empty operation list will trigger an error.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| init | <code>boolean</code> | (optional) Default is false. |

<a name="DataProvider+cleanParameters"></a>

### cleanParameters()
Cleans the parameter list from the *requestObject*.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+delete"></a>

### delete(recordIndex)
Executes a DELETE request. Operation items should be added before calling this method.<br>
If the DataProvider's property *markDeleted* is *true*, it will perform a delete in the local data for visual effect, but an update in the database.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| recordIndex | <code>Integer</code> | (optional) The index of the item to be deleted |

<a name="DataProvider+exec"></a>

### exec(operation)
Executes an ORM's SQL Operation. If the operation requires parameters that are not added in the "beforeLoad" or "beforeExec" events, they should be added before this method is executed.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| operation | <code>String</code> | The operation name from the ORM. |

<a name="DataProvider+getChildren"></a>

### getChildren(pkValue) ⇒ <code>Array</code>
Returns an array containing the generational children of a record.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| pkValue | <code>pkValue</code> | The primary key value to evaluate. |

<a name="DataProvider+getComponents"></a>

### getComponents()
Returns the array containing the components which will be notify of changes in the data provider.<br>
The component must have a load() function.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getID"></a>

### getID()
Returns the component's unique identifier.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getIndex"></a>

### getIndex(pkValue)
Returns the index of the provided primary key value in the *selectObject*'s data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| pkValue | <code>String</code> | The primary key value to search for. |

<a name="DataProvider+getIndexItem"></a>

### getIndexItem(pkValue)
Returns the item object of the provided primary key value in the *selectObject*'s data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| pkValue | <code>String</code> | The primary key value to search for. |

<a name="DataProvider+getIndexItemOf"></a>

### getIndexItemOf(columnName, value)
Returns the item object of the entity matching the provided column and value in the *selectObject*'s data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| columnName | <code>String</code> | The column name use to filter |
| value | <code>Object</code> | The value use to filter. |

<a name="DataProvider+getIndexOf"></a>

### getIndexOf(columnName, value)
Returns the index of the entity matching the provided column and value in the *selectObject*'s data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| columnName | <code>String</code> | The column name use to filter |
| value | <code>Object</code> | The value use to filter. |

<a name="DataProvider+getItem"></a>

### getItem(column)
Gets the object item of the first item in the *selectObject*'s data.
If the column is provided, it returns the value of the column in the first position.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| column | <code>String</code> | (optional) Column name whose value will be returned |

<a name="DataProvider+getItemAt"></a>

### getItemAt(index, column) ⇒ <code>Object</code>
Gets the object item from *selectObject*'s data at the provided index position.
If a column is provided, it returns the value of the column at the provided position.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| index | <code>Integer</code> | The object item's index position |
| column | <code>String</code> | (optional) The column name whose value will be returned |

<a name="DataProvider+getJSON"></a>

### getJSON() ⇒ <code>JSON</code>
Return the data provider data in JSON format

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getLangID"></a>

### getLangID() ⇒ <code>String</code>
Get the langID if it has been replaced.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getOperationIndex"></a>

### getOperationIndex()
Return the value of the operation index. This is usually synchronized with the selected index value.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getOperationItem"></a>

### getOperationItem(index)
Returns the operation Item from the *operationObject*. If the index is not provided, return the first one. If the DataProvider does not have data, it returns an empty object.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| index | <code>integer</code> | The operation index (optional). |

<a name="DataProvider+getPkColumn"></a>

### getPkColumn()
Returns the name of the primary key column.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getPKValue"></a>

### getPKValue()
Returns the primary key's value of the selected data item.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getSelectedItem"></a>

### getSelectedItem(columnName)
Returns the *selectObject's* item using the *selectedIndex* property. By default, the *selectedIndex* is 0;

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| columnName | <code>String</code> | The column to return. If not provided return the item object. |

<a name="DataProvider+getSelectName"></a>

### getSelectName()
Returns the selected name to be used to load the data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getService"></a>

### getService()
Returns the service path.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+getSortColumn"></a>

### getSortColumn() ⇒ <code>String</code>
Returns the name of the column used for data sorting.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
**Returns**: <code>String</code> - - Column name  
<a name="DataProvider+getSortDirection"></a>

### getSortDirection() ⇒ <code>Integer</code>
Gets the sorting direction. 1 is an ancestor, and -1 is a descendant.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
**Returns**: <code>Integer</code> - - Sorting Direction  
<a name="DataProvider+getSQLSortColumn"></a>

### getSQLSortColumn() ⇒ <code>String</code>
Returns the column used for sorting with added SQL keywords 'asc' or 'desc' based on the sorting direction.
If the sorting column is composite ("column, column"),  the SQL direction keyword will be added to each column.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+insert"></a>

### insert()
Executes an INSERT request. Operation items should be added before calling this method.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+isTreeData"></a>

### isTreeData()
Return a boolean indicating if the data is set to be tree structured

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+length"></a>

### length()
Returns the number of records in the data array. This is similar to the *size()* method.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+load"></a>

### load(internalCall)
Submits the operations from the *requestObject* and loads the response from the Outlet service into the *selectObject*.
The parameter is only for the frame's work internal use.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| internalCall | <code>boolean</code> | (Optional) True if call internally within the DataProvider |

<a name="DataProvider+loadJSON"></a>

### loadJSON(json)
Load data from a JSON string into the *selectObject"'s data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| json | <code>String</code> | The JSON structure to be parsed. |

<a name="DataProvider+on"></a>

### on
Load events to respond to the DataProvider's interactions. To set an event, use this code: ```DataProvider.on(<eventName>, function(){<code>})```.

**Kind**: instance property of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| eventName | <code>String</code> | The event's name. |
| eventFunction | <code>function</code> | The function to be triggered. |

<a name="DataProvider+operationObject"></a>

### operationObject
An object containing the returned Outlet Service data after insert, update, delete, exec, or batch.

**Kind**: instance property of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+recordSync"></a>

### recordSync(syncSelectName)
Executes the SELECT name provided in the recordSync intialization parameter to sync the loaded record with the new database record data. This will only affect the selected item.
If the parameter syncSelectName is provided it overwrites the default select.
If the SELECT requires query parameters, these should be added using the "beforeRecordSync" event.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type |
| --- | --- |
| syncSelectName | <code>String</code> | 

<a name="DataProvider+select"></a>

### select(selectName)
Executes a SELECT request. By default, it uses the select's name configured in the DataProvider. If a different request needs to be executed, it has to be provided as a parameter. Query parameters should be added before calling this method.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| selectName | <code>String</code> | (optional) (optional) The name of a select from the ORM. |

<a name="DataProvider+selectObject"></a>

### selectObject
An object containing the data returned from the Outlet Service after a select operation.

**Kind**: instance property of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+setItem"></a>

### setItem(column, value)
Sets the column's value of the first item in the *selectObject*'s data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| column | <code>String</code> | The target column. |
| value | <code>String</code> | The value. |

<a name="DataProvider+setItemAt"></a>

### setItemAt(index, column, value)
Sets the column's value of the *selectObject*'s data at the provided index.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| index | <code>Integer</code> | Array index target. |
| column | <code>String</code> | The target column. |
| value | <code>String</code> | The value. |

<a name="DataProvider+setLangID"></a>

### setLangID((String})
Set the langID, it is used to overwrite the session's loaded *langID* variable.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Description |
| --- | --- |
| (String} | newLangID - The new langID |

<a name="DataProvider+setOperationAction"></a>

### setOperationAction(action, operation)
Sets an action in the *operationObject*. After setting an operation action, it becomes the active action and is ready to receive operation items.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| action | <code>String</code> | The action to execute: select, insert, update, delete, exec, batch. |
| operation | <code>String</code> | (optional) The name of the operation when action is set to exec. |

<a name="DataProvider+setOperationItem"></a>

### setOperationItem(column, value)
Sets an operation item to the current operation action. The item contains the column and value to be operated on.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Description |
| --- | --- |
| column | The column name |
| value | The value |

<a name="DataProvider+setParameter"></a>

### setParameter(column, value, type, secure)
Sets a parameter in the *requestObject*. If the parameter exists, it gets updated.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| column | <code>String</code> | The column name |
| value | <code>Object</code> | The value |
| type | <code>String</code> | (optional) One character value (S,I,N,D,T) to force data convertion |
| secure | <code>booelan</code> | (optional) To inndicates if the value is encrypted. To overwrite what has been define in the ORM. |

<a name="DataProvider+setSelectedIndex"></a>

### setSelectedIndex(index1, index2)
Changes the internal data index to the provided value. By default, the selected index should be synchronized with the operation index. The selected index is connected to the view, such as a table, which could display the rows in a different order than the DataProvider order.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| index1 | <code>Integer</code> | Index to the view. |
| index2 | <code>Integer</code> | Index to the operation (Optional). |

<a name="DataProvider+setSelectName"></a>

### setSelectName(newSelectName)
Set the name of the select from the ORM, which will be used to load the data.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| newSelectName | <code>String</code> | The new select name. |

<a name="DataProvider+setSortColumn"></a>

### setSortColumn(column, direction)
Initializes the sorting column and/or direction before the DataProvider loads the data. The direction is optional.
If the sorting happens in the database, then before executing a select, the sort column has to be set up to match the select order.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| column | <code>String</code> | Column name |
| direction | <code>Integer</code> | Sorting direction. 1 - accedant, -1 is descendant |

<a name="DataProvider+setTimeout"></a>

### setTimeout()
The number of milliseconds before triggering a timeout error. The default value is 30 seconds.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+size"></a>

### size()
Returns the number of records in the data array.  This is similar to the *length()* method.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+sort"></a>

### sort(column, changeOrder)
Sorts, or orders, the data by the provided column. This does not work if the DataProvider is set to *treeData="true"*.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| column | <code>String</code> | Column to sort |
| changeOrder | <code>Boolean</code> | (Optional) If set to false cancels order switch. |

<a name="DataProvider+sourceType"></a>

### sourceType
Indicates the type of data source. These could be:<br>
SQL : From SQL database<br>
Local :  Loaded using the loadJSON method. This JSON structure is provided as part of the DataProvider content.<br>
JSON : Data from file containing JSON.

**Kind**: instance property of [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+update"></a>

### update(recordIndex)
Executes an UPDATE request. Operation items should be added before calling this method.

**Kind**: instance method of [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| recordIndex | <code>Integer</code> | (optional) The index of the item to be updated |

<a name="DataProvider+Event_afterBatch"></a>

## Events
### on:afterBatch
This event is triggered after the batch action is executed. It is created with the ```DataProvider.on("afterBatch", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_afterDelete"></a>

### on:afterDelete
This event is triggered after the delete action is executed. It is created with the ```DataProvider.on("afterDelete", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_afterExec"></a>

### on:afterExec (operation)
This event is triggered after the exec action is executed. It is created with the ```DataProvider.on("afterExec", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| operation | <code>String</code> | The operation to be executed. |

<a name="DataProvider+Event_afterInsert"></a>

### on:afterInsert
This event is triggered after the insert action is executed. It is created with the ```DataProvider.on("afterInsert", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_afterLoad"></a>

### on:afterLoad (action, operation)
This event is triggered after the load action is executed. It is created with the ```DataProvider.on("afterLoad", function(action,operation){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| action | <code>String</code> | The action to be executed. |
| operation | <code>String</code> | The operation to be executed. |

<a name="DataProvider+Event_afterRecordSync"></a>

### on:afterRecordSync (selectName)
This event is triggered after the record sync action is executed. It is created with the ```DataProvider.on("afterRecordSync", function(selectName){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| selectName | <code>String</code> | The name of the select with in the ORM to be executed. |

<a name="DataProvider+Event_afterSelect"></a>

### on:afterSelect (selectName)
This event is triggered after the select action is executed. It is created with the ```DataProvider.on("afterSelect", function(selectName){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| selectName | <code>String</code> | The name of the select with in the ORM to be executed. |

<a name="DataProvider+Event_afterUpdate"></a>

### on:afterUpdate
This event is triggered after the update action is executed. It is created with the ```DataProvider.on("afterUpdate", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_beforeBatch"></a>

### on:beforeBatch
This event is triggered before the batch action is executed. If the event function returns *false* the process is canceled. Created with the ```DataProvider.on("beforeBatch", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_beforeDelete"></a>

### on:beforeDelete
This event id triggered before the delete action is executed. If the event function returns *false* the process is canceled. Created with the ```DataProvider.on("beforeDelete", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_beforeExec"></a>

### on:beforeExec (operation)
This event is triggered before the exec action is executed. If the event function returns *false* the process is canceled. Created with the ```DataProvider.on("beforeExec", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| operation | <code>String</code> | The operation to be executed. |

<a name="DataProvider+Event_beforeInsert"></a>

### on:beforeInsert
This event is triggered before the insert action is executed. If the event function returns *false* the process is canceled. Created with the ```DataProvider.on("beforeInsert", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_beforeLoad"></a>

### on:beforeLoad (action, operation)
This event is triggered before the load action is executed. If the event function returns *false* the process is canceled. It is created with the ```DataProvider.on("beforeLoad", function(action,operation){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| action | <code>String</code> | The action to be executed. |
| operation | <code>String</code> | The operation to be executed. |

<a name="DataProvider+Event_beforeRecordSync"></a>

### on:beforeRecordSync (selectName)
This event is triggered before the record sync action is executed. If the event function returns *false* the process is canceled. Created with the ```DataProvider.on("beforeRecordSync", function(selectName){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| selectName | <code>String</code> | (Optional) The name of the select to be called. |

<a name="DataProvider+Event_beforeSelect"></a>

### on:beforeSelect (selectName)
This event is triggered before the select action is executed. If the event function returns *false* the process is canceled. Created with the ```DataProvider.on("beforeSelect", function(selectName){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| selectName | <code>String</code> | The name of the select to be called. |

<a name="DataProvider+Event_beforeUpdate"></a>

### on:beforeUpdate
This event is triggered before the update action is executed. If the event function returns *false* the process is canceled. Created with the ```DataProvider.on("beforeUpdate", function(){})``` method.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  
<a name="DataProvider+Event_error"></a>

### on:error (error)
This Event is triggered when an error has occurred. It is created with the ```DataProvider.on("error", function(errorObject){})``` method.
If the event returns an object, this will replace the existing operationObject.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| error | <code>Object</code> | The returned error object. |

<a name="DataProvider+Event_markDeleted"></a>

### on:markDeleted (requestObject)
This event is triggered before a delete action is processed. Created with the ```DataProvider.on("markDeleted", function(requestObject){})``` method. The event is triggered before the event "beforeDelete", so the data changes are considered part of the original submission process and not affected by other internal actions.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| requestObject | <code>Object</code> | The return objected to be operated. |

<a name="DataProvider+Event_processLoadedData"></a>

### on:processLoadedData (returnObject) ⇒ <code>Object</code>
This event is triggered when the received data is being processed. It is created with the ```DataProvider.on("processLoadedData", function(returnObject){})``` method. If the event returns an object, this will replace the existing *selectObject*.
This event can process the received data before loading it into the *selectObject*.

**Kind**: event emitted by [<code>DataProvider</code>](#DataProvider)  

| Param | Type | Description |
| --- | --- | --- |
| returnObject | <code>Object</code> | The return objected to be operated. |


