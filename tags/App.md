# silk:App
This tag defines a SilkBuilder Application and is required. It loads the application's environment, which is necessary for the other Silk Components to operate.

## Tag Definition
Used standalone:
```xml
<silk:App
  id=""
  title=""
  theme="default"
  timeout="true"
  role=""
  ipFilter=""
  loader="true"
  renderIf=""
  jsLib=""
  bodyClass=""
/>
```
Used as a container:
```xml
<silk:App
  id=""
  title=""
  theme="default"
  timeout="true"
  role=""
  ipFilter=""
  loader="true"
  renderIf=""
  jsLib=""
  bodyClass=""
>
   Contains: Other HTML and/or Silk components. *
</silk:App>
```

## Properties 
<sup>*</sup>Required property.
### id
The app's unique identifier.<br>This is added during SilkBuilder's code rendering.<br>Default Value: *Empty*.
### title
Used to define the web page title that the navigator will display.<br>Default Value: *Empty*.
### theme
The name of the theme defines the styles used by the components. This property is only necessary if the application uses a different template from the "default". The theme value is defined as the session variable 'silkTheme' and is automatically loaded.<br>Default Value: *default*.
### timeout
Defines if the application will timeout and request authentication. The default value is "true" and can be disabled by setting the property to "false". It is only required if the value will be set to "false".<br>Default Value: *true*.
### role
Set the roles that are authorized to run the application. It should contain a list of string values separated by commas. These roles will be checked against the user's roles loaded at authentication time. By default, it is empty, allowing access to any logged-in user. The validation process only happens if a value is provided.<br>Default Value: *Empty*.
### ipFilter
Will restrict the application use to the provided IP filter.<br>Default Value: *Empty*.
### loader
Defines if the loader image (.gif) will be displayed. The default value is "true".<br>Default Value: *true*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
### jsLib
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Remove the library element from the library list.<br>At run time, the remaining element in the library list will be removed.<br>Default Value: *Empty*.
### bodyClass
Sets the class for the BODY tag<br>Default Value: *Empty*.
