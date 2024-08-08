
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
