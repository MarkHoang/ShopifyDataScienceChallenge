## 1A

From observing the dataset and exploratory data analysis, each line refers to one order placed by a customer, which may include multiple pairs of shoes. 

Additionally, there seems to be an outlier for shop 78 as their 1 shoe order was priced at 25725 which would have skewed our calculation, assuming it is faulty data since 25725 is an unlikely price for a pair of shoes.

It would appear that the AOV calculation currently is done as an aggregate for all sneaker shops taking total revenue divided by total number of orders (5000), which does not communicate much in terms of individual shops’ performance and would not be useful for actionable steps for each respective shop.

However, this information could definitely be useful for Shopify’s internal analysis on overall consumer spending in the category.

A better way to evaluate the data and give more segregated insights would be to calculate AOV per shop using the same Total Order Amount/ Orders but for each shop.

## 1B

Aside from the AOV for each shop, a metric I would report from the dataset is the **average shoe price across all shops**. This could be used by individual shops as a measure to position their brand and perceived value to customers. 

## 1C
Assuming order amounts do not take into account promotions and discounts,

If we take into account the outlier (Shop 78) then the average shoe price would be: **$407.99**
If we don’t take into account the outlier, then the average shoe price would be: **$152.26**

## 2A

SELECT COUNT (Orders.OrderID) AS 'Total Orders by Speedy Express'  <br/>
FROM Shippers, Orders <br/>
WHERE Shippers.ShipperID = Orders.ShipperID AND <br/>
Shippers.ShipperID = 1 <br/>

**SOLUTION: 54**

## 2B

SELECT TOP 1 \* <br/>
FROM ( <br/>
	SELECT Employees.LastName, Count(\*) <br/>
	FROM Employees, Orders <br/>
	WHERE Employees.EmployeeID = Orders.EmployeeID <br/>
	GROUP BY Employees.LastName <br/>
	Order by Count("*") Desc)  <br/>

**SOLUTION: Peacock (40 orders)**

## 2C

SELECT TOP 1 \*
FROM ( <br/>
	SELECT Products.ProductName, Count(\*) <br/>
	FROM Orders, OrderDetails, Customers, Products <br/>
	WHERE Orders.OrderID = OrderDetails.OrderID AND <br/>
    		Customers.Country = 'Germany' AND <br/>
        		Products.ProductID = OrderDetails.ProductID AND <br/>
        		Orders.CustomerID = Customers.CustomerID <br/>
	GROUP BY Products.ProductName <br/>
	Order by Count(\*) Desc)  <br/>

**SOLUTION: Gorgonzola Telino (ordered 5 times)**
