---
sidebar_position: 1
pagination_next: null
pagination_prev: null
title: Constructors
---

### [dbo.constructors]
| Column name | Key | Data type | Allow NULLs | Default | Description |
| ------- | ------- | ------- | ------- | ------- | ------- |
| **constructorId** |  Primary Key | INT | ☐ |  |  | 
| **constructorRef** |  | VARCHAR(255) | ☐ |  | Unique constructor identifier | 
| **name** |  | VARCHAR(255) | ☐ |  | Constructor name | 
| **url** |  | VARCHAR(2048) | ☐ |  | Constructor Wikipedia page | 
| **nationalityID** | FK_constructors_NationalityID (dbo.nationalities nationalityID) | INT | ☑ |  | Foreign Key to nationalities | 

### Table Relationships

![Constructors](/img/table-relationships/constructors.png)

### Where Used
Where is this table referenced and what columns are used? The below table shows that information.

### [dbo.constructors]
| Parent_schemaName | Parent_tableName | Parent_columnName | Schema | table | column | constraint_name |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| dbo | constructors | constructorId | dbo | constructorStandings | constructorId | FK_ConstructorStandings_ConstructorID | 
| dbo | constructors | constructorId | dbo | constructorResults | constructorId | FK_ConstructorResults_ConstructorID | 
| dbo | constructors | constructorId | dbo | driverNumbers | constructorID | PK_driverNumbers_constructorID | 
| dbo | constructors | constructorId | dbo | resultDriverConstructor | constructorID | PK_resultDriverConstructor_constructorID | 
| dbo | constructors | constructorId | dbo | qualifying | constructorId | FK_Qualifying_ConstructorID | 

### Example Query

```sql
SELECT 
	[constructorId]
	,[constructorRef]
	,[name]
	,[url]
	,n.[nationalityID]
	,n.nationality
FROM 
	[SequelFormula].[dbo].[constructors] c 

	INNER JOIN [dbo].[nationalities] n
		ON n.nationalityID = c.nationalityID
```

### Example Output

|**constructorId**|**constructorRef**|**name**|**url**|**nationalityID**|  
|---|---|---|---|---| 
|1|mclaren|McLaren|http://en.wikipedia.org/wiki/McLaren|10| 
|2|bmw_sauber|BMW Sauber|http://en.wikipedia.org/wiki/BMW_Sauber|21| 