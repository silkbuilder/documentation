# silk:Page
In a multi-page format application the **silk:Page** component is used to define the panels (columns) the application will use to place the SilkBuilder Components. Typically, a multi-page application consists of multiple pages.

## Tag Definition
Used as a container:
```xml
<silk:Page
  id=""
  stage=""
  returnPage=""
  tabsNav=""
  smLayout=""
  mdLayout=""
  rgLayout=""
  lgLayout=""
  xlLayout=""
  xxLayout=""
  renderIf=""
  hasHeader=""
>
   Contains: SilkBuilder components and HTML components.
</silk:Page>
```

## Properties 
<sup>*</sup>Required property.
### id<sup>*</sup>
The unique page identifier. No other component should use this name. A JavaScript object will be created with the same ID name for code interaction.<br>Default Value: *Empty*.
### stage<sup>*</sup>
A short name (A, B, A1, B1) that will be used with the layout properties to define the page's behavior.<br>Default Value: *Empty*.
### returnPage
The ID of the page to navigate to when the user clicks on the return icon. This is only necessary if the return page is different from the immediate page located on the left.<br>Default Value: *Empty*.
### tabsNav
The name of the tabVar if the page will be organized in tabs.<br>Default Value: *Empty*.
### smLayout<sup>*</sup>
The page layout distribution for small screens.<br>Default Value: *Empty*.
### mdLayout<sup>*</sup>
The page layout distribution for mid-size screens.<br>Default Value: *Empty*.
### rgLayout<sup>*</sup>
The page layout distribution for regular-size screens.<br>Default Value: *Empty*.
### lgLayout<sup>*</sup>
The page layout distribution for long screens.<br>Default Value: *Empty*.
### xlLayout<sup>*</sup>
The page layout distribution for extra-long screens.<br>Default Value: *Empty*.
### xxLayout<sup>*</sup>
The page layout distribution for extra extra long size screens.<br>Default Value: *Empty*.
### renderIf
It contains the logic sentence defining whether the component should be rendered.<br>The logic statement's explanation is in the <a href="how_to/server_code_logic.md">Server Code Logic</a> documentation.<br>Default Value: *Empty*.
### hasHeader
Default Value: *Empty*.
