## Data Analysis

##### [1.  Customer / Subscriber Ratio](  #1--query-to-create-list-of-yearly-trip-count-for-customerssubscribers)

##### [2.  Popular Months](               #2--query-to-create-list-of-yearly-most-popular-months-for-customerssubscribers)

##### [3.  Popular Days](                 #3--query-to-create-list-of-yearly-most-popular-days-for-customerssubscribers)

##### [4.  Time Periods](                 #4--query-to-create-list-of-yearly-most-popular-time-periods-for-customerssubscribers)

##### [5.  Trip Durations](               #5--query-to-create-list-of-yearly-most-popular-trip-durations-for-customerssubscribers)

##### [6.  Age Groups and Gender](        #6--query-to-create-list-of-different-gender-and-age-groups-of-subscribers-for-each-year)

##### [7.  Most Used Start Stations](     #72--query-to-create-a-list-of-yearly-10-most-popular-start-stations-for-customerssubscribers)

##### [8.  Most Used End Stations](       #82--query-to-create-a-list-of-yearly-10-most-popular-end-stations-for-customerssubscribers)

##### [9.  Popular Routes](               #92--query-to-create-a-list-of-yearly-10-most-popular-route-for-customerssubscribers)

<br />

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

| trip_year |  usertype  |   count   |
|   :---:   |    ---     |    ---:   |
|   2017    | Customer   |   836.864 |
|   2017    | Subscriber | 2.988.733 |
|   2018    | Customer   |   676.162 |
|   2018    | Subscriber | 2.914.506 |
|   2019    | Customer   |   879.188 |
|   2019    | Subscriber | 2.912.917 |

###### [Back to top](#data-analysis)

<br />

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

| trip_year | usertype | trip_month |  count  |
|   :---:   |  :---:   |   :---:    |   ---:  |
|   2017    | Customer |     1      |   5.316 |
|   2017    | Customer |     2      |  23.587 |
|   2017    | Customer |     3      |  12.496 |
|   2017    | Customer |     4      |  61.247 |
|   2017    | Customer |     5      |  82.319 |
|   2017    | Customer |     6      | 132.190 |
|   2017    | Customer |     7      | 179.379 |
|   2017    | Customer |     8      | 146.056 |
|   2017    | Customer |     9      | 116.191 |
|   2017    | Customer |    10      |  58.809 |
|   2017    | Customer |    11      |  12.699 |
|   2017    | Customer |    12      |   6.575 |

###### [Back to top](#data-analysis)

<br />

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

| trip_year |  usertype  | trip_day  |  count  |
|   :---:   |     ---    |    ---    |   ---:  |
|   2017    |  Customer  |  Friday   |  96.453 |
|   2017    |  Customer  |  Monday   | 106.775 |
|   2017    |  Customer  |  Saturday | 224.613 |
|   2017    |  Customer  |  Sunday   | 201.476 |
|   2017    |  Customer  |  Thursday |  67.910 |
|   2017    |  Customer  |  Tuesday  |  77.836 |
|   2017    |  Customer  | Wednesday |  61.801 |
|   2017    | Subscriber |  Friday   | 457.670 |
|   2017    | Subscriber |  Monday   | 471.600 |
|   2017    | Subscriber |  Saturday | 306.103 |
|   2017    | Subscriber |  Sunday   | 290.821 |
|   2017    | Subscriber |  Thursday | 481.591 |
|   2017    | Subscriber |  Tuesday  | 500.423 |
|   2017    | Subscriber | Wednesday | 480.525 |

###### [Back to top](#data-analysis)

<br />

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

| trip_year |  usertype  |  time_period  |  count  |
|   :---:   |    ---     |      ---      |   ---:  |
|   2017    |  Customer  | 00:00 - 06:00 |  14.604 |
|   2017    |  Customer  | 06:00 - 08:00 |   9.134 |
|   2017    |  Customer  | 08:00 - 10:00 |  43.005 |
|   2017    |  Customer  | 10:00 - 14:00 | 277.093 |
|   2017    |  Customer  | 14:00 - 17:00 | 256.071 |
|   2017    |  Customer  | 17:00 - 20:00 | 164.413 |
|   2017    |  Customer  | 20:00 - 00:00 |  72.544 |
|   2017    | Subscriber | 00:00 - 06:00 |  72.659 |
|   2017    | Subscriber | 06:00 - 08:00 | 317.769 |
|   2017    | Subscriber | 08:00 - 10:00 | 420.820 |
|   2017    | Subscriber | 10:00 - 14:00 | 525.088 |
|   2017    | Subscriber | 14:00 - 17:00 | 587.370 |
|   2017    | Subscriber | 17:00 - 20:00 | 798.473 |
|   2017    | Subscriber | 20:00 - 00:00 | 266.554 |

