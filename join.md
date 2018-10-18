## Exercises
> How do you find related data held in two separate data tables?
- By using the JOIN statement. You would structure the query like this: `SELECT db1.name, db2.name FROM db1 JOIN db2 ON db1.product_id = db2.id;`

> Explain, in your own words, the difference between `INNER JOIN`, `LEFT OUTER JOIN`, and `RIGHT OUTER JOIN`. Give a real world example for each.
- `INNER JOIN` outputs only the data specified in the query. If I made a query like `SELECT user.name, product.name FROM user JOIN product ON user.product_id = product.id;`, I would be implicitly calling for an inner join. This join would specifically **only** list the user.name and product.name columns that were specified where `user.product_id` was the same as `product.id`.
- `LEFT OUTER JOIN` outputs the same data as `INNER JOIN` does, but also outputs a row for every row in the first table that does not satisfy the `JOIN` condition. For example, the following would output the full list of students that are enrolled in this specific class, and additionally will output students that are not, with a `class.name` value of `null`:
```SQL
SELECT student.name, class.name
FROM student
LEFT OUTER JOIN classes
ON student.class_id = class.id;
```
- `RIGHT OUTER JOIN` outputs the same data as `INNER JOIN` does, but also outputs a row for every row in the second table that does not satisfy the `JOIN` condition. For example, the following would output a full list of students that are enrolled in this specific class, and additionally will output classes that do not have any students enrolled, with a `student.name` value of `null`.
```SQL
SELECT student.name, class.name
FROM student
RIGHT OUTER JOIN classes
ON student.class_id = class.id;
```

> Define primary key and foreign key. Give a real world example for each.
- A primary key is the unique identifier for a tuple. A foreign key is an identifier that is unique to another table, but does not need to be unique within the current table. For example, for the following query, the `student` table might have a unique identifier held within the `id` column, which would be the primary key for each tuple within the `student` table. However, the `student` table may also contain the `class_id` column to indicate the class the student is currently enrolled in. This is the foreign key. While this `class_id` attribute may match the data stored within the `id` column of the `class` table, it is foreign to the `student` table.
```SQL
SELECT student.name, class.name
FROM student
JOIN class
ON student.class_id = class.id;
```

> Define aliasing.
- Aliasing is the technique of creating shorter variable names to replace the table name in a query.

> Change this query so that you are using aliasing.

```SQL
SELECT professor.name, compensation.salary, compensation.vacation_days
FROM professor
JOIN compensation
ON professor.id = compensation.professor_id;
```
would be changed to:

```SQL
SELECT p.name, c.salary, c.vacation_days
FROM professor AS p
JOIN compensation AS c
ON p.id = c.professor_id;
```

> Why would you use a natural join? Give a real world example.
- You would use a natural join as a shorthand for only returning the columns that have the same names in all of the tables you are querying. For example, if I only wanted to return the name of a user and the name of the product they bought, I might use the following query:

```SQL
SELECT *
FROM users
NATURAL JOIN products;
```

> Using the given Employee schema and data, write queries to find the following information.

- List all employees and all shifts.

```SQL
SELECT *
FROM employees, shifts;
```

> Using the given adoption schema and data, please write queries to retrieve the following information and include the results.

---

- Create a list of all volunteers. If the volunteer is fostering a dog, include each dog as well.

```SQL
SELECT v.id, v.first_name, v.last_name, d.name
FROM volunteers AS v
LEFT OUTER JOIN dogs AS d
ON v.foster_dog_id = d.id;
```

Returns

| id  | first_name | last_name  | name      |
| --- | ---------- | ---------- | --------- |
| 2   | Rubeus     | Hagrid     | Munchkin  |
| 5   | Marjorie   | Dursley    | Marmaduke |
| 4   | Sirius     | Black      |           |
| 3   | Remus      | Lupin      |           |
| 1   | Albus      | Dumbledore |           |

---

- The cat's name, adopter's name, and adopted date for each cat adopted within the past month to be displayed as part of the "Happy Tail" social media promotion which posts recent successful adoptions.

```SQL
SELECT cats.name, adopters.first_name, adopters.last_name, cat_adoptions.date
FROM cat_adoptions
JOIN cats
ON cats.id = cat_adoptions.cat_id
JOIN adopters
ON adopters.id = cat_adoptions.adopter_id
WHERE CURRENT_DATE - INTERVAL '30 DAYS' < cat_adoptions.date;
```

Returns

| name     | first_name | last_name | date                     |
| -------- | ---------- | --------- | ------------------------ |
| Mushi    | Arabella   | Figg      | 2018-09-28T00:00:00.000Z |
| Victoire | Argus      | Filch     | 2018-10-03T00:00:00.000Z |

---

- Create a list of adopters who have not yet chosen a dog to adopt.

```SQL
SELECT a.first_name, a.last_name
FROM adopters AS a
LEFT OUTER JOIN dog_adoptions AS d
ON a.id = d.adopter_id
WHERE d.adopter_id IS NULL;
```

Returns

| first_name | last_name |
| ---------- | --------- |
| Hermione   | Granger   |
| Arabella   | Figg      |

---
- Lists of all cats and all dogs who have not been adopted.

```SQL
SELECT c.name
FROM cats AS c
LEFT OUTER JOIN cat_adoptions AS a
ON c.id = a.cat_id
WHERE a.date IS NULL;

SELECT d.name
FROM dogs AS d
LEFT OUTER JOIN dog_adoptions AS a
ON d.id = a.dog_id
WHERE a.date IS NULL;
```

Returns

| name     |
| -------- |
| Seashell |
| Nala     |

And

| name      |
| --------- |
| Munchkin  |
| Boujee    |
| Lassie    |
| Marley    |
| Marmaduke |

---

- The name of the person who adopted Rosco.

```SQL
SELECT a.first_name, a.last_name, d.name
FROM dogs AS d
JOIN dog_adoptions
ON d.id = dog_adoptions.dog_id
JOIN adopters AS a
ON a.id = dog_adoptions.adopter_id;
```

Returns

| first_name | last_name | name  |
| ---------- | --------- | ----- |
| Argus      | Filch     | Rosco |

---

> Using the given Library schema and data, write queries applying the following scenarios and include the results.

---

- To determine if the library should buy more copies of a given book, please provide the names and position, in order, of all the patrons with a hold (request for a book with all copies checked out) on "Advanced Potion-Making".

```SQL
SELECT p.name, h.rank
FROM patrons AS p
JOIN holds AS h
ON p.id = h.patron_id AND h.isbn = '9136884926'
ORDER BY h.rank ASC;
```

Returns

| name           | rank |
| -------------- | ---- |
| Terry Boot     | 1    |
| Cedric Diggory | 2    |

---

- List all of the library patrons. If they have one or more books checked out, list the books with the patrons.

```SQL
SELECT p.name, b.title
FROM patrons AS p
LEFT OUTER JOIN transactions AS t
ON p.id = t.patron_id
  AND (t.checked_out_date IS NOT NULL AND t.checked_in_date IS NULL)
LEFT OUTER JOIN books AS b
ON t.isbn = b.isbn
ORDER BY p.name ASC;
```

Returns

| name             | title                                   |
| ---------------- | --------------------------------------- |
| Cedric Diggory   | Fantastic Beasts and Where to Find Them |
| Cho Chang        |                                         |
| Hermione Granger |                                         |
| Padma Patil      |                                         |
| Terry Boot       | Advanced Potion-Making                  |

---