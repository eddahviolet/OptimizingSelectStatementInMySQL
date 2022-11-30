# OptimizingSelectStatementInMySQL

I am using indexes on a table column to enhance query performance. I will be using these two tables Orders table and Employees table

![Orders](https://user-images.githubusercontent.com/106580846/204541153-0f5ce0bb-63ef-47f8-b479-bf52256339eb.png)
![Employees](https://user-images.githubusercontent.com/106580846/204541164-110d8534-d396-43de-9c11-03fcb92e5dba.png)

Task 1: Add an indexed Column

We regularly perform searches againts the ClientID column such as to find the order placed by clients. For instance, finding the order placed by the client "Cl1" we would normally use the query:

SELECT * FROM Orders WHERE ClientID ="Cl1"; 

We do not yet have indexes which would optimize this query as shown by the explain statement below

![explain 11](https://user-images.githubusercontent.com/106580846/204542580-0a1aeaf2-8522-4d1e-b1e0-eaabd0a066d9.jpg)

We optimize this query by creating an index named IdxClientID on the ClientID column of the Orders table.

![indexing](https://user-images.githubusercontent.com/106580846/204546964-77828fca-a84f-48b0-af1c-bf41102efb30.jpg)


Then when we run the same SELECT statement as above with the EXPLAIN statement this is the output, we can see in the possible keys and keys column thers is now an index where it previosuly indicated "Null"

![explain 22](https://user-images.githubusercontent.com/106580846/204543132-90984374-d226-494e-9746-468cb3adb53d.jpg)

Task 2: Use wildcard with Indexes
On the Employees table. we need to find an employee with the last name Tolo. Normally we would have written the following query to complete this task
SELECT * FROM Employees WHERE FullName LIKE "%Tolo";
We want to use indexes to optimize this query however, indexes dont work with leading wildcards instead use trailing wildcards
Hence we will add a new column to the Employees table called ReverseFullName, create an index and use a trailing wildcard

![add new column](https://user-images.githubusercontent.com/106580846/204546438-54449a49-2da3-4848-b02c-258fbe346739.jpg)

Populate the ReverseFullName column with the name of each employee as its values, but in reverse.

![reverse name](https://user-images.githubusercontent.com/106580846/204547287-dbfb5cc4-b7a5-43b9-9097-cb5c477dcc36.jpg)
 
 The Employees table would now look like this
 
 ![reverse full name table](https://user-images.githubusercontent.com/106580846/204737593-a2754f61-3c08-46c6-9101-7f5b2f52090a.jpg)

 Create an index named IdxReverseFullName on the ReverseFullName column

![reversename index](https://user-images.githubusercontent.com/106580846/204738233-d77f4b59-64f5-403d-98ac-e0d2e09d0dae.png)

Then use the SELECT query using a trailing wildcard instead of the leading wildcard

The result:

![trailing wildcard](https://user-images.githubusercontent.com/106580846/204739256-51f63d41-e327-418d-bcb4-200df96b836a.png)

