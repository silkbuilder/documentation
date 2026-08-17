# File to Response

A common development task is retrieving a file from a folder and returning it to the client. In this scenario, the folder is not accessible directly through the web server's document root, so you need a service that reads the file on the server side and streams it back to the client. This way, the service never discloses the folder's actual location on disk.

  To build this kind of service, SilkBuilder provides the `Http` class, which includes a `fileToResponse()` method. This method is overloaded and can be used in the following ways:

  ```java
  void fileToResponse(String filePath, HttpServletResponse response);
  ```

  Sends the file at `filePath` to the client through `response`. The content type is inferred automatically from the file extension.

  ```java
  void fileToResponse(String filePath, HttpServletResponse response, String contentType);
  ```

  Same as above, but `contentType` is set explicitly, overriding whatever the file extension would suggest.

  ```java
  void fileToResponse(String filePath, HttpServletResponse response, String contentType, String alternativeFilePath);
  ```

Same as above, but if `filePath` does not exist, `alternativeFilePath` is used instead (useful for serving a default or placeholder file). If `contentType` is `null`, the content type is chosen based on the file extension of whichever path is actually used.

  ## Code Samples

Below is a simple example that serves a fixed, hardcoded file.

  ```java
  <java>@ page
    import="com.oopsclick.silk.utils.Http"
    trimDirectiveWhitespaces="true"
  </java>
  <java>
  
    String filePath = "/opt/images/smiley.png";
  
    Http.fileToResponse(filePath, response);
  
  </java>
  ```

This next example builds the `filePath` dynamically from a request parameter:

  ```java
  <java>@ page
    import="com.oopsclick.silk.utils.Http, com.oopsclick.silk.utils.FileTool"
    trimDirectiveWhitespaces="true"
  </java>
  <java>
  
    String fileName = request.getParameter("filename");
    if( fileName==null ) return;
  
    String filePath = "/opt/images/"+FileTool.getFileNameOnly(fileName);
  
    Http.fileToResponse(filePath, response);
  
  </java>
  ```

  > **Security note:** Even with `getFileNameOnly()` in place, treat request parameters as untrusted by default. `FileTool.getFileNameOnly()` mitigates path traversal by discarding any directory segments the caller supplies — for example, a value like `filename=../../etc/passwd` is reduced to just `passwd` before it's concatenated into `filePath`, so the client cannot escape the `/opt/images/` folder this way. This makes the pattern shown above safe against traversal specifically, but it's still good practice to further validate the resulting file name (e.g., against an allow-list of extensions, or confirming the file actually exists under the expected folder) before serving it.
  >
  > The second example uses the `getFileNameOnly` method from the `FileTool` class to strip any directory segments and return only the file name from the provided parameter.

  ## Service Visibility

A service built with `fileToResponse()` can be exposed as either a **Private Service** or a **Public Service**:

  - **Private Service** — the user must be signed in before the service can be used.
  - **Public Service** — the service can be accessed by anyone who knows the service URL, with no sign-in required.
