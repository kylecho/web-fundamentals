# Foundations of Programming: Databases [Link](https://www.youtube.com/playlist?list=PLnxBrInqFEs7DqOUljmVlgZ_xRRSsyesu)

## Problems Database Solves

* **Size**             - how big is the database? what happens when it gets really big?
* **Ease of Updating** - How many people update the database? 10 people? 100 people?
* **Accuracy**         - Any blank field? typos?
* **Security**         - Who gets the access to the data?
* **Redundancy**       - Duplicates, which one is true?
* **Importance**       - Data can be critical to business

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
+------DBMS------+
|                |  * DBMS software: surrounds your databases
|  +----------+  |
|  |          |  |
|  | database |  |  * Database: your data and your rules
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
+----Database----+
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

In most Relational DBMS, "Many-to-Many" relationships cannot be rendered directly. However, it can be done indirectly.

A separate table dedicated for "linking" two other tables is required to emulate this "Many-to-Many" relationships.

Below is the visualization of "Many-to-Many" relationships:

```
             +------------+------------+------------+------------+
"Author"     | AuthorID   | FirstName  | LastName   | Email      |
 table       +------------+------------+------------+------------+
             | 445        | Tucker     | Morrison   | tucker@... |
             +------------+------------+------------+------------+
             | 446        | Robert     | Allen      | rob@...    |
             +------------+------------+------------+------------+
             | 447        | Jordan     | Winters    | jw1965@... |
             +------+-----+------------+------------+------------+
                    |
                    |
                   /|\
+------------+------+-----+
| Customer   | Order      |     "AuthorBook"    "BookAuthor"
+------------+------------+        table     or    table
| 1145       | 447        |
+------------+------------+
| 1145       | 445        |     "junction" or "linking" table
+------------+------------+
| 1146       | 446        |
+------------+------------+
| 1147       | 447        |
+-----+------+------------+
     \|/
      |
      |
+-----+------+---------------------+------------+------------+
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

* **A** : Atomic - indivisible - the transaction completely happens or not at all - all or nothing
* **C** : Consistent - any transaction must take the database from one valid state to another valid state based on the rules 
* **I** : Isolated - locked for the moment when transaction is processing
* **D** : Durable - robust - once transaction is successful, it will be successful

ACID principal is featured in all Relational Database Systems.

## Introduction to SQL - Structured Query Language

SQL is a **declarative query language** not a procedural, imperative language.

It means with SQL, you type what you want, you don't need to structure an algorithm.

```
+------------+---------------------+------------+------------+
| BookID     | Title               | PubDate    | ListPrice  |
+------------+---------------------+------------+------------+ 
| 1145       | Designing Databases | 3/1/2012   | $45.00     |
+------------+---------------------+------------+------------+
| 1146       | SQLite Made Simple  | 4/11/2012  | $39.95     |
+------------+---------------------+------------+------------+
| 1147       | Pocket Guide to SQL | 5/21/2012  | $19.95     |
+------------+---------------------+------------+------------+
```

Given that we have the above table and we want any book with the price higher than $40.

### With a procedural, and imperative language:

1. We would need to loop each row in the table
2. And compare each item in ListPrice column to check if it is higher than $40.

In pseudocode, it will look like:

```
for each b in Books
  if price > 40
    add b to expensive_books_array
  else
    ignore
  end
end

