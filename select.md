# Exercises

> Write out a generic `SELECT` statement.
```SQL
SELECT * from database WHERE id > 10;
```

> Create a fun way to remember the order of operations in a `SELECT` statement, such a mnemonic.
- The order of operations when constructing a SELECT query is: SELECT, FROM, and (optionally) WHERE. I've created the following mnemonic to remember the correct order:
  - S - Super
  - F - Fluffy
  - W - Waffles

> Given this `dogs` table, write queries to select the following pieces of data (intake teams typically guess the breed of shelter dogs, so the `breed` column may have multiple words. For example: "Labrador Collie mix):
- Display the name, gender and age of all dogs that are part Labrador.
```SQL
SELECT name, gender, age
FROM dogs
WHERE breed LIKE "%Labrador%";
```
- Display the ids of all dogs that are under 1 year old.
```SQL
SELECT id
FROM dogs
WHERE age < 1;
```
- Display the name and age of all dogs that are female and over 35 lbs.
```SQL
SELECT name, age
FROM dogs
WHERE gender = "female" AND weight > 35;
```
- Display all of the information about all dogs that are not Shepard mixes.
```SQL
SELECT *
FROM dogs
WHERE breed NOT LIKE "%Shepard%";
```
- Display the id, age, weight, and breed of all dogs that are either over 60 lbs. or Great Danes.
```SQL
SELECT id, age, weight, breed
FROM dogs
WHERE weight > 60 OR breed LIKE "%Great Dane%";
```

> Given this `cats` table, what records are returned from these queries?
```SQL
SELECT name, adoption_date FROM cats;
```
- Returns the name and adoption_date columns for every cat in the database.
```SQL
SELECT name, age FROM cats;
```
- Returns the name and age columns for every cat in the database.

> From the cats table, write queries to select the following pieces of data:
- Display all the information about all of the available cats.
```SQL
SELECT *
FROM cats;
```
- Display the name and sex of all cats who are 7 years old. 
```SQL
SELECT name, sex
FROM cats
WHERE age = 7;
```
- Find all of the names of the cats, so you don't choose duplicate names for new cats.
```SQL
SELECT names
FROM cats;
```

> List each comparison operator and explain why you would use it. Include a real world example of each.
- `<` is the less than operator. I might use it to select something like the first 20 users to join my web site by saying `SELECT * from users WHERE id < 21;`
- `>` is the greater than operator. I might use it to select all cats that are older than 1 year old by saying `SELECT * from cats WHERE age > 1;`
- `<=` is the less than or equal to operator. I might use it to select all guests who are able to eat from the kids menu by saying `SELECT name, is_kid FROM guests WHERE age <= 12;`
- `>=` is the greater than or equal to operator. I might use it to select all guests who are able to ride a specific roller coaster by saying `SELECT name FROM coaster_1 WHERE height >= 42;`
- `=` is the equals operator. I might use it to select all of the transactions by a specific user on my e-commerce site by saying `SELECT * FROM transactions WHERE user_id = 43243;`
- `!=` or `<>` are equivalent operators that mean 'does not equal'. I might use it to ensure I do not include query results from any deposits in my banking app by saying `SELECT * FROM checking_activity WHERE transaction_type != 'DEPOSIT';`
- `LIKE` is the operator used to find partial matches within strings. I might use it to display data for people whose last name contains the queried last name, including a potentially hyphenated version, by saying `SELECT * FROM family_tree WHERE last_name LIKE '%Gude%';`

> From the `cats` tables, what data is returned from these queries?
```SQL
SELECT name FROM cats WHERE gender = 'F';
```
- This query will return the names of all female cats.
```SQL
SELECT name FROM cats WHERE age <> 3;
```
- This query will return the names of all cats that aren't 3 years old.
```SQL
SELECT ID FROM cats WHERE name != 'Mushi' AND gender = 'M';
```
- This query will return the ID of all male cats who aren't named 'Mushi'.