# Foundations of Programming: Databases [Link](https://www.youtube.com/playlist?list=PLnxBrInqFEs7DqOUljmVlgZ_xRRSsyesu)

## Problems Database Solves

* Size - how big is the database? what happens when it gets really big?
* Ease of Updating - How many people update the database? 10 people? 100 people?
* Accuracy - Any blank field? typos?
* Security - Who gets the access to the data?
* Redundancy - Duplicates, which one is true?
* Importance - Data can be critical to business

## What is Database?

* Oracle
* SQL Server
* DB2
* MySQL
* PostgreSQL
* SQLite
* MS Access
* MongoDB
* ...

These aren't databases! These are the Database Management Systems (DBMS).

```
+----------------+
|                |    DBMS software: surrounds your databases
|  +----------+  |
|  |          |  |
|  | database |  |    Database: your data and your rules
|  |          |  |
|  +----------+  |
|                |
|  +----------+  |
|  |          |  |
|  | database |  |
|  |          |  |
|  +----------+  |
|                |
+----------------+
```

Sometimes business have more than one DBMS.

## Types of DBMS


```
Relational DBMS| NoSQL DBMS| Hierarchical DBMS | Network DBMS | Object-Oriented DBMS |
--------------------------------------------------------------------------------------
Oracle         | Cassandra |         .         |       .      |           .          |
SQL Server     | CouchDB   |         .         |       .      |           .          |
DB2            | MongoDB   |         .         |       .      |           .          |
MySQL          |     .     |                   |              |                      |
PostgreSQL     |     .     |                   |              |                      |
SQLite         |     .     |                   |              |                      |
MS Access      |           |                   |              |                      |
       .       |           |                   |              |                      |

``` 

## Relational Database Features

```
+----------------+
|                |  * Database: your data and your rules
|  +----------+  |
|  |          |  |
|  |  table   |  |  * Table: repeating information of data; colums and rows 
|  |          |  |
|  +----------+  |  * Colums: Each column represents one piece of data; name and type; (imposing rules)
|                |
|  +----------+  |  * Rows: Each row represents one single order, customer, or employee (structured)
|  |          |  |
|  |  table   |  |  * Unique: Settings for a column: unique or not unique; meaning that rows will be unique or not
|  |          |  |
|  +----------+  |  * Primary Key (PK): Unique ID for the table, most important for a table 
|                |
+----------------+
```

## Defining Table Relationships

Adding relationships from one table to another. Relationships are made based on keys.

### Customer table

* CustomerID (column): Primary Key (PK)

When CustomerID is used in the Order table, it is not unique. This key becomes "Foreign Key"

### Order table

* OrderID (column): Primary Key (PK) - link it with CustomerID (column)


## One-to-Many Relationships (very common)

The relationship between Customer table and Order table is "one to many" relationship, because one customer can have many orders.

Examples:

```
+------------+           /+------------+
| Customer   |------------| Order      |  * One Customer "has many" Orders
+------------+           \+------------+

+------------+ 1 infinity +------------+
| Category   |------------| Products   |  * One Category "has infinity" Products
+------------+            +------------+

+------------+           /+------------+
| Department |------------| Employees  |  * One Department "has many" Employees
+------------+           \+------------+

+------------+           /+------------+
| Classroom  |------------| Students   |  * One Classroom "has many" Students
+------------+           \+------------+
```

## Many-to-Many Relationships (occasionally required)

### Small Problem

Harder to describe than "One-to-Many" relationships

### Bigger Problem

In most Relational DBMS, "Many-to-Many" relationships cannot be rendered directly. It can be done indirectly.

Visualized "Many-to-Many" relationships

```
             +------------+------------+------------+------------+
"Author"     | AuthorID   | FirstName  | LastName   | Email      |
 table       +------------+------------+------------+------------+
             | 445        | Tucker     | Morrison   | tucker@... |
             +------------+------------+------------+------------+
             | 446        | Robert     | Allen      | rob@...    |
             +------------+------------+------------+------------+
             | 447        | Jordan     | Winters    | jw1965@... |
             +------------+------------+------------+------------+
                    |
                    |
                   /|\
+------------+------------+
| Customer   | Order      |     "AuthorBook"    "BookAuthor"
+------------+------------+        table     or    table
| 1145       | 447        |
+------------+------------+
| 1145       | 445        |     "junction" or "linking" table
+------------+------------+
| 1146       | 446        |
+------------+------------+
| 1147       | 447        |
+------------+------------+
     \|/
      |
      |
+------------+---------------------+------------+------------+
| BookID     | Title               | PubDate    | ListPrice  |     "Book"
+------------+---------------------+------------+------------+      table
| 1145       | Designing Databases | 3/1/2012   | $45.00     |
+------------+---------------------+------------+------------+
| 1146       | SQLite Made Simple  | 4/11/2012  | $39.95     |
+------------+---------------------+------------+------------+
| 1147       | Pocket Guide to SQL | 5/21/2012  | $19.95     |
+------------+---------------------+------------+------------+
```
## Transactions and the ACID test

Transaction is incredibly important.

### ACID

* A: Atomic - indivisible - the transaction completely happens or not at all - all or nothing
* C: Consistent - any transaction must take the database from one valid state to another valid state based on the rules 
* I: Isolated - locked for the moment when transaction is processing
* D: Durable - robust - once transaction is successful, it will be successful

ACID principal is featured in all Relational Database Systems.

# Introduction to SQL - Structured Query Language

SQL is a **declarative query language**
not a procedural, imperative language
