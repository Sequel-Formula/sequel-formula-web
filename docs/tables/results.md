---
sidebar_position: 1
pagination_next: null
pagination_prev: null
title: Results
---

### [dbo.results]
| Column name | Key | Data type | Allow NULLs | Default | Description |
| ------- | ------- | ------- | ------- | ------- | ------- |
| **resultId** |  Primary Key | INT IDENTITY | ☐ |  |  | 
| **resultTypeId** | FK_Results_ResultTypeID (dbo.resultType resultTypeID) | INT | ☐ |  | Result Type E.G. Sprint Result | 
| **raceId** |  | INT | ☐ |  | Foreign key link to races table | 
| **number** |  | INT | ☑ |  | Driver number | 
| **grid** |  | INT | ☐ | 0 | Starting grid position | 
| **position** |  | INT | ☑ |  | Official classification, if applicable | 
| **positionOrder** |  | INT | ☐ | 0 | Driver position for ordering purposes | 
| **points** |  | FLOAT | ☐ | 0 | Driver points for race | 
| **laps** |  | INT | ☐ | 0 | Number of completed laps | 
| **milliseconds** |  | INT | ☑ |  | Finishing time in milliseconds | 
| **fastestLap** |  | INT | ☑ |  | Lap number of fastest lap | 
| **rank** |  | INT | ☑ | 0 | Fastest lap rank, compared to other | 
| **statusId** |  | INT | ☐ | 0 | Fastest lap speed (km/h) e.g. "213.874" | 
| **positionTextID** |  | INT | ☑ |  | Foreign Key link to positionText | 
| **fastestLapTime** |  | TIME | ☑ |  | Fastest lap time e.g. "1:27.453" | 
| **fastestLapSpeed** |  | DECIMAL | ☑ |  | Fastest lap speed (km/h) e.g. "213.874" | 
| **time** |  | TIME | ☑ |  | Finishing time or gap |  


### Table Relationships

![Results](/img/table-relationships/results.png)

### Where Used
Where is this table referenced and what columns are used? The below table shows that information.

### [dbo.results]
| Parent_schemaName | Parent_tableName | Parent_columnName | Schema | table | column | constraint_name |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| dbo | results | resultId | dbo | resultDriverConstructor | resultID | PK_resultDriverConstructor_resultID | 

### Example Query

```sql
SELECT 
	r.[resultId]
	,rt.resultTypeId AS [result_type]
    ,ra.name AS [race_name]
	,sea.year
    ,CONCAT(d.forename, ' ',d.surname) AS [driver_name]
    ,c.name AS [constructor]
    ,r.[number]
    ,[grid]
    ,[position]
    ,[positionOrder]
    ,[points]
    ,[laps]
    ,r.[time]
    ,[milliseconds]
    ,[fastestLap]
	,r.rank
    ,[fastestLapTime]
    ,s.status
    ,pt.positionText
FROM 
	[dbo].[results] r

	INNER JOIN [dbo].[resultType] rt
		ON r.resultTypeID = rt.resultTypeID

	INNER JOIN [dbo].[races] ra
		ON r.raceId = ra.raceId

	INNER JOIN [dbo].[raceDriverConstructor] rc
		ON rc.resultID = r.resultID

	INNER JOIN [dbo].[constructors] c
		ON c.constructorId = rc.constructorID

	INNER JOIN [dbo].[drivers] d 
		ON d.driverId = rc.driverId

	LEFT JOIN [dbo].[status] s 
		ON s.statusId = r.statusId

	LEFT JOIN [dbo].[positionText] pt 
		ON pt.positionTextID = r.positionTextID

	INNER JOIN [dbo].[seasons] sea
		ON sea.year = ra.year
WHERE
	ra.year = '2023'
	AND ra.name = 'British Grand Prix'
```

### Example Output

|**resultId**|**resultTypeId**|**raceId**|**driverId**|**constructorId**|**number**|**grid**|**position**|**positionOrder**|**points**|**laps**|**milliseconds**|**fastestLap**|**rank**|**statusId**|**positionTextID**|**fastestLapTime**|**fastestLapSpeed**|**time**|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---| 
|1|1|18|1|1|22|1|1|1|10|58|5690616|39|2|1|1|00:01:27.452|218.300|01:34:50.616| 
|2|18|2|2|3|5|2|2|8|58|5696094|41|3|1|2|00:01:27.739|217.586|00:00:05.477| 