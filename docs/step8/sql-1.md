✍️ 200개 이상 팔린 상품명과 그 수량을 수량 기준 내림차순으로 보여주세요.

```
SELECT A.ProductID
    ,  A.ProductName
    ,  A.TotalQuantity
  FROM (
        SELECT Products.ProductID
            ,  Products.ProductName
            ,  SUM(OrderDetails.Quantity) TotalQuantity
          FROM Products
         INNER JOIN OrderDetails
            ON Products.ProductID = OrderDetails.ProductID
         GROUP BY Products.ProductID
        HAVING SUM(OrderDetails.Quantity) >= 200
    ) A
 ORDER BY A.TotalQuantity DESC;


ProductID	ProductName                 TotalQuantity
60	        Camembert Pierrot           1577
59	        Raclette Courdavault        1496
31	        Gorgonzola Telino           1397
56	        Gnocchi di nonna Alice      1263
16	        Pavlova                     1158
75	        Rhönbräu Klosterbier        1155
...
```

​

✍️ 많이 주문한 순으로 고객 리스트(ID, 고객명)를 구해주세요.

```
SELECT Customers.CustomerID
    ,  Customers.CustomerName
    ,  CASE WHEN Orders.CustomerID IS NULL THEN 0
            ELSE Orders.OrderQuantity END OrderQuantity
  FROM Customers
  LEFT JOIN (
        SELECT Orders.CustomerID
            ,  SUM(OrderDetails.Quantity) OrderQuantity
          FROM Orders
         INNER JOIN OrderDetails
            ON Orders.OrderID = OrderDetails.OrderID
         GROUP BY Orders.CustomerID
    ) Orders
    ON Customers.CustomerID = Orders.CustomerID
 ORDER BY Orders.OrderQuantity DESC;
```

​

✍️ 많은 돈을 지출한 순으로 고객 리스트를 구해주세요.

```
SELECT Customers.CustomerID
    ,  Customers.CustomerName
    ,  CASE WHEN Orders.CustomerID IS NULL THEN 0
            ELSE Orders.OrderAmount END OrderAmount
  FROM Customers
  LEFT JOIN (
        SELECT Orders.CustomerID
            ,  SUM(OrderDetails.Quantity * Products.Price) OrderAmount
          FROM Orders
         INNER JOIN OrderDetails
            ON Orders.OrderID = OrderDetails.OrderID
         INNER JOIN Products
            ON OrderDetails.ProductID = Products.ProductID
         GROUP BY Orders.CustomerID
    ) Orders
    ON Customers.CustomerID = Orders.CustomerID
 ORDER BY Orders.OrderAmount DESC;
```
