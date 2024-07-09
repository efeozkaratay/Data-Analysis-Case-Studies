## Data Preparation

### Bike Trips Table

####  1.  Adjusted all column names and data types to match table structure for all bike trip tables;

``` sql
--  Query to change data type of column;

ALTER TABLE    table_name
ALTER COLUMN   column_name  DATA_TYPE

-- Query to change column name;

EXEC sp_RENAME 'table_name.old_column_name' , 'new_column_name', 'COLUMN'
```

#####  1.1.  Encountered an error during changing datatype from nvarchar(50) to float for one column caused by decimal separator;
  
``` sql
--  First step;

UPDATE  Divvy_Trips_2018_Q3
SET     tripduration = REPLACE(tripduration, '.0', '')

--  Second step;

UPDATE  Divvy_Trips_2018_Q3
SET     tripduration = REPLACE(tripduration, ',', '')

--  Final step;

ALTER TABLE   Divvy_Trips_2018_Q3
ALTER COLUMN  tripduration FLOAT
```

####  2.  Combined bike trips tables together;

#####  2.1.  Query to combine quarterly table together and create yearly bike trip table (to be repeated for 2018 and 2019 tables)

``` sql
SELECT  *
INTO    Bike_Trips_2017
FROM
(
        SELECT	*  FROM	[Divvy_Trips_2017_Q1]
        UNION ALL
        SELECT	*  FROM	[Divvy_Trips_2017_Q2]
        UNION ALL
        SELECT	*  FROM	[Divvy_Trips_2017_Q3]
        UNION ALL
        SELECT	*  FROM	[Divvy_Trips_2017_Q4]
) a
```
#####  2.2.  Query to combine yearly tables together and create a table with all bike trips

``` sql
SELECT	*
INTO    Bike_Trips
FROM
(
        SELECT	*  FROM	[Bike_Trips_2017]
        UNION ALL
        SELECT	*  FROM	[Bİke_Trips_2018]
        UNION ALL
        SELECT	*  FROM	[Bike_Trips_2019]
) a
```

####  3.  Added columns to Bike_Trips table for further analysis;

#####  3.1.  Query to add year of trip column

``` sql
ALTER TABLE  Bike_Trips
ADD          trip_year		INT NULL

UPDATE       Bike_Trips
SET          trip_year  =  YEAR(start_time)
```

#####  3.2.  Query to add month of trip column

``` sql
ALTER TABLE  Bike_Trips
ADD          trip_month  INT  NULL

UPDATE       Bike_Trips
SET          trip_month  =  MONTH(start_time)
```

#####  3.3.  Query to add start hour of trip column

``` sql
ALTER TABLE  Bike_Trips
ADD          trip_hour  INT  NULL

UPDATE       Bike_Trips
SET          trip_hour = DATEPART(HOUR, start_time)
```

#####  3.4.  Query to add day of trip column

``` sql
ALTER TABLE  Bike_Trips
ADD          trip_day  VARCHAR(10)  NULL

UPDATE       Bike_Trips
SET          trip_day = DATENAME(DW, start_time)
```

#####  3.5.  Query to add trip duration column in HH:MM format

 ```sql
ALTER TABLE  Bike_Trips
ADD          trip_duration  NVARCHAR(20)  NULL

UPDATE       Bike_Trips
SET          trip_duration  =  LEFT(CONVERT(CHAR(8), DATEADD(MINUTE, DATEDIFF(minute, start_time, end_time), 0), 108), 5)
```

#####  3.6.  Query to add user age column

``` sql
ALTER TABLE  Bike_Trips
ADD          user_age  INT  NULL

UPDATE       Bike_Trips
SET          user_age = trip_year – birthyear
```

#####  3.7.  Query to add trip_route column

``` sql
ALTER TABLE  Bike_Data
ADD          trip_route VARCHAR(50)

UPDATE       Bike_Data
SET          trip_route = CONCAT(start_id, ' - ', end_id)
```

### Bike Stations

####  1.  Changed altitude-longitude columns data types to decimal(9,6) for Tableau visualisations. 

``` sql
--  Imported these columns to SQL Server as NVARCHAR(50) to prevent data loss;

ALTER TABLE    Bike_Stations
ALTER COLUMN   latitude   DECIMAL(9,6)

ALTER TABLE    Bike_Stations
ALTER COLUMN   longitude  DECIMAL(9,6)
```