###### [Back to top](#data-analysis)

<br />

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

| trip_year |  usertype  | duration_group |   count   |
|   :---:   |    ---     |      ---:      |    ---:   |
|   2017    |  Customer  |    <15 Minutes |   211.872 |
|   2017    |  Customer  |    1-2 Hours   |    53.858 |
|   2017    |  Customer  |  15-30 Minutes |   390.926 |
|   2017    |  Customer  |    2-4 Hours   |    13.523 |
|   2017    |  Customer  |  30-60 Minutes |   163.490 |
|   2017    |  Customer  |    4-6 Hours   |     1.661 |
|   2017    |  Customer  |     6+ Hours   |     1.534 |
|   2017    | Subscriber |    <15 Minutes | 2.277.108 |
|   2017    | Subscriber |    1-2 Hours   |     4.543 |
|   2017    | Subscriber |  15-30 Minutes |   653.833 |
|   2017    | Subscriber |    2-4 Hours   |       957 |
|   2017    | Subscriber |  30-60 Minutes |    51.259 |
|   2017    | Subscriber |    4-6 Hours   |       248 |
|   2017    | Subscriber |     6+ Hours   |       785 |

###### [Back to top](#data-analysis)

<br />

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

| trip_year | age_group | gender |  count  |
|   :---:   |   :---:   |   ---  |   ---:  |
|   2017    |   15-20   | Female |  10.069 |
|   2017    |   15-20   |  Male  |  23.312 |
|   2017    |   21-25   | Female | 122.703 |
|   2017    |   21-25   |  Male  | 287.680 |
|   2017    |   26-30   | Female | 231.800 |
|   2017    |   26-30   |  Male  | 589.107 |
|   2017    |   31-35   | Female | 149.833 |
|   2017    |   31-35   |  Male  | 454.051 |
|   2017    |   36-40   | Female |  72.451 |
|   2017    |   36-40   |  Male  | 277.246 |
|   2017    |   41-45   | Female |  39.190 |
|   2017    |   41-45   |  Male  | 175.628 |
|   2017    |   46-50   | Female |  41.433 |
|   2017    |   46-50   |  Male  | 146.473 |
|   2017    |   51-55   | Female |  37.857 |
|   2017    |   51-55   |  Male  | 124.371 |

###### [Back to top](#data-analysis)

<br />

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

<br />

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

