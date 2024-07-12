## Data Cleaning
a
<br />

This section is for documentation of data cleaning process. After performing the queries below on Microsoft SQL Server, rows with duplicate values, NULL values or rows with few other conditions will be deleted and Bike Trip data will be ready for analysis.

<br />

###  A.  Bike Trips Table

<br />

#### 1.  Deleted rows with conditions below;

#####  1.1.  Trips take more than 24 hours;

``` sql
DELETE  FROM  Bike_Trips
WHERE         DATEDIFF(MINUTE, start_time, end_time) >= (24*60)
```

<br />

#####  1.2.  Trips with Start Time later than End Time;

``` sql
DELETE  FROM  Bike_Trips
WHERE         end_time < start_time
```

<br />

#####  1.3.  Subscribers with invalid age (too young or too old);

``` sql
DELETE  FROM  Bike_Trips
WHERE         user_age  IS  NOT NULL
              AND 
              (
              user_age <= 15
              OR
              user_age >  80
              )
```

<br />

#####  1.4.  Subscribers with NULL value for age or gender;

``` sql
DELETE  FROM  Bike_Trips
WHERE         usertype = 'Subscriber'
              AND 
              (
              user_age  IS  NULL
              OR
              gender    IS  NULL
              )
```

<br />

#####  1.5.  Duplicate rows (trip_id);

######  1.5.1.  Query to check existence of duplicate rows by trip_id column;

``` sql
SELECT
      trip_id,
      COUNT(trip_id) AS count
FROM  Bike_Trips
GROUP BY
      trip_id
HAVING
      COUNT(trip_id) > 1
ORDER BY
      count DESC
```

######  1.5.2.  Query to list duplicate rows (to be deleted by next query);

``` sql
SELECT  *
FROM    (
        SELECT  *,
                rn = ROW_NUMBER()  OVER(PARTITION BY trip_id  ORDER BY (SELECT NULL))
        FROM    Bike_Trips
        ) AS    duplicate
WHERE
        rn > 1
```

######  1.5.3.  Query to delete duplicate rows by trip_id column;

``` sql
DELETE  duplicate
FROM    (
        SELECT  *,
                rn = ROW_NUMBER()  OVER(PARTITION BY trip_id  ORDER BY (SELECT NULL))
        FROM    Bike_Trips
        )  AS   duplicate
WHERE
        rn > 1
```

<br />

####  2.  Updated 7 rows with usertype labeled as ‘Dependent’ to ‘Customer’;

``` sql
UPDATE  Bike_Trips
SET     usertype = 'Customer'
WHERE   usertype = 'Dependent'
```

<br />

####  3.  Checked for NULL values (Customers with NULL age/gender is valid);

``` sql
SELECT  *
FROM    Bike_Trips
WHERE
        trip_id           IS NULL
    OR  start_time        IS NULL
    OR  end_time          IS NULL	
    OR  bikeid            IS NULL	
    OR  tripduration      IS NULL	
    OR  from_station_id   IS NULL	
    OR  from_station_name IS NULL	
    OR  to_station_id     IS NULL	
    OR  to_station_name   IS NULL	
    OR  trip_duration     IS NULL	
    OR  trip_year         IS NULL	
    OR  trip_month        IS NULL	
    OR  trip_day          IS NULL	
    OR  trip_hour         IS NULL	
    OR  usertype          IS NULL
    OR  (usertype = 'Subscriber' 
        AND
        (gender   IS NULL
        OR
        user_age  IS NULL)
        )
```

<br />

### B.  Bike Stations Table

<br />

####  1.  Deleted rows with NULL values on latitude/longitude columns;

``` sql
DELETE  FROM  Bike_Stations
WHERE         latitude  IS  NULL
              OR
              longitude	IS  NULL
```

<br />

#### 2. Deleted duplicate rows (id column)

#####  2.1.  Query to check existence of duplicate rows by id column;

``` sql
SELECT
      id,
      COUNT(id)  AS  count
FROM  Bike_Stations
GROUP BY
      id
HAVING
      COUNT(id) > 1
ORDER BY
      count DESC
```

#####  2.2.  Query to list duplicate rows (to be deleted by next query);

``` sql
SELECT  *
FROM    (
        SELECT  *,
                rn = ROW_NUMBER()  OVER(PARTITION BY  id  ORDER BY  (SELECT NULL))
        FROM    Bike_Stations
        )  AS   duplicate
WHERE
        rn > 1
```

##### 2.3.  Query to delete duplicate rows by id column;

``` sql
DELETE  duplicate
FROM    (
        SELECT  *,
                rn = ROW_NUMBER()  OVER(PARTITION BY  id  ORDER BY  (SELECT NULL))
        FROM    Divvy_Stations
        )  AS   duplicate
WHERE
        rn > 1
```

<br />

###  C.  Joining Bike Trips and Bike Station tables and final cleaning;

<br />

####  1.  Query to join Bike_Trips and Bike_Stations tables and create new Bike_Data table with coordinates;

``` sql
SELECT  *
INTO    Bike_Data
FROM
        (
        SELECT
          table1.*,
          Bike_Stations.id        AS  end_id,
          Bike_Stations.name      AS  end_station,
          Bike_Stations.latitude  AS  end_latitude,
          Bike_Stations.longitude AS  end_longitude
        FROM
          (
          SELECT
              Bike_Trips.*,
              Bike_Stations.id        AS  start_id,
              Bike_Stations.name      AS  start_station,
              Bike_Stations.latitude  AS  start_latitude,
              Bike_Stations.longitude AS  start_longitude
          FROM
              Bike_Trips
          LEFT JOIN
              Bike_Stations
          ON
              Bike_Trips.from_station_id = Bike_Stations.id
          )   AS  table1
LEFT JOIN
        Bike_Stations
ON
        table1.to_station_id = Bike_Stations.id
        ) a
```

<br />

####  2.  Deleted rows with NULL values for longitude/latitude columns;

``` sql
--  These records are trips performed by Divvy staff for maintenance (587 rows)

DELETE  FROM  Bike_Data
WHERE         start_id  IS  NULL
              OR
              end_id    IS  NULL
```

<br />

####  3.  Dropped unnecessary columns for analysis;

``` sql
ALTER  TABLE    Bike_Data
DROP   COLUMN   start_time,
                end_time,
                bikeid,
                tripduration,
                from_station_id,
                from_station_name,
                to_station_id,
                to_station_name,
                birthyear
```

###### [Back to top](#data-cleaning)
