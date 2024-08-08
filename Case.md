##  1.1.  Find the latest StoreStock for each StoreCode, ProductCode pair

``` sql

SELECT   StoreCode,
         ProductCode,
         Date,
         StoreStock
FROM     (
         SELECT  *,
                 ROW_NUMBER() OVER(
                                  PARTITION BY StoreCode, ProductCode ORDER BY Date DESC
                                  ) AS row_count
         FROM    stock.dbo.inventory_position
         ) AS    T
WHERE    T.row_count <= 1

```

##  1.2  Sum sales by BuildingType

``` sql

SELECT     BuildingType,
           SUM(SalesRevenue)            AS  TotalSales
FROM       stock.dbo.inventory_position AS  i
LEFT JOIN  stock.dbo.store              AS  s
ON         i.StoreCode = s.StoreCode
GROUP BY   BuildingType
ORDER BY   TotalSales DESC

```

##  1.3  List stores description which have sales revenue lower than 50TL in 2014 May

``` sql

(
SELECT     DISTINCT(store.StoreDescription)
FROM       stock.dbo.inventory_position
LEFT JOIN  stock.dbo.store
ON         inventory_position.StoreCode = store.StoreCode 
WHERE      NOT EXISTS ( 
                      SELECT  * 
                      FROM    stock.dbo.inventory_position
                      WHERE   inventory_position.StoreCode = store.StoreCode
                              AND 
                              inventory_position.Date BETWEEN '2014-05-01' AND '2014-05-31'
                      )
)

UNION ALL

(
SELECT     store.StoreDescription
FROM       stock.dbo.inventory_position
LEFT JOIN  stock.dbo.store
ON         inventory_position.StoreCode = store.StoreCode
WHERE      inventory_position.Date BETWEEN '2014-05-01' AND '2014-05-31'
GROUP BY   store.StoreDescription
HAVING     SUM(inventory_position.SalesRevenue) < 50
)

ORDER BY   store.StoreDescription ASC

```

##  1.4  In February 2014, what is the difference between the highest-selling store and the least-selling store? 

###  Option A

``` sql

SELECT TOP(1)
       (
       SELECT  MAX(sum)
       FROM    (
               SELECT    SUM(SalesRevenue) AS sum 
               FROM      inventory_position 
               WHERE     Date BETWEEN '2014-02-01' AND '2014-02-28'
               GROUP BY  StoreCode
               ) a
       )
       - 
       (
       SELECT  MIN(sum) 
       FROM    (
               SELECT    SUM(SalesRevenue) AS sum 
               FROM      inventory_position 
               WHERE     Date BETWEEN '2014-02-01' AND '2014-02-28'
               GROUP BY  StoreCode
               ) b
       )       AS dif
FROM   inventory_position

```

###  Option B

``` sql
SELECT TOP(1)
       (
       SELECT    TOP(1)
                 SUM(SalesRevenue) AS TotalSales
       FROM      inventory_position
       WHERE     Date  BETWEEN '2014-02-01' AND '2014-02-28'
       GROUP BY  StoreCode
       ORDER BY  TotalSales DESC
       )
       - 
       (
       SELECT    TOP(1)
                 SUM(SalesRevenue) AS TotalSales
       FROM      inventory_position
       WHERE     Date  BETWEEN '2014-02-01' AND '2014-02-28'
       GROUP BY  StoreCode
       ORDER BY  TotalSales ASC
       ) AS dif
FROM
       inventory_position

```