| trip_year |  usertype  | start_id |           start_station             | trip_count | start_latitude | start_longitude |
|   :---:   |    ---     |   ---:   |                ---                  |    ---:    |     :---:      |      :---:      |
|   2017    |  Customer  |     35   | Streeter Dr & Grand Ave             |   77.368   |    41.892278   |    -87.612043   |
|   2017    |  Customer  |     76   | Lake Shore Dr & Monroe St           |   42.151   |    41.880958   |    -87.616743   |
|   2017    |  Customer  |    268   | Lake Shore Dr & North Blvd          |   28.096   |    41.911722   |    -87.626804   |
|   2017    |  Customer  |    177   | Theater on the Lake                 |   26.399   |    41.926277   |    -87.630834   |
|   2017    |  Customer  |      3   | Shedd Aquarium                      |   25.242   |    41.867226   |    -87.615355   |
|   2017    |  Customer  |     90   | Millennium Park                     |   23.457   |    41.881032   |    -87.624084   |
|   2017    |  Customer  |     85   | Michigan Ave & Oak St               |   23.180   |    41.900960   |    -87.623777   |
|   2017    |  Customer  |    341   | Adler Planetarium                   |   17.929   |    41.866095   |    -87.607267   |
|   2017    |  Customer  |      6   | Dusable Harbor                      |   17.639   |    41.885042   |    -87.612795   |
|   2017    |  Customer  |      4   | Burnham Harbor                      |   13.413   |    41.856268   |    -87.613348   |
|   2017    | Subscriber |    192   | Canal St & Adams St                 |   48.855   |    41.879255   |    -87.639904   |
|   2017    | Subscriber |     91   | Clinton St & Washington Blvd        |   47.977   |    41.883380   |    -87.641170   |
|   2017    | Subscriber |     77   | Clinton St & Madison St             |   42.386   |    41.882242   |    -87.641066   |
|   2017    | Subscriber |    133   | Kingsbury St & Kinzie St            |   32.914   |    41.889177   |    -87.638506   |
|   2017    | Subscriber |    287   | Franklin St & Arcade Pl             |   32.237   |    41.880317   |    -87.635185   |
|   2017    | Subscriber |    174   | Canal St & Madison St               |   31.885   |    41.882091   |    -87.639833   |
|   2017    | Subscriber |    195   | Columbus Dr & Randolph St           |   29.039   |    41.884728   |    -87.619521   |
|   2017    | Subscriber |     81   | Daley Center Plaza                  |   28.579   |    41.884451   |    -87.629892   |
|   2017    | Subscriber |    100   | Orleans St & Merchandise Mart Plaza |   27.357   |    41.888243   |    -87.636390   |
|   2017    | Subscriber |     43   | Michigan Ave & Washington St        |   25.931   |    41.883550   |    -87.624180   |

###### [Back to top](#data-analysis)

<br />

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

<br />

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

| trip_year |  usertype  | end_id |             end_station             | trip_count | end_latitude | end_longitude |
|   :---:   |    ---     |  ---:  |                ---                  |    ---:    |    :---:     |     :---:     |
|   2017    |  Customer  |    35  | Streeter Dr & Grand Ave             |   85.673   |   41.892278  |   -87.612043  |
|   2017    |  Customer  |    76  | Lake Shore Dr & Monroe St           |   38.933   |   41.880958  |   -87.616743  |
|   2017    |  Customer  |   268  | Lake Shore Dr & North Blvd          |   30.503   |   41.911722  |   -87.626804  |
|   2017    |  Customer  |   177  | Theater on the Lake                 |   29.618   |   41.926277  |   -87.630834  |
|   2017    |  Customer  |    90  | Millennium Park                     |   27.385   |   41.881032  |   -87.624084  |
|   2017    |  Customer  |    85  | Michigan Ave & Oak St               |   26.061   |   41.900960  |   -87.623777  |
|   2017    |  Customer  |     3  | Shedd Aquarium                      |   23.285   |   41.867226  |   -87.615355  |
|   2017    |  Customer  |   341  | Adler Planetarium                   |   17.003   |   41.866095  |   -87.607267  |
|   2017    |  Customer  |     4  | Burnham Harbor                      |   13.672   |   41.856268  |   -87.613348  |
|   2017    |  Customer  |     6  | Dusable Harbor                      |   13.628   |   41.885042  |   -87.612795  |
|   2017    | Subscriber |   192  | Canal St & Adams St                 |   50.808   |   41.879255  |   -87.639904  |
|   2017    | Subscriber |    77  | Clinton St & Madison St             |   48.465   |   41.882242  |   -87.641066  |
|   2017    | Subscriber |    91  | Clinton St & Washington Blvd        |   45.292   |   41.883380  |   -87.641170  |
|   2017    | Subscriber |   133  | Kingsbury St & Kinzie St            |   32.591   |   41.889177  |   -87.638506  |
|   2017    | Subscriber |   174  | Canal St & Madison St               |   29.434   |   41.882091  |   -87.639833  |
|   2017    | Subscriber |    81  | Daley Center Plaza                  |   28.781   |   41.884451  |   -87.629892  |
|   2017    | Subscriber |    43  | Michigan Ave & Washington St        |   28.701   |   41.883550  |   -87.624180  |
|   2017    | Subscriber |   287  | Franklin St & Arcade Pl             |   26.709   |   41.880317  |   -87.635185  |
|   2017    | Subscriber |   100  | Orleans St & Merchandise Mart Plaza |   24.812   |   41.888243  |   -87.636390  |
|   2017    | Subscriber |   110  | State St & Erie St                  |   23.163   |   41.893992  |   -87.629318  |

