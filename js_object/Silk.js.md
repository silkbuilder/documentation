# Silk
 The Silk class defines the global methods, properties, and events of a SilkBuilder application. It is uniquely instantiated as the **silk** object when the ```<silk:App>``` tag is processed in the application.  Other components use the created **silk** object for their internal operations. The user does not need to instantiate this class.

**Kind**: global class  
## Properties

| Name | Type | Description |
| --- | --- | --- |
| pageList | <code>Array</code> | An array containing the list of Page objects used by the application. |
| dpLoader | <code>Array</code> | An array containing the list of DataProvider objects used by the application. |
| $screen | <code>Object</code> | A jQuery object pointing to the page's container. |
| focusedPage | <code>String</code> | The name of the page is currently in focus. |
| $focusedPage | <code>Object</code> | A jQuery object pointing to the focused page. |
| focusedPageIndex | <code>Integer</code> | The index of the page currently in focus. |



## Constructor
 <a name="_new"></a>

### new Silk()
Returns a Silk instance. **Do not instantiate manually.**

## Methods
 <a name="+alert"></a>

### alert(title, message, icon, configuration)
Extends the [SweetAlert2](https://sweetalert2.github.io/) dialog object. Use it by calling ```alert(title, message, icon);``` or ```alert(configuration_object);```.

**Kind**: instance method of [<code>Silk</code>](#Silk)  

| Param | Type | Description |
| --- | --- | --- |
| title | <code>String</code> | The dialog's title. |
| message | <code>String</code> | The dialog's message. |
| icon | <code>String</code> | The icon's name. |
| configuration | <code>Object</code> | An object with the SweetAlert2 configuration. When using this, the other parameters should not be used. |

<a name="Silk+getScreenMode"></a>

### getScreenMode() ⇒ <code>Integer</code>
Returns the screen mode based on the window's width. The return values are:
* 0 - Small. Under 544px width.
* 1 - Medium. Between 544px and 769px.
* 2 - Regular. Between 768px and 1025px.
* 3 - Large. Between 1024px and 1401px.
* 4 - Extra Large. Between 1400px and 1900px.
* 5 - Extra extra large. Above 1900px;

**Kind**: instance method of [<code>Silk</code>](#Silk)  
<a name="Silk+layoutScreens"></a>

### layoutScreens()
Distributes and visualizes the pages based on the screen's width.

**Kind**: instance method of [<code>Silk</code>](#Silk)  
<a name="Silk+on"></a>

### on
Load events to respond to the global interactions. To set an event, use this code: ```on(<eventName>, function(){<code>})```.

**Kind**: instance property of [<code>Silk</code>](#Silk)  

| Param | Type | Description |
| --- | --- | --- |
| eventName | <code>String</code> | The event's name. |
| eventFunction | <code>function</code> | The function to be triggered. |

<a name="Silk+toast"></a>

### toast(title, message, icon, configuration)
Extends the [SweetAlert2](https://sweetalert2.github.io/) toas object. The toast is a window that delivers a message, opening for a few seconds. Use it by calling ```toast(title, message,icon);``` or ```toast(configuraition_object);```.

**Kind**: instance method of [<code>Silk</code>](#Silk)  

| Param | Type | Description |
| --- | --- | --- |
| title | <code>String</code> | The dialog's title. |
| message | <code>String</code> | The dialog's message. |
| icon | <code>String</code> | The icon's name. |
| configuration | <code>Object</code> | An object with the SweetAlert2 configuration. When using this, the other parameters should not be used. |

<a name="Silk+event_afterDPLoad"></a>

### "event:afterDPLoad"
This event is triggered after the DataProviders marked with *autoLoad=true* have finished loading for the first time. Created with the ```on("afterDPLoad", function(){})``` method.

**Kind**: event emitted by [<code>Silk</code>](#Silk)  
<a name="Silk+event_beforeDPLoad"></a>

### "event:beforeDPLoad"
This event is triggered before the DataProviders marked with *autoLoad=true* are loaded for the first time. Created with the ```on("beforeDPLoad", function(){})``` method.

**Kind**: event emitted by [<code>Silk</code>](#Silk)  
<a name="Silk+Event_resize"></a>

## Events
### on:resize
This event is triggered every time the navigator is resized. It is also triggered after the pages have been distributed. Created with the ```on("resize", function(){})``` method.

**Kind**: event emitted by [<code>Silk</code>](#Silk)  

