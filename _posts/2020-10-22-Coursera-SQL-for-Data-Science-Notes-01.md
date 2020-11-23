---
title: "Coursera: SQL for Data Science Notes 01"
date: 2020-11-03
categories: SQL
# permalink: /:categories/:title
---

### Relational Database Management System (DBMS)

- Microsoft SQL Server
- MySQL
- IBM DB2 Oracle
- Apache Open Office Base
- Sybase ASE
- **SQLite**
- PostgreSQL

### ER Diagram Notation

- Chen Notation
- Crow's Foot Notation
- UML Class Diagram Notation

### Data Modeling

#### Type of cardinality:

- one-to-one
- one-to-many
- many-to-many

#### Star Scheme VS Snow Flake

### Create Temporary Table

### Adding comments

#### SELECT

    {% highlight sql %}
    SELECT prod_name
    FROM Products
    LIMIT 5;
    {% endhighlight %}

### Filtering with SQL

- WHERE

  - =
  - <>
  - <
  - \>
  - BETWEEN
  - IN -- to find specific values

    {% highlight sql %}
    SELECT Extended_Step
    From salary_range_by_job_classification
    WHERE Pay_type IN ("M", "H", "D")
    {% endhighlight %}

  - OR -- only the first conditon is to be evaluated
  - OR with AND -- put OR inside (), beacase SQL processes AND before OR
  - NOT
    {% highlight sql %}
    -- To exclude some data
    SELECT
    MIN(Biweekly_high_Rate)
    FROM salary_range_by_job_classification
    WHERE Biweekly_high_Rate not IN ("\$0.00");
    {% endhighlight %}

- LIKE (predicate)
  - %
    - "%Pizza"
    - "Pizza%"
    - "%Pizza%"
  - \_, not supported by DB2
    - "\_Pizza"
  - [], not supported by SQLite

### Sorting with ORDER BY

- ORDER BY, can order by a column that is not selected; can order by multiple columns. ALWAYS is the last in the query.
  - DESC
  - ASC

### Math Operations

- \+
- \-
- \*
- /
- with AS
- the order of operations. In the United States, the popular mnemonic device, "Please excuse my dear Aunt Sally".
  - parentheses
  - exponents
  - multiplication
  - division
  - addition
  - subtraction

### Aggregate Functions

- AVG(column_name) AS "alias"
- COUNT() AS "alias"
  - COUNT(\*) AS "alias", including all the rows in a table containing values or NULL values
  - COUNT(column_name) AS "alias", counts all the rows in a specific column ignoring NULL values
- MIN(column_name) AS "alias", NULL values will be ignored
- MAX(column_name) AS "alias", NULL values will be ignored
- SUM(column_name) AS "alias"

  - SUM(column1 \* column2) AS "alias"

- DISTINCT keyword

### Grouping Data with SQL

- GROUP BY
- HAVING

### Count numbers from query result

    {% highlight sql %}
    SELECT COUNT(DISTINCT Name)
    From Playlists;
    {% endhighlight %}

### Subqueries

### Joins

- Cartesian (Cross) Joins
- Inner Join
- Self Join
- Left Join (SQLite only has left joins)
- Right Join (SQLite does not have)
- Full Outer Join (SQLite does not have)
- Union

### Text strings

### Date and time

- DATE
- TIME
- DATETIME

### STRFTIME("%Y, %m %d", "now")

### SELECT DATE("now")

### CASE
