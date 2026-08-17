# Utility Functions


<a name="callFunction"></a>

## callFunction(fnString) ⇒ <code>Object</code>
Calls and executes the provided function's name without parameters.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| fnString | <code>String</code> | The function's name |

<a name="dateToString"></a>

## dateToString(date) ⇒ <code>String</code>
Convert a Date object to the Silk string-date with formar "YYY-MM-DD HH:MM:SS.MMS". Sample: "2022-09-09 09:40:43.226".
The Silk ORM returns and received date data in this format.

**Kind**: global function  

| Param | Description |
| --- | --- |
| date | The Date object to be converted |

<a name="doesFileExist"></a>

## doesFileExist(urlToFile) ⇒ <code>Boolean</code>
Verifies is the URL of a resource file exist or is accesible in host server.

**Kind**: global function  

| Param | Description |
| --- | --- |
| urlToFile | The file' URL. |

<a name="downloadText"></a>

## downloadText(content, contentType, fileName)
Function to download the provided text into a file.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| content | <code>String</code> | The text to download |
| contentType | <code>String</code> | The content type to download |
| fileName | <code>String</code> | Name of the file |

<a name="escapeHtml"></a>

## escapeHtml()
Escapes HTML to be displayed with in a div.

**Kind**: global function  
<a name="getBootstrapBreakpoint"></a>

## getBootstrapBreakpoint() ⇒ <code>&#x27;xxl&#x27;</code> \| <code>&#x27;xl&#x27;</code> \| <code>&#x27;lg&#x27;</code> \| <code>&#x27;md&#x27;</code> \| <code>&#x27;sm&#x27;</code> \| <code>&#x27;xs&#x27;</code> \| <code>&#x27;xxx&#x27;</code>
Determines the current active Bootstrap 5 responsive breakpoint based on
the viewport width, using CSS media queries via `window.matchMedia`.

Breakpoints are checked in descending order (xxl -> xs), so the largest
matching breakpoint is returned first.

**Kind**: global function  
**Returns**: <code>&#x27;xxl&#x27;</code> \| <code>&#x27;xl&#x27;</code> \| <code>&#x27;lg&#x27;</code> \| <code>&#x27;md&#x27;</code> \| <code>&#x27;sm&#x27;</code> \| <code>&#x27;xs&#x27;</code> \| <code>&#x27;xxx&#x27;</code> - The key of the
  current Bootstrap 5 breakpoint, or `'xxx'` if no breakpoint matches
  (e.g. when run in a non-browser environment without `window`).  
**Example**  
```js
const bp = getBootstrap5Breakpoint();
if (bp === 'xs' || bp === 'sm') {
  // handle mobile layout
}
```
<a name="getFormattedValue"></a>

## getFormattedValue(value, formatter) ⇒ <code>String</code>
Formats the value to specify pattern.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| value | <code>Object</code> | The value to get formated |
| formatter | <code>String</code> | The formating pattern or template |

<a name="getNumber"></a>

## getNumber(value, precision) ⇒ <code>Number</code>
Converts any provided value into a number.

**Kind**: global function  

| Param | Default | Description |
| --- | --- | --- |
| value |  | The value to be converted to a number. |
| precision | <code>2</code> | The decimal places. |

<a name="getObjectType"></a>

## getObjectType(obj) ⇒ <code>String</code>
Return the type of the object.

**Kind**: global function  

| Param | Description |
| --- | --- |
| obj | The object to evaluate. |

<a name="getRandomColor"></a>

## getRandomColor() ⇒ <code>String</code>
Returns the HEX value of ransom color.

**Kind**: global function  
<a name="getTemplateData"></a>