return expensive_books_array
```
### With SQL

With SQL, you don't describe the steps, you describe the outcome.

Something like "I want all books more than $40".

or:

`SELECT * FROM Books WHERE ListPrice > 40`

Will give you:

```
+------------+---------------------+------------+------------+
| BookID     | Title               | PubDate    | ListPrice  |
+------------+---------------------+------------+------------+ 
| 1145       | Designing Databases | 3/1/2012   | $45.00     |
+------------+---------------------+------------+------------+
```

You can do with SQL:

* **C** - Create
* **R** - Read
* **U** - Update
* **D** - Delete

You can also describe database with SQL.

## Database Modeling

Planning is vital. Relational Database reward up-front planning. 

Building a database is like getting tattoed. You really want it to be correct the first time you do it.

Database schema should be built patient, methodical, and step-by-step.

## Planning Your Database

Two initial questions you need to ask yourself before starting:

### 1. What is the point?

####What is this database for?

In most cases, you are building a database to support an application whether that is a desktop or mobile web app but say you are building an online bookstore. It is easy to say the point to the databases is to store product in order information and think you are done. This might be true but what is the intention of this bookstore whether it is a website or an application because wherever you want to go over the next year or two or five should affect what you are building right now. So even having an elevator pitch our mission statement as corny as that might sound will help you build a better database.

####Because if you have something like:

"It's a database to store product and order information."

####or:

"We help customers find books,\n
discover what others thought about them,\n
purchase and track their orders,\n
contribute their own reviews and opinions,\n
and learn about other products they might like\n
based on people with similar reading habits."

You are going to build a very different database from the second description than you would from the first one.

### 2. What do you have already?

You might be lucky enough to be building this for a completely new business when nothing has happened yet. But most of the time there is some existing processed. This database is intended to replace or supplement even if it is a manual one. If so get any physical assets together, printouts order sheets, filing cabinets, and of course people it is going to help you figure out what data you need to keep track of.

* Physical items - forms, order sheets, printouts, handouts
* People and expertise
* An existing "database" - spreadsheets, text files

Take the opportunity to fix any problems that you have so you not just recreating the same problems in you brand new database schema. So understanding what you already have is essential before you can answer the first real question when designing a database which is what entities do you have. We know that the relational database consists of one or more tables. Tables are the basic building block of a relational database. You will create separate tables for each entity that he's each object to each thing that needs to be represented in the database.

We're using the word "entity" here just to keep things a little loose and abstract. We are trying to identify what entities we naturally have rather than just directly asking what tables do I need to go and make. 

Example of Entities:

```
+------------+            +------------+            +------------+
| Customer   |            | Order      |            | Paycheck   |
+------------+            +------------+            +------------+

+------------+                                      +------------+           
| Order      |                                      | Employee   |
+------------+            +------------+            +------------+
                          | Blog Post  |
+------------+            +------------+            +------------+
| Order Item |                                      | Department |
+------------+                                      +------------+

+------------+            +------------+
| Product    |            | Students   |
+------------+            +------------+
```

Some of you entities might represent things that exist in the real world: customer, product, employee, a patient, asset, but others could be more abstract: a blog entry, a category, comment, appointment, sidebar. There is some debate whether to use plural or singular nouns when naming your entities or tables. Is it a customer entity or a customers entity. I'm strongly in preference for singular nouns for tables. That also seems more natural when you describe your entities that way. 

We are interested in the relationships between entities only. Methods, inheritances can be thought later.

### Entity Relationship (or ER Modeling)

```
+------------+            +------------+            +------------+
| Customer   |            | Order      |            | Paycheck   |
+------------+            +------------+            +------------+
     | places                                            | for
+------------+                                      +------------+           
| Order      |                                      | Employee   |
+------------+            +------------+            +------------+
     | contains           | Blog Post  |                 | is in
+------------+            +------------+            +------------+
| Order Item |                                      | Department |
+------------+                                      +------------+
     | refers to
+------------+            +------------+
| Product    |            | Students   |
+------------+            +------------+
```

## Identifying Columns and Selecting Data Types

After figuring out a list of what entities need to exist, you take a look at each one to specify exactly what data is important to store about that.

### Entities and Attributes


```
 ------------            
( name       )-----+           
 ------------      |     
                   |           
 ------------      |                                     
( email      )-----+                                 
 ------------      |       +------------+         
                   +-------+ Customer   |             
 ------------      |       +------------+        
( address    )-----+          entity                  
 ------------      |                         
                   |
 ------------      |     
