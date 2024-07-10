## SQL Server Queries For Data Analysis

####  1.  Query to create list of yearly trip count for customers/subscribers;

``` sql
SELECT  trip_year,
        usertype,
        COUNT(*) as count
FROM
        Bike_Data
GROUP BY
        trip_year,
        usertype
ORDER BY
        trip_year,
        usertype
```

####  2.  Query to create list of yearly most popular months for customers/subscribers;

``` sql
SELECT  trip_year,
        usertype,
        trip_month,
        COUNT(*) as count
FROM
        Bike_Data
GROUP BY
        trip_year,
        usertype,
        trip_month
ORDER BY
        trip_year,
        usertype,
        trip_month
```

####  3.  Query to create list of yearly most popular days for customers/subscribers;

``` sql
SELECT  trip_year,
        usertype,
        trip_day,
        COUNT(*) as count
FROM
        Bike_Data
GROUP BY
        trip_year,
        usertype,
        trip_day
ORDER BY
        trip_year,
        usertype,
        trip_day
```

####  4.  Query to create list of yearly most popular time periods for customers/subscribers;

``` sql
SELECT 
        trip_year,
        usertype,
        CASE
          WHEN  trip_hour  BETWEEN  0   AND  5   THEN  '00:00 - 06:00'
          WHEN  trip_hour  BETWEEN  6   AND  7   THEN  '06:00 - 08:00'
          WHEN  trip_hour  BETWEEN  8   AND  9   THEN  '08:00 - 10:00'
          WHEN  trip_hour  BETWEEN  10  AND  13  THEN  '10:00 - 14:00'
          WHEN  trip_hour  BETWEEN  14  AND  16  THEN  '14:00 - 17:00'
          WHEN  trip_hour  BETWEEN  17  AND  19  THEN  '17:00 - 20:00'
          WHEN  trip_hour  BETWEEN  20  AND  23  THEN  '20:00 - 00:00'
        END AS  time_period,
        COUNT(*)  AS  count
FROM
        Bike_Data
GROUP BY
        trip_year,
        usertype,
        CASE
          WHEN  trip_hour  BETWEEN  0   AND  5   THEN  '00:00 - 06:00'
          WHEN  trip_hour  BETWEEN  6   AND  7   THEN  '06:00 - 08:00'
          WHEN  trip_hour  BETWEEN  8   AND  9   THEN  '08:00 - 10:00'
          WHEN  trip_hour  BETWEEN  10  AND  13  THEN  '10:00 - 14:00'
          WHEN  trip_hour  BETWEEN  14  AND  16  THEN  '14:00 - 17:00'
          WHEN  trip_hour  BETWEEN  17  AND  19  THEN  '17:00 - 20:00'
          WHEN  trip_hour  BETWEEN  20  AND  23  THEN  '20:00 - 00:00'
        END
ORDER BY
        trip_year,
        usertype,
        time_period
```

####  5.  Query to create list of yearly most popular trip durations for customers/subscribers;

``` sql
SELECT 
        trip_year,
        usertype,
        CASE
          WHEN  trip_duration  BETWEEN  '00:00'  AND  '00:15'  THEN  '<15 Minutes'
          WHEN  trip_duration  BETWEEN  '00:16'  AND  '00:30'  THEN  '15-30 Minutes'
          WHEN  trip_duration  BETWEEN  '00:31'  AND  '01:00'  THEN  '30-60 Minutes'
          WHEN  trip_duration  BETWEEN  '01:01'  AND  '02:00'  THEN  '1-2 Hours'
          WHEN  trip_duration  BETWEEN  '02:01'  AND  '04:00'  THEN  '2-4 Hours'
          WHEN  trip_duration  BETWEEN  '04:01'  AND  '06:00'  THEN  '4-6 Hours'
          WHEN  trip_duration  >        '06:00'                THEN  '6+ Hours'
        END AS duration_group,
        COUNT(*) as count
FROM
        Bike_Data
GROUP BY
        trip_year,
        usertype,
        CASE
          WHEN  trip_duration  BETWEEN  '00:00'  AND  '00:15'  THEN  '<15 Minutes'
          WHEN  trip_duration  BETWEEN  '00:16'  AND  '00:30'  THEN  '15-30 Minutes'
          WHEN  trip_duration  BETWEEN  '00:31'  AND  '01:00'  THEN  '30-60 Minutes'
          WHEN  trip_duration  BETWEEN  '01:01'  AND  '02:00'  THEN  '1-2 Hours'
          WHEN  trip_duration  BETWEEN  '02:01'  AND  '04:00'  THEN  '2-4 Hours'
          WHEN  trip_duration  BETWEEN  '04:01'  AND  '06:00'  THEN  '4-6 Hours'
          WHEN  trip_duration  >        '06:00'                THEN  '6+ Hours'
        END
ORDER BY
        trip_year,
        usertype,
        duration_group
```

####  6.  Query to create list of different gender and age groups of subscribers for each year;

