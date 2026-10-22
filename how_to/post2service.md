# Sending Data to a Service for Processing

To send data to an HTTP service for processing, use the SilkBuilder JavaScript function `postToService()`.

This function submits data via a POST request to the provided URL. It uses XHR (XMLHttpRequest) internally so that, for long-running operations, chunked progress messages can optionally be reported to a `progressFunction` while the request is still in progress. Chunk messaging is not required — for a typical request/response call, the service can simply return its JSON result directly, with no chunk messages involved. The function expects the complete response body to be pure, valid JSON — any non-JSON content in the final response will cause the call to fail.

## Parameters

| Parameter        | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| serviceURL       | The URL of the target service.                               |
| data             | Plain JS object containing the data to be submitted.         |
| handleFunction   | The function that will be called once the operation ends.    |
| context          | The context (`this` value) applied to the callback functions. |
| progressFunction | Function called with each new chunk of response text. Optional — only needed if the service sends chunk messages for a long-running process. |
| timeout          | Timeout in milliseconds (`0` = no timeout).                  |

## The `handleFunction`

When the service finishes its operation, `handleFunction` is called with two parameters:

- **success**: `true` if the operation completed without problems; `false` if an error was detected.
- **response**:
  - If `success` is `true`, this contains the service response data, deserialized from JSON.
  - If `success` is `false`, this contains an object describing the error, with the following elements:
    - **error**: The error type.
    - **responseText**: The raw `responseText` from the `XMLHttpRequest`.
    - **exception**: The exception caught by the internal try/catch statement, if any.

Errors are also printed to the browser's JavaScript console to help with debugging.

Calling a service that returns the name and address associated with a given id. This is a simple, non-chunked call — `progressFunction` isn't needed here because the service responds directly with its result:

```javascript
postToService(
	"/api/load-name",
	{ id: 42 },
	function(success, result) {
		if( success ){
			console.log("Name:", result.name);
			console.log("Address:", result.address);
		}else{
			/*
			 * Process action if the process had an error.
			 */
		}
	}
);
```

## The `progressFunction`

For long-running operations, a service can optionally send progress updates before its final result. When it does, `progressFunction` receives each chunk message as its parameter, called once for every chunk the service releases while the request is still in flight.

This callback is useful for reporting progress to the user during long-running operations, since it fires before the final response arrives — for example, to update a progress bar or status message as each stage of a lengthy process completes. If a service doesn't send chunk messages, `progressFunction` and `context` can simply be omitted from the call, as shown in the example above.

A call that accepts chunked progress messages from the service as it works:

```javascript
postToService(
	"/api/long-running",
	{ id: 42 },
	function(success, result) {
		if( success ){
			console.log("Name:", result.name);
			console.log("Address:", result.address);
		}else{
			/*
			 * Process action if the process had an error.
			 */
		}
	},
	this,
	function(chunk) { console.log("chunk:", chunk); }
);
```

## SilkBuilder Service with Chunk Messaging

Below is sample code for a **SilkBuilder** service configured to send chunk messages back to `postToService`, using the `writeToResponse` method of the `Http` class. This pattern is only needed when the service reports progress on a long-running process — a service that just returns a result can skip chunking entirely and write its JSON normally in the JSP body.

The method `writeToResponse` expects two paramater: response and text. The main class is `com.oopsclick.silk.utils.Http`.

```java
void writeToResponse(HttpServletResponse response, String text)
```

Sample code:

```java
<java>@ page
	import="com.oopsclick.silk.utils.Http"
	contentType="text/plain; charset=UTF-8" pageEncoding="UTF-8"
	trimDirectiveWhitespaces="true"
</java>
<java>

	Http.writeToResponse(response, "Starting long-running process...");
	Thread.sleep(1200);

	Http.writeToResponse(response, "Validating input data...");
	Thread.sleep(1000);

	Http.writeToResponse(response, "Processing records (25%)...");
	Thread.sleep(1500);

	Http.writeToResponse(response, "Processing records (60%)...");
	Thread.sleep(1200);

	Http.writeToResponse(response, "Processing records (100%)...");
	Thread.sleep(800);

	Http.writeToResponse(response, "Generating final result...");
	Thread.sleep(600);

	/*
	 * JSON created manually for testing purposes
	 */
	Http.writeToResponse(
		response,
		"{"+
			"\"success\":true,"+
			"\"message\":\"Process completed successfully\","+
			"\"timestamp\":\""+ System.currentTimeMillis() + "\","+
			"\"recordsProcessed\":42"+
		"}"
	);

</java>
```

Each call to `Http.writeToResponse` before the final one sends an intermediate progress message, which is captured by `progressFunction` on the client. The last call sends the final JSON payload, which is what gets passed to `handleFunction` as the `response` parameter once the request completes.

> **WARNING**: Keep the following in mind when working with `postToService`:
>
> - Chunk messages must not contain the `{` symbol, or the message will be ignored by the client.
> - **If the service sends chunk messages**, the final JSON result must also be written using `writeToResponse`. Writing it directly in the JSP body instead will cause it to be ignored.
> - **If the service does not send chunk messages**, chunking isn't required at all — the JSON result can simply be written as normal JSP body content, without going through `writeToResponse`.
