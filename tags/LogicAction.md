# silk:LogicAction
The component **silk:LogicAction** links an element, or function, to a LogicGrid and will be affected by the logic result of the provided criteria. If the component is an object, the toggle method will be operated. If the element is a function, the logic result will be passed as a parameter.

It can operate as a standalone component or contain the criteria values.

## Tag Definition
Used standalone:
```xml
<silk:LogicAction
  logicGrid=""
  target=""
  criteria=""
/>
```
Used as a container:
```xml
<silk:LogicAction
  logicGrid=""
  target=""
  criteria=""
>
   Contains: The group values determining the outcome of the logic action: value1:value2:...
</silk:LogicAction>
```

## Properties 
<sup>*</sup>Required property.
### logicGrid
Sets the LogicGrid connected to the logic action. This is required if the action is defined outside a LogicGrid container.<br>Default Value: *Empty*.
### target<sup>*</sup>
Defines the component or components, separated by commas, that are toggled by the logic action. This could include the name of a function that will be called every time the logic status changes.<br>Default Value: *Empty*.
### criteria<sup>*</sup>
The group values determining the outcome of the logic action: value1:value2:...<br>This gets overwrite if the criteria is provided as tag body.<br>Default Value: *Empty*.
