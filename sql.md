> List the commands for adding, updating, and deleting data.
- INSERT INTO: Creates new data and inserts it into the table.
- UPDATE: Updates existing data in a table.
- DELETE: Deletes an entry from a table

> Explain the structure for each type of command.

> What are some of the data types that can be used in tables? Give a real-world example of each.
- money: can be used to store currencies, perhaps for prices
- int: can be used to store simple integers, like quantities in inventory
- text: can be a string of characters, potentially to hold a description for an item
- date: can be used to store a formatted date, potentially to store a sign-up date, or a customer's birthday

> Decide how to create a new table to hold a list of people invited to a wedding dinner. The table needs to have first and last names, whether they sent an RSVP, the number of guests they are bringing, and the number of meals (1 for adults, 1/2 for children).

```SQL
CREATE TABLE wedding_guests (
  first_name text,
  last_name text,
  rsvp boolean,
  guests int,
  meals numeric(5, 1)
);

ALTER TABLE wedding_guests ADD COLUMN thank_you boolean SET DEFAULT false;

ALTER TABLE wedding_guests DROP COLUMN meals;

ALTER TABLE wedding_guests ADD COLUMN table int;

DROP TABLE wedding_guests;
```

> Write a command to create a new table to hold the books in a library with the columns ISBN, title, author, genre, publishing-date, number of copies, and available copies.

```SQL
CREATE TABLE library (
  ISBN int,
  title text,
  author text,
  genre text,
  publishing_date date,
  total_copies int,
  available_copies int
);

INSERT INTO library (ISBN, title, author, genre, publishing_date, total_copies, available_copies)
VALUES
(0553103547, 'A Game of Thrones', 'Martin, George R. R.', 'Fantasy', 1996-08-01, 10, 1),
(9780062420701, 'To Kill a Mockingbird', 'Harper Lee', 'Southern Gothic', 1960-07-11, 10, 4),
(9780143111580, 'Dune', 'Frank Herbert', 'Science Fiction', 1965-08-01, 10, 7);

UPDATE library 
  SET available_copies=available_copies - 1 
WHERE ISBN = 9780062420701;

DELETE FROM library
WHERE ISBN = 0553103547;
```

> Write a command to make a new table to hold spacecrafts. Information should include id, name, year launched, country of origin, a brief description of mission, orbiting body, if it is currently operating, and its approximate miles from earth.

```SQL
CREATE table spacecrafts (
  id int,
  craft_name text,
  year_launched int,
  country text,
  description text,
  orbiting_body text,
  currently_operating boolean,
  miles_from_earth bigint
);

INSERT into spacecrafts (id, craft_name, year_launched, country, description, orbiting_body, currently_operating, miles_from_earth)
VALUES
(10321, 'Voyager 1', 1977, 'United States', 'Space probe sent to study the outer solar system', null, TRUE, 13229000000),
(25008, 'Cassini-Huygens', 1997, 'Multinational', 'Space probe sent to study Saturn', 'Saturn', FALSE, 1000000000),
(36576, 'Akatsuki', 2010, 'Japan', 'Space probe sent to study Venus', 'Venus', TRUE, 162000000);

DELETE FROM spacecrafts
  WHERE id = 36576;

UPDATE spacecrafts
  SET currently_operating = FALSE
  WHERE id = 10321;
```

> Write a command to create a new table to hold the emails in your inbox. This table should include an id, the subject line, the sender, any additional recipients, the body of the email, the timestamp, whether or not you've read the email, and the id of the email chain it's in.

```SQL
CREATE table email (
  message_id int,
  subject text,
  sender text,
  copied text[],
  body text,
  time_sent timestamptz,
  read boolean,
  message_chain_id int
);

INSERT into email
VALUES
(1, 'Welcome!', 'greg.jones@company.com', 'maria.jenkins@company.com', 'Welcome to the company Josh!', 2018-10-13 13:31:21-07, TRUE, 1),
(2, 'Re: Welcome!', 'maria.jenkins@company.com', 'Yes, welcome!', 2018-10-13 13:45:32-07, FALSE, 1),
(3, 'Get to Work', 'james.smithington@company.com', 'Enough chit-chat, get to work!', );

DELETE FROM email WHERE message_id = 2;

UPDATE email SET read = FALSE WHERE message_id = 1;
```