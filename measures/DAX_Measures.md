Copilotmaymakemistakes 1
PizzaSalesSQLQueries
PizzaSalesSQLQueries
A.KPI’s--1.TotalRevenue
SELECTSUM(total_price)ASTotal_RevenueFROMpizza_sales;--3.AverageOrderValue
SELECT(SUM(total_price)/COUNT(DISTINCTorder_id))ASAvg_order_ValueFROMpizza_sales;--5.TotalPizzasSold
SELECTSUM(quantity)ASTotal_pizza_soldFROMpizza_sales;--7.TotalOrders
SELECTCOUNT(DISTINCTorder_id)ASTotal_OrdersFROMpizza_sales;--9.AveragePizzasPerOrder
SELECTCAST(CAST(SUM(quantity)ASDECIMAL(10,2))/
CAST(COUNT(DISTINCTorder_id)ASDECIMAL(10,2))ASDECIMAL(10,2))AS
Avg_Pizzas_per_order
FROMpizza_sales;
B.DailyTrendforTotalOrders
SELECTDATENAME(DW,order_date)ASorder_day,COUNT(DISTINCTorder_id)AStotal_orders
FROMpizza_sales
GROUPBYDATENAME(DW,order_date);
C.MonthlyTrendforOrders
SELECTDATENAME(MONTH,order_date)ASMonth_Name,COUNT(DISTINCTorder_id)AS
Total_Orders
FROMpizza_sales
GROUPBYDATENAME(MONTH,order_date);
D.%ofSalesbyPizzaCategory
SELECTpizza_category,CAST(SUM(total_price)ASDECIMAL(10,2))AStotal_revenue,
CAST(SUM(total_price)*100/(SELECTSUM(total_price)FROMpizza_sales)ASDECIMAL(10,2))
ASPCT
FROMpizza_sales
GROUPBYpizza_category;
Copilotmaymakemistakes 2
E.%ofSalesbyPizzaSize
SELECTpizza_size,CAST(SUM(total_price)ASDECIMAL(10,2))AStotal_revenue,
CAST(SUM(total_price)*100/(SELECTSUM(total_price)FROMpizza_sales)ASDECIMAL(10,2))
ASPCT
FROMpizza_sales
GROUPBYpizza_size
ORDERBYpizza_size;
F.TotalPizzasSoldbyPizzaCategory(February)
SELECTpizza_category,SUM(quantity)ASTotal_Quantity_Sold
FROMpizza_sales
WHEREMONTH(order_date)=2
GROUPBYpizza_category
ORDERBYTotal_Quantity_SoldDESC;
G.Top5PizzasbyRevenue
SELECTTOP5pizza_name,SUM(total_price)ASTotal_Revenue
FROMpizza_sales
GROUPBYpizza_name
ORDERBYTotal_RevenueDESC;
H.Bottom5PizzasbyRevenue
SELECTTOP5pizza_name,SUM(total_price)ASTotal_Revenue
FROMpizza_sales
GROUPBYpizza_name
ORDERBYTotal_RevenueASC;
I.Top5PizzasbyQuantity
SELECTTOP5pizza_name,SUM(quantity)ASTotal_Pizza_Sold
FROMpizza_sales
GROUPBYpizza_name
ORDERBYTotal_Pizza_SoldDESC;
J.Bottom5PizzasbyQuantity
SELECTTOP5pizza_name,SUM(quantity)ASTotal_Pizza_Sold
FROMpizza_sales
GROUPBYpizza_name
ORDERBYTotal_Pizza_SoldASC;
K. Top 5 Pizzas by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROMpizza_sales
GROUPBYpizza_name
ORDERBYTotal_Orders DESC;
L. Bottom 5 Pizzas by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROMpizza_sales
GROUPBYpizza_name
ORDERBYTotal_Orders ASC;
3
Copilot may make mistakes
