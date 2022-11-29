# OptimizingSelectStatementInMySQL

I am using indexes on a table column to enhance query performance. I will be using these two tables Orders table and Employees table

![Orders](https://user-images.githubusercontent.com/106580846/204541153-0f5ce0bb-63ef-47f8-b479-bf52256339eb.png)
![Employees](https://user-images.githubusercontent.com/106580846/204541164-110d8534-d396-43de-9c11-03fcb92e5dba.png)

We regularly need to search the table by the ClientID such as to find the order placed by the client Cl1. We would normally use the query

SELECT * FROM Orders WHERE ClientID ='Cl1'; 

We do not yet have indexes which would optimize this query as shown by the explain statement below

![explain 11](https://user-images.githubusercontent.com/106580846/204542580-0a1aeaf2-8522-4d1e-b1e0-eaabd0a066d9.jpg)

We optimize this query by creating an index named IdxClientID on the ClientID column of the Orders table. Then when we run the same SELECT statement as above with the EXPLAIN statement this is the output

![explain 22](https://user-images.githubusercontent.com/106580846/204543132-90984374-d226-494e-9746-468cb3adb53d.jpg)
