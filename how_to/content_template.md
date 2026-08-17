# Content Template

Some Silk Tags use their HTML content to define temples to show the data combined with HTML. The tags are:

- silk:Column's content
- silk:Tile's content
- silk:Input using the template property

This method allows for the creation of elaborated HTML structures.

## Data Binding

Data binding is the process that establishes a connection between the app UI and the data it displays. SilkBuilder provides data values to the components by data-biding to the DataProvider object.

The data-biding with the HTML content is done in the template using curly brackets "{ }" or double curly brackets "{{ }}," containing the name of the property to be displayed.

A simple data binding sample could be by using silk:Column to display a cell containing the firstName property of the selected record in the DataProvider.

```xml
<silk:Column>{firstName}</silk:Column>
```

A slightly more elaborate sample could include more data in the cell.

```xml
<silk:Column>
  <div>{firstName} {lastName}</div>
  <div>Birdthday: {birthday}</div>
</silk:Column>
```

In this case, the table cell will show the firstName and lastName inside a div tag and the birthday in a second div tag, simulating internal rows.

A more complex sample could be the inclusion of the Card Bootstrap component in a silk:Tile. This sample will use double curly brackets.

```xml
<silk:Tile id="eventList" dataSource="eventDP" >
  <div class="card" style="width: 18rem;">
    <img src="{{imageURL}}" class="card-img-top" alt="...">
    <div class="card-body">
      <h5 class="card-title">{{eventName}}</h5>
      <p class="card-text">{{description}}</p>
      <a href="/event/location/{{eventID}}" class="btn btn-primary">More...</a>
    </div>
  </div>
</silk:Tile>
```

This template will use the properties: imageURL, eventName, description, eventID.

## Data Formating

The data extracted from the *DataProvider* during the data binding process can receive a formatting pattern added to the data binding template after a pipe symbol, separating the property name "|."

```xml
{startDate|<formating-pattern>}
```

Silk Builder provides common patterns to help data formatting during development:

- {column|date} - Renders the date as MM/dd/yyy
- {column|time} - Renders the date as hh:mm: a
- {column|datetime} - Renders the date as MM/dd/yyy hh:mm: a
- {column|numeric} - Renders number as ##'###,###
- {column|number} - Renders number as ##'###,###
- {column|integer} - Renders number as ##'###,###
- {column|decimal} - Renders decimal number as ##'###,###.00
- {column|byte} - Renders as ###KB or ###MB 
- {column|upper} - All characters to upper case
- {column|lower} - All characters to lower case
- {column|firstCap} - First characters to upper case

Patterns can also be created manually using [this guide](https://github.com/asual/jquery-format). An example is found below.

```
{column|MM/dd/yyy} {salary|##'###,###.00}
```

## Data Renderer

If formatting patterns fall short of expectations, a function can be used to create the desired effect. This pattern is used in the following way:

```javascript
{column|fn:<function>}
```

This example sends the *firstName*'s value to the function *formatName*.

```javascript
{firstName|fn:formatName}
```

The function should receive the property value and return a text value.

```javascript
/*
 * Function will wrap the firstName in bold if the name is "Mary".
 */
formatName = function(value, index, item){
  if( value=="Mary" ) return "<b>"+value+"</b>";
  return value;
}
```

## DataProvider Query

If the column's value is the primary key of a *DataProvider*, this can be used to query the *DataProvider* and extract a desired column's value using this pattern.

```javascript
{column|dp:DataProvider:dpColumn}
```

This example will query the DataProvider *countryDP* using the *countryID* column and will render the found country's name.

```
{countryID|dp:countryDP:countryName}
```

## Logical Data Rendering

HTML tags used in the template can be filtered using JavaScript logical statements. For this, adding the property "*renderIf" to the HTML tag and* setting the rational criteria is necessary.

In the example below, the DIV containing the *firstName* column will render if the property *age* exceeds 10.

```xml
<div renderIf="{age}>10" >{firstName}<div>
```

It is essential to understand that this is only a visualization restriction, not a data access restriction. The *firstName* column exists in the *DataProvider* and can be accessed using JavaScript. If it is crucial to refrain from downloading the information to the client, then it is essential to configure the data restriction settings in the SQL query.
