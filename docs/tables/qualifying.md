---
sidebar_position: 1
pagination_next: null
pagination_prev: null
title: Qualifying
---

### [dbo.qualifying]
| Column name | Key | Data type | Allow NULLs | Default | Description |
| ------- | ------- | ------- | ------- | ------- | ------- |
| **qualifyId** |  Primary Key | INT | ☐ |  |  | 
| **raceId** | FK_Qualifying_RaceID (dbo.races raceId) | INT | ☐ | 0 | Foreign key link to races table  | 
| **driverId** | FK_Qualifying_DriverID (dbo.drivers driverId) | INT | ☐ | 0 | Foreign key link to drivers table | 
| **constructorId** | FK_Qualifying_ConstructorID (dbo.constructors constructorId) | INT | ☐ | 0 | Foreign key link to constructors table | 
| **number** |  | INT | ☐ | 0 | Driver number | 
| **position** |  | INT | ☑ |  | Qualifying position | 
| **q1** |  | TIME | ☑ |  | Q1 lap time e.g. "1:21.374" | 
| **q2** |  | TIME | ☑ |  | Q2 lap time | 
| **q3** |  | TIME | ☑ |  | Q3 lap time | 

### Table Relationships

![Qualifying](/img/table-relationships/qualifying.png)

### Where Used
Where is this table referenced and what columns are used? The below table shows that information.

### Example Query

```sql
SELECT 
	[qualifyId]
	,r.[raceId]
	,r.name AS [race_name]
	,d.[driverId]
	,CONCAT(d.forename,' ',d.surname) AS [driver_name]
	,c.[constructorId]
	,c.name AS [constructor_name]
	,q.[number]
	,[position]
	,[q1]
	,[q2]
	,[q3]
FROM 
	[dbo].[qualifying] q

	INNER JOIN [dbo].[races] r
		ON q.raceId = r.raceId

	INNER JOIN [dbo].[drivers] d
		ON d.driverId = q.driverId

	INNER JOIN [dbo].[constructors] c
		ON c.constructorId = q.constructorId
WHERE 
	r.year = '2023'
```

### Example Output

|**qualifyId**|**raceId**|**driverId**|**constructorId**|**number**|**position**|**q1**|**q2**|**q3**|  
|---|---|---|---|---|---|---|---|---| 
|1|18|1|1|22|1|00:01:26.572|00:01:25.187|00:01:26.714| 
|2|18|9|2|4|2|00:01:26.103|00:01:25.315|00:01:26.869| 