## Bike Trip Case Study Dataset

### Bike Trips Data

<br />

Downloaded bike trips data for 2017, 2018 and 2019 from [Divvy Database](https://divvy-tripdata.s3.amazonaws.com/index.html) and imported cvs files to SQL Server;

-  Divvy_Trips_2017_Q1
-  Divvy_Trips_2017_Q2
-  Divvy_Trips_2017_Q3
-  Divvy_Trips_2017_Q4
-  Divvy_Trips_2018_Q1
-  Divvy_Trips_2018_Q2
-  Divvy_Trips_2018_Q3
-  Divvy_Trips_2018_Q4
-  Divvy_Trips_2019_Q1
-  Divvy_Trips_2019_Q2
-  Divvy_Trips_2019_Q3
-  Divvy_Trips_2019_Q4

<br />

Data structure of bike trips tables;

<br />

|  Column  |  Data Type  |
|  ---  |  ---  |
|  trip_id  |  int  |
|  start_time  |  datetime2(7)  |
|  end_time  |  datetime2(7)  |
|  bikeid  |  int  |
|  tripduration  |float  |
|  from_station_id  |  smallint  |
|  from_station_name  |  nvarchar(50)  |
|  to_station_id  |  smallint  |
|  to_station_name  |  nvarchar(50)  |
|  usertype  |nvarchar(50)  |
|  gender  |  nvarchar(50)  |
|  birthyear  |  int  |

<br />

### Bike Station Data 

<br />

Downloaded bike stations data from [Chicago Data Portal](https://data.cityofchicago.org/Transportation/Divvy-Trips/fg6s-gzvg/about_data) and imported cvs file to SQL Server;

-  Bike_Stations

<br />

Data structure of bike stations table;

<br />

|  Column  |  Data Type  |
|  ---  |  ---  |
|  id  |  smallint  |
|  name  |  nvarchar(50)  |
|  latitude  |  decimal(9, 6)  |
|  longitude  |  decimal(9, 6)  |
