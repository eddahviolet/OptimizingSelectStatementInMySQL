# OptimizingSelectStatementInMySQL

I am using indexes on a table column to enhance query performance. I will be using these two tables Orders table and Employees table

![Orders](https://user-images.githubusercontent.com/106580846/204541153-0f5ce0bb-63ef-47f8-b479-bf52256339eb.png)
![Employees](https://user-images.githubusercontent.com/106580846/204541164-110d8534-d396-43de-9c11-03fcb92e5dba.png)

Task 1: Add an indexed Column

We regularly perform searches againts the ClientID column such as to find the order placed by the client Cl1. We would normally use the query

SELECT * FROM Orders WHERE ClientID ='Cl1'; 

We do not yet have indexes which would optimize this query as shown by the explain statement below

![explain 11](https://user-images.githubusercontent.com/106580846/204542580-0a1aeaf2-8522-4d1e-b1e0-eaabd0a066d9.jpg)

We optimize this query by creating an index named IdxClientID on the ClientID column of the Orders table.

![indexing](https://user-images.githubusercontent.com/106580846/204546964-77828fca-a84f-48b0-af1c-bf41102efb30.jpg)


Then when we run the same SELECT statement as above with the EXPLAIN statement this is the output

![explain 22](https://user-images.githubusercontent.com/106580846/204543132-90984374-d226-494e-9746-468cb3adb53d.jpg)

Task 2: Use wildcard with Indexes
We need to find an employee with the last Tolo. Normally we would have written the following query to complete this task
SELECT * FROM Employees WHERE FullName LIKE '%Tolo';
However, there’s an index on the FullName column which the query cannot use because it contains a leading wildcard (%) in the WHERE clause condition.
Hencw we will Add a new column to the Employees table called ReverseFullName

![add new column](https://user-images.githubusercontent.com/106580846/204546438-54449a49-2da3-4848-b02c-258fbe346739.jpg)

Populate the ReverseFullName column with the name of each employee as its values, but in reverse.

![reverse name](https://user-images.githubusercontent.com/106580846/204547287-dbfb5cc4-b7a5-43b9-9097-cb5c477dcc36.jpg)
 
 Create an index named IdxReverseFullName on the ReverseFullName column

