## Data Preparation

### Bike Trips Table

1. Adjusted all column names and data types to match table structure for all bike trip tables;

``` sql
--  Query to change data type of column;

ALTER TABLE    table_name
ALTER COLUMN   column_name  DATA_TYPE

-- Query to change column name;

EXEC sp_RENAME 'table_name.old_column_name' , 'new_column_name', 'COLUMN'
```

  1.1.  Encountered an error during changing datatype from nvarchar(50) to float for one column caused by decimal separator;
  
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