###### [Back to top](#data-analysis)

<br />

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

<br />

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

|trip_year|  usertype  |trip_route | start_station| end_station |trip_count | start_latitude | start_longitude | end_latitude | end_longitude |
|  :---:  |     ---    |   ---:    |      ---     |     ---     |   ---:    |     :---:      |      :---:      |    :---:     |     :---:     |
|  2017   |  Customer  |  76 - 35  | Lake Shore   | Streeter D  |  10.971   |    41.880958   |    -87.616743   |   41.892278  |   -87.612043  |
|  2017   |  Customer  |  35 - 35  | Streeter Dr  | Streeter D  |   9.128   |    41.892278   |    -87.612043   |   41.892278  |   -87.612043  |
|  2017   |  Customer  |  35 - 268 | Streeter Dr  | Lake Shore  |   6.628   |    41.892278   |    -87.612043   |   41.911722  |   -87.626804  |
|  2017   |  Customer  |  35 - 76  | Streeter Dr  | Lake Shore  |   6.311   |    41.892278   |    -87.612043   |   41.880958  |   -87.616743  |
|  2017   |  Customer  |  35 - 177 | Streeter Dr  | Theater on  |   6.147   |    41.892278   |    -87.612043   |   41.926277  |   -87.630834  |
|  2017   |  Customer  | 268 - 35  | Lake Shore   | Streeter D  |   6.076   |    41.911722   |    -87.626804   |   41.892278  |   -87.612043  |
|  2017   |  Customer  | 177 - 35  | Theater on   | Streeter D  |   5.495   |    41.926277   |    -87.630834   |   41.892278  |   -87.612043  |
|  2017   |  Customer  |  76 - 76  | Lake Shore   | Lake Shore  |   4.931   |    41.880958   |    -87.616743   |   41.880958  |   -87.616743  |
|  2017   |  Customer  |  35 - 85  | Streeter Dr  | Michigan A  |   4.092   |    41.892278   |    -87.612043   |   41.900960  |   -87.623777  |
|  2017   |  Customer  |  35 - 90  | Streeter Dr  | Millennium  |   3.750   |    41.892278   |    -87.612043   |   41.881032  |   -87.624084  |
|  2017   | Subscriber |  18 - 43  | Wacker Dr    | Michigan A  |   3.042   |    41.883132   |    -87.637321   |   41.883550  |   -87.624180  |
|  2017   | Subscriber | 149 - 148 | Calumet Ave  | State St    |   2.724   |    41.834900   |    -87.617930   |   41.834734  |   -87.625813  |
|  2017   | Subscriber | 320 - 241 | Loomis St    | Morgan St   |   2.711   |    41.872187   |    -87.661501   |   41.871737  |   -87.651030  |
|  2017   | Subscriber | 174 - 43  | Canal St     | Michigan A  |   2.682   |    41.882091   |    -87.639833   |   41.883550  |   -87.624180  |
|  2017   | Subscriber | 237 - 148 | Martin Luth  | State St    |   2.603   |    41.842052   |    -87.617000   |   41.834734  |   -87.625813  |
|  2017   | Subscriber |  43 - 192 | Michigan A   | Canal St    |   2.578   |    41.883550   |    -87.624180   |   41.879255  |   -87.639904  |
|  2017   | Subscriber | 195 - 91  | Columbus D   | Clinton St  |   2.505   |    41.884728   |    -87.619521   |   41.883380  |   -87.641170  |
|  2017   | Subscriber | 192 - 43  | Canal St     | Michigan A  |   2.472   |    41.879255   |    -87.639904   |   41.883550  |   -87.624180  |
|  2017   | Subscriber | 148 - 149 | State St     | Calumet A   |   2.441   |    41.834734   |    -87.625813   |   41.834900  |   -87.617930  |
|  2017   | Subscriber |  91 - 43  | Clinton St   | Michigan A  |   2.409   |    41.883380   |    -87.641170   |   41.883550  |   -87.624180  |

###### [Back to top](#data-analysis)
