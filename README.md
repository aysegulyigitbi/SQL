# SQL Server LAG Function 

Hello everyone! Today, we'll be exploring the LAG function of SQL Server's analytic functions to calculate the difference in stock quantities for multiple product groups based on their previous day's stock levels.

In other words, the LAG function will come to our rescue!

First, let's define the LAG function. It's used to retrieve the value of a previous row, one or more rows before the current row, from a dataset. When using the LAG function, it's common for the first row to return NULL values.

Note: The LAG function is the opposite of the LEAD function, which retrieves the value of a row that follows the current row.

Let's start by getting familiar with our table.

![image](https://user-images.githubusercontent.com/127193220/226164761-4cb363b8-4e84-4708-9c0e-9362933d4bfc.png)

Our first step will be to use the LAG function to display the previous day's stock quantities in a new column. Since we'll be sorting by date in this column, we shouldn't forget to include the date column in our ORDER BY command.

Secondly, to calculate the differences in our current stock quantities based on the previous order quantities, we'll subtract the previously obtained order quantity column from our current quantity column.

SQL Query:

SELECT Stok_Kodu, Tarih, Miktar,

LAG(Miktar,1,0) OVER(PARTITION BY Stok_Kodu ORDER BY Tarih) AS Önceki_Miktar,

Miktar — LAG(Miktar,1,0) OVER(PARTITION BY Stok_Kodu ORDER BY Tarih) AS Fark

FROM [dbo].[Stok]

When we run our query, we can see that our stock codes are grouped sequentially according to dates, and at the same time, we can reach the previous stock amount information and the stock amount differences of our product on the previous date in the difference column.

![image](https://user-images.githubusercontent.com/127193220/226164911-b81c7732-de0b-4c0b-9745-4ed0046ec970.png)