## getTemplateData(template, index, item, renderer) ⇒ <code>String</code>
Replaces the columns, enclosed with "{" or ""{{", found in a provided template with the attributes found in the the provided item. Then apply a renderer if provided.
Some templates:
{row-index} - Renders the row number starting with 1. Usually use to display the row number in a table.
{dp-inded} - Renders the data provider index used when building the row.
{ms-value} - Render the current milliseconds. Usually used as a unique variable when displaying images.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| template | <code>String</code> | The string containing the columns to replace. |
| index | <code>Integer</code> | The index position in the list |
| item | <code>Objet</code> | The object containing the attributes to be used to replace. |
| renderer | <code>String</code> | The function to be used as data renderer. |

<a name="getToday"></a>

## getToday() ⇒ <code>Date</code>
Return the current date and time

**Kind**: global function  
<a name="getTodayString"></a>

## getTodayString()
Return the current date and time in silk's string format.

**Kind**: global function  
<a name="getUUID"></a>

## getUUID() ⇒ <code>String</code>
Generates a UUID Value.

**Kind**: global function  
<a name="ifTag"></a>

## ifTag($container)
Evaluates HTML tags for keepIf property in the provided JQuery object. If tags found evaluates the attribute data-if criteria to keep or remove the tag.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| $container | <code>Object</code> | JQuery object to evaluate. if undefined evaluates all the html document |

<a name="ifUndefined"></a>

## ifUndefined(value, option) ⇒ <code>Object</code>
Analyzes if the provided value is undefined or null. If tyes it return the provided option.

**Kind**: global function  

| Param | Description |
| --- | --- |
| value | The value to evaluate. |
| option | The option to return if the value is undefined or null. |

<a name="inIframe"></a>

## inIframe() ⇒ <code>Boolean</code>
Verifies if a web application is running inside an iframe

**Kind**: global function  
<a name="isEmail"></a>

## isEmail(email, singel) ⇒ <code>Boolean</code>
Verifies if the provided string contains a valid email. Multiples comma separated emails are validated individually. If one or more emails are invalid it return false.
if the parameter "single" is true, or exist, the validation expect only one email address.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| email | <code>String</code> | The email address or a comma separated list of email addresses. |
| singel | <code>Boolean</code> | Only evalutes one email address |

<a name="isEmpty"></a>

## isEmpty(object) ⇒ <code>Boolean</code>
Returns true if the object is undefined or null or empty.

**Kind**: global function  

| Param | Description |
| --- | --- |
| object | The object to evaluate. |

<a name="isIn"></a>

## isIn() ⇒ <code>Boolean</code>
Function to verify if the first parameter matches the other parameter values. The second parameter can be an array. It is not extrict compparizon.

**Kind**: global function  
<a name="isNotEmpty"></a>

## isNotEmpty(object) ⇒ <code>Boolean</code>
Returns true if the object is not undefined or null or empty.

**Kind**: global function  

| Param | Description |
| --- | --- |
| object | The object to evaluate. |

<a name="isNumeric"></a>

## isNumeric()
Returns true if the provided parameter is a number

**Kind**: global function  
<a name="isRunningStandalone"></a>

## isRunningStandalone() ⇒ <code>Boolean</code>
Verifies if the web application is running standalone (PWA)

**Kind**: global function  
<a name="left"></a>

## left(str, n) ⇒ <code>String</code>
Returns a string with the provided number of characters starting from the left.

**Kind**: global function  

| Param | Description |
| --- | --- |
| str | The string to operate |
| n | The number of character to return |

<a name="postToService"></a>

## postToService(serviceURL, data, handleFunction, context, progressFunction, timeout)
Executes a POST to the provided URL. Uses XHR so that chunked responses
can be reported via progressFunction while the request is still in progress.
Expects the complete response body to be pure, valid JSON.

**Kind**: global function  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| serviceURL | <code>String</code> |  |  |
| data | <code>Object</code> |  | Plain JS object (serialized as form-urlencoded) |
| handleFunction | <code>function</code> |  | called as handleFunction(success, responseOrError) |
| context | <code>\*</code> |  | `this` value for the callbacks (optional) |
| progressFunction | <code>function</code> |  | called with each new chunk of response text |
| timeout | <code>Number</code> | <code>0</code> | Timeout in milliseconds (0 = no timeout) |

<a name="removeTrailingEmptyParagraphs"></a>

## removeTrailingEmptyParagraphs(html) ⇒ <code>string</code>
Removes one or more trailing "empty" <p> paragraphs from the end of an
HTML string.

A paragraph is considered empty if it contains nothing but whitespace,
a non-breaking space (&nbsp;), and/or a single <br> — which covers the
common leftover empty paragraphs that rich-text editors like Quill tend
to append after the last real line of content.

The removal repeats until no more trailing empty paragraphs are found,
so multiple stacked empty paragraphs at the end of the string are all
stripped, not just the last one.

Implementation note: this is a lightweight regex-based cleanup, not a
full HTML parse — it assumes reasonably well-formed markup and only
looks at the tail of the string. It won't catch empty paragraphs that
contain nested empty elements (e.g. <p><span></span></p>) or malformed
HTML. For those cases, parse via DOMParser and walk body.lastElementChild
instead.

**Kind**: global function  
**Returns**: <code>string</code> - The input string with trailing empty <p> tags removed.
  Returns the input unchanged (as-is) if it isn't a string.  

| Param | Type | Description |
| --- | --- | --- |
| html | <code>string</code> | The HTML string to clean up. |

**Example**  
```js
removeTrailingEmptyParagraphs('<p>Hello</p><p></p>');
// => "<p>Hello</p>"
```
**Example**  
```js
removeTrailingEmptyParagraphs('<p>Hello</p><p><br></p>');
// => "<p>Hello</p>"
```
**Example**  
```js
removeTrailingEmptyParagraphs('<p>Hello</p><p>&nbsp;</p><p></p>');
// => "<p>Hello</p>"
```
**Example**  
```js
removeTrailingEmptyParagraphs('<p></p>');
// => ""
```
<a name="renderCode"></a>

## renderCode() ⇒ <code>String</code>
Takes code text and replaces the tabs with hard spaces and in lines.

**Kind**: global function  

| Type | Description |
| --- | --- |
| <code>String</code> | The code to format |

<a name="replaceAll"></a>

## replaceAll(target, search, replace) ⇒ <code>String</code>
Function replaceAll to replace all the existing string to a new one.

**Kind**: global function  

| Param | Description |
| --- | --- |
| target | The text to operate |
| search | The text to search |
| replace | The replacement text |

<a name="right"></a>

## right(str, n) ⇒ <code>String</code>
Returns a string with the provided number of characters starting from the right.

**Kind**: global function  

| Param | Description |
| --- | --- |
| str | The string to operate |
| n | The number of character to return |

<a name="roundNumber"></a>

## roundNumber(value, precision) ⇒ <code>Number</code>
Rounds a number to the provided decimal place

**Kind**: global function  

| Param | Default | Description |
| --- | --- | --- |
| value |  | The number to be rounded. |
| precision | <code>0</code> | The rounding decimal place. |

<a name="sanitize"></a>

## sanitize(text) ⇒ <code>String</code>
Cleans data from HTML tags.

**Kind**: global function  

| Param | Type | Description |
| --- | --- | --- |
| text | <code>String</code> | The text to sanitize. |

<a name="stringToDate"></a>

## stringToDate(stringDate) ⇒ <code>Date</code>
Convert a Silk string-date data to data object. The string should have the formar "YYY-MM-DD HH:MM:SS.MMS". Sample: "2022-09-09 09:40:43.226".
The Silk ORM returns and received date data in this format.

**Kind**: global function  

| Param | Description |
| --- | --- |
| stringDate | The SILK string-date value to be converted. |


