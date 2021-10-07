---
layout:     post
title:      SQL Study Notes
date:       2021-10-07
summary:   SQL Study Notes from Grok Learning
categories: SQL
---

# Introduction to SQL

## Introduction

### SQL Introduction

The standard query language for database systems is SQL - which stands for *Structured Query Language*.

SQL is a *declarative language* which means that you use it to describe *what* data you are interested in, but not *how* it should be retrieved. The database system uses a variety of algorithms internally to produce the query result. With declarative languages such as SQL, you do not need to worry about these implementation details.

**Your First Query**

Run the below SQL query by clicking the button in the top right corner above it:

```sql
SELECT studentId, name
  FROM Student;
```

### Relations, Attributes, Tuples

SQL is used to perform *queries* on a *relational database*, and is executed by the software which manages the database, called the *Database Management System* (DBMS). Some examples of DBMSs include [PostgreSQL](http://www.postgresql.org/), [Oracle](http://www.oracle.com/au/index.html), and [MySQL](https://www.mysql.com/). We will be using *PostgreSQL*.

A relational database contains *relations* (or tables), consisting of *attributes* (columns) and *tuples* (rows). The terms for "relation" and "table" are sometimes used interchangeably, however tables are the concrete representation of relations (an abstract concept).

![Relation, attributes, and tuples represented as a table, columns, and rows.](https://groklearning-cdn.com/modules/wKqwCpgXEAMATxkN3RhnGS/Relational_database_terms.svg)

**Note**

Even though we typically visualise a relational database with tables, keep in mind that, in contrast to tables, there is no order defined within a relation - it is a set, not a list.

### Schemas

As you saw, our example `Student` table has these columns/attributes: `studentId`, `name`, `address`, and `age`.

A database's structure, including tables and attributes, is called its *schema*. Schemas can be represented diagrammatically:

![Example Schema ](https://groklearning-cdn.com/modules/hvgkkUtkY4imFvsqwhjgVk/exampledb.png)

**Primary Keys**

Each row in a table can have a unique identifier (e.g. `studentId`). The attributes which make up this unique identifier are called the table's *primary key*, shown underlined in the above diagram.

**Querying a Table**

To query the values of some attributes of a table, we use `SELECT` queries. The example below lists all students by `studentId`:

```sql
SELECT studentId
  FROM Student;
```

### Names and Ages

Your task is to write an SQL query. Your query must output the `name` and `age` of all students in the `Student` table.

![Example Schema ](https://groklearning-cdn.com/modules/hvgkkUtkY4imFvsqwhjgVk/exampledb.png)

```sql
select name, age
from Student
```

## SQL Syntax

### The `*` Wildcard

The `*` (asterisk) wildcard is a useful shortcut when writing SQL queries. You can use the `*` wildcard in the `SELECT` clause to refer to a complete tuple of a table with all its attributes. For example:

```sql
SELECT *
  FROM Student;
```

This query retrieves the complete rows from the `Student` table with all available attributes. This is especially handy if you do not know the table's exact schema, or if the schema is very complex (to save you listing a lot of attributes after `SELECT`).

### SQL Syntax

Check by running these two queries if they are the same:

```sql
SELECT * FROM Student;
```

```sql
select
  *
from
  student;
```

From this example you should be able to see:

-   You can have as many spaces, tabs or newlines in your query as you like. Use this to format the query for best readability.
-   SQL is **case-insensitive**: e.g. it doesn't matter whether you write `SELECT` or `select`. It is convention to use capitalized keywords to make the syntax clear.
-   SQL queries always end with a semicolon (`;`).

### Listing All Students

Your task is to write an SQL query. Your query must output all entries in the `Student` table and all available `Student` attributes.

![Example Schema ](https://groklearning-cdn.com/modules/hvgkkUtkY4imFvsqwhjgVk/exampledb.png)

```sql
select *
from Student
```

## Strings and the WHERE Clause

### The `WHERE` Clause

The following query retrieves the name of the student with student ID `307088592`:

```sql
SELECT name
  FROM Student
 WHERE studentId = 307088592;
```

Each part of an SQL query is called a *clause*. So far we have seen the `SELECT` and `FROM` clauses. The `WHERE` clause limits a query to operate on specific rows which match given criteria (some filter condition).

So in above's example, we list only those students from the `Student` table where the corresponding `studentID` value equals `307088592`.

### Strings in SQL

Run this query which compares two strings:

```sql
SELECT 'Text' = 'text';
```

It returns `f` (for `false`) meaning the two texts are different.

There are two important syntax rules when dealing with text strings in SQL:

-   Strings **must** be enclosed in **single quotes** (`'`). For example: `... WHERE name = 'Michael'`
    Double quotes (`"`) have a different meaning in SQL.
-   Text data inside a database is **case-sensitive**. This means that if you are querying a string attribute, you must search for exactly the same text as stored in the database.

### Results for INFO2120

Your task is to write an SQL query to output the result list for `'INFO2120'`, using data in the `Enrolled` table. Your query's result should have two columns:

1.  the `studentId` of each student who took INFO2120 at any point in time (ignore which year or semester the subject was taught);
2.  the `grade` that student received for INFO2120.

```sql
select studentId, grade
from Enrolled
where uosCode = 'INFO2120';
```

## Aggregates in SQL

### The `COUNT()` Aggregate Function

The following query counts the total number of students stored in the `Student` table:

```sql
SELECT COUNT(*)
  FROM Student;
```

It is often useful to perform an operation over a collection of results (counting, summing, averaging, etc.). In SQL these operations are handled by *aggregate functions* such as `COUNT()`.

Using `COUNT(*)` counts the total number of rows in the table, regardless of any `NULL` values. If you specify a column name instead of `*` as the parameter for `COUNT()`, then only *non-*`NULL` values in that column will be counted. For example:

```sql
SELECT COUNT(grade)
  FROM Enrolled;
```

This last example counts all enrolments where there is a known grade, ignoring any rows with a `NULL` value for the grade.

### Further Aggregate Functions

There are many more aggregate functions available in a DBMS. Some others available in PostgreSQL include:

-   `MAX(`*expression*`)`

    Maximum value of *expression* across all input values: `SELECT MAX(age) FROM Student;`

-   `MIN(`*expression*`)`

    Minimum value of *expression* across all input values: `SELECT MIN(age) FROM Student;`

-   `AVG(`*expression*`)`

    Average (arithmetic mean) of all input values: `SELECT AVG(age) FROM Student;`

-   `SUM(`*expression*`)`

    Sum of *expression* across all input values: `SELECT SUM(age) FROM Student;`

### How many UoS are available?

Write an SQL query that determines how many units of study are listed in the database.

![Example Schema ](https://groklearning-cdn.com/modules/hvgkkUtkY4imFvsqwhjgVk/exampledb.png)

```sql
select count(*)
from UnitOfStudy;
```

### Average Student Age

Write an SQL query that determines the average age of all students.

![Example Schema ](https://groklearning-cdn.com/modules/hvgkkUtkY4imFvsqwhjgVk/exampledb.png)

```sql
select avg(age)
from Student
```

# FilmDB Example Schema

## FilmDB Example Schema

### A Film Database

Our example schema for the SQL problems of the coming weeks is the film database of a film database. It consists of **seven tables** that contain data about films, actors who play in those films, how films are categorised and in which languages films are playing:

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

### FilmDB Table Descriptions

The meanings of the individual tables are:

-   `Film`

    The central table with the core facts about the available films; includes rental rates and replacement costs.

-   `Actor`

    A table about all actors (names and nationality) which play in the films.

-   `Category`

    A list of film categories.

-   `Language`

    A list of languages that are spoken in the films.

-   `Country`

    A list of countries from which the actors are from.

-   `Film_Actor`

    A film as typically multiple actors, while an actor is of course allowed to occur in more than one film. This is a *many-to-many* relationship which requires an own table, the `Film_Actor` table.

-   `Film_Category`

    Implements another *many-to-many* relationship. A film can have more than one category, as well as there can be more than one film per category.

### Listing all Countries

Your task is to write an SQL query to list all countries that are stored in the database. Your query should return all available attributes of the `Country` table.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

```sql
select *
from Country
```

### How many Films?

Your task is to write an SQL query that outputs how many films are stored in the database.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(*)
from Film
```

### Film 271

Using a `WHERE` clause, the `SELECT` statement of SQL also allows to restrict a query to just those tuples that fulfuil a filter condition.

Write an SQL query that shows all details of the `Film` whose `film_id` is `271`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select *
from Film
where film_id = '271'
```

### Flash Wars Release Year

In SQL, we are not restricted to numeric values, but also can query with strings. Just remember that strings have to be enclosed in single quotes in SQL, and that string comparisons are case-sensitive.

Write an SQL query that finds which year the `Film` called `'FLASH WARS'` was released.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select release_year
from Film
where title = 'FLASH WARS'
```

### Listing Australian Actors

Write an SQL query to list all Australian actors stored in the database. Your query should return two columns: the `first_name` and `last_name` of the person.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select first_name, last_name
from Actor
where nationality = 'AU'
```

# Introduction to DML/DDL SQL

## SQL DML Commands

### SQL's Data Manipulation Language

Let's start by looking at data modifications. SQL offers the following commands to manipulate the data in an existing database instance:

-   `INSERT`

    Used to insert a new row into a table.

-   `DELETE`

    Used to delete zero or more rows from a table.

-   `UPDATE`

    Used to update the content of zero or more rows in a table.

### The `INSERT` Command

The `INSERT` command adds a new row to the specified table. The general syntax is:

```sql
INSERT INTO <tablename>
     VALUES (...);
```

If you do not specify the schema of *<tablename>*, then the values have to be listed in exactly the same order as specified in the database schema.

**Example:** The following adds `'Dutch'` as fourth language to the `Language` table.

```sql
INSERT INTO Language
     VALUES (4, 'Dutch');
SELECT * FROM Language;
```

Play around with this statement and see what happens if you do specify the values in the wrong order: `VALUES ('Dutch', 4)`

If in doubt, you can always explicitly list the attributes, which you try to insert, as part of the `INSERT` statement:

```sql
INSERT INTO Language(name, language_id)
     VALUES ('Dutch', 4);
```

With PostgreSQL, the `INSERT` statement returns two values: the first one is an internal id (typically 0), the second is the number of rows inserted (should be 1 in our examples).

Tip: You can also use sub-queries (`SELECT ...`) inside the `VALUES` list to retrieve a value from the current database instance which you would like to use in your new row. This is very handy if you want to link to existing data as part of a *foreign key* value.

### The `UPDATE` Command

The `UPDATE` command modifies the data in one or more rows of the specified table. The general syntax is:

```sql
UPDATE <tablename>
   SET <expression>
 WHERE <condition>;
```

where

-   `<tablename>` refers to an existing table name in the database schema.
-   `<expression>` is a comma-separated list of `attr = <value>` expressions that compute a new value for one or more attributes based on constants and other attribute values. It can be a complex computation or even include sub-queries with `SELECT`.
-   `<condition>` refers to a filtering condition, which must be true for such tuples that shall get updated. Basically, you can use anything here which you can use in the `WHERE` clause of a SQL query too.

**Example:** Let's update the country name of Switzerland, in case you ever wondered why the Swiss country code is CH.

```sql
SELECT * FROM Country;
UPDATE Country
   SET name = 'Confoederatio Helvetica'
 WHERE short_code = 'CH';
SELECT * FROM Country;
```

```
+------------+------------+-------------+
| country_id | short_code |    name     |
+------------+------------+-------------+
|          1 | AU         | Australia   |
|          2 | AT         | Austria     |
|          3 | BR         | Brazil      |
|          4 | CA         | Canada      |
|          5 | CH         | Switzerland |
+------------+------------+-------------+
(5 rows)

UPDATE 1
+------------+------------+-------------------------+
| country_id | short_code |          name           |
+------------+------------+-------------------------+
|          1 | AU         | Australia               |
|          2 | AT         | Austria                 |
|          3 | BR         | Brazil                  |
|          4 | CA         | Canada                  |
|          5 | CH         | Confoederatio Helvetica |
+------------+------------+-------------------------+
(5 rows)
```

Notice how the `UPDATE` command returns the number of rows being affected.

**Careful!**

If you omit the `WHERE` clause, then **all** rows in *tablename* are updated!

### The `DELETE` Command

The `DELETE` command removes one or more rows from the specified table. The general syntax is:

```sql
DELETE FROM <tablename>
      WHERE <condition>;
```

This deletes all tuples from the table `<tablename>` where the boolean expression `<condition>` evaluates to true.

**Example:** Let's delete German from the language table.

```sql
SELECT * FROM Language;
DELETE FROM Language WHERE name = 'German';
SELECT * FROM Language;
```

```
+-------------+----------------------+
| language_id |         name         |
+-------------+----------------------+
|           1 | English              |
|           2 | French               |
|           3 | German               |
+-------------+----------------------+
(3 rows)

DELETE 1
+-------------+----------------------+
| language_id |         name         |
+-------------+----------------------+
|           1 | English              |
|           2 | French               |
+-------------+----------------------+
(2 rows)
```

Similar to the other DML commands, `DELETE` returns the number of rows being deleted.

**Careful!**

If you omit the `WHERE` clause, then **all** tuples in *tablename* are deleted.

### A New Actor

Add a new actor into the `Actor` table for `'Arnold Schwarzenegger'` with ID `4711`. Arnold is born in Austria.

**Hint**

An `Actor`'s `nationality` must be an *[ISO 3166-1-alpha-2](http://www.iso.org/iso/english_country_names_and_code_elements)* `short_code` from the `Country` table.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
insert into Actor
values(4711, 'Arnold', 'Schwarzenegger', 'AT')
```

### Updating a Film

Update the database so that `rental_rate` of the `Film` `'ANGELS LIFE'` is increased by 20%.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
update Film
set rental_rate = rental_rate * 1.2
where title = 'ANGELS LIFE'
```

## SQL DDL Commands

### Creating Tables with `CREATE TABLE`

The `CREATE TABLE` command extends the current database schema with a new table. The general syntax is:

```sql
CREATE TABLE <tablename> (
  <attr1> <TYPE1>,
  <attr2> <TYPE2>,
  ...
);
```

Each attribute must have a specific *domain type*. The most common types are:

-   `SMALLINT` — 2 byte numeric integer value
-   `INTEGER` — 4 byte numeric integer value
-   `FLOAT` — 8 byte floating point value
-   `CHAR(n)` — fixed-length string of `n` characters
-   `VARCHAR(n)` — variable-length string of `0` to `n` characters

**Example:** The following creates a new `Continent` table and adds `'Asia'` as first entry.

```sql
CREATE TABLE Continent (
   id   INTEGER,
   name VARCHAR(50)
);
INSERT INTO Continent VALUES (1, 'Asia');
SELECT * FROM Continent;
```

### Consistency Constraints

You can add *consistency constraints* as part of the schema when using `CREATE TABLE`. The most common consistency constraints are:

-   `PRIMARY KEY`

    Declares an attribute (or several) as *the* unique identifier for rows in the table.

-   `NOT NULL`

    Forces every row in the table to have a value for this attribute.

-   `DEFAULT <default_value>`

    Specify a default value for an attribute.

**Example:** The following ensures every `Continent` can occur only once and that a name must be given (`NOT NULL` contraint).

```sql
CREATE TABLE Continent (
   id   INTEGER     PRIMARY KEY,
   name VARCHAR(50) NOT NULL
);
INSERT INTO Continent VALUES (1, 'Asia');
SELECT * FROM Continent;
```

To see how these constraints work, try to duplicate the `INSERT` statement, or try to leave out the name of a continent, then press the play button again.

### Foreign Key Constraints

A *foreign key constraint* specifies that values stored for an attribute (or set of attributes) in one table must match values stored in a different table.

**Example:** The following creates a `Mountain` table that also stores in which continent a mountain lies.

```sql
CREATE TABLE Continent (
   id   INTEGER     PRIMARY KEY,
   name VARCHAR(50) NOT NULL
);
CREATE TABLE Mountain (
   name      VARCHAR(50) PRIMARY KEY,
   continent INTEGER     REFERENCES Continent(id)
);
INSERT INTO Continent VALUES (1, 'Asia');
INSERT INTO Mountain  VALUES ('Mount Everest', 1);
```

In the above example, `continent` is a *foreign key* referencing the `Continent` table. This means every value stored for `continent` in `Mountain` *must* also exist in the `Continent` table.
Explore this by modifying the second `INSERT` statements in above's example with a non-existing continent value.

```sql
CREATE TABLE Continent (
   id   INTEGER     PRIMARY KEY,
   name VARCHAR(50) NOT NULL
);
CREATE TABLE Mountain (
   name      VARCHAR(50) PRIMARY KEY,
   continent INTEGER     REFERENCES Continent(id)
);
INSERT INTO Continent VALUES (1, 'Asia');
INSERT INTO Mountain  VALUES ('Mount Everest', 2);
```

```
CREATE TABLE
CREATE TABLE
INSERT 0 1
psql:query.sql:10: ERROR:  insert or update on table "mountain" violates foreign key constraint "mountain_continent_fkey"
DETAIL:  Key (continent)=(2) is not present in table "continent".
```

Note: The domain type of the foreign key must match the domain type of the referenced attribute. And we only can reference attributes which are at least a *candidate key* - this means they are declared either `PRIMARY KEY` or `UNIQUE`.

**Example 2:** We can also have several foreign keys in the same table to different target tables. Here is the `CREATE TABLE` DDL statement for the `Film_Actor` table:

```sql
CREATE TABLE Film_Actor (
   actor_id INTEGER REFERENCES Actor(actor_id),
   film_id  INTEGER REFERENCES Film(film_id),
   PRIMARY KEY (actor_id, film_id)
);
```

In the above example, `actor_id` and `film_id` are *foreign keys* referencing the `Film` and `Actor` tables, respectively. This means every value stored for `actor_id` in `Film_Actor` *must* also exist in the `Actor` table, and similarly for `film_id`.

The general syntax is:

```sql
CREATE TABLE <tablename> (
  <attr1> ... REFERENCES <other_table>(<other_attr>),
  ...
);
```

### Deleting tables with `DROP TABLE`

Existing tables can be removed from a schema with the `DROP TABLE` command. For example:

```sql
DROP TABLE <tablename>;
```

**Careful**

All data stored in the table is lost when using `DROP TABLE`!

### Creating Tables

Provide the SQL statements that create two tables for the following scenario:

-   Each `Person` is identified by a unique driver's license number (`license`) and has a `name` (a string of max 50 characters).
-   A `Car` has a registration number (`regno` - a string of always 6 characters) and a `model` (e.g. `'Porsche 911'` - we allow 30 characters for the model name).
-   Each car has at most one `Person` as its `driver` - or none.
-   We need to know the name of each `Person`.
-   The model of a `Car` can be unknown.

Example data `INSERT` statements for these new tables:

```sql
INSERT INTO Person
     VALUES (4711, 'Hugh Jackman');

INSERT INTO Car
     VALUES ('ABC123', 'Porsche 911', 4711);
```

``` sql
CREATE TABLE Person (
    license INTEGER PRIMARY KEY,
    name VARCHAR(50) NOT NULL
);
CREATE TABLE Car (
    regno CHAR(6) PRIMARY KEY,
    model VARCHAR(30),
    driver INTEGER REFERENCES Person(license)
);

INSERT INTO Person
     VALUES (4711, 'Hugh Jackman');

INSERT INTO Car
     VALUES ('ABC123', 'Porsche 911', 4711);
```

### Storing Film Studios

Write an SQL DDL statement that extends the DVD Shop database with an additional table for film studios, called `Studio`. Each `Studio` must have:

1.  a unique `studio_id` identifier (integer)
2.  a `name` of up-to 50 characters length which must be given
3.  an `address` (up-to 100 chars long)
4.  a specific `country` (store the short code)

Make sure that the studio's `country` references the `Country` table. Both `country` and `name` must always be stored for a `Studio`, but the `address` is optional.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
CREATE TABLE Studio (
    studio_id INTEGER PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    address VARCHAR(100),
    country CHAR(2) REFERENCES Country(short_code) NOT NULL
);
```

# Range Queries and Logical Connectives

## Range Queries

### Query Types in SQL

Depending on the kind of filter condition in the `WHERE` clause, we can distinguish two general kinds of queries:

-   *point queries*

    search for individual database entries, typically specified with an equality (`=`) condition. Example:

    ```sql
    SELECT *
      FROM Student
     WHERE studentId = 305422153;
    ```

-   *range queries*

    select multiple rows in a defined value range. Example:

    ```sql
    SELECT *
      FROM Student
     WHERE age < 25;
    ```

### Comparison Operators

Here is a list of the main comparison operators in SQL which are useful for formulating `WHERE` filter conditions:

| Operator  | Meaning                                 | Example                       |
| :-------- | :-------------------------------------- | :---------------------------- |
| =         | equal to                                | `WHERE age = 20`              |
| >         | greater than                            | `WHERE age > 20`              |
| >=        | greater than or equal                   | `WHERE age >= 20`             |
| <         | smaller than                            | `WHERE age < 25`              |
| <=        | smaller than or equal                   | `WHERE age <= 25`             |
| `BETWEEN` | between start and end value (inclusive) | `WHERE age BETWEEN 20 and 25` |
| `IN`      | set of valid values                     | `WHERE age IN (20,21,22)`     |

### Range Queries

A common usage pattern for SQL queries are *range queries* which select a range of data from the input set based on same range expression: A `WHERE` clause that selects multiple rows with (one or more) attribute(s) whose value lies in a certain value range.

Let's have a look at an example of a range query. The following query selects all student entries with a `age` in the range of 20 to 25:

```sql
SELECT *
  FROM Student
 WHERE age >= 20 AND age <= 25
```

### Range Queries with `BETWEEN`

Range queries with a known upper and lower bound can be conveniently expressed using the `BETWEEN` operator.

**Example 1:** The same query than on the previous slide which is looking for students in the age range of 20 to 25.

```sql
SELECT *
  FROM Student
 WHERE age BETWEEN 20 and 25;
```

`BETWEEN x AND y` selects all tuples that have corresponding comparison values between `x` and `y` (inclusive). It specifies a closed value interval where both limits are included.

**Example 2:** `BETWEEN` comparisons also work for string values.

```sql
SELECT *
  FROM Enrolled
 WHERE grade BETWEEN 'CR' and 'D';
```

### Range Queries with `IN`

To check for several discrete and not necessarily consecutive values, the `IN` comparison operator helps.

**Example 1:** Because grade values are not in alphabetical order, the last query from the previous slide is better expressed as follows.

```sql
SELECT *
  FROM Enrolled
 WHERE grade IN ('CR', 'D', 'HD');
```

The `IN` comparison operator is a test for value-set membership: You list in the brackets after the `IN` keyword all allowed values, which the query should check for. A tuple is then shown in the result if its comparison attribute has a value which is part of this set of known values.

**Example 2:** Find any student whose age is *either* 20 *or* 25.

```sql
SELECT *
  FROM Student
 WHERE age IN (20, 25)
```

```
+-----------+-----------------+---------+-----+
| studentid |      name       | address | age |
+-----------+-----------------+---------+-----+
| 305678453 | Pauline Winters | Bondi   |  20 |
+-----------+-----------------+---------+-----+
(1 row)
```

**Note**

Notice the difference between the `BETWEEN` and `IN` queries:

```sql
SELECT *
  FROM Student
 WHERE age BETWEEN 20 and 25;
```

```
+-----------+-----------------+----------+-----+
| studentid |      name       | address  | age |
+-----------+-----------------+----------+-----+
| 305422153 | Sally Waters    | Coogee   |  22 |
| 305678453 | Pauline Winters | Bondi    |  20 |
| 309145324 | Victoria Tan    | Maroubra |  23 |
+-----------+-----------------+----------+-----+
(3 rows)
```

While this `BETWEEN` query searches for all students with an age in the range of 20 to 25, the `IN` query in Example 2 explicitly tests for just two ages: 20 and 25. While the former query finds also students of age 22 and 23, the latter shows only one student of age 20 because there is no student in the example data set with age 25.

### Film Shop Database Refresher

Last week, in Grok we started querying an example DVD Shop Film database. Here a brief reminder on its schema: It consists of **seven tables** that contain data about films, actors who play in those films, how films are categorised and in which languages films are playing:

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

### Long Films

Write an SQL query that shows how many films run for *longer* than 3 hours.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

```sql
select count(film_id)
from Film
where length > 3 * 60;
```

### 90s Films

Your task is to write an SQL query that lists all movies released in the period 1990 to 1999 (inclusive). Your query should return the following columns:

1.  `title`,
2.  `release_year`, and
3.  `description` of the film.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select title, release_year, description
from Film
where release_year between 1990 and 1999
```

## Logical Conjunctions and Disjunctions

### Logical Conjunctions with `AND`

So far, we only used single filter conditions in our SQL query. SQL is however much more flexible and allows us to specify more complex, compound filter conditions using logical connectives. The most common one is the `AND` operator which defines a [logical conjunction](https://en.wikipedia.org/wiki/Logical_conjunction). It allows to combine two or more filter conditions together so that a tuple will appear in the result if and only if *all* specified conditions are true.

**Example:**

```sql
SELECT *
  FROM Student
 WHERE age = 19 AND address = 'Newtown';
```

The above example finds us all students who are both 19 *and* who live in Newtown.

### Logical Disjunctions with `OR`

Filter conditions can also be build using *logical disjunctions*. In SQL, [logical disjunctions](https://en.wikipedia.org/wiki/Logical_disjunction) are expressed with the `OR` operator. This allows to combine two or more filter conditions together where *any one* of them must be true for a tuple to be in the result.

**Example:** The following SQL query finds all students who *either* are 19 *or* who live in Newtown.

```sql
SELECT *
  FROM Student
 WHERE age = 19 OR address = 'Newtown';
```

```
+-----------+--------------+------------+-----+
| studentid |     name     |  address   | age |
+-----------+--------------+------------+-----+
| 307088592 | John Smith   | Newtown    |  19 |
| 316424328 | Matthew Long | Camperdown |  19 |
+-----------+--------------+------------+-----+
(2 rows)
```

See how the result differs from our `AND` query from the previous slide:

```sql
SELECT *
  FROM Student
 WHERE age = 19 AND address = 'Newtown';
```

```
+-----------+------------+---------+-----+
| studentid |    name    | address | age |
+-----------+------------+---------+-----+
| 307088592 | John Smith | Newtown |  19 |
+-----------+------------+---------+-----+
(1 row)
```

### Cheap Rentals

Write an SQL query that lists all PG-rated movies that can be rented for *less* than 1 dollar. Your query should return the following three columns:

1.  the film `title`,
2.  the `release_year` of the film, and
3.  the `rental_rate` of the film.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

```sql
select title, release_year, rental_rate
from Film
where rating = 'PG' and rental_rate < 1
```

### Multiple Filter Conditions

For a filter condition at the `WHERE` clause, you can combine multiple conditions using conjunctions (`AND`) and disjunctions (`OR`).

**Example 1:** Multiple conjunctions.

```sql
SELECT uosCode, grade
  FROM Enrolled
 WHERE studentId = 305678453
       AND year  = 2010
       AND semester = 'S1';
```

**Example 2:** Multiple disjunctions.

```sql
SELECT *
  FROM Student
 WHERE address    = 'Bondi'
       OR address = 'Maroubra'
       OR age < 20;
```

### Complex `WHERE` Conditions

For more complex query conditions, you can also combine `AND` and `OR` operators using brackets to create a compound condition. This way, you can write basically arbitrarily complex filter conditions as long as you follow the [Boolean logic](https://en.wikipedia.org/wiki/Boolean_logic) rules.

**Example 1:**

```sql
SELECT *
  FROM Student
 WHERE (age = 19 AND address = 'Newtown')
    OR (age = 20 AND address = 'Bondi');
```

Whether you formulate your query with `AND` or `OR` as outer connective, is up-to which logical formulation you prefer.

**Example 2:** The same query in [conjunctive normal form](https://en.wikipedia.org/wiki/Conjunctive_normal_form).

```sql
SELECT *
  FROM Student
 WHERE (age = 19 OR age = 20)
   AND (age = 19 OR address = 'Bondi')
   AND (age = 20 OR address = 'Newtown')
   AND (address = 'Newtown' OR address = 'Bondi');
```

## Negation

### Inequality Conditions in SQL

How do we search for something in a database which *differs* from a search condition?

This is a special type of a range query, where the result is the inverse of an equality or point query. The easiest way to write those queries is to use the *inequality* comparison. That filters all tuples which do have a different value than the one compared to. In SQL, we have the choice to write this as either `<>` or `!=`.

**Example:**

```sql
SELECT *
  FROM Student
 WHERE age <> 19;
```

Above's query finds all students with a *different* age than 19.
Now edit the query and use the alternative formulation with `!=`.

### Negation with `NOT`

Another approach is to use *negation*. In SQL, you can negate any single or compound condition using the `NOT` operator:

```sql
SELECT *
  FROM Student
 WHERE NOT (age = 19);
```

Negation also works for more complex compound conditions:

```sql
SELECT *
  FROM Student
 WHERE NOT (age = 19 OR age = 20);
```

### Foreign-language Films

Write an SQL query that counts how many *foreign-language* films are in the `Film` table. A *foreign-language* film is a `Film` that has a different `language_id` than the `original_language_id`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(*)
from Film
where language_id != original_language_id
```

# Ordering, Distinct and Pattern Matching

## Ordering results with ORDER BY

### Ordering Results with `ORDER BY`

Relational databases are working with **sets** of tuples without any pre-defined order. However we sometimes would like to have a result in a certain order. In this case, we can explicitly specify the required result order in SQL with the `ORDER BY` clause.

**Example:** The following example query lists all students in ascending (increasing) order by their `studentId`.

```sql
SELECT *
  FROM Student
 ORDER BY studentId;
```

If you remove the `ORDER BY` clause from the previous query and run it again, you will see that students are returned in an arbitrary order.

SQL's `ORDER BY` clause, demonstrated above, allows you to ask the database for an explicit ordering of the result table.

**Note:** The relational data model is defined over *sets* of tuples. Since sets are unordered collections, query results are produced in no specific order unless `ORDER BY` is used.

### Using `WHERE` with `ORDER BY`

Here is an example of using the `WHERE` clause with `ORDER BY`:

```sql
SELECT *
  FROM Student
 WHERE age > 20
 ORDER BY studentId;
```

Note that `ORDER BY` can only be used at the end of your query, after any `WHERE` clause.

### Ascending and Descending Order

Try running the following query which contains an `ORDER BY` clause:

```sql
SELECT studentId, age
  FROM Student
 ORDER BY age DESC;
```

You should be able to tell that students were sorted in *descending* (decreasing) order by their `age`. This is due to using the `DESC` sorting option.

**Note:** If no sort option is specified (i.e. neither `ASC` nor `DESC`), the results will be sorted in ascending order. This was demonstrated in the previous slide.

### Multi-Attribute Ordering

SQL allows multiple attributes in the `ORDER BY` clause. For example:

```sql
SELECT studentId, age, address
  FROM Student
 ORDER BY age DESC, address ASC;
```

In this result table, students are first sorted by `age` in *descending* (`DESC`) order. Any students with the same `age` are then sorted by their `address` in, *ascending* (`ASC`) order. Note how this is specified in the query's `ORDER BY` clause: `age DESC, address ASC`.

**Hint:** Although this example only uses 2 attributes in the `ORDER BY` clause, SQL allows any number of attributes to be specified.

### Languages Z-A

Write an SQL query to list every `Language` stored in the database. Your query should return all available `Language` attributes, and the results should be in *reverse alphabetical order* (Z to A) based on their `name`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select *
from Language
order by name desc
```

## Unique Results with DISTINCT

### Duplicate Elimination with `DISTINCT`

While the relational data model is defined over *sets* of tuples, SQL for efficiency reasons allows *multisets*. In other words, SQL does not check whether some result row has already been found or not. That is unless you tell SQL to do so with the `DISTINCT` keyword as part of its `SELECT` clause.

Let's look at an example of how `DISTINCT` is used. The following query lists all addresses from students once, even if more than one student lives in the same suburb:

```sql
SELECT DISTINCT address
  FROM Student;
```

If you remove the `DISTINCT` keyword in above's query, you will see that Newtown gets reported more than once because three students live there.

Another example is the following query that lists all units of study taken by a student `316424328` only once, even if they appear more than once in the student's transcript:

```sql
SELECT DISTINCT uosCode
  FROM Enrolled
 WHERE studentId = 316424328;
```

### Keeping Duplicates

While we can remove duplicates in the result with the `DISTINCT` keyword, we can also explicitly keep them using `ALL`.

**Example:**

```sql
SELECT ALL address
  FROM Student
 WHERE age BETWEEN 18 and 25;
```

This is not very useful when querying just single tables, but later on we will come back to this when we look at querying multiple tables and especially with sub-queries.

### Counting Distinct Values

The `DISTINCT` keyword can also be used within aggregate functions such as `COUNT()` to only consider distinct values. For example:

```sql
SELECT COUNT(DISTINCT grade)
  FROM Enrolled
 WHERE studentId = 316424328
```

Above's query counts how many *distinct* grades the student with sid 316424328 achieved. If you remove the `DISTINCT` keyword, you will see that there are actually 3 overall grades recorded for that student, but only 2 distinct grades.

### Different Original Languages

Write a SQL query that determines how many *different* original languages are used by films in our database.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(distinct original_language_id)
from Film
```

## Pattern Matching with SQL

### Text Pattern Matching with `LIKE`

The following query lists all units of study which start with 'Database':

```sql
SELECT uosCode, uosName
  FROM UnitOfStudy
 WHERE uosName LIKE 'Database%';
```

Now try this example, where the pattern is changed to `'%Database%'`:

```sql
SELECT uosCode, uosName
  FROM UnitOfStudy
 WHERE uosName LIKE '%Database%';
```

SQL's `LIKE` comparison operator returns true if a string value matches a given pattern. In the above example, the pattern was `'%Database%'`, where the percent signs are *placeholders* representing any sequence of zero or more characters.

**Hint:** You can also find strings which do **not** match the pattern, by using `NOT LIKE`.

### Placeholders in `LIKE` Predicates

Below is another example of using `LIKE` - try running it:

```sql
SELECT uosCode, uosName
  FROM UnitOfStudy
 WHERE uosCode LIKE 'INFO1___';
```

```
+----------+--------------------+
| uoscode  |      uosname       |
+----------+--------------------+
| INFO1003 | Introduction to IT |
+----------+--------------------+
(1 row)
```

This example finds all first-year 'INFO' units of study by using the underscore (`_`) placeholder to match 3 single characters. In other words, `uosCode` must start with `'INFO1'` followed by exactly three characters (3 x `_` placeholder).

**Placeholder Summary**

-   `%` matches any string of 0 to unlimited many characters
-   `_` matches exactly one character

### Case-(in)sensitivity with `LIKE`

SQL's `LIKE` comparisons are case-sensitive by default. For example:

```sql
SELECT 'USyd' LIKE 'usyd';
```

```
+----------+
| ?column? |
+----------+
| f        |
+----------+
(1 row)
```

The above returns `f` for `false`, indicating the string `'USyd'` does not match the pattern `'usyd'`. We can achieve *case-insensitive* pattern matching by ensuring both strings are lowercase. SQL's `LOWER()` function converts any string value to lowercase:

```sql
SELECT LOWER('USyd') LIKE 'usyd';
```

```
+----------+
| ?column? |
+----------+
| t        |
+----------+
(1 row)
```

This second example now returns `t` for `true`, because the string `'USyd'` is converted to lowercase before being used with `LIKE`; resulting in a case-insensitive comparison.

**Tip**

This is very useful to query text in a database where you are not sure about its exact lowercase/uppercase spelling. In this case, use an explicit `lower` conversion for *case-insensitive matching*:

```sql
SELECT uosCode, uosName
  FROM UnitOfStudy
 WHERE LOWER(uosName) LIKE '%systems%';
```

### Advanced: Regex Pattern Matching

While `LIKE` is the standard pattern matching operator in SQL, modern SQL processors provide more sophisticated pattern searches.

-   PostgreSQL provides a `SIMILAR TO` operator that includes SQL's definition of regular expressions (cf. [online documentation of PostgreSQL about pattern matching](http://www.postgresql.org/docs/current/static/functions-matching.html)).
-   Other DBMSs such as Oracle offer a `regexp_like` function that can process POSIX regular expressions (cf. [Oracle's documentation of its `regexp_like` function](http://stanford.edu/dept/itss/docs/oracle/10g/server.101/b10759/conditions018.htm)).

Below is an example of regular expression pattern matching in PostgreSQL. This example matches all subjects whose `title` starts with `'Advanced'` or `'Data'`.

```sql
SELECT uosCode, uosName
  FROM UnitOfStudy
 WHERE uosName SIMILAR TO '(Advanced|Data)%';
```

Another example that finds all COMP-coded units of study:

```sql
SELECT uosCode, uosName
  FROM UnitOfStudy
 WHERE uosCode SIMILAR TO 'COMP[[:digit:]]{4}';
```

The previous query looks for all units of study which have a unit of study code that starts with `COMP` followed by 4 digits.

### Mad Scientists

Your task is to write an SQL query that outputs how many films are about a `'Mad Scientist'` (as mentioned in the film's `description`). The output of your query should be just the number of such films.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(description)
from Film
where description like '%Mad Scientist%'
```

### R-rated Deleted Scenes

Your task is to write an SQL query that lists all films that are rated `'R'` and have `'Deleted Scenes'` as one of their special features. Your query should list each `Film`'s:

1.  `title` (in alphabetical order)
2.  `release_year`

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select title, release_year
from Film
where rating = 'R' and special_features like '%Deleted Scenes%'
order by title
```

# NULL Values and Views

## Handling NULL values

### Checking for `NULL` Values

An important feature of relational databases are `NULL` 'values' which allow them to represent that some data is *not known* (yet).

The following example lists the student IDs of all students who have no `grade` stored:

```sql
SELECT studentId
  FROM Enrolled
 WHERE grade IS NULL;
```

Notice the third line: `WHERE grade IS NULL`. SQL databases support storing a special value to indicate *unknown* information: `NULL`

SQL has two comparison operators to check for `NULL`:

-   `<expr> IS NULL`

    This checks whether a given `<expr>` is `NULL` and yields *true* if this is the case.

-   `<expr> IS NOT NULL`

    This checks the reverse, i.e. whether a given `<expr>` is *not* `NULL`.

### What Value has `NULL`?

`NULL` is a very common and at the same time also quite tricky concept in relational databases that is worthwhile a closer look.

As said before, `NULL` represents unknown information. Actually strictly speaking, it is an indicator for unknown information, rather than an actual data value itself.

In particular, `NULL` is not an empty string:

```sql
SELECT '' IS NULL;
```

```
+----------+
| ?column? |
+----------+
| f        |
+----------+
(1 row)
```

This query returns `f` for `false` because for SQL `NULL` is not an empty string.

Example 2: `NULL` is also not 0 in the numeric space.

```sql
SELECT 0 IS NULL;
```

```
+----------+
| ?column? |
+----------+
| f        |
+----------+
(1 row)
```

### Three-Valued Logic

This special standing of `NULL` has some far-reaching implications to comparison operations in queries.

Try running this query which compares the number `1` with `NULL` using the normal equality comparison operator (`=`):

```sql
SELECT 1 = NULL;
```

```
+----------+
| ?column? |
+----------+
|          |
+----------+
(1 row)
```

You should see that the above query returns an empty cell, which represents a `NULL` result. But why does it not return `f` (for `false`)?

The inclusion of `NULL` in the type system of SQL leads to a *three-valued logic* for comparison operations. Any comparison with `NULL` cannot be decided, and is neither *true* nor *false*; it is instead ***unknown\***. As in the example above, if you try to compare any known value with `NULL`, the result is `NULL`.

In other words, it is impossible to tell whether a known value like `1` equals an unknown value (`NULL`), so the result of comparing them is unknown (`NULL`). This is why SQL has the special comparison operators `IS NULL` and `IS NOT NULL`.

### Three-Valued Logic Expressions

Below is the result table for comparison and Boolean operators with SQL's three-valued logic:

| `a`    | `b`    | `a = b` | `a AND b` | `a OR b` | `NOT a` | `a IS NULL` |
| :----- | :----- | :------ | :-------- | :------- | :------ | :---------- |
| true   | true   | true    | true      | true     | false   | false       |
| true   | false  | false   | false     | true     | false   | false       |
| false  | true   | false   | false     | true     | true    | false       |
| false  | false  | true    | false     | false    | true    | false       |
| true   | `NULL` | unknown | unknown   | true     | false   | false       |
| false  | `NULL` | unknown | false     | unknown  | true    | false       |
| `NULL` | true   | unknown | unknown   | true     | unknown | true        |
| `NULL` | false  | unknown | false     | unknown  | unknown | true        |
| `NULL` | `NULL` | unknown | unknown   | unknown  | unknown | true        |

### Top-Level Categories

Your task is to write an SQL query that lists all film categories in the `Category` table which have no parent category (`NULL`). Your query should list the `name` of these 'top-level' categories in alphabetical order

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select name
from Category
where parent_cat is null
order by name
```

### Aggregation Functions and `NULL`

Another special aspect of `NULL` is how aggregate functions treat it. Most aggregate functions simply ignore any `NULL` - with the notably exception of `COUNT(*)` that always counts all tuples.

**Example 1:** How many entries are in the `Student` table?

```sql
SELECT COUNT(*) FROM Student;
```

```
+-------+
| count |
+-------+
|    11 |
+-------+
(1 row)
```

**Example 2:** If you use the `COUNT` function on a specific column, it will ignore any `NULL`.

```sql
SELECT COUNT(age) FROM Student;
```

```
+-------+
| count |
+-------+
|     9 |
+-------+
(1 row)
```

The difference between these two queries is that the second `COUNT(age)` query does ignore every `NULL` age - and in this example, there are two students with an unknown `age`:

```sql
SELECT COUNT(*)
  FROM Student
 WHERE age IS NULL;
```

```
+-------+
| count |
+-------+
|     2 |
+-------+
(1 row)
```

**Careful**

Where you have to be careful is when you combine a `COUNT(*)` with other aggregate function which ignore `NULL`s:

```sql
SELECT AVG(age) FROM Student;
SELECT SUM(age) / COUNT(*) AS avg FROM Student;
```

```
+---------------------+
|         avg         |
+---------------------+
| 20.1111111111111111 |
+---------------------+
(1 row)

+-----+
| avg |
+-----+
|  16 |
+-----+
(1 row)
```

In this example, we would expect both queries to return the same result. But they do not. Because when we try to manually calculate the average, `COUNT(*)` counts the tuples with unknown age too, which results in a different denominator than used by the built-in `AVG()` function. Oops!

### Films without Original Language?

Write a SQL query that determines how many films have no (known) original language.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(*)
from Film
where original_language_id is null
```

### Making `NULL` Visible

As you have seen, `NULL` is normally not shown in the database output at all. This makes it however sometimes hard to see, especially when you have some string attributes with `NULL` 'values', so that you can not distinguish in the output between an empty string and `NULL`.

Most databases allow to make `NULL` visible in the output with some special commands. In our PostgreSQL system, this can be done with the `\pset` command:

```sql
\pset null '[NULL]'
SELECT * FROM Enrolled;
```

```
Null display is "[NULL]".
+-----------+----------+----------+------+--------+
| studentid | uoscode  | semester | year | grade  |
+-----------+----------+----------+------+--------+
| 609187546 | INFS1405 | S2       | 2016 | [NULL] |
| 316424328 | INFO2120 | S1       | 2010 | D      |
| 305678453 | INFO2120 | S1       | 2010 | HD     |
| 316424328 | INFO3005 | S1       | 2005 | CR     |
| 200022153 | INFO3404 | S2       | 2008 | P      |
| 316424328 | COMP5338 | S1       | 2006 | D      |
| 404246989 | INFS1405 | S2       | 2016 | [NULL] |
| 309145324 | INFO2120 | S1       | 2010 | F      |
| 609187546 | INFO2005 | S2       | 2004 | D      |
| 207088592 | COMP5138 | S1       | 2016 | [NULL] |
+-----------+----------+----------+------+--------+
```

Note that this is specific to the `psql` command of PostgreSQL. In pgAdmin, it will not work. If you use another database system, consult its manual on how to do the same there.

### The `COALESCE` Function

There is another way to make `NULL` visible in a query, not just for producing a human-readable result, but also for NULL-safe string as part of a query condition. SQL provides the `COALESCE` function to explicitly 'replace' a `NULL` value with a meaningful value during query evaluation.

The `COALESCE(expr, value_if_null)` function returns the second argument (`value_if_null`) if the expression in the first argument (`expr`) evaluates to `NULL`.

**Example:**

```sql
SELECT studentId, COALESCE(grade, '[UNKNOWN]')
  FROM Enrolled;
```

```
+-----------+-----------+
| studentid | coalesce  |
+-----------+-----------+
| 609187546 | [UNKNOWN] |
| 316424328 | D         |
| 305678453 | HD        |
| 316424328 | CR        |
| 200022153 | P         |
| 316424328 | D         |
| 404246989 | [UNKNOWN] |
| 309145324 | F         |
| 609187546 | D         |
| 207088592 | [UNKNOWN] |
+-----------+-----------+
(10 rows)
```

You can use this function also inside the `WHERE` clause of a query, for example for a weird `IS NOT NULL` test (please don't use it the same way - this is just a syntax example):

```sql
SELECT studentId, grade
  FROM Enrolled
 WHERE COALESCE(grade, '[UNKNOWN]') != '[UNKNOWN]';
```

```
+-----------+-------+
| studentid | grade |
+-----------+-------+
| 316424328 | D     |
| 305678453 | HD    |
| 316424328 | CR    |
| 200022153 | P     |
| 316424328 | D     |
| 309145324 | F     |
| 609187546 | D     |
+-----------+-------+
(7 rows)
```

## Creating and Dropping SQL Views

### The `CREATE VIEW` Statement

The `CREATE VIEW` DDL statement extends the current database schema with a new *view*:

```sql
CREATE VIEW CurrentStudents AS
  SELECT studentId, uosCode, semester
    FROM Enrolled
   WHERE year = 2016;

SELECT *
  FROM CurrentStudents;
```

The above example creates a new view called `CurrentStudents`, then performs a `SELECT` over it. A view is like a “stored” query. Once created, it can be queried like a table (it has a name and a schema).

The general syntax to define a new view in SQL is:

```sql
CREATE VIEW name AS <query>;
```

### Views ≠ Tables

Although a view is queried like a table, there is nothing stored in it. The contents are dynamically retrieved from the underlying tables each time it is referenced in a query.

**Hint**

The `AS` renaming operator of `SELECT` can be used to define custom names for the view attributes. For example:

```sql
SELECT studentId AS sid
  FROM Student;
```

### The `DROP VIEW` Command

Existing views can be removed with the `DROP VIEW` command. The general syntax is:

```sql
DROP VIEW <viewname>;
```

### Simple Film View

Your task is to write an SQL DDL statement which creates a new view called `FilmCostList`. This view should list all non-foreign-language films (films without an `original_language_id`) of the `Film` table just with the following attributes:

1.  `title` - the `title` of each film
2.  `year` - the `release_year` of each film
3.  `costs` - the `rental_rate` of each film

Your view should list those films in alphabetical order by `title`. Films with the same `title` should be further ordered by `year`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
create view FilmCostList as
select title, release_year as year, rental_rate as costs
from Film
where original_language_id is null
order by title, year;

select *
from FilmCostList
```

### Dramatic Viewing

Your task is to write an SQL DDL statement which creates a new view called `LengthyDramas`. This view should list all `'drama'` films (as mentioned in their `description` *regardless of capitalisation*) which have a running time over `90` minutes. Your view needs to have the following attributes:

1.  `id` - the `film_id` of each drama
2.  `title` - the `title` of each drama
3.  `year` - the `release_year` of each drama
4.  `minutes` - the `length` of each drama

Your view also needs to list dramas in reverse order of their running time (`minutes`). Any dramas with the same running time should be further sorted in alphabetical order by their `title`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
create view LengthyDramas as
select film_id as id, title, release_year as year, length as minutes
from Film
where lower(description) like '%drama%' and length > 90
order by length desc, title;

select * from LengthyDramas
```

# Introduction to Joins

## SQL Joins

### Joining Tables in SQL

Up until now, all our examples and questions have only queried single tables. However, in SQL we can also combine data from multiple tables, typically by following foreign-key relationships. This operation is called a *Join*.

For example, the following query lists all students enrolled in `'INFO2120'` by joining two tables - `Student` and `Enrolled`:

```sql
SELECT Student.studentId, name
  FROM Student, Enrolled
 WHERE Student.studentId = Enrolled.studentId
       AND Enrolled.uosCode = 'INFO2120';
```

From the above example you should be able to see:

1.  All tables accessed by the query are listed in the `FROM` clause.
2.  The `WHERE` clause includes a *join condition* which relates tuples from both relations. In this example, the join condition is:
    `Student.studentId = Enrolled.studentId`.

### Formulating Join Conditions

The most frequently used join condition is to relate the value of the *foreign key* attribute(s) of one table to the same value of the corresponding *primary key* in the second table.

In our previous example, `Student.studentId` is a primary key referenced by the foreign key `Enrolled.studentId`:

![Example Schema ](https://groklearning-cdn.com/modules/79oPWvJToJiq692udYDExg/exampledb-studid-fk.png)

The join condition `Student.studentId = Enrolled.studentId` specifies that we want each enrollment record paired with its corresponding student, and not any other student.

**Equi-Join:** The join condition above tests for equality, hence this kind of join is also referred to as *Equi-Join*.

Note that even though in this case, the foreign key and primary key were both called `studentId`, this may not be the case in different schemas. It is called an *equi-join* as long as two attributes, whatever name, are compared in the join condition with an equality (`=`) comparison.

### Missing Join Conditions

A common mistake when trying to join two tables is to forget one of the join conditions.

**As a rule-of-thumb**, whenever there is more than one table listed in the `FROM` clause, each table should be used in at least one join condition in the `WHERE` clause.

Try running a modified version of our query from the previous slide *without* its join condition (`Student.studentId = Enrolled.studentId`):

```sql
SELECT *
  FROM Student, Enrolled
 WHERE Enrolled.uosCode = 'INFO2120'
 LIMIT 5;
```

```
+-----------+--------------+---------+-----+-----------+----------+----------+------+-------+
| studentid |     name     | address | age | studentid | uoscode  | semester | year | grade |
+-----------+--------------+---------+-----+-----------+----------+----------+------+-------+
| 307088592 | John Smith   | Newtown |  19 | 316424328 | INFO2120 | S1       | 2010 | D     |
| 307088592 | John Smith   | Newtown |  19 | 305678453 | INFO2120 | S1       | 2010 | HD    |
| 307088592 | John Smith   | Newtown |  19 | 309145324 | INFO2120 | S1       | 2010 | F     |
| 305422153 | Sally Waters | Coogee  |  22 | 316424328 | INFO2120 | S1       | 2010 | D     |
| 305422153 | Sally Waters | Coogee  |  22 | 305678453 | INFO2120 | S1       | 2010 | HD    |
+-----------+--------------+---------+-----+-----------+----------+----------+------+-------+
(5 rows)
```

When join conditions are missed, the result is a *cartesian join* - every row of each listed table combined with every row of every other listed table (subject to any `WHERE` conditions). In this case, every student record has been combined with every `INFO2120` enrolment record. This is rarely the desired result.

###  Lonely Actors

Your task is to write an SQL query that finds the number of actors who acted in the `Film` entitled `'ALONE TRIP'`. Your query should return just the number of actors.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(actor_id)
from Film, Film_actor
where Film.film_id = Film_Actor.film_id and title = 'ALONE TRIP'
```

### Qualifying Common Attributes

A common problem with join queries is that some attributes in those tables, typically the join attributes, share the same name. For example, both `Enrolled` and `Student` have an attribute called `studentId`. If you try to use this attribute in a join query without disambiguating, the DBMS will return an error:

```sql
SELECT studentId
  FROM Student, Enrolled
 WHERE studentId = studentId;
```

```
psql:query.sql:2: ERROR:  column reference "studentid" is ambiguous
LINE 1: SELECT studentId
```

This error (*column reference "studentid" is ambiguous*) can be resolved by instead referring to either `Student.studentId` or `Enrolled.studentId` as desired. For example:

```sql
SELECT Student.studentId
  FROM Student, Enrolled
 WHERE Student.studentId = Enrolled.studentId;
```

```
+-----------+
| studentid |
+-----------+
| 316424328 |
| 305678453 |
| 316424328 |
| 305422153 |
| 316424328 |
| 309145324 |
| 309187546 |
+-----------+
(7 rows)
```

### Table Aliases

If two attributes in joined tables have the same name, you need to qualify those attributes with their table name whenever you use them (see the join condition in the previous example: `Student.studentId = Enrolled.studentId`).

To help with this, SQL allows a *table alias* to be defined after each table in the `FROM` clause. Any name can be used as an alias, but typically you would opt for something short like `S` for `Student`. Keeping some resemblance to the original table name assists with readability.

Here's our previous example join, using table aliases:

```sql
SELECT S.studentId
  FROM Student S, Enrolled E
 WHERE S.studentId = E.studentId;
```

### Multiple Explicit Joins

We can also join more than two tables in one query. Just list all involved tables in the `FROM` clause, ensuring that you specify all join conditions in the `WHERE` clause.

Let's look at an example of a three-way join. The following finds the student IDs and names of all students enrolled in the subject `'Database Systems I'`:

```sql
SELECT S.studentId, name
  FROM Student S, Enrolled E, UnitOfStudy U
 WHERE S.studentId = E.studentId
       AND U.uosCode = E.uosCode
       AND U.uosName = 'Database Systems I';
```

Note that there are two join conditions now; combining `Enrolled` tuples with both the corresponding `Student` tuples using the correct `studentId` value (`S.studentId = E.studentId`), as well as with the corresponding entry in `UnitOfStudy` for the `'Database Systems I'` course (`U.uosCode = E.uosCode`).

![3-Way Join Schema ](https://groklearning-cdn.com/modules/pSVQU6z5i46ASs9MgvbLLD/exampledb-3wayjoin.png)

### Johnny Cage's Films

Your task is to write an SQL query that lists the `title` of every `Film` in which the `Actor` named `JOHNNY CAGE` has appeared. The titles should be in alphabetical order.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select title
from Film natural join Film_Actor natural join Actor
where first_name = 'JOHNNY' and last_name = 'CAGE'
order by title
```

## Natural Joins

### Natural Joins (⋈)

A very convenient way for joining two tables is the `NATURAL JOIN`.

A *natural join* between two tables combines those tuples whose values agree in all common attributes, ie. those that are named the same. These are typically the foreign-key - primary-key pairs. These common attributes are also shown only once in the result.
In SQL, we can use the explicit `NATURAL JOIN` keyword for this in the `FROM` clause.

**Example:**

```sql
SELECT *
  FROM Student NATURAL JOIN Enrolled
 WHERE uosCode = 'INFO2120';
```

The above example query joins the tables `Student` and `Enrolled` by attributes of the same name which must have the same value. In our schema, this is the `studentId` attribute. So the `NATURAL JOIN` combines all those Student and Enrolled tuples where `Student.studentId = Enrolled.studentId`. Additionally, because of its `WHERE` clause, the query above does this only for the `'INFO2120'` unit of study.

### Natural Join vs. Explicit Equi-Join

Note that the `NATURAL JOIN` shows the *join attributes only once* in the result. Compare for example the result of our `NATURAL JOIN` query from the previous slide...

```sql
SELECT *
  FROM Student NATURAL JOIN Enrolled
 WHERE uosCode = 'INFO2120';
```

```
+-----------+-----------------+------------+-----+----------+----------+------+-------+
| studentid |      name       |  address   | age | uoscode  | semester | year | grade |
+-----------+-----------------+------------+-----+----------+----------+------+-------+
| 305678453 | Pauline Winters | Bondi      |  20 | INFO2120 | S1       | 2010 | HD    |
| 316424328 | Matthew Long    | Camperdown |  19 | INFO2120 | S1       | 2010 | D     |
| 309145324 | Victoria Tan    | Maroubra   |  23 | INFO2120 | S1       | 2010 | F     |
+-----------+-----------------+------------+-----+----------+----------+------+-------+
(3 rows)
```

... with the result of the similar query at the start of this chapter which used an explicit equi-coin condition:

```sql
SELECT *
  FROM Student S, Enrolled E
 WHERE S.studentId = E.studentId
       AND uosCode = 'INFO2120';
```

```
+-----------+-----------------+------------+-----+-----------+----------+----------+------+-------+
| studentid |      name       |  address   | age | studentid | uoscode  | semester | year | grade |
+-----------+-----------------+------------+-----+-----------+----------+----------+------+-------+
| 305678453 | Pauline Winters | Bondi      |  20 | 305678453 | INFO2120 | S1       | 2010 | HD    |
| 316424328 | Matthew Long    | Camperdown |  19 | 316424328 | INFO2120 | S1       | 2010 | D     |
| 309145324 | Victoria Tan    | Maroubra   |  23 | 309145324 | INFO2120 | S1       | 2010 | F     |
+-----------+-----------------+------------+-----+-----------+----------+----------+------+-------+
(3 rows)
```

If you execute both queries and scroll the results a bit to the right, you see that in the second case, the `studentId` is shown twice because both tables contain that attribute. In contrast, the natural join shows the studentId only once in its result, even if we use `SELECT *` (meaning 'show all result attributes').

### Films with British Actors

Your task is to write an SQL query that lists the distinct `film_id`s of all films that have at least one British actor (nationality `'UK'`). Try to make use of SQL's `NATURAL JOIN` operator in your solution.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select distinct film_id
from Film natural join Film_Actor natural join Actor
where nationality = 'UK'
```

### Multi-way Natural Joins

We can also use the `NATURAL JOIN` keyword in a sequence of multiple consecutive joins.

**Example:** The query from the previous slide 'Multiple Explicit Joins' can be formulated more compactly as follows:

```sql
SELECT studentId, name
  FROM (Student NATURAL JOIN Enrolled E)
                NATURAL JOIN UnitOfStudy
 WHERE uosName = 'Database Systems I';
```

**A word of caution:** The `NATURAL JOIN` checks for equality of *all* attributes of the same name. It does not matter what these attributes mean; if they are named the same in both joined tables, they are considered in the join condition.

### Natural Join Caveat

An unexpected side-effect of the behaviour of `NATURAL JOIN` is evident when using it on two tables with *no common attributes*.

**Example:** Wrong Natural Join Usage
What result do you expect from the following query?

```sql
SELECT studentId, uosCode
  FROM Student NATURAL JOIN UnitOfStudy;
```

This query indeed produces a result which *looks like* a join result - but it is not! The query actually produced a *cross join*, also called the *cross product* of both tables. It combined each `Student` tuple with all `UnitOfStudy` tuples, regardless of their content, because there were no common attributes to check for equality. This is typically not what you want, so take care when using `NATURAL JOIN` operations!

**Technical Background**

The reason for this behaviour becomes clear once we look at the formal definition of the natural join in relational algebra:

$R \bowtie S = \pi_{unique\_attributes} ( \sigma_{equality\_of\_common\_attributes} ( R \times S ) )$

This means that a natural join between two relations R and S is equivalent to filter the results of the cross-product of the two relations $(R \times S)$ by an equality condition on common attributes ($\sigma_{equality\_of\_common\_attributes}(\dots)$) with subsequent projection on just the unique attributes ($\pi_{unique\_attributes}(\dots)$).

But if there are no common attributes, the filter operation has no condition anymore, and the *unique attributes* are simply *all attributes*. And so we are left with a simple cross product: $R \times S$

### R-rated Horror Films

Your task is to write an SQL query that lists every `Film` in the `Category` `'Horror'` that is rated `'R'`, in alphabetical order by `title`. Your query should return these attributes:

1.  `film_id`;
2.  `title`; and
3.  `release_year`.

Try to make use of SQL's `NATURAL JOIN` operator in your answer.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, release_year
from Film natural join Film_Category natural join Category
where rating = 'R' and name = 'Horror'
order by title
```

# Inner and Outer Joins

## The JOIN Operator

### More on Joins

In the previous tutorial chapter we introduced the *join* as the core database operation to combine tuples from multiple tables. We also learned about the *natural join* and how it automatically combines tuples from two relations based on equality of common attributes.

But a few questions remained open:

1.  How do we join two tables without common attributes?
2.  Do we always need to test for equality, or could the *join condition* be something more generic?
3.  What can we do for tuples without a join partner in the joined table?

We will introduce solutions to all these questions in more detail in the following pages.

### SQL's `JOIN` Operator (`INNER JOIN`)

Because joining two tables is an important operation, SQL provides an explicit `JOIN` operator to clarify the query semantics.

The common case to combine two relations is to perform a so-called *inner join* when two tuples from each of the two relations are combined if and only if a *join condition* is true. The standard SQL keyword is the `INNER JOIN` operator inside a `FROM` clause. As a shortcut, this is also just called `JOIN`.

There are two syntax options to specify the join condition:

-   `r1 JOIN r2 ON (`  *condition*  `)`

    Combines tuples from relations `r1` and `r2` whenever **condition** is true.

-   `r1 JOIN r2 USING (`  *field(s)*  `)`

    Combines tuples from relations `r1` and `r2` whenever all listed **field(s)** have the same values in both tuples. Note that this obviously assumes that these attributes occur with the same name in both relations!

Note that in its most generic form, the join condition behind the `JOIN ... ON` variant can be an arbitrary Boolean condition which is neither restricted to an equality test, nor does it require common attribute names.

### Examples of using `JOIN`

Let's have a look at some examples of how the `JOIN ... ON` operator can be used. We begin with an example where two tables do not share any common attributes.

**Example 1:** The following query finds the name of the lecturers of COMP5138 in the different years.

```sql
SELECT year, name
  FROM AcademicStaff
       JOIN Lecture ON (id = lecturer)
 WHERE uosCode = 'COMP5138';
```

Note that the join attributes have different names in this example. The query needs to combine tuples from the `AcademicStaff` and `Lecture` relations where the `lecturer` attribute of `Lecture` has the same value as the `id` attribute of the `AcademicStaff` relation.

### Further `JOIN` Examples

We also can use the `JOIN` operator with an arbitrary join condition.

**Example 2:** The following query finds all units of study which have *less* credit points than INFO2120.

```sql
SELECT U2.uoscode, U2.credits
  FROM UnitOfStudy U1 JOIN UnitOfStudy U2
                        ON (U2.credits < U1.credits)
 WHERE U1.uosCode = 'INFO2120';
```

**Example 3:** Not very commonly used, but it even works with multiple conditions with logical connectors.

```sql
SELECT U2.uoscode, U2.credits
  FROM UnitOfStudy U1 JOIN UnitOfStudy U2
       ON (U1.uosCode = 'INFO2120'
           AND U2.credits < U1.credits);
```

### Examples of `JOIN USING`

The second variant of the *inner join* uses one or more common attributes, which are listed after the `USING` keyword, to join two tables. If tuples from both tables agree on those attributes they are combined into the result. Common attributes occur only once in the result.

**Example:** The following query finds the name of students who have enrolled in INFO2120.

```sql
SELECT name
  FROM Student
       INNER JOIN Enrolled USING (studentId)
 WHERE uosCode = 'INFO2120';
```

The query combines tuples from the `Student` and `Enrolled` relations where both have the *same* `studentId` value, but only using `Enrolled` entries with `uosCode = 'INFO2120'`.

The `NATURAL JOIN` operator is actually just a shortcut for an inner join with `USING` where the list of common attributes is automatically determined. You can verify this by rewriting above's query with a `NATURAL JOIN` operator and `SELECT *`.

As we demonstrated last chapter, the use of `NATURAL JOIN` is risky in case there are no common attributes. As this can happen through schema changes over the lifetime of a database, good practice is to always use the `JOIN ... USING` variant in queries.

### Cast of 'American Circus'

Your task is to write an SQL query that lists the `first_name` and `last_name` of every `Actor` who played in the `Film` entitled `'AMERICAN CIRCUS'`, in alphabetical order by last name. Try to use SQL's `INNER JOIN` operator in your answer.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select first_name, last_name
from film inner join Film_Actor using (film_id) inner join Actor using (actor_id)
where title = 'AMERICAN CIRCUS'
order by last_name
```

### Categories and their Parents

Your task is to write an SQL query that lists all film sub-categories and their corresponding parent categories. Your query's result should contain the following attributes:

1.  `category_id`;
2.  `category` - the name of the category; and
3.  `parent` - the name of the category's parent category.

You should ignore any category which does not have a parent category, i.e. your query's result table should contain no `NULL`s.

Try to use SQL's `INNER JOIN` operator in your answer.

**Hint:** The attribute `Category.parent_cat` is a foreign key referencing `Category.category_id`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select Child.category_id, Child.name as category, Parent.name as parent
from Category Child inner join Category Parent on Child.parent_cat = Parent.category_id
```

### Actors' Countries

We are looking for the correct way to join two tables which have no attributes in common. The following query tries to find the `Country name` for the `nationality` of every `Actor` with last name `'DEPP'`:

```sql
SELECT first_name, last_name,
       name AS country_name
  FROM Actor NATURAL JOIN Country
 WHERE last_name = 'DEPP';
```

But it does not give the correct result. Do you see why?

![image-20211006133800819](https://i.loli.net/2021/10/06/lPjeIbEozfkLyAD.png)

Your task is to write an SQL query which formulates this join correctly. Your query should return the following attributes (as in the example above):

1.  `first_name` - the first name of each actor;
2.  `last_name` - the last name of each actor; and
3.  `country_name` - the country name of each actor's nationality.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
SELECT first_name, last_name,
       name AS country_name
 FROM Actor JOIN Country on Actor.nationality = Country.short_code
 WHERE last_name = 'DEPP';
```

### `JOIN` Tips

Joining is a very common database operation, but there are some pitfalls which you should avoid. The following is a short summary of the main 'Lessons Learned' when joining two tables:

1.  When you list more than one table in the `FROM` clause of a query, make sure that every table is mentioned with at least one `JOIN` operator or in at least one explicit join condition.
2.  When using the `NATURAL JOIN` operator, ensure that both tables indeed share common attributes. Otherwise the query result will be the cross product of the tables which is typically wrong.
3.  When using the `NATURAL JOIN` operator, ensure that you indeed want to join on *all* common attributes.
4.  Consider using `JOIN ... USING (...)` with an explicit list of join attributes instead of the `NATURAL JOIN` operator. This avoids the issues (2) and (3) above, while also future-proofing your query against schema changes.

## Outer Joins

### Outer Joins

The normal `JOIN` operation combines tuples from two tables whenever the *join condition* is true. This always requires two tuples (one from each relation), and if there is no join partner available on one side, there is also no result tuple produced.

The `OUTER JOIN` operator produces a resulting join tuple even if there is no join partner available in one of the input relations. The result tuple is filled with `NULL` values on the corresponding side.

There are three variants of an `OUTER JOIN` possible:

-   `r1 LEFT OUTER JOIN r2`

    Keep all input tuples of the left input relation `r1` in the result even if there is no join partner from `r2`. Fill with `NULL`s on the right side if required

-   `r1 RIGHT OUTER JOIN r2`

    Keep all input tuples of the right input relation `r2` in the result even if there is no join partner from `r1`. Fill with `NULL`s on the left side if required

-   `r1 FULL OUTER JOIN r2`

    Keep all input tuples of either input relation (`r1` or `r2`) in the result even if there is no join partner. Fill with `NULL`s on the corresponding side(s) if required.

### LEFT OUTER JOIN

Let's look at an example of a `LEFT OUTER JOIN`.

**Example:** The following query lists all students by `studentId`, `name`, and the `uosCode` of all units they have taken - or none if they haven't enrolled yet.

```sql
SELECT studentId, name, uosCode
  FROM Student
       LEFT OUTER JOIN Enrolled USING (studentId)
 ORDER BY studentId, uosCode;
```

```
+-----------+-----------------+----------+
| studentid |      name       | uoscode  |
+-----------+-----------------+----------+
| 305422153 | Sally Waters    | INFO3404 |
| 305678453 | Pauline Winters | INFO2120 |
| 307088592 | John Smith      |          |
| 309145324 | Victoria Tan    | INFO2120 |
| 309187546 | Niang Jin Phan  | INFO2005 |
| 316424328 | Matthew Long    | COMP5338 |
| 316424328 | Matthew Long    | INFO2120 |
| 316424328 | Matthew Long    | INFO3005 |
+-----------+-----------------+----------+
(8 rows)
```

Since this query uses a `LEFT OUTER JOIN`, all students will be listed even if they have not yet enrolled in any subject. In this case, when there is no join partner from the `Enrolled` table, the student is still in the result, but with a `NULL` `uosCode` (cf. entry for `'John Smith'`).

You can see the difference yourself by replacing the `LEFT OUTER JOIN` with an `INNER JOIN` in the example, then re-running it.

``` sql
SELECT studentId, name, uosCode
  FROM Student
       INNER JOIN Enrolled USING (studentId)
 ORDER BY studentId, uosCode;
```

```
+-----------+-----------------+----------+
| studentid |      name       | uoscode  |
+-----------+-----------------+----------+
| 305422153 | Sally Waters    | INFO3404 |
| 305678453 | Pauline Winters | INFO2120 |
| 309145324 | Victoria Tan    | INFO2120 |
| 309187546 | Niang Jin Phan  | INFO2005 |
| 316424328 | Matthew Long    | COMP5338 |
| 316424328 | Matthew Long    | INFO2120 |
| 316424328 | Matthew Long    | INFO3005 |
+-----------+-----------------+----------+
(7 rows)
```

### RIGHT OUTER JOIN

The `RIGHT OUTER JOIN` operation keeps tuples in the result from the relation on the right-hand side of the join even if there is no join partner in the left relation.

**Example:** The following query lists all units of study by their `uosCode` and `uosName`, and all the enrolled students by `studentId` - or none if no student has enrolled yet.

```sql
SELECT studentId, uosCode, uosName
  FROM Enrolled
       RIGHT OUTER JOIN UnitOfStudy USING (uosCode)
 ORDER BY uosCode;
```

```
+-----------+----------+-----------------------------------------+
| studentid | uoscode  |                 uosname                 |
+-----------+----------+-----------------------------------------+
|           | COMP5046 | Statistical Natural Language Processing |
|           | COMP5138 | Database Management Systems             |
| 316424328 | COMP5338 | Advanced Data Models                    |
|           | COMP5703 | Information Technology Project          |
|           | INFO1003 | Introduction to IT                      |
| 309187546 | INFO2005 | Database Management Introductory        |
| 316424328 | INFO2120 | Database Systems I                      |
| 309145324 | INFO2120 | Database Systems I                      |
| 305678453 | INFO2120 | Database Systems I                      |
| 316424328 | INFO3005 | Organisational Database Systems         |
| 305422153 | INFO3404 | Database Systems II                     |
|           | MATH1002 | Linear Algebra                          |
+-----------+----------+-----------------------------------------+
(12 rows)
```

Since this query uses a `RIGHT OUTER JOIN`, all units of study will be listed even if they have no student enrolled. When there is no join partner for some subject, it is still in the result, but with a `NULL` `studentId`.

Again, experiment with how the result differs if you replace the `RIGHT OUTER JOIN` with an `INNER JOIN` in the above query.

```sql
SELECT studentId, uosCode, uosName
  FROM Enrolled
       INNER JOIN UnitOfStudy USING (uosCode)
 ORDER BY uosCode;
```

```
+-----------+----------+----------------------------------+
| studentid | uoscode  |             uosname              |
+-----------+----------+----------------------------------+
| 316424328 | COMP5338 | Advanced Data Models             |
| 309187546 | INFO2005 | Database Management Introductory |
| 305678453 | INFO2120 | Database Systems I               |
| 316424328 | INFO2120 | Database Systems I               |
| 309145324 | INFO2120 | Database Systems I               |
| 316424328 | INFO3005 | Organisational Database Systems  |
| 305422153 | INFO3404 | Database Systems II              |
+-----------+----------+----------------------------------+
(7 rows)
```

### FULL OUTER JOIN

The `FULL OUTER JOIN` operation keeps tuples from both sides of the join regardless of whether there is a join partner or not.

**Example:** The following query lists all lectures by their `uosCode` and `year`, and all used classrooms by `classroomId` and number of `seats`.

```sql
SELECT uosCode, year, classroomId, seats
  FROM Lecture
       FULL OUTER JOIN Classroom USING (classroomId)
 ORDER BY uosCode;
```

```
+----------+------+-------------+-------+
| uoscode  | year | classroomid | seats |
+----------+------+-------------+-------+
| COMP5046 | 2010 | SITLT       |    50 |
| COMP5138 | 2010 | FarrelLT    |   190 |
| COMP5138 | 2006 | SITLT       |    50 |
| COMP5338 | 2016 |             |       |
| INFO2005 | 2004 | CAR159      |   290 |
| INFO2120 | 2006 | CAR175      |   160 |
| INFO2120 | 2010 | QuadLT      |   261 |
| INFO2120 | 2009 | CAR159      |   290 |
| INFO3005 | 2005 |             |       |
| INFO3404 | 2008 | CheLT4      |   145 |
|          |      | EAA         |   500 |
|          |      | BoschLT1    |   270 |
|          |      | CAR157      |   290 |
|          |      | CAR173      |   127 |
|          |      | MechLT      |   100 |
|          |      | BoschLT4    |   300 |
|          |      | BoschLT2    |   267 |
|          |      | BoschLT3    |   300 |
|          |      | EALT        |   200 |
+----------+------+-------------+-------+
(19 rows)
```

Since this query uses a `FULL OUTER JOIN`, all lectures will be listed even if they have no classroom assigned yet, as well as all classrooms regardless on whether there is a lecture scheduled there or not.

When there is no join partner for some lecture (on the left) or some classroom (on the right), it is still in the result, but combined with `NULL`s on the other side.

Again, experiment with the given query and see how its result differs if you replace the `FULL OUTER JOIN` with an `INNER JOIN`, a `LEFT OUTER JOIN` or a `RIGHT OUTER JOIN`.

```
Inner Join
+----------+------+-------------+-------+
| uoscode  | year | classroomid | seats |
+----------+------+-------------+-------+
| COMP5046 | 2010 | SITLT       |    50 |
| COMP5138 | 2010 | FarrelLT    |   190 |
| COMP5138 | 2006 | SITLT       |    50 |
| INFO2005 | 2004 | CAR159      |   290 |
| INFO2120 | 2010 | QuadLT      |   261 |
| INFO2120 | 2009 | CAR159      |   290 |
| INFO2120 | 2006 | CAR175      |   160 |
| INFO3404 | 2008 | CheLT4      |   145 |
+----------+------+-------------+-------+
(8 rows)

Left Outer Join
+----------+------+-------------+-------+
| uoscode  | year | classroomid | seats |
+----------+------+-------------+-------+
| COMP5046 | 2010 | SITLT       |    50 |
| COMP5138 | 2006 | SITLT       |    50 |
| COMP5138 | 2010 | FarrelLT    |   190 |
| COMP5338 | 2016 |             |       |
| INFO2005 | 2004 | CAR159      |   290 |
| INFO2120 | 2006 | CAR175      |   160 |
| INFO2120 | 2009 | CAR159      |   290 |
| INFO2120 | 2010 | QuadLT      |   261 |
| INFO3005 | 2005 |             |       |
| INFO3404 | 2008 | CheLT4      |   145 |
+----------+------+-------------+-------+
(10 rows)

Right Outer Join
+----------+------+-------------+-------+
| uoscode  | year | classroomid | seats |
+----------+------+-------------+-------+
| COMP5046 | 2010 | SITLT       |    50 |
| COMP5138 | 2010 | FarrelLT    |   190 |
| COMP5138 | 2006 | SITLT       |    50 |
| INFO2005 | 2004 | CAR159      |   290 |
| INFO2120 | 2006 | CAR175      |   160 |
| INFO2120 | 2010 | QuadLT      |   261 |
| INFO2120 | 2009 | CAR159      |   290 |
| INFO3404 | 2008 | CheLT4      |   145 |
|          |      | BoschLT3    |   300 |
|          |      | EALT        |   200 |
|          |      | EAA         |   500 |
|          |      | BoschLT1    |   270 |
|          |      | CAR157      |   290 |
|          |      | CAR173      |   127 |
|          |      | MechLT      |   100 |
|          |      | BoschLT4    |   300 |
|          |      | BoschLT2    |   267 |
+----------+------+-------------+-------+
(17 rows)
```

### Cast of Films from 2004

Your task is to write an SQL query to return the title of all films released in `2004` and all cast members (`Actor`s) who played in those films. Your query should return the following columns:

1.  Title of the `Film`;
2.  First name of the `Actor`, or `N/A` if the film has no actors; and
3.  Last name of the `Actor`, or `N/A` if the film has no actors.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select title, coalesce(first_name, 'N/A'), coalesce(last_name, 'N/A')
from Film left outer join Film_Actor using(film_id) full outer join Actor using(actor_id)
where release_year = 2004
```

# Set Operations and Cross-Joins

## Set Operations

### SQL Set Operations

SQL allows to combine the results of different queries with standard mathematical set operators. The following set operators are supported:

| Operator    | Meaning                                                      |
| :---------- | :----------------------------------------------------------- |
| `UNION`     | Set union $(r_1 \cup r_2)$                                   |
| `INTERSECT` | Set intersection $(r_1 \cap r_2)$                            |
| `EXCEPT`    | Set difference $(r_1 \backslash r_2)$. Note that in some SQL dialects, notably Oracle, this can be called `MINUS`. |

When using these set operations, it is important to use brackets `( ... )` to correctly group queries between set operators. This is especially important if you want to order the overall result with `ORDER BY` at the end.

**Important to note**

The SQL set operators require that all input relations (i.e. the result of each subquery that is combined with either `UNION`, `INTERSECT`, or `EXCEPT`) have the same schema!

### The `UNION` operator

The `UNION` operator combines the results of two queries using a set union.

The following combines the output of the three static `SELECT` statements, each producing a single row with some example constants:

```sql
  SELECT 1, 'a'
UNION
  SELECT 2, 'c'
UNION
  SELECT 3, 'b'
```

Running this example, you get the output:

```
+----------+----------+
| ?column? | ?column? |
+----------+----------+
|        1 | a        |
|        2 | c        |
|        3 | b        |
+----------+----------+
(3 rows)
```

### The `INTERSECT` operator

The `INTERSECT` operator combines the results of two queries by determining their set intersection.

The following query finds the set of students (by `studentId`) who have both INFO2120 and INFO3005 in their transcript:

```sql
  SELECT studentId
    FROM Enrolled
   WHERE uosCode = 'INFO2120'
INTERSECT
  SELECT studentId
    FROM Enrolled
   WHERE uosCode = 'INFO3005'
```

### The `EXCEPT` operator

The `EXCEPT` operator removes all tuples from the first result set that also exist in the second result set.

The following query finds the set of students (by `studentId`) who have taken INFO2120, but have **not** taken INFO3005 thus far:

```sql
  SELECT studentId
    FROM Enrolled
   WHERE uosCode = 'INFO2120'
         AND grade IS NOT NULL
EXCEPT
  SELECT studentId
    FROM Enrolled
   WHERE uosCode = 'INFO3005'
```

**Note on Oracle**

Note that in Oracle, the syntax differs from the SQL standard. There this set minus operator is called `MINUS`.

### Set Schema Requirement

The set operators require that all input relations have the same schema. In other words, queries that are combined with either `UNION`, `INTERSECT`, or `EXCEPT` need to return their result in the same format.

The following query tries to identify all countries which have at least one actor named 'DEPP':

```sql
(
  SELECT name
    FROM Country
)
INTERSECT
(
  SELECT actor_id, nationality
    FROM Actor
   WHERE last_name = 'DEPP'
)
```

But it seems we made a mistake in the query formulation. Do you see why?

Your task is to write an SQL query which formulates this `INTERSECT` query correctly. Your query should just return the matching country short name(s) as result.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

```sql
select nationality as name
from Actor
where last_name = 'DEPP'
intersect
select short_code
from Country
```

### Ordering of Set Results

The result of the different set operations are naturally *sets* themselves, which means they are returned unordered.

If you need the final result of a set-query in a certain order, you must encapsulate it in a `ORDER BY` clause. The usage of brackets is now important to get the correct scope of the order operation.

**Example:**

```sql
(
  SELECT 'a' AS value
)
UNION
(
  SELECT 'c' AS value
)
UNION
(
  SELECT 'b' AS value
)
ORDER BY value
```

Note that the result of the previous query is ordered alphabetically. What does this differ from the result without `ORDER BY`? Try removing that clause, or simply comment it out by putting two dashes in front of it: `-- ORDER BY value`

### Duplicates in Set Results

By default, the set operations return results without duplicates. If you need to keep all input values, even if they occur multiple times in the result, you can use a set operation with the `ALL` keyword.

**Example 1:** `UNION` by default removes duplicates.

```sql
  SELECT 1, 'a'
UNION
  SELECT 1, 'a'
UNION
  SELECT 2, 'b'
```

**Example 2:** The same query with `UNION ALL` keeps duplicates.

```sql
  SELECT 1, 'a'
UNION ALL
  SELECT 1, 'a'
UNION ALL
  SELECT 2, 'b'
```

The same `ALL` modifier is available to all set operators:

-   `UNION ALL` see above
-   `INTERSECT ALL` keeps duplicates in intersections
-   `EXCEPT ALL` keeps duplicates after set difference

### List all Country and Language names together

Write a SQL query that lists together in one list all names of countries and all names of languages as stored in our database. The list shall be given in alphabetical order.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

```sql
(select name as name from Country)
union all
(select name as name from Language)
order by name
```

###  Find films that have two categories

Write an SQL query that finds all films (by `film_id` and `title`) categorised as both `Drama` and `Family` film.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

```sql
select film_id, title
from Film natural join Film_Category natural join Category
where name = 'Drama'
intersect
select film_id, title
from Film natural join Film_Category natural join Category
where name = 'Family'
```

## Cartesian Product

### Cartesian Product

Another way of combining tuples from two tables is by computing the *cartesian product*. The simplest way is by simply naming two relations in the `FROM` clause without any further join condition.

**Example:** The following lists all possible combinations of studentIds as found in the `Student` table.

```sql
  SELECT S1.studentId AS Id1, S2.studentId AS Id2
    FROM Student S1, Student S2
```

### The `CROSS JOIN` operator

While often the unintended side-effect of a wrongly formulated join query, sometimes we indeed would like to combine *all* tuples of two given relations with the *cartesian product*.

The corresponding SQL operator is the `CROSS JOIN`.

**Example:** The same query from the previous slide, now formulated with a CROSS JOIN.

```sql
  SELECT S1.studentId AS Id1, S2.studentId AS Id2
    FROM Student S1 CROSS JOIN Student S2
```

### Finding Duplicate Actors

Your task is to write an SQL query that finds all entries in the Actor table where the `first_name` and `last_name` are the same as another actor's first and last names. For example:

```
+----------+------------+------------+
| actor_id | first_name | last_name  |
+----------+------------+------------+
|        1 | JOHN       | APPLESEED  |
|       22 | JOHN       | APPLESEED  |
|       32 | MARK       | ZUCKERBERG |
|       44 | MARK       | ZUCKERBERG |
+----------+------------+------------+
(4 rows)
```

Your query's result table must contain these columns:

1.  `actor_id`;
2.  `first_name`; and
3.  `last_name`.

The results should be listed in alphabetical order by `first_name` and `last_name`, then in increasing order by `actor_id` for actors with the same names.

Try to use SQL's `CROSS JOIN` operator in your answer!

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select A.actor_id, A.first_name, A.last_name
from Actor A cross join Actor B
where A.first_name = B.first_name and A.last_name = B.last_name and A.actor_id != B.actor_id
order by first_name, last_name, actor_id
```

# Math and String Operations

## Mathematical Functions and Operators

### Working with Numbers and Strings

A common task in an SQL query is to compute some values based on data stored in the database. Database systems provide a variety of functions to do so, depending on the different data types.

-   Numerical Data

    SQL supports an [extensive variety of mathematical operators and functions](http://www.postgresql.org/docs/current/static/functions-math.html) to work with numerical data (integers and floating point numbers).

-   String Data

    An almost even [longer list of string operators and functions](http://www.postgresql.org/docs/current/static/functions-string.html) allows to converted, format, concatenated and pattern match text data.

### Mathematical operators in `SELECT`

You can use a number of mathematical operators directly in any `SELECT` or `WHERE` clause. The core operators are as follows:

| Operator | Meaning       | Example         | Result |
| :------- | :------------ | :-------------- | :----- |
| `+`      | addition      | `SELECT 10 + 2` | `12`   |
| `-`      | subtraction   | `SELECT 10 - 2` | `8`    |
| `*`      | multipication | `SELECT 7*6`    | `42`   |
| `/`      | division      | `SELECT 42/7`   | `6`    |

You can use those operators to compute complex mathematical expression as part of an SQL query. Let's have a look at an example:

```sql
SELECT 1050 * (1 + 0.10) AS "price incl GST"
```

For further operators supported by PostgreSQL see [its documentation about its mathematical functions and operators](http://www.postgresql.org/docs/current/static/functions-math.html).

**Note for Oracle users**

While PostgreSQL allows to directly use the `SELECT` statement to evaluate a mathematical expression, in Oracle you always have to select `FROM` some table. The usual workaround with Oracle is that there's a standard single-row table in every Oracle instance, called `Dual` that can be used to let Oracle run a `SELECT` query exactly once. The same example query in Oracle syntax:

```sql
SELECT 1050 * (1 + 0.10) AS "price incl GST"
  FROM Dual
```

### Mathematical functions in SQL

SQL provides a number of mathematical functions to be used in the `SELECT` or the `WHERE` clause:

-   `mod(a, b)`

    Computes the remainder of `a / b`.

-   `round(n, d)`

    Rounds `n` to `d` decimal places.

-   `trunc(n, d)`

    Truncates `n` to `d` decimal places.

-   `ceil(n)`

    Computes the smallest integer value not less than `n`.

-   `floor(n)`

    Computes the largest integer value not greater than `n`.

-   `abs(n)`

    Computes the absolute value of `n`.

Here's an example of the above functions:

```sql
SELECT mod(15, 4), round(15.67, 1),
       trunc(15.67, 1), ceil(15.67),
       floor(15.67), abs(-121.4)
```

When run, this query produces the following output:

```
+-----+-------+-------+------+-------+-------+
| mod | round | trunc | ceil | floor |  abs  |
+-----+-------+-------+------+-------+-------+
|   3 |  15.7 |  15.6 |   16 |    15 | 121.4 |
+-----+-------+-------+------+-------+-------+
(1 row)
```

### NaN` versus `NULL

SQL supports a few special values for floating point data:

-   NaN

    not-a-number

-   infinity

    infinity, larger than any number

-   -infinity

    negative infinity, smaller than all numbers

All these special values have to be given as a string in SQL, so eg. 'NaN or 'infinity', even when addressing a `FLOAT` attribute.

What is the difference between NaN and NULL? Let's have a look:

 ``` sql
 CREATE TABLE Test ( val FLOAT );
 INSERT INTO  Test VALUES (0), ('NaN'), (NULL);

 \pset null '[NULL]'
 SELECT * FROM Test;
 SELECT * FROM Test WHERE val IS NULL;
 ```

```
CREATE TABLE
INSERT 0 3
+--------+
|  val   |
+--------+
|      0 |
|    NaN |
| [NULL] |
+--------+
(3 rows)
+--------+
|  val   |
+--------+
| [NULL] |
+--------+
(1 row)
```

As you see, `NaN` is not considered `NULL`, but it is also no valid number, as any comparison with a real number will be false. Try it with different values in above's example.

**Note**

In most implementations of the "not-a-number" concept, `NaN` is not considered equal to any other numeric value (including `NaN`). In order to allow numeric values to be sorted, PostgreSQL treats NaN values as equal, and greater than all non-NaN values though...

This leads to the following comparison table where all these special values compare to themselves but not to `NULL`, nor matches `NULL` itself:

```sql
CREATE TABLE Test ( v FLOAT );
INSERT INTO  Test VALUES
  (0),(1),(-1),('NaN'),('infinity'),('-infinity'),(NULL);
SELECT * FROM Test A, Test B WHERE A.v=B.v;
```

Note how the code inserted *seven* values, including a NULL, and what the self-join query, that checks for `v=v`, then returns.

### R-rated Chronography

Your task is to write an SQL query to calculate the length of every `'R'`-rated `Film` in `hours` and `minutes`. Your query's result must have the following columns:

1.  `film_id` of the `Film`;
2.  `title` of the `Film`;
3.  `hours` - length of the `Film` in hours; and
4.  `minutes` - length of the `Film` in minutes.

The results should be listed in decreasing order of film length.

**Reminder:** The values stored for `Film.length` are in minutes.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, length / 60 as hours, mod(length, 60) as minutes
from Film
where rating = 'R'
order by length desc
```

### A Slice of Pi

The number π (Pi) is used in many types of calculations, such as finding the area of a disc. Pi has an infinite number of digits after its decimal point, so calculations involving π typically use an approximation of 3 to 6 significant figures - eg. 3.14 is Pi with 3 significant figures.

One simple formula for approximating the value of π is dividing 355 by 113. Your task is to write a `SELECT` statement that computes π with 3, 4 and 5 significant figures using this division technique. Try to make your query as simple as possible. The naming of the result columns is irrelevant for this question.

**Note:** Pi does not usually get rounded! In mathematics, these types of numbers (infinite series) are used in computations with a certain precision without any form of rounding, but with as many positions of the infinite series after the decimal point as required.

**Automatic data type conversions**

Be aware that some DBMSs behave differently regarding automatic data type conversions. In PostgreSQL, a division of two `Integer` values yields an `Integer` result, ignoring any remainder: e.g. `2 / 3 = 0`

In PostgreSQL you can force a decimal result by supplying decimal input values: e.g. `2.0 / 3.0 = 0.66667`

Oracle does this differently to PostgreSQL; it always converts a fractional result to a real number: e.g. `2 / 3 = 0.66667`

``` sql
select trunc(355.0 / 113.0, 2) as pi_2dec, trunc(355.0 / 113.0, 3) as pi_3dec, trunc(355.0 / 113.0, 4) as pi_4dec
```

### `SERIAL` Type

PostgreSQL supports one special type for attributes which are artificial, unique identifiers: `SERIAL`

A `SERIAL` can be treated as an `integer` value in most circumstances, but is especially useful for creating tables and inserting new data, as PostgreSQL will automatically create a new value for each new insert.

```sql
CREATE TABLE Test (
    id  SERIAL,
    val CHAR
);
INSERT INTO Test(val) VALUES ('a'), ('b');
SELECT * FROM Test;
```

Note that we did not provide any value for 'id' in above's insert statement. When run, this query produces the following output:

```
CREATE TABLE
INSERT 0 2
+----+-----+
| id | val |
+----+-----+
|  1 | a   |
|  2 | b   |
+----+-----+
(2 rows)
```

The `SERIAL` type is actually not a real type, but a mere syntax convenience to easily specify a table attribute that is connected with an internal counter which produces strictly monotonically increasing values for each new entry. The technical details can be found in the [corresponding section of the PostgreSQL documentation](http://www.postgresql.org/docs/9.2/static/datatype-numeric.html#DATATYPE-SERIAL).

## String Operations and Functions

### String Operators in `SELECT`

There are a number of string operators and functions available in the `SELECT` clause. The core operators and functions are as follows:

| Item       | Meaning                          | Example                         | Result          |
| :--------- | :------------------------------- | :------------------------------ | :-------------- |
| `||`       | String concatenation             | `SELECT 'Hello, ' || 'world!'`  | `Hello, world!` |
| `lower(s)` | Convert string `s` to lower case | `SELECT lower('Hello, world!')` | `hello, world!` |
| `upper(s)` | Convert string `s` to upper case | `SELECT upper('Hello, world!')` | `HELLO, WORLD!` |

Here's a larger example of the string concatenation operator to formualte whole names for people from their first and last names:

```sql
SELECT first_name || ' ' || last_name AS name
  FROM Student
```

For further operators supported by PostgreSQL see [its documentation about its string operators and functions](http://www.postgresql.org/docs/current/static/functions-string.html).

### Concatenated Names

Your task is to write an SQL query to list the `actor_id` and `fullname` of every `Actor` whose `last_name` begins with `'A'`. The name of each `Actor` should be given as a single value in the format

```
<LAST NAME>, <FIRST NAME>
```

For example:

```
+----------+---------------------+
| actor_id |      fullname       |
+----------+---------------------+
|        1 | APPLESEED, JENNIFER |
|       25 | ANGIE, JUDY         |
       ...   ...
```

Your query's result must have the following columns:

1.  `actor_id`; and
2.  `fullname` - in the format given above.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select actor_id, last_name || ', ' || first_name as fullname
from Actor
where last_name like 'A%'
```

# Dates and Time

## Date Types and Values in SQL

### Handling dates and times in SQL

SQL supports several data types and function to handling date and time in SQL.

The following data types available to store date and time values in relational databases:

| Data type   | Description     | Example value                     |
| :---------- | :-------------- | :-------------------------------- |
| `DATE`      | A date          | `'2011-04-03'`                    |
| `TIME`      | A time          | `'19:14:06.977434+11'`            |
| `TIMESTAMP` | A date and time | `'2011-04-03 19:14:33.974799+11'` |

### Using date and time types

Let's look at an example. The following code creates an `Orders` table with an ordering date and an update timestamp, then performs an `INSERT` and `SELECT` using the new table:

```sql
CREATE TABLE Orders (
   orderId     INTEGER PRIMARY KEY,
   customer    VARCHAR(50),
   value       FLOAT,
   orderDate   DATE,
   lastUpdated TIMESTAMP
);

INSERT INTO Orders
VALUES
  (1, 'USyd', 125.56, CURRENT_DATE, CURRENT_TIMESTAMP);

SELECT orderDate, lastUpdated
  FROM Orders;
```

As you can see, we successfully inserted the `CURRENT_DATE` and `CURRENT_TIMESTAMP` for our new order.

### Date and time constants

PostgreSQL provides access to a number of date and time constants. Some of them are shown below:

-   `CURRENT_DATE`

    The date component of the current system time.

-   `CURRENT_TIME`

    The time component of the current system time.

-   `CURRENT_TIMESTAMP`

    The full current system time.

-   `NOW()`

    A function alias for `CURRENT_TIME`.

### Using date and time constants

Let's have a look at an example of how you use the date and time constants. Try running the following example:

```sql
SELECT CURRENT_TIMESTAMP;
```

As you can see, this returns the current timestamp. Note that our servers work with [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time), so the time might be off by 10-11 hours from Sydney.

For more information, see the [online documentation of PostgreSQL on date types and functions](http://www.postgresql.org/docs/current/static/functions-datetime.html).

**Note for Oracle users**

In Oracle, every query needs a `FROM` clause, so the above query becomes:

```sql
SELECT CURRENT_TIMESTAMP
FROM Dual;
```

### Film Screenings

Your task is to write an SQL DDL `CREATE TABLE` statement that extends our film database by adding a new table called `Film_Screening` to store information about film screenings (i.e. when and where a particular film is being shown). This new table must have the following columns:

1.  `screening_id` - a unique identifier for each screening;
2.  `film_id` - the ID of the `Film` being screened (foreign key, must be given);
3.  `theatre` - the name of the theatre where the screeening will take place (maximum of 50 characters);
4.  `start_time` - the date and time of the screening (must be given);
5.  `film_start` - the time the film actually starts (after any pre-film advertisements finish);
6.  `last_tickets` - the last possible date to buy tickets for the screening.

You need to make use of three different SQL date/time types in your DDL statement.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
create table Film_Screening (
    screening_id int primary key,
    film_id int references Film(film_id) not null,
    theatre varchar(50),
    start_time timestamp not null,
    film_start time,
    last_tickets date
)
```

## Working with Dates and Times

### SQL's `EXTRACT` function

SQL's `EXTRACT` function provides access to the individual time fields of a `DATE`, `TIME` or `TIMESTAMP` value. The general syntax for it is:

```sql
EXTRACT(<component> FROM <date_or_time_value>)
```

The `EXTRACT` function supports the following parameters for `<component>`:

| Component | Meaning                                                      |
| :-------- | :----------------------------------------------------------- |
| `DAY`     | Retrieve the **day** of a `DATE` or `TIMESTAMP` value.       |
| `MONTH`   | Retrieve the **month** of a `DATE` or `TIMESTAMP` value.     |
| `YEAR`    | Retrieve the **year** of a `DATE` or `TIMESTAMP` value.      |
| `HOUR`    | Retrieve the **hour** of a `TIME` or `TIMESTAMP` value.      |
| `MINUTE`  | Retrieve the **minute** field of a `TIME` or `TIMESTAMP` value. |
| `SECOND`  | Retrieve the **second** of a `TIME` or `TIMESTAMP` value.    |

Some database systems support even more detailed specifications of individual time component, for example for `TIMEZONE` and `DOY` (day-of-the-year). The above should basically always work.

Note that this function supports different field specifications depending on which database system you work with. You can find further information about the `EXTRACT` function in [the online documentation of PostgreSQL](http://www.postgresql.org/docs/current/static/functions-datetime.html#FUNCTIONS-DATETIME-EXTRACT). More details on the Oracle support of `EXTRACT` [can be found here](http://download.oracle.com/docs/cd/B19306_01/server.102/b14200/functions050.htm).

### Using `EXTRACT`

Let's have a look at some examples of using the `EXTRACT` function. Get the details of all orders that have been placed in the year 2011:

```sql
SELECT *
  FROM Orders
 WHERE EXTRACT(year FROM orderDate) = 2011
```

Retrieve the day of a given order:

```sql
SELECT EXTRACT(day FROM orderdate)
  FROM Orders
 WHERE orderid = 123456789
```

Determine the average order values per month in the year 2011:

```sql
SELECT AVG(orderValue)
  FROM Orders
 WHERE EXTRACT(year FROM orderDate) = 2011
 GROUP BY EXTRACT(month FROM orderDate)
```

### Films from the Decade

Your task is to write an SQL query that determines the number of films that have been released in the last 10 years (including the current year).

Your query's result should have a single column called `count`.

**Note**: Do not assume a specific year for your query. Write a generic query using the current system clock so that the same query would also work next year without modification.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(film_id)
from Film
where extract(year from current_timestamp) - release_year between 0 and 9;
```

### Leap Films

Your task is to write an SQL query that determines the number of films that were released in a *[leap year](https://en.wikipedia.org/wiki/Leap_year)*. Your query's result should have a single column called `count`.

**Hint**

In PostgreSQL, you can extract the day of the year from a date string like this:

```sql
SELECT EXTRACT(DOY FROM DATE '2016-04-22');
```

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select count(film_id)
from Film
where extract(doy from date (
    concat(release_year, '-12-31')
)) = 366
```

## Time Zones

### Time zones in SQL

In today's global usage of information systems, it is important to distinguish in which time zone a user application is running versus in which time zone the database server is working. This is especially valid for Australia, where even within the same country, we have several timezones...

SQL has a couple of time-related data types and constants, some of which support local time zones. In some SQL databases, this comes automatic (e.g. the `CURRENT_TIMESTAMP` constant or PostgreSQL's `NOW()` function), in some you have to explicitly specify it (e.g. in a `CREATE TABLE` statement with a data type `TIMESTAMP WITH TIME ZONE`).

For example, you can ask PostgreSQL to give you the time in a specific time zone with the `AT TIME ZONE` option. PostgreSQL supports [all standard time zone names](http://www.postgresql.org/docs/7.2/static/timezones.html). For example, to get the current time in 'Australia Eastern Standard Time' (AEST):

```sql
SELECT CURRENT_TIMESTAMP AT TIME ZONE 'AEST';
```

### Time zone support in `EXTRACT`

SQL's `EXTRACT` allows us to extract time zone information from `TIME` and `TIMESTAMP` values:

| Component         | Meaning                                                      |
| :---------------- | :----------------------------------------------------------- |
| `TIMEZONE`        | Retrieve the timezone offset from UTC in seconds of a `TIMESTAMP` value. |
| `TIMEZONE_HOUR`   | Retrieve the hour component of the timezone offset from UTC of a `TIMESTAMP` value |
| `TIMEZONE_MINUTE` | Retrieve the minute component of the timezone offset from UTC of a `TIMESTAMP` value. |

The above should work for different database systems, e.g. PostgreSQL and Oracle in our case. If in doubt, check the online documentation of your specific database system.

### Examples

Let's have a look at a concrete example of extracting time zone information using the `EXTRACT` function. Get the details of all orders that have been placed in the timezone 'UTC+10:00':

```sql
SELECT *
  FROM Orders
 WHERE EXTRACT(timezone_hour FROM orderTime) = 10
   AND EXTRACT(timezone_minute FROM orderTime) = 0
```

Retrieve the time zone offset (in seconds) of the server's current timestamp:

```sql
SELECT EXTRACT(timezone FROM CURRENT_TIMESTAMP);
```

Another approach is using the SQL `to_char()` function which also allows to convert a `TIMESTAMP` into a string with some control on how this can be done. Furthermore, some parameters allow tight control on how numbers are converted into strings, e.g. with leading plus or minus sign, or formatted with leading 0's etc.

### Find the Server's Timezone

Your task is to write an SQL query that uses SQL's time constants to dynamically determine the timezone the database server is configured to use.

Your query should return the timezone as a single string value with the timezone offset relative to the [Coordinated Universal Time (UTC)](https://en.wikipedia.org/wiki/Coordinated_Universal_Time). The single output column should be named `tz_offset`, and the value should be in the form:

```
UTC<SIGN><HOURS>:<MINUTES>
```

where `<HOURS>` and `<MINUTES>` use two digits in 24-hour format, padded with leading zeroes if necessary.

**Example:** if the server used India's timezone the output should be:

```
+-----------+
| tz_offset |
+-----------+
| UTC+05:30 |
+-----------+
(1 row)
```

``` sql
select 'UTC' ||
left(to_char(current_timestamp, 'tz'), 1) ||
-- only display sign

right('0' || abs(extract(timezone_hour from current_timestamp)), 2) ||
-- only display hour
-- some hour also include sign, so we need abs() here
-- concat '0' in order to prevent some hour only have one digit

':' ||

right('0' || extract(timezone_minute from current_timestamp), 2)
-- only display minute
-- concat '0' in order to prevent some minumte only have one digit

as tz_offset
```

# SQL Subqueries

## Nesting SQL Queries

### Nesting SQL Queries

Some complex questions can best be answered by using subqueries. You can nest SQL queries within each other at basically every clause of a SFW-statement (see below for examples).

Subqueries can be *co-related* or *non co-related* with the outer query.

### Co-related subqueries

A *co-related* subquery is executed for each tuple of the outer query. This means that its search condition refers to at least one attribute of the outer query.

The following checks for each student `S` whether there is at least one entry in the `Enrolled` table for that student in INFO2120:

```sql
SELECT studentId, name
  FROM Student S
 WHERE EXISTS (SELECT *
                 FROM Enrolled E
                WHERE E.studentId = S.studentId
                      AND uosCode = 'INFO2120')
```

Note how the inner sub-query is co-related with the outer query by the use of `S.studentId` in its `WHERE` clause. `S` is the name of the relation in the outer query.

### Non-co-related subqueries

A *non-co-related* subquery is executed only once and then its result used for all tuples of the outer query.

This example is the same as the one on the previous slide, but with a non-co-related subquery. Note how the student tuples of the outer SFW-query (SFW: SELECT-FROM-WHERE) are not used in the inner SFW-query:

```sql
SELECT studentId, name
  FROM Student
 WHERE studentId IN (SELECT E.studentId
                       FROM Enrolled E
                      WHERE E.uosCode = 'INFO2120')
```

### Subqueries in the `FROM` clause

Subqueries can basically used everywhere in an SQL query, in particular they are not restricted to the `WHERE` clause.

**Example:** Here's an example of a subquery in the `FROM` clause.

```sql
SELECT name
  FROM (SELECT studentId, name, grade
          FROM Student
               JOIN Enrolled USING (studentId)) AS E
 WHERE grade = 'HD'
```

Note that PostgreSQL requires you to give the result of a sub-query in the `FROM` clause a name using the `AS` rename operator.

### Subqueries in the `WHERE` clause

Here's another example of a subquery in the `WHERE` clause.

**Example:** This query retrieves the student who has the best mark in INFO2120 2010sem1.

```sql
SELECT studentId, name
  FROM Student
       JOIN Enrolled USING (studentId)
 WHERE uosCode  = 'INFO2120'
       AND year = 2010
       AND semester = 'S1'
       AND grade = (SELECT MAX(grade)
                      FROM Enrolled
                     WHERE uosCode  = 'INFO2120'
                           AND year = 2010
                           AND semester = 'S1')
```

### Cheapest Rentals from 2006

Suppose we want to find the cheapest films to rent of those released in `2006` (i.e. with the lowest `rental_rate`). We try to use the following SQL query:

```sql
SELECT film_id, title
  FROM Film
 WHERE rental_rate = MIN(rental_rate)
       AND release_year = 2006
 ORDER BY title;
```

However, this query **gives an error** when we run it!

Your task is to write an SQL query that correctly finds the `film_id` and `title` of every `Film` released in `2006` which has the lowest `rental_rate` for films released in `2006`.

The results should be listed in alphabetical order by `title`.

**Note** that we are interested in the lowest rental rate of films *released in 2006*, not the lowest rental rate of *all* films!

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title
from Film
where release_year = 2006 and rental_rate = (
    select min(rental_rate)
    from Film
    where release_year = 2006
)
order by title
```

### Film Casts with Penelope Guiness

Your task is to write an SQL query that returns the full cast of every `Film` in which `'PENELOPE GUINESS'` played. Your query's result should contain the following attribtues:

1.  `film_id`;
2.  `title`;
3.  `actor_id`;
4.  `first_name`; and
5.  `last_name`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, actor_id, first_name, last_name
from Film natural join Film_Actor natural join Actor
where film_id in (
    select film_id
    from Film_Actor natural join Actor
    where first_name = 'PENELOPE' and last_name = 'GUINESS'
)
```

## EXISTS and NOT EXISTS

### Subqueries with `EXISTS`

You can use another SQL query within the `WHERE` clause of an SQL query. The most common usage is to check whether a certain complex condition is true with regard to the current query value using the `EXISTS` (or reverse: `NOT EXISTS`) operator.

Let's look at an example of using `EXISTS` with a subquery. The following query retrieves the `studentId` and `name` of each student where the subquery can find at least one `Enrolled` entry with an HD grade for the corresponding student:

```sql
SELECT studentId, name
  FROM Student S
 WHERE EXISTS (SELECT *
                 FROM Enrolled E
                WHERE E.studentId = S.studentId
                      AND E.grade = 'HD')
```

This is a so-called *co-related subquery* which tests the inner condition, that there is a HD, for each student of the outer query (Cf. condition `E.studentId = S.studentId`).

### Films from 2000

Your task is to write an SQL query that lists all films that were released in the year `2000` and have *at least one person acting in them*. Your query's result should contain the following columns, with the results in alphabetical order by `title`:

1.  `film_id`; and
2.  `title`.

Try to make use of a subquery in your answer!

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title
from Film F
where exists (
    select *
    from Film_Actor FA
    where F.film_id = FA.film_id
) and release_year = 2000
order by title
```

### Subqueries with `NOT EXISTS`

Similarly, here's an example of `NOT EXISTS` with a subquery. The following query retrieves the `studentId` and `name` of all students who never failed any subject:

```sql
SELECT studentId, name
  FROM Student S
 WHERE NOT EXISTS (SELECT *
                     FROM Enrolled E
                    WHERE E.studentId = S.studentId
                          AND E.grade = 'F')
```

### Films without Actors

Your task is to write an SQL query that lists every `Film` which has *nobody acting in it*. Your query's result should contain the following columns, with results listed in ascending order of the `film_id`:

1.  `film_id`;
2.  `title`; and
3.  `release_year`.

Try to make use of a subquery in your answer!

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, release_year
from Film F
where not exists (
    select *
    from Film_Actor FA
    where F.film_id = FA.film_id
)
order by film_id
```

# Grouping and Filtering

## Grouping Results

### Grouping with `GROUP BY` (I)

Some questions, such as when computing some statistics about a data set, require to compare different subsets of the data. A simple `SELECT-FROM-WHERE` cannot do this as it computes any statistics (such as `AVG` or `COUNT` functions) for all data at once.

What we need instead is a mechanism for *grouping* of co-related data sets together and then to compute the statistics per each group. This is what SQL's `GROUP BY` clause is for.

### Grouping results `GROUP BY` (II)

SQL's `GROUP BY` clause allows to partition a query results into groups of values that have some common attributes, and to combine than those groups together into one result row (typically using some aggregate functions). The general syntax is as follows:

```sql
  SELECT <result_list>
    FROM <relation(s)>
   WHERE <condition>
GROUP BY <list_of_attributes>
```

The following query lists all units of study (`uos_code`) from the last ten years together with how many students were enrolled in each of the units:

```sql
SELECT uosCode, COUNT(studentId) AS enrolments
  FROM Enrolled
 WHERE year >= 2006
 GROUP BY uosCode
```

### Grouping attributes (I)

Grouping means that we are combining all rows within the same group to just one result row. This is only possible if the column values that are listed in the result row are the same for the whole group. This means that we can only list two kinds of columns in the result of a `GROUP BY` query:

1.  Table attributes by which the group is defined. That is, anything that is listed in the `GROUP BY` clause.
2.  Aggregate values that are computed from all rows within the same group (e.g. using `COUNT(*)` or `SUM(...)`).

### Grouping attributes (II)

Note in particular you cannot list an attribute in the `SELECT` clause of a grouping query that is not at the same time also listed behind `GROUP BY`. For example, the following query **will not** work:

```sql
SELECT uosCode, year, COUNT(studentId)
  FROM Enrolled
 WHERE year >= 2006
 GROUP BY uosCode
```

The reason is that one of its result attributes listed in the `SELECT` clause (the `year`) is not used for the grouping. Hence the database system cannot guarantee that there we be only one year for all the rows within the same group. This is not allowed.

To make this example query work, you need to ensure that all attribute names which are listed behind `SELECT` are also listed behind `GROUP BY`. So above's query is correct as follows:

```sql
SELECT uosCode, year, COUNT(studentId)
  FROM Enrolled
 WHERE year >= 2006
 GROUP BY uosCode, year
```

### Release Year Stats

Your task is to write an SQL query that lists how many `Film`s were released in each `release_year`. Your query should output the following columns:

1.  `release_year`; and
2.  `number_of_films` - the number of films released in this year.

The result should be ordered with the most popular years first; years with the same number of films should be listed chronologically.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select release_year, count(film_id) as number_of_films
from Film
group by release_year
order by number_of_films desc, release_year
```

### Film Category Usage

Your task is to write an SQL query that determines the usage of `Film` categories throughout our database. Your query result shall have three columns:

1.  `category_id`;
2.  `name` of the `Category`;
3.  `count` of films that belong to this `Category` (or zero if there are none).

The result shall be ordered with the most frequent categories first, then less frequent categories. Categories with the same `count` shall be further ordered alphabetically by `name`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select category_id, name, count(Film_Category.film_id)
from Category full outer join Film_Category using (category_id)
group by category_id, name
order by count desc, name
```

## Filtering Groups with HAVING

### Filtering Groups with `HAVING`

We have already looked at at SQL's `GROUP BY` clause that allows uys to partition a query results into groups of values that have some common attributes. The `HAVING` clause further extends this by allowing us to specify a filter condition that each group must fulfil in order to be processed.

The general `SELECT` query syntax is as follows:

```sql
  SELECT <result_list>
    FROM <relation(s)>
   WHERE <per_tuple_condition>
GROUP BY <list_of_attributes>
  HAVING <per_group_condition>
```

It is important to note that the role of `HAVING` is different than what the `WHERE` clause is doing:

-   the `WHERE` clause filters *individual tuples* **before** they are grouped via `GROUP BY`
-   the `HAVING` clause filters *whole groups* **after** they have been formed with `GROUP BY`

### An example use of `HAVING`

The following query lists all units of study (`uosCode`) from the last ten years together with how many students are enrolled in each of the units, *that have at least 2 students enrolled*:

```sql
  SELECT uosCode, COUNT(studentId) AS enrolments
    FROM Enrolled
   WHERE year >= 2010
GROUP BY uosCode
  HAVING COUNT(studentId) >= 2
```

### Filtered Nationality Stats

Your task is to write an SQL query that lists all `Actor` nationalities and how many actors are of each `nationality`. **Only show nationalities with \*at least 2\* associated actors.**

The results must be in descending order by number of actors (i.e. the most frequent nationality first), and then for nationalities with the same number of actors, alphabetically by `nationality`. Your query should thus output two columns:

1.  The `nationality` short code; and
2.  Number of actors associated with this nationality.

The naming of the result columns is irrelevant in this question.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select nationality, count(nationality)
from Actor
group by nationality
having count(nationality) >= 2
order by count desc, nationality
```

### At Least Five Actors

Your task is to write an SQL query that lists every `Film` which has at least five actors playing in it. Your query result should have three columns:

1.  `film_id` of the `Film`;
2.  `title` of the `Film`; and
3.  `count` - number of `Actor`s who played in this `Film`.

Your query's results should be in alphabetical order by `title`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, count(actor_id)
from Film natural join Film_Actor
group by film_id, title
having count(actor_id) >= 5
order by title
```

# Limiting and Ranking Results

## Limiting the Output Size

### Limiting the output size

Many DBMS (though not all) support a `LIMIT` clause to restrict the size of the output to a pre-defined number of tuples. This clause would come at the end of a SFW-query:

```sql
SELECT <expression>
  FROM <tables>
 WHERE <condition>
 ORDER BY <sort_expression>
 LIMIT <positive_integer>
```

### An example use of `LIMIT`

The following list the top three students of an MATH1001 class (assuming that `grade` is a numerical score!):

```sql
SELECT sid, name, grade
  FROM Student
       JOIN Transcript USING (sid)
 WHERE uos_code = 'MATH1001'
 ORDER BY grade DESC
 LIMIT 3
```

See the [PostgreSQL online documentation about the `LIMIT` clause](http://www.postgresql.org/docs/current/static/sql-select.html#SQL-LIMIT) for further syntax details of this clause.

### Don't Lose that Film!

Your task is to write an SQL query to find the the `Film` with the highest `replacement_cost`. Your query should only return a single result row, with the following columns:

1.  `title` of the `Film`; and
2.  `replacement_cost` of the `Film`.

If there are several films with the highest value for `replacement_cost`, then your query can return any one of these.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select title, replacement_cost
from Film
order by replacement_cost desc
limit 1
```

### Top Five Actor Nationalities

Your task is to write an SQL query to list the names of the top-5 countries, according to the number of `Actor`s who are of that `nationality`. Your query's result should have the following columns:

1.  `country` - the `name` of the `Country`; and
2.  `num_actors` - the number of `Actor`s who have this `Country` as their `nationality`.

Furthermore, the results should be listed in decreasing order by `num_actors`. Any countries with the same number of actors should be further sorted in alphabetical order by their names.

**Hint**

`Actor.nationality` is a foreign key referencing `Country.short_code`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select name as country, count(actor_id) as num_actors
from Actor inner join Country on nationality = short_code
group by country
order by num_actors desc, country
limit 5
```

## Top-N Queries

### Top-N queries in SQL

So-called top-n queries determine the top n result tuples for a given condition. There are two approaches to compute such queries in SQL.

### Top-N with `ORDER BY` and `LIMIT`

The straight-forward approach is to use a combination of `ORDER BY` and `LIMIT` to first order the result by the ranking condition, and then restrict the result to the specified n top result rows.

For example, here's a query to find the top 3 students in INFO1903:

```sql
SELECT sid, name
  FROM Student
       NATURAL JOIN Enrolled
 WHERE uos_code = 'INFO1903'
 ORDER BY mark DESC   -- assuming a numerical mark column
 LIMIT 3
```

There's one limitation with this approach in that it cannot give any running number (rank) to each result row. As such, if we want to have '#1' next to the best student and then '#2' with the next, we need to look into SQL's new *window functions*.

### Top Ten American Actors

Your task is to write an SQL query that lists the top-10 `Actor`s from the `'US'` according to the number of `Film`s they have played in. Your query's result must have the following columns:

1.  `first_name` of the `Actor`;
2.  `last_name` of the `Actor`; and
3.  `films` - number of `Film`s the `Actor` has played in.

Your query should produce an *ordinal ranking* in descending order by number of films. For actors who played in the same number of films, show those in alphabetical order of their name (first and last name).

Note that we are asking for an [ordinal ranking](https://en.wikipedia.org/wiki/Ranking), meaning even if two actors played in the same number of films, they should be considered as separate entries within the top-10 list.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select first_name, last_name, count(film_id) as films
from Film_Actor natural join Actor
where nationality = 'US'
group by actor_id, first_name, last_name
order by films desc, first_name, last_name
limit 10
```

### Top-N with window functions

Another, more sophisticated approach uses a recent extension to SQL (which we will cover in the OLAP section later on). The so-called *window functions* are new extensions in SQL:1999 that allow to compute aggregate over a set of values *relative to the current row*. These windows can be ordered and there is also a new `rank()` function that gives each entry a number of which rank it has regarding to a window.

For example, here's a query to calculate the top 3 students with rank using SQL's new window function:

```sql
SELECT sid, name, rank() OVER (ORDER BY mark DESC)
  FROM Student
       NATURAL JOIN Enrolled
 WHERE uos_code = 'INFO1903'
 LIMIT 3
```

The above query just produces one window over actually all rows of the INFO1903 class list, and then orders the tuples in that 'window' according to descending mark. The `rank()` function than numbers those rows through from 1 to n.

The PostgreSQL online documentation gives some further information on [the `LIMIT` clause](http://www.postgresql.org/docs/current/static/sql-select.html#SQL-LIMIT) and [the SQL window functions](http://www.postgresql.org/docs/current/static/tutorial-window.html).

### Ranking Film Categories

Your task is to write an SQL query to produce a ranked listing of the top-5 categories according to how many films are associated with each category. Your query's result must have the following columns:

1.  `rank` - the ranking of the `Category`;
2.  `category` - the `name` of the `Category`; and
3.  `films` - the number of films belonging to the `Category`.

The results should be ordered primarily by `rank` in increasing order, then alphabetically by `name` (for any categories which have the same ranking).

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select rank() over (order by count(film_id) desc) as rank,
    name as category,
    count(film_id) as films
from Film_Category natural join Category
group by name
order by rank, name
limit 5
```

# SQL Conditional Expressions

## Conditional Expressions

### SQL's `CASE` statement

Most SQL dialects allow to retrieve certain values based on a conditional expression in the `SELECT` clause of a query. These are achieved using the `CASE` statement. These `CASE` expressions allow to output different results based on a known set of input values.

The general syntax for `CASE` is:

```sql
SELECT  CASE WHEN <condition1> THEN <expr>
             WHEN <condition2> THEN <expr>
             ...
             ELSE <expr>
        END
  FROM ...
```

### `CASE` in Oracle

In Oracle, the `DECODE()` function solves the same problem as PostgreSQL's `CASE` operator.

For example, the same example as the previous slide using `DECODE()` is:

```sql
SELECT sid, name, decode(gender, 'M', 'male', 'F', 'female', 'other')
  FROM Student
```

### An example use of `CASE`

The following query lists the names and genders of students, where the gender is decoded into a more readable form:

```sql
SELECT sid, name, CASE WHEN gender='M' THEN 'male'
                       WHEN gender='F' THEN 'female'
                       ELSE                 'other'
                  END
  FROM Student
```

### Interpreting Film Ratings

Your task is to write an SQL query that lists every `Film` released between 2002 and 2006 (inclusive). Your query's result should contain the following columns:

-   `film_id`;
-   `title`;
-   `release_year`;
-   `rating`; and
-   `rating_def` - the rating definition, as given below.

| Rating | Definition                                                   |
| :----- | :----------------------------------------------------------- |
| G      | General Audiences. All Ages Admitted.                        |
| PG     | Parental Guidance Suggested. Some Material May Not Be Suitable For Children. |
| PG-13  | Parents Strongly Cautioned. Some Material May Be Inappropriate For Children Under 13. |
| R      | Restricted. Children Under 17 Require Accompanying Parent or Adult Guardian. |
| NC-17  | No One 17 and Under Admitted.                                |

Source: [Film ratings of the Motion Picture Association of America](http://filmratings.com/downloads/130207_mpaa_rating-poster.pdf).

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, release_year, rating, case
    when rating = 'G' then 'General Audiences. All Ages Admitted.'
    when rating = 'PG' then 'Parental Guidance Suggested. Some Material May Not Be Suitable For Children.'
    when rating = 'PG-13' then 'Parents Strongly Cautioned. Some Material May Be Inappropriate For Children Under 13.'
    when rating = 'R' then 'Restricted. Children Under 17 Require Accompanying Parent or Adult Guardian.'
    when rating = 'NC-17' then 'No One 17 and Under Admitted.'
    end as rating_def
from Film
where release_year between 2002 and 2006
```

### SQL's `COALESCE` function

The `COALESCE()` function returns the first value from its parameter list that is not `NULL`. It is typically used to replace unknown (`NULL`) attribute values with some default value.

The following query lists the grades of students, with a 'unknown' whenever a grade is `NULL`:

```sql
SELECT sid, COALESCE(grade, 'unknown')
  FROM Transcript
 WHERE year = 2011
       AND semester = 'sem1'
```

###  NULL to TBD

Your task is to write an SQL query that outputs every `Film`, in reverse-chronological order of `release_year`; then in alphabetical order by `title` (for any films with the same `release_year`). If any `Film` has a `rating` of `NULL` (i.e. the rating is unknown), this should be replaced with the placeholder `TBD` in your query's result table.

Your query's result must have the following columns:

1.  `film_id`;
2.  `title`;
3.  `release_year`; and
4.  `rating` - or `TBD` if unknown.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, release_year, coalesce(rating, 'TBD') as rating
from Film
order by release_year desc, title
```

### SQL's `NULLIF` function

The reverse of the `COALESCE()` function is SQL's `NULLIF` function:
`NULLIF(value1, value2)` returns a `NULL` if *value1* equals *value2*:

**Example:** Assume a `Measurement (sensor, temperature, ts)` table which contains some 'NaN' values in its temperature column:

```sql
SELECT ts, NULLIF(temperature, 'NaN')
  FROM Measurements
```

The `NULLIF` function is useful if you have, for example, data imported into your database which has some special strings (eg. 'n/a' or 'NaN' for not-a-number) in some of its fields rather than NULLs. For the purpose of a query, those special values can then be converted on the fly to a NULL.

### Déjà Vu

For this question, some films have their `rating` stored as `'TBD'` where the final rating has not yet been decided by the MPAA.

Your task is to write an SQL query that outputs every `Film`, in reverse-chronological order of `release_year`; then in alphabetical order by `title` (for any films with the same `release_year`). If any `Film` has a `rating` of `'TBD'`, this should be replaced with `NULL` in your query's result table (i.e. no value shown for `rating`).

Your query's result must have the following columns:

1.  `film_id`;
2.  `title`;
3.  `release_year`; and
4.  `rating` - or `NULL` if not yet decided.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, release_year, nullif(rating, 'TBD') as rating
from Film
order by release_year desc, title
```

### SQL's `GREATEST` and `LEAST`

```sql
 GREATEST (value1 [, ...] )
 LEAST (value1 [, ...] )
```

The `GREATEST` function selects the largest value of a list of expressions. Correspondingly, the `LEAST` functions returns the smallest value from the list. Note that this list does not need to be sorted.

```sql
SELECT GREATEST(6, 42, 7), LEAST(7, 6, 42);
```

Basically, `LEAST` and `GREATEST` are equivalent to the mathematical functions min() and max(). The difference to SQL's `MIN()` and `MAX()` is that the latter aggregate over the same attribute in *multiple rows*, while the former choose the value from a number of expressions for just *one row*.

### Swanky Late Fees

Our DVD Film Shop charges an extra fee when a `Film` is returned late. The late fee is calculated according to the following formula:

$$fee = \max(rate \times days, cost)$$

where:

-   fee is the late fee;
-   rate is the `rental_rate`;
-   days is the *number of days* by which the `Film` is late; and
-   cost is the `replacement_cost`.

Your task is to write an SQL query to calculate the `late_fee` according to the formula above for every `Film` in which the `Actor` named `'JOE SWANK'` played. These films were all due to be returned on ***24 March, 2016\*** but were returned late on ***12 April, 2016\***.

Your query's result must have the following columns:

1.  `film_id`;
2.  `title`;
3.  `rental_rate`;
4.  `replacement_cost`;
5.  `late_fee`.

**Hint:** You may want to revise the notes on handling dates in SQL.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, rental_rate, replacement_cost,
    (
        greatest(rental_rate *
            (
            extract(doy from date '2016-04-12') - extract(doy from date '2016-03-24')
            ), replacement_cost)
    ) as late_fee
from Film natural join Film_Actor natural join Actor
where first_name = 'JOE' and last_name = 'SWANK'
```

# Advanced SQL

## For-All Queries in SQL

### Relational division in SQL

An interesting example of the usefulness of subqueries and grouping problem is how to formulate "for-all" queries in SQL; for example, "find students who have taken all subjects of a given major". These kind of queries are queries that require a *relational division*.

However, as there is no direct relational division operator in SQL, we have to use some trick to re-formulate the question so that we can express it in SQL. We discuss here two approaches: one by comparing two sets using set-minus, the other by counting the set sizes and making sure that they are the same.

### Relational division using set difference

There is no "for-all" quantification in SQL so that we cannot directly express that some condition is true *for all cases*. However, we can reformulate this into an existence test: something is true for-all cases if there does not exists any counter-example.

The following query finds all students that have taken all 'COMP' coded units using a co-related sub-query and SQL's set difference operator (`EXCEPT`):

```sql
SELECT sid, name
  FROM Student S
 WHERE NOT EXISTS (  SELECT uosCode
                       FROM UnitOfStudy
                      WHERE uosCode LIKE 'COMP%'
                   EXCEPT
                     SELECT uosCode
                       FROM Enrolled E
                      WHERE E.uos_code LIKE 'COMP%'
                            AND E.sid=S.sid
                  )
```

### Relational division by counting sets

A very efficient approach to express the relational division in SQL is to compare the size of the involved sets: Something is true for all possible cases if the number of cases where it is true is the same size than all possible cases (and we used the same condition in both).

Who has taken all COMP-coded subjects? Using the idea that if a student has taken all COMP subjects, the number of their COMP grades must the the same as the number of their COMP units:

```sql
  SELECT sid, name
    FROM Student
         NATURAL JOIN Enrolled
   WHERE uosCode LIKE '%COMP%'
GROUP BY sid, name
   HAVING COUNT(grade) = (SELECT COUNT(*)
                            FROM UnitOfStudy
                           WHERE uosCode LIKE '%COMP%')
```

### "Mmmm Chocolat"

Your task is to write an SQL query to list the `fullname` (`'``<first_name> <last_name>``'`) of every `Actor` who acted in *every* `Film` which had a `title` starting with `'CHOCOLAT'`. The results should be in alphabetical order of each person's `fullname`.

Your query's result must have the following columns:

1.  `actor_id`; and
2.  `fullname`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select Actor.actor_id, concat(first_name, ' ', last_name) as fullname
from Film_Actor natural join Actor natural join Film
where title like 'CHOCOLAT%'
group by Actor.actor_id
having count(film_id) = (
    select count(film_id)
    from Film
    where title like 'CHOCOLAT%')
order by fullname
```

## Testing for Set Equality

### Checking set equality

An interesting problem in SQL is to test whether two given sets of tuples are the same. Note that in SQL, we cannot do so with a simple `(set A) = (set B)` comparison...

One possible approach is to to use the insight that two sets A and B are the same if and only if their respective difference is empty: that is, when $A \backslash B = \emptyset$ and $B \backslash A = \emptyset$.

This kind of condition can now be formulated in SQL using set operations and the `NOT EXISTS` operator as illustrated in the following two examples.

### Example (I)

Assume two relations `R(a INT, b INT)` and `S(c INT, d INT)`. To test whether both relations have exactly the same content, we can follow our idea from above with the following query:

```sql
SELECT 'R and S are the same'
 WHERE NOT EXISTS (  SELECT a, b
                       FROM R
                   EXCEPT
                     SELECT c, d
                       FROM S)
       AND NOT EXISTS (  SELECT c, d
                           FROM S
                       EXCEPT
                         SELECT a, b
                           FROM R)
```

### Example (II)

Rather than to test whether two whole relations are exactly the same, one typically has to check whether a set of dependant values for two given keys is the same (like in a 1:N relationship). The same idea can be applied, but it needs two correlated subqueries now:

Assume three relations: `R(a, ...)`, `S(a, ...)`, and `T(a, c)`. To check whether certain values from `R` and from `S` have the same set of dependent values in `T`, we can use the following query:

```sql
SELECT R.a, S.a
  FROM R, S
 WHERE NOT EXISTS (  SELECT c
                       FROM T
                      WHERE T.a = R.a
                     EXCEPT
                       SELECT c
                         FROM T
                        WHERE T.a = S.a)
       AND NOT EXISTS (  SELECT c
                           FROM T
                          WHERE T.a = S.a
                       EXCEPT
                         SELECT c
                           FROM T
                          WHERE T.a = R.a)
```

### Performance Optimizations

However be careful that these kind of approaches can take quite some time if the involved tables are large. So a good idea is to include some filter conditions that keep intermediate sizes small. For example, when two sets are the same, their size is the same too. So you could filter out all potential candidate sets which don't have the same size.

Further, to avoid to return duplicate pairs of values that come from the same domain (e.g. in the second example, you actually use a self-join between `R` and itself, named `R1` and `R2`), you could add a clause to avoid scanning the pairs twice:

```sql
... WHERE R1.a > R2.a AND NOT EXISTS (...
```

### Identical Casts

Your task is to write an SQL query to list the `film_id` and `title` of every `Film` which has exactly the same cast acting in it as any other `Film`.

Your query's result must have the following columns:

1.  `film_id`; and
2.  `title`.

The results should be listed in increasing order of `film_id`, and no `film_id` should be listed more than once.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select distinct R.film_id, R.title
from Film R, Film S
where not exists (
    select actor_id
    from Film_Actor T
    where T.film_id = R.film_id
    except
    select actor_id
    from Film_Actor T
    where T.film_id = S.film_id
) and not exists (
    select actor_id
    from Film_Actor T
    where T.film_id = S.film_id
    except
    select actor_id
    from Film_Actor T
    where T.film_id = R.film_id
) and R.film_id != S.film_id
order by film_id

-- FilmR(film_id, ..), FilmS(film_id, ..), Film_ActorT(film_id, actor_id)
```

## Special Aggregation Functions

### Special Aggregate Functions

Most of SQL's aggregate functions are defined for integer or real numbers (such as `SUM(...)` or `MAX(...)`).

Some database systems, such as PostgreSQL, also provide special functions to 'aggregate' string values from several sub-strings. Unfortunately, these parts of SQL are not well standardised so that you always have to check against the system documentation on which capabilities are available in your specific system.

For a detailed overview of the aggregate functions that are available in PostgreSQL, see the [Section 9.20 in the online documentation of PostgreSQL](http://www.postgresql.org/docs/current/static/functions-aggregate.html).

### The `string_agg` function

One example for a special aggregate function is PostgreSQL's `string_agg(expression, separator)` function: it aggregates all strings of a given set together by concatenating them into a single string with *separator* characters in between.

**Example:** The following produces a single result row per lecturer which includes a string with a comma-separated list of all units of studies taught by an academic.

```sql
SELECT lecturer, string_agg(uosCode, ',')
  FROM UoSOffering
 GROUP BY lecturer;
```

### Ordered `string_agg`

Some aggregation functions even allow to specify an order on how values should be aggregated. To do so, an explicit `ORDER BY` sub-clause is added to the aggregate function, for example:
`string_agg(expression, separator ORDER BY attributes)`

**Example:** The following returns the units of study as taught by each lecturer *in chronological order by year and semester*. This is achieved via the `ORDER` clause as part of the `string_agg()` function:

```sql
SELECT lecturer,
       string_agg(uosCode, ',' ORDER BY year, semester) AS "units taught"
  FROM UoSOffering
 GROUP BY lecturer
 ORDER BY lecturer;
```

Additionally, we also return the list of all the lecturers in order of the instructor ID.

### Film Cat_aggories

Your task is to write an SQL query to list every `Film` and every `Category` to which it directly belongs, one result row per film. The results should be shown in increasing order of `film_id`.

Your query's result must have the following columns:

1.  `film_id`;
2.  `title`; and
3.  `cat_agg` - comma-delimited list of the `Film`'s direct categories *in alphabetical order*.

For example, if a `Film` belonged to the categories named `Sci-Fi` *and* `Comedy`, its value for `cat_agg` would be `Comedy,Sci-Fi`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title, string_agg(name, ',' order by name) as cat_agg
from Film natural join Film_Category natural join Category
group by film_id, title
```

## Subqueries in the HAVING Clause

### Subqueries in the `HAVING` Clause

Here's an example of a subquery in the `HAVING` clause. This query determines the average mark of all subjects (per year and subject) that have more students enrolled than INFO2120 in the first semester, 2011:

```sql
SELECT AVG(mark)
  FROM Enrolled
 GROUP BY uos_code, semester
HAVING COUNT(sid) > (SELECT COUNT(sid)
                       FROM Enrolled
                      WHERE uos_code = 'INFO2120'
                            AND semester = '2011sem1')
```

### Film Countagories

Your task is to write an SQL query to list every `Film` which belongs to the largest number of categories, one result row per film.

Your query's result should have the following columns:

1.  `film_id`;
2.  `film_title`;
3.  `count` - number of categories to which the `Film` belongs; and
4.  `categories` - the `name` of every `Category` to which the `Film` belongs, comma-delimited, in alphabetical order.

The results should be listed in alphabetical order of the `film_title`.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
select film_id, title as film_title, count(category_id), string_agg(name, ',' order by name) as categories
from Film natural join Film_category natural join Category
group by film_id, title
having count(category_id) = (
    select count(category_id)
    from Film_Category
    group by film_id
    order by count desc
    limit 1
)
order by film_title
```

# SQL Integrity and Security

## Integrity Constraint

### Data Integrity Constraints

As part of a database schema, we can specify a variety of *static integrity constraints*:

-   Domain Constraints

    for each attribute, we have to specify a valid data domain (such as `INTEGER` or `VARCHAR`) and whether it can be `NULL` or not

-   Key Constraints

    by defining certain attributes as `UNIQUE`, `PRIMARY KEY` or `FOREIGN KEY`

-   Semantic Constraints

    with the `CHECK()` clause we can define more complex Boolean conditions which must hold for all data in a table

### Domain Constraints

The most elementary form of an integrity constraint when we declare the domain type for an attribute. We can also allow an attribute to become `NULL` (which is the default) or not. For the latter, we simply add `NOT NULL` to an attribute specification.

With the `DEFAULT` clause we can define a default value for an attribute which is used if no specific value is provided by a user.

**Example:** The following introduces a `Classroom` table whose `name` must be given, but whose `capacity` is optionally (can be `NULL`), and the `kind` of the classroom, if not specified, is `'slopped'`.

```sql
CREATE TABLE Classroom (
    name     VARCHAR(8)  NOT NULL,
    capacity INTEGER     NULL,
    kind     VARCHAR(10) DEFAULT 'slopped'
);
```

What will be inserted in above's `Classroom` table with the following insert statement? Try it out!

```sql
INSERT INTO Classroom VALUES ('SIT123');
```

### Key Constraints

In the DDL chapter, we had already introduced *key constraints*:

-   `UNIQUE`

    Declares an attribute to be a *candidate key* in that no two tuples in the same relation can have the same value for a unique attribute. A unique attribute is allowed to be `NULL` though.

-   `PRIMARY KEY`

    Declares an attribute (or several) as the unique identifier for rows in the table. No two tuples in the same relation can have the same values for the `PRIMARY KEY` attribute(s), and they are also automatically `NOT NULL`.

-   `FOREIGN KEY`

    Introduces a foreign key that refers to the candidate or primary key of a parent table.

**Example:** Every `Classroom` is uniquely identifier by their `name`; hence we make this attribute the `PRIMARY KEY`.

```sql
CREATE TABLE Classroom (
    name     VARCHAR(8)  PRIMARY KEY,
    capacity INTEGER     NULL,
    kind     VARCHAR(10) DEFAULT 'slopped'
);
```

### CHECK Constraints

We can specify semantic integrity constraints on a table via the `CHECK ( <condition> )` clause of the `CREATE TABLE` statement. With this clause we define a Boolean `condition` that must be true for all data stored in that table.

The CHECK clause can comes in two forms:

**1. CHECK as inline constraint:**

```sql
CREATE TABLE Classroom (
    name     VARCHAR(8) PRIMARY KEY,
    capacity INTEGER    CHECK (capacity > 0),
    kind     VARCHAR(10)
);
```

**2. CHECK as separate table constraint:**

```sql
CREATE TABLE Classroom (
   name     VARCHAR(8) PRIMARY KEY,
   capacity INTEGER,
   kind     VARCHAR(10),
   CONSTRAINT capacityChk CHECK (capacity >0)
);
INSERT INTO Classroom VALUES ('SIT123', NULL, 'tiered');
```

Do you think above's `INSERT` statement with a NULL capacity will work? What happens if you try to insert a 0 capacity? Try it out!

Note: The `CONSTRAINT` clause used in Example 2 can be used for all kinds of integrity constraints, not just for CHECK. It allows to introduce names per constraint which can be very helpful to later identify constraint violations.

### CREATE DOMAIN

With the `CREATE DOMAIN` statement, we can introduce user-defined domains into a database schema. This basically means to rename an existing data domain coupled with a value restriction. This allows us to easily and consistently reuse these definitions in multiple table definitions.

**Example:** With the following we introduce `GradingScheme` domain that is a restriction of the `CHAR` domain to the values valid for a certain grading scheme. When then use our new domain to declare a `Transcript` table.

```sql
CREATE DOMAIN GradingScheme
       CHAR(2) CHECK (value in ('FA','PA','CR','DI','HD'));
CREATE TABLE Transcript (
    studid   INTEGER,
    uosCode  CHAR(8),
    grade    GradingScheme
);
INSERT INTO Transcript VALUES (1234, 'COMP2120', 'CR');
SELECT * FROM Transcript;
```

Modify above's example and see what happens if you try to insert an invalid value for grade, such as 'W' or 6.

### Using Integrity Constraints

Provide SQL data definition statements (DDL) that create a `Airplane` table and a user-defined domain `Distance` with the following characteristics. Capture as many of the integrity constraints as possible as part of the `CREATE TABLE` statement:

-   Each `Airplane` is uniquely identified by an alphanumerical `model` code of up-to 10 characters, such as 'A380' or 'DC10'.
-   Each airplane has a `manufacturer`, which is given as a string of max 50 characters. A manufactuer must be given.
-   An airplane can have a non-negative `flight_range` of up-to 25,000 km; specifying an airplane's range is optional.
-   An airplane has a `cruise_speed` of more than 200 km/h; specifying an airplane's cruise speed is optional.
-   Every airplane has an `enginetype` which is either a `turbofan`, a `turbojet`, or a `turboprop`. If not specified, this should be a `turbofan` nowadays. It should however be able to hold a string of max 50 characters.
-   An airplane had a `first_flight` at a certain date - which might be unknown.

Specifically for the flight range, create a user-defined `DOMAIN` called `Distance` which represents a non-negative integer distance.

The following `INSERT` statements should work with the new table:

```sql
INSERT INTO Airplane
     VALUES ('A380',   'Airbus', 15700, 1050, 'turbofan', '2005-04-27');

INSERT INTO Airplane
     VALUES ('Do 228', 'Dornier', NULL, 352, 'turboprop', '1981-03-28');

INSERT INTO Airplane
     VALUES ('DC10',  'McDonnell Douglas');
```

``` sql
create domain Distance
    integer check (value between 0 and 25000);

create table Airplane (
    model varchar(10) primary key,
    manufacturer varchar(50) not null,
    flight_range Distance,
    cruise_speed int check (cruise_speed > 200),
    enginetype varchar(50) default 'turbofan' check (enginetype in ('turbofan', 'turbojet', 'turboprop')),
    first_flight date
);
```

### Referential Integrity

Relational database system guarantee *referential integrity* of all foreign key attributes: for each foreign key value, there must be a matching tuple in the referenced table with the same value in its key. By default, any modification which would break this is disallowed.

As part of a `FOREIGN KEY` clause we can configure this behaviour:

```sql
FOREIGN KEY (<attrs>) REFERENCES <tab> ON DELETE <option>
FOREIGN KEY (<attrs>) REFERENCES <tab> ON UPDATE <option>
```

We have four options:

| `NO ACTION`   | The modification *on the referenced row* is not allowed as long as there is still a foreign key value pointing to it. This is the default behaviour. |
| ------------- | ------------------------------------------------------------ |
| `CASCADE`     | The same modification *on the referenced row* is also applied to the referencing tuple with the foreign key. |
| `SET NULL`    | The foreign key is set to `NULL` once *the referenced row* is modified. |
| `SET DEFAULT` | The foreign key is set to its default value once *the referenced row* is modified. This assumes that we have specified a default value with the `DEFAULT` clause. |

### `CASCADE` Example

The most commonly used referential integrity option, besides `NO ACTION`, is to `CASCADE` the modification to the referencing tuples.

**Example:**

```sql
CREATE TABLE Classroom (
   name     VARCHAR(10) PRIMARY KEY,
   capacity INTEGER CHECK (capacity >0)
);
CREATE TABLE Lecture (
   uosCode  CHAR(8) PRIMARY KEY,
   room     VARCHAR(10),
   FOREIGN KEY (room) REFERENCES Classroom(name)
);
INSERT INTO Classroom VALUES ('SIT123', 50);
INSERT INTO Lecture   VALUES ('INFO2820', 'SIT123');
UPDATE Classroom SET name='SIT LT123' WHERE name='SIT123';
```

As you can see, the `UDPATE` statement above is rejected, because the classroom 'SIT123' is still referenced from a tuple in the `Lecture` table.
How would you extend the `FOREIGN KEY` clause in the example such that above's update statement is working?

### Creating an Inventory

Your task is to introduce to the film database an `Inventory` table. The `Inventory` table shall keep track of how many copies of a given film are in stock at some store (we extended the schema with a new `Store` table for this):

1.  `inventory_id` - a surrogate primary key (integer) used to uniquely identify each item in `Inventory`;
2.  `film_id` - a foreign key pointing to the film this item represents; cannot be `NULL`;
3.  `store_id` - a foreign key pointing to an existing `Store` table;
4.  `quantity` - an integer count on how many copies of the film are still in stock; must be greater or equal 0;
5.  `last_update` - the timestamp that the row was created or most recently updated; cannot be `NULL`.

Include in your table definition all necessary primary keys and foreign keys. For foreign keys, make sure that if a `Film` gets deleted, the corresponding inventory is deleted too. If a store gets dropped from the database, the corresponding inventory shall be set to NULL. If for whatever reason the ID of either a `Film` or a `Store` gets updated, the `Inventory` should automatically reflect the same change.

![Film database schema diagram](https://groklearning-cdn.com/modules/6mqXpZfBbnhWxssSYhWu8K/FilmDB_Schema_withStore.svg)

``` sql
create table Inventory (
    inventory_id int primary key,
    film_id smallint not null references Film(film_id) on delete cascade on update cascade,
    store_id int references Store(store_id) on delete set null on update cascade,
    quantity int check (quantity >= 0),
    last_update timestamp not null
)
```

## SQL Security

### Access Authorization

A database is shared by many users. This raises the question: Who can do what in a database?

**Access Privileges:** The creator of a table or a view automatically has all access rights - or *privileges* - on it. She can then decide which privileges are also granted to other users.

Privileges can be assigned to either individual **users** (in some systems also just called *logins*) or to a group of users via the **role** mechanism: A **role** is a logical grouping of access privileges which can then be assigned to several individual users.

**Access Control Commands:** Access privileges are managed on the table level in SQL. There are two main commands:

-   `GRANT` assigns a certain privilege to an individual user or a role
-   `REVOKE` removes some privilege from an user or a role

### `GRANT` Command

The `GRANT` statement allows to assign access privileges to individual users or roles. The command has the form:

```sql
GRANT <privilege> ON <relation(s)> TO <list_of_users>
```

**Example:**

```sql
GRANT INSERT ON Student TO Bob
```

The most commonly used privileges are:

| **`SELECT`**     | privilege to query a table                                   |
| ---------------- | ------------------------------------------------------------ |
| **`INSERT`**     | privilege to insert data into a table                        |
| **`DELETE`**     | privilege to delete data from a table                        |
| **`UPDATE`**     | privilege to update a table                                  |
| **`REFERENCES`** | privilege to define a foreign key in another table that references a table |

All these privileges are per table. The `UPDATE` and `REFERENCES` options also can be restricted to a specific column:
**Examples:**

```sql
GRANT UPDATE(grade)   ON Enrolled TO Chomsky;
GRANT REFERENCES(sid) ON Student  TO Einstein;
```

### WITH GRANT OPTION

The `GRANT` command additionally supports an option to allow users to pass on their privileges to other users. This is useful in order to establish access hierarchies.

**Example:**

```sql
GRANT INSERT ON Student TO Chomsky WITH GRANT OPTION
```

After this option, user `Chomsky` could pass the `INSERT` privilege on to a third user.

### `REVOKE` Command

The `REVOKE` statement allows to revoke an access privileges from individual users or roles. The **`ALL`** keyword allows to remove all privileges in one command. The command has the form:

```sql
REVOKE <privilege> ON <relation(s)> FROM <list_of_users>
```

**Example:** The following removes the INSERT privilege on the `Student` table from `Alice`, and *all* privileges on the tables `Student` and `Enrolled` from `Bob`.

```sql
REVOKE INSERT ON Student FROM Chomsky;
REVOKE ALL    ON Student,Enrolled FROM Einstein;
```

### Restricting Data Access

There are currently two users in the film database: `Alice` and `Bob`.

Your task is to `GRANT` `Bob` the *minimally neccesary* access privileges so that he can create the following table, as well as read details of actors from the `Actor` table, but nothing else (note: you can assume Bob already has the ability to create tables within the film database):

```sql
CREATE TABLE FanPage (
   url         VARCHAR(100) PRIMARY KEY,
   title       VARCHAR(100) NOT NULL,
   about_actor SMALLINT REFERENCES Actor,
   country     CHAR(2)  REFERENCES Country(short_code)
);
```

On the other hand, `Alice` currently is allowed to do everything on the tables `Film`, `Film_Actor`, and `Actor`. In her case, your task is to use the `REVOKE` and `GRANT` commands to restrict her privileges to just being able to query the `Film` table, as well as to insert new films or update existing films, but nothing else.

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
grant select on Actor to Bob;
grant references on Actor to Bob;
grant references(short_code) on Country to Bob;

revoke all on Film, Film_Actor, Actor from Alice;
grant select on Film to Alice;
grant insert on Film to Alice;
grant update on Film to Alice
```

### Roles

The `CREATE ROLE` command allows to introduce a grouping of access privileges which then can be granted together to individual users in a single `GRANT` statement. This is extremely useful to organise group-based access control and should always be the preferred method for discretional access control.

**Example:** The following creates a role `Lecturer` which can read the `Enrolled` relation and update only its `grade` attribute. The last command assigns the user 'jon' the role `Lecturer`.

```sql
CREATE ROLE Lecturer;
GRANT SELECT ON Enrolled TO Lecturer;
GRANT UPDATE(grade) ON Enrolled TO Lecturer;
GRANT Lecturer to jon;
```

### `CREATE VIEW` Revisited

The `CREATE VIEW` DDL statement extends the current database schema with a new *view*:

```sql
CREATE VIEW CurrentStudents AS
  SELECT studentId, uosCode, semester
    FROM Enrolled
   WHERE year = 2016;

SELECT *
  FROM CurrentStudents;
```

The above example creates a new view called `CurrentStudents`, then performs a `SELECT` over it. A view is like a “stored” query. Once created, it can be queried like a table (it has a name and a schema).

The general syntax to define a new view in SQL is:

```sql
CREATE VIEW name AS <query>;
```

### Views and Access Rights

One shortcoming of SQL's approach to access control is that it only works on the granularity of whole tables (with the exception of the `UPDATE` privilege). But we cannot, for example, restrict read access to just single rows or columns using the standard `GRANT` statement.

The solution is to use views and to grant access then to views instead of the underlying base tables.

**Example:**

```sql
CREATE VIEW ClassListNoMarks AS
     SELECT studentId, uosCode,
       FROM Enrolled;
GRANT SELECT ON ClassListNoMarks TO SomeUser;
```

With the help of the view `ClassListNoMarks` we were able to restrict the read access for *SomeUser* to just the `studentId` and the `uosCode` columns of the table Enrolled. The `grade` column is now hidden for *SomeUser*.

### Family-friendly Film Access

Your task is to organise the access to the film database for *shop assistants* and *shop admins*. You can assume that there already exist two users in the database: `Alice` and `Bob`.

First write a `CREATE VIEW` statement that extends our film database by adding a new view `FamilyFilms` which restricts the access to selected attributes of family-friendly films. These are all 'G'-rated films (G: general audience) and only with the following attributes:

1.  `title` - the title of a `Film`;
2.  `release_year` - the release year of a `Film`;
3.  `description` - the description of a `Film`;
4.  `length` - the length of a `Film`;
5.  `rental_duration` - the rental duration of a `Film`;
6.  `rental_rate` - the rental rate of a `Film`.

Next, organise the access privileges by creating roles `ShopAssistant` and `ShopAdmin` such that a `ShopAssistant` can only see family friendly films and update nothing, while a `ShopAdmin` is allowed to read both films and the new view. Additionally, a `ShopAdmin` is allowed to insert new films and to update the rental rate of an existing film. A `ShopAdmin` shall also be allowed to pass on the read access on `FamilyFilms`, as well as the update privilege for the rental rates of films to other users.

Finally, make user `Alice` a shop admin, and user `Bob` a shop assistant (both users already exist in the database).

![Film database schema diagram](https://groklearning-cdn.com/modules/tqdWF4WxxgiVjW7nsVeu65/FilmDB_Schema.svg)

``` sql
create view FamilyFilms as
select title, release_year, description, length, rental_duration, rental_rate
from Film
where rating = 'G';

create role ShopAssistant;
create role ShopAdmin;

grant select on FamilyFilms to ShopAssistant;
grant select on Film to ShopAdmin;
grant insert on Film to ShopAdmin;
grant update(rental_rate) on Film to ShopAdmin with grant option;
grant select on FamilyFilms to ShopAdmin with grant option;

grant ShopAssistant to Bob;
grant ShopAdmin to Alice

```

# SQL Stored Procedures and Functions

## Stored Procedures



