# Variables

Variables are created using the "Application Variables" option located in the "Options" folder of the selected system. The Application Variables screen is divided between "Variable Groups" and "Variables." This is the environment for managing variables used globally by the system. This is also the option to translate the variables if necessary.

## Creating Variables

### Variable Groups

Variables are organized into groups. Click the + (plus) icon located in the top right in Variable Group header. In the dialog box, enter the "Group Tag" use as the key to group the variable. This is not a "name" and should not contain spaces. This tag will be used when filtering variables in an SQL statement.

### Variable List

After selecting a variable group, variables can be added by clicking the + (plus) icon in the top-right corner of the Variable header.

When creating a variable these data has to be filled:

1. **Value**: The numeric identifier of the value. This is the data that will be stored in the table's column. This is required.
2. **Label**: The descriptive name visible to the user when interacting with the variable. This is required.
3. **Key**: An alphanumeric identifier that can be used programmatically with logic actions. A key is much easier to use and recognize in the code than a number. *Not required*.

## Storage and Syncronization

Variables are part of the translation tags stored in the SilkBuilder data repository. When the system gets synchronized, the variables are copied to the SilkClient's data repository. This process only happens during a full synchronization, not during a project or partial synchronization. Every time a variable is created or modified, a full synchronization is required for the SilkClient to use it.

## Accesing Variables

Variables are easily accessible using the view "silkVariable" located in the SilkBuilder and SilkClient data repository. When accessing variables in SilkBuilder, it is important to provide the "silkSystemID" in the query. 

```sql
select
	value,
	label,
	keyValue
from silkVariable
where groupName = 'personStatus'
and silkSystemID = 10 -- This will be removed when used in the silkClient
```

**NOTICE:** Even though the line `and silkSystemID = 10` could create a conflict when deployed to the production server, when the framework is executed in the  SilkClient, the line containing the `silkSystemID` will be removed from the query. It is important to keep this line alone, not containing other columns, because it will also be removed.



If the system's tables will exist in the same database as the SilkClient 



```sql
create view silkVariable as
select
	*
from [db-schema].silkVariable
where silkSystemID = 10
```





## Using Variables