( phone      )-----+      
 ------------ 
  attributes

```

As a rule, when defining a table, say "Employee", you are going to go as individual as possible. That way you can do more things with the data for example, you can sort your data without extracting anything.

```
Decide how you want to name your attributes:
FirstName or first_name, firstname, fName, strFirstName, firstName, etc.


Attributes    Kind of Data     Default Data
-------------------------------------------------------------------------------------------------
FirstName     character        not NULL
LastName      character        not NULL
DataHired     date             not NULL    default: today
SalaryGrade   integer          not NULL
AddressLine1  character        not NULL
AddressLine2  character        NULL
City          character        not NULL
State         character(2)     not NULL
Zip           character        not NULL
Email         character        not NULL    pattern match: email
Photo         binary           NULL
(etc.)
```
When you get in to use a specific DBMS, you will just have a cheat-sheet or bookmark of all the available data types until you know get to know  them.

Flexibility is usually our friend in programming, but it is not what you are looking for in most Relational Databases. What you are hoping to end up with is that for each table (each entity) you have you will have a reasonable list of the columns to create and data allowed in each column. Defining your column as exactly as possible means that your database will enforce these rules on those columns and your data will stay valid and consistent.

## Choosing Primary Keys

Each value should have a primary key. Each employee, customer, book needs to have a unique primary key, and we need a column that is used for the primary key. But DBMS can choose a primary key using an existing column for example ISBN.

```
+------------+-------------------------------+------------+------------+-----+
| ISBN       | Title                         | ReleaseDate| ListPrice  | ... |
+------------+-------------------------------+------------+------------+-----+
| 1596717521 | JavaScript Essential Training | 6/1/2011   | $149.95    |     |
+------------+-------------------------------+------------+------------+-----+
| 321158814  | Building Rich Internet Apps   | 3/2/2003   | $39.95     |     |
+------------+-------------------------------+------------+------------+-----+
| 765359146  | Red                           | 11/1/2008  | $7.95      |     |
+------------+-------------------------------+------------+------------+-----+
Primary Key(PK)
 (natural key)

```
In some many case, it doesn't occur. For example, Customer table will not have a column for primary key. FirstName, LastName, Email, Address, etc can all be shared. They do not gurantee to be unique. In this case, we would just add a CustomerID column.

* CustomerID - Primary Key(PK), integer, auto-increment.

## Using Composite Keys

One option for primary key you may find useful is something called "composite keys". This is when two rows combine together to make a unique key.

Example, Yearbook:

```
+---------------------+------+-----------+-----------+--------------+-----+
| School              | Year | ListPrice | PageCount | UnitsInStock | ... |
+---------------------+------+-----------+-----------+--------------+-----+
| Orchard High        | 2010 | $29.95    | 144       | 32           |     |
+---------------------+------+-----------+-----------+--------------+-----+
| Orchard High        | 2011 | $34.95    | 132       | 14           |     |
+---------------------+------+-----------+-----------+--------------+-----+
| Lawstone Elementary | 2010 | $29.95    | 161       | 0            |     |
+---------------------+------+-----------+-----------+--------------+-----+
| Lawstone Elementary | 2011 | $29.95    | 155       | 38           |     |
+---------------------+------+-----------+-----------+--------------+-----+
| Lawstone Elementary | 2012 | $34.95    | 172       | 144          |     |
+---------------------+------+-----------+-----------+--------------+-----+
|          ...        |      |           |           |              |     |
+---------------------+------+-----------+-----------+--------------+-----+

|                            |
+----------------------------+
        Primary Key (PK)
        (composite key) - composed of two or more values

```
None of these columns are potentially be a primary key. There is nothing here inherently unique. What we can do is combine them.

If we combine "School" column and "Year" column, they can be represented as a primary key.

One place you will see them is they are used when joining tables together, to create "Many-to-Many" relationships.

## Creating Relationships




