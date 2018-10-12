####Questions
> What data types do each of these values represent?
- "A Clockwork Orange": TEXT
- 42: INT
- 09/02/1945: DATE
- 98.7: FLOAT
- $15.99: Not a real type, would have to either store 15.99 as CURRENCY or MONEY, or "15.99" as TEXT

> Explain when a database would be used. Explain when a text file would be used.
- You would need a database when you needed to store a large amount of data that should persist after the program is done running. A text file could be used if you needed to store a known small amount of data, but would not be very good if you needed the storage space to be extensible to an unknown degree in the future.

> Describe one difference between SQL and other languages.
- SQL is a declarative language vs. a procedural language.

> Explain how the pieces of a database system fit together at a high level.
- The pieces of a database function like a table. You are able to query the database to select the data from specified columns in a specified table based on the information you give it. If you wanted to get the data from the 'Name' and 'Email' columns for a specific user ID, you can do that.

> Explain the meaning of table, row, column, and value.
- A table is a collection of rows and columns that form cells at the intersections of each row/column. Each cell contains a value.
- A row is a horizontal line of data.
- A column is a vertical line of data. Each column usually has a 'head' that contains the name of the column. Each cell in a column usually holds the same type of data, such as a name, data, etc.
- A value is the data that is stored at a specific cell in a table. It can be one of many data types, such as text, integer, date, float, etc.

> List three data types that can be used in a table.
- Integer
- Float
- Date

> Given this payments table, provide an English description of the following queries and include their results:

```SQL
SELECT date, amount
FROM payments;

SELECT amount
FROM payments
WHERE amount > 500;

SELECT *
FROM payments
WHERE payee = 'Mega Foods';
```
- I'm looking for all the dates and amounts from the payments table.
  - This would return all of the dates and amounts in the entire payments table.

- I'm looking for the amounts that are more than 500.
  - This would return all of the amounts in the payments table where the value of the amount is greater than 500.

- I'm looking for all of the data for the payee Mega Foods.
  - This would return all pieces of data where the payee was Mega Foods.

> Given this `users` table, write SQL queries using the following criteria, and include the output: 

```SQL
SELECT email, signup
FROM users
WHERE user = 'DeAndre Data';

SELECT userid
FROM users
WHERE email = 'aleesia.algorithm@uw.edu'

SELECT *
FROM users
WHERE userid = 4;
```