``` sql
SELECT 
        trip_year,
        CASE
          WHEN  user_age  BETWEEN  16  AND  20  THEN  '15-20'
          WHEN  user_age  BETWEEN  21  AND  25  THEN  '21-25'
          WHEN  user_age  BETWEEN  26  AND  30  THEN  '26-30'
          WHEN  user_age  BETWEEN  31  AND  35  THEN  '31-35'
          WHEN  user_age  BETWEEN  36  AND  40  THEN  '36-40'
          WHEN  user_age  BETWEEN  41  AND  45  THEN  '41-45'
          WHEN  user_age  BETWEEN  46  AND  50  THEN  '46-50'
          WHEN  user_age  BETWEEN  51  AND  55  THEN  '51-55'
          WHEN  user_age  BETWEEN  56  AND  60  THEN  '56-60'
          WHEN  user_age  BETWEEN  61  AND  65  THEN  '61-65'
          WHEN  user_age  BETWEEN  66  AND  70  THEN  '66-70'
          WHEN  user_age  BETWEEN  71  AND  75  THEN  '71-75'
          WHEN  user_age  BETWEEN  76  AND  80  THEN  '76-80'
        END  AS  age_group,
        gender,
        COUNT(*)  AS  count
FROM
        Bike_Data
WHERE
        usertype = 'Subscriber'
GROUP BY
        trip_year,
        CASE
          WHEN  user_age  BETWEEN  16  AND  20  THEN  '15-20'
          WHEN  user_age  BETWEEN  21  AND  25  THEN  '21-25'
          WHEN  user_age  BETWEEN  26  AND  30  THEN  '26-30'
          WHEN  user_age  BETWEEN  31  AND  35  THEN  '31-35'
          WHEN  user_age  BETWEEN  36  AND  40  THEN  '36-40'
          WHEN  user_age  BETWEEN  41  AND  45  THEN  '41-45'
          WHEN  user_age  BETWEEN  46  AND  50  THEN  '46-50'
          WHEN  user_age  BETWEEN  51  AND  55  THEN  '51-55'
          WHEN  user_age  BETWEEN  56  AND  60  THEN  '56-60'
          WHEN  user_age  BETWEEN  61  AND  65  THEN  '61-65'
          WHEN  user_age  BETWEEN  66  AND  70  THEN  '66-70'
          WHEN  user_age  BETWEEN  71  AND  75  THEN  '71-75'
          WHEN  user_age  BETWEEN  76  AND  80  THEN  '76-80'
        END,
        gender
ORDER BY
        trip_year,
        age_group,
        gender
```

####  7.  Most popular start stations by year and user type;

#####  7.1.  Query to create a new table with trip counts of each start station by year and user type;

``` sql
SELECT  *
INTO    Start_Stations
FROM
        (
        SELECT
            trip_year,
            usertype,
            start_id,
            start_station,
            COUNT(*)  AS  trip_count,
            start_latitude,
            start_longitude
        FROM
            Bike_Data
        GROUP BY
            trip_year,
            usertype,
            start_id,
            start_station,
            start_latitude,
            start_longitude
        )  a
```

#####  7.2.  Query to create a list of yearly 10 most popular start stations for customers/subscribers;

``` sql
SELECT  
        trip_year,
        usertype,
        start_id,
        start_station,
        trip_count,
        start_latitude,
        start_longitude
FROM
        (
        SELECT 
              *,
              ROW_NUMBER() OVER(partition by trip_year, usertype ORDER BY trip_count DESC) AS row_count
        FROM
              Start_Stations
        ) AS  T
WHERE 
        T.row_count <= 10
```

####  8.  Most popular end stations by year and user type;

#####  8.1.  Query to create a new table with trip counts of each end station by year and user type;

``` sql
SELECT  *
INTO    End_Stations
FROM
        (
        SELECT
              trip_year,
              usertype,
              end_id,
              end_station,
              COUNT(*)  AS  trip_count,
              end_latitude,
              end_longitude
        FROM
              Bike_Data
        GROUP BY
              trip_year,
              usertype,
              end_id,
              end_station,
              end_latitude,
              end_longitude
        )  a
```

#####  8.2.  Query to create a list of yearly 10 most popular end stations for customers/subscribers;

``` sql
SELECT  
        trip_year,
        usertype,
        end_id,
        end_station,
        trip_count,
        end_latitude,
        end_longitude
FROM
        (
        SELECT 
              *,
              ROW_NUMBER() OVER(partition by trip_year, usertype ORDER BY trip_count DESC) AS row_count
        FROM
              End_Stations
        ) AS T
WHERE 
        T.row_count <= 10
```

####  9.  Most popular trip routes by year and user type;

#####  9.1.  Query to create a new table with trip counts of each route by year and user type;

``` sql
SELECT  *
INTO    Trip_Routes
FROM
        (
        SELECT
              trip_year,
              usertype,
              trip_route,
              start_station,
              end_station,
              COUNT(*)  AS  trip_count,
              start_latitude,
              start_longitude,
              end_latitude,
              end_longitude
        FROM
              Bike_Data
        GROUP BY
              trip_year,
              usertype,
              trip_route,
              start_station,
              end_station,
              start_latitude,
              start_longitude,
              end_latitude,
              end_longitude
        ) a
```

#####  9.2.  Query to create a list of yearly 10 most popular route for customers/subscribers;

``` sql
SELECT  
        trip_year,
        usertype,
        trip_route,
        start_station,
        end_station,
        trip_count,
        start_latitude,
        start_longitude,
        end_latitude,
        end_longitude
FROM
        (
        SELECT 
              *,
              ROW_NUMBER() OVER(partition by trip_year, usertype ORDER BY trip_count DESC) AS row_count
        FROM
              Trip_Routes
        ) AS T
WHERE 
        T.row_count <= 10
```
