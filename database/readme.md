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
+----+-------+            +------------+            +----+-------+
     | places                                            | for
+----+-------+                                      +----+-------+           
| Order      |                                      | Employee   |
+----+-------+            +------------+            +----+-------+
     | contains           | Blog Post  |                 | is in
+----+-------+            +------------+            +----+-------+
| Order Item |                                      | Department |
+----+-------+                                      +------------+
     | refers to
+----+-------+            +------------+
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

You are organizing data into individual tables. Many of these tables need to know about each other.

ER diagram shows some kind of relationship exists between your entities, but to actually build this in a database, we need to say what these relationships are.

While it is common in an ER diagram to usa a phrase or a verb to describe it like "contains", or "refers to", or "belongs to" that is for your benefit. Database can't describe it that way.

###There are only three kinds of relationships(cardinality) options:

1. One-to-One
2. One-to-Many
3. Many-to-Many 

### The Natural Order of DB Design

```
+-----------------+            +-----------------+
| Customer        |            | Order           |
+-----------------+            +-----------------+
| CustomerID (PK) |            | OrderId (PK)    |
| FirstName       |           /| Date            |
| LastName        +------------+ TotalDue        |
| Email           |           \| Status          |
| Phone           |            | Salesperson     |
| AddressLine1    |            | DiscountCode    |
| ...             |            | ...             |
+-----------------+            +-----------------+

```
It is necessary to define the primary key then it becoms possible to define the relationship.

## Defining One-to-Many Relationships

It is the most common relationship.

```
+-----------------+            +-----------------+
| Customer        |            | Order           |
+-----------------+            +-----------------+
| CustomerID (PK) |            | OrderId (PK)    |
| FirstName       |           /| Date            |
| LastName        +------------+ TotalDue        |
| Email           |           \| Status          |
| Phone           |            | Salesperson     |
| AddressLine1    |            | DiscountCode    |
| ...             |            | ...             |
+-----------------+            +-----------------+
```

One customer can have many orders. Meaning that one "Customer" row can have many "Order" rows. But each "Order" row is only for one "Customer".

1. We need to define the primary key for both Customer table and Order table.

2. Next, implementing new One-to-Many relationship, requires a change to whatever table that represents the "Many" side of the relationship. So to relate Customer to Order table, I don't need to change anything about the Customer table. That's the One side.

3. We need to add some extra information to the order table, and it is the key to the Customer table, so "CustomerID" and this again is called a "foreign key" (FK) that represents a column in this order table that is a key to a row in a different table. This will specifically refer to one and only one Customer table. You might find the CustomerID occurs more than once in Order, but it is always pointing to only one row in Customer. And we always make the change to the "Many" side of the relationship because it is the only way to do it. I can add one column with one value to every order row that will always point to a correct customer.

The column name of the foreign key does not have to be same as the name of the primary key in the other table. In our case of the example, the name of foreign key can be "PlacedBy" instead of using the same "CustomerID" as its name. However, the data type should match.

### Multiple Relationships

It is also very common to have one table to takes part in multiple relationships. A customer can have many orders. We get a "One-to-Many" relationship here. But we may decide that our customers can have multiple different addresses they may ship to. So we might add a new table for Address and have another "One-to-Many" relationship between Customer and Address. This is perfectly acceptable and very common.

```
+-----------------+           /+-----------------+
| Customer        +------------+ Order           |
+--------+--------+           \+-----------------+
         |
        /|\
+--------+--------+
| Address         |
+-----------------+
```
### Many Side of a Relationship can be One Side in Another rRlationship

Another option is that a table that is on the "Many" side of "One-to-Many" relationship could be on the "One" side of another. For example, Order might be the "Many" side of the Customer-to-Order relationship, but Order itself could have many Order-items so, it is going to be the "One" in this relationship. One Customer has many Orders, One Order can have many Order-items.

There is no standard for diagram, but it is generally like this:

* A box for each table with the name of the table at the top
* The column names (optionally with data types)
* Indication of PK and FK next to the column
* The relationship connector lines between tables

```
+-----------------+            +-----------------+
| Customer        |            | Order           |
+-----------------+            +-----------------+
| CustomerID (PK) |            | OrderId (PK)    |
| FirstName       |           /| Date            |
| LastName        +------------+ TotalDue        |
| Email           |           \| Status          |
| Phone           |            | CustomerID (FK) |
| AddressLine1    |            | DiscountCode    |
| ...             |            | ...             |
+-----------------+            +-----------------+
```

## Exploring One-to-One Relationships

It is possible to create a "One-to-One" relationships in your database, but it is unusual. 

Let's say we have employee and driver's license. If we make two separate entities, we are not counting the case when an employee actually possesses multiple driver's licenses in multiple states or countries. Even if we are only considering emolopyee's primary license, so although we have two physical entities, in some cases, it makes more sense to just combine two tables together.

However, there is a case when you think it is a "One-to-One" relationship is not actually so.

Take a look at this example:

```
       OrderID +-----------------+
          Date | Order           |
     Total Due |                 |
           ... |                 |
               +--------+--------+
                        |
                        |
                        |
                        |
                       /|\
  OrderID (FK) +--------+--------+                 +-----------------+ ProductID                
      Quantity | OrderItem       |\                | Product         | Description
ProductID (FK) |                 +-----------------+                 | ListPrice
           ... |                 |/  many-to-one   |                 | ...
               +-----------------+                 +-----------------+
```
* An Order has many OderItems
* Some people may think OrderItem and Product is a "One-to-One" relationship
* But actually, many OrderItems have one Product, whici is "Many-to-One" relationship

Make sure you are looking at your relationships in both ways, particularly when you think you have found a One-to-One.

## Defining Many-to-Many Relationships

Consider we have Class and Student as our entities.

* A Class can be attended by multiple Students
* A Student can attend multiple Classes

This is a Many-to-Many relationship and we cannot add one column either table that would successfully represent all the possible combinations.

In a relational database, you cannot represent a Many-to-Many relationship directly. You need to create a new table to link the two. In the several names for this kind of table; A join table, or a junction table, a linking table, a bridging table, a cross-reference table. It doesn't matter whatever you prefer. By convention, the name with this table is just usually made up by taking the names of the two tables that it's cross referencing and putting them together. So in this case "ClassStudent" or "StudentClass" either would work.

There is a one-to-many relationship from Class to the ClassStudent linking table, and another one-to-many relationship from the Student table to the ClassStudent table. But the ClassStudent has only foreign keys to each tables.

This case is where we could make our primary key for the ClassStudent table as composite key. ClassID is not unique, and StudentID is not unique, but combining two together will be unique.

A One-to-Many relationship can sometimes found to be a Many-to-Many relationship later. An example is Department and Employee relationship. Usually, an employee works for a department. But it could happen that an employee has multiple duties under multiple departments. If this is a case and you need to reflect this relationship to the system, the relationship between Department and Employee needs to be changed to Many-to-Many.

## Referential Integrity and Relationship Rules

###Referential Constraint

A feature in DBMS that restricts you from doing something that violates the relationships between entities. For example, you won't be able to add an order row to assign it to a customer who is not yet available in the Customer table. If I want to add a new order to a new customer, I will need to create a new customer first. It would allow a customer without an order, but it wouldn't allow an order for a non-existent customer.

### Referential Integrity

I cannot modify a CustomerID of an existing Order for a non-existing customer. If I have a customerID of 367 and this customer have two orders and if I delete this customer 367, DBMS will do different things based on your settings and rules.

### Cascading Delete

One option you have when deleting between tables that have relationships is called a cascading delete. With this option, if I delete a customer with CustomerID 367, it will automatically delete any associated orders. One delete could theoretically delete many connected rows in other tables.

### Cascading Nullify (rarely used)

In this option, if I delete a customer, it will look for the foreign keys in the related table, and set the value of the foreign key to null. What we are doing here is removing the relationship but keeping the related rows alive.

### No Action (default in most DBMS)

If you have a related tables and if you attempt to delete one row that is linked with a row in another table, it will refuse and not let you do that. Just as when I add I had to add a customer first then order, if I want to delete, I will have to delete the order first then delete a customer.

## Database Normalization

```
first normal form -> second normal form -> third normal form
      (1NF)                 (2NF)                (3NF)


```

The entire point of normalization is to make your database easier and more reliable to work with. You usually will end up creating a few new tables as part of the proccess. But the end result is your database will contain a minimum of duplicate or redundant data. It will contain data that's easy to get to, easier to edit, maintain, and you can perform operations even difficult ones on you database without creating garbage in it, without invalidating the state of it, and it is something we will do as part of our initial design, and it is something that we would reapply when a database design is revisited.

Normalization is not an ivory tower, theoretical, academic thing that people talk about but nobody really does in the real world. Everybody does this. If you are a working database administrator, or database designer, you can do normalization in your sleep. It is a core competence of the job. It is important and as you will see we have already been doing a little of it.

## Applying First Normal Form (1NF)

Before we apply the first normal form (1NF), we are assuming that we already have set our columns and primary keys. The first First normal form says that each of our columns and each of our tables should contain one value, and there should be no repeating groups.

### One value for each column and row

```
+------------+-----------+----------+------------+-----+--------------------------------+
| EmployeeID | FirstName | LastName | Email      | ... | ComputerSerial                 |
+------------+-----------+----------+------------+-----+--------------------------------+
| 551        | Les       | Adams    | ladams@    | ... | XP5435512 , XA5543231          |
+------------+-----------+----------+------------+-----+--------------------------------+
| 552        | Jill      | Baker    | jbaker@    | ... | WA2324451                      |
+------------+-----------+----------+------------+-----+--------------------------------+
| 553        | Stephen   | Jackson  | s.jackson@ | ... | BC32345412 , ZZ87656 , XX21312 |
+------------+-----------+----------+------------+-----+--------------------------------+
                                                                 violates 1NF
```

Each column in each row should have one and only one value. Having more than one value means it becomes harder to get, sort, mangage the data.

### No repeating group

```
+------------+-----------+----------+------------+-----+----------------+-----------------+-----------------+
| EmployeeID | FirstName | LastName | Email      | ... | ComputerSerial | ComputerSerial2 | ComputerSerial3 |
+------------+-----------+----------+------------+-----+----------------+-----------------+-----------------+
| 551        | Les       | Adams    | ladams@    | ... | XP5435512      | XA5543231       |                 |
+------------+-----------+----------+------------+-----+----------------+-----------------+-----------------+
| 552        | Jill      | Baker    | jbaker@    | ... | WA2324451      |                 |                 |
+------------+-----------+----------+------------+-----+----------------+-----------------+-----------------+
| 553        | Stephen   | Jackson  | s.jackson@ | ... | BC32345412     | ZZ87656         | XX21312         |
+------------+-----------+----------+------------+-----+----------------+-----------------+-----------------+
                                                                           violates 1NF
```

There should be no repeating groups. The classic sign of repeating group column is the column of the same name is and a number tagged on the end of it just to make it unique. This is a sign of inflexible design.

### Solution

```
                      Employee
+------------+-----------+----------+------------+-----+
| EmployeeID | FirstName | LastName | Email      | ... |
+------------+-----------+----------+------------+-----+
| 551        | Les       | Adams    | ladams@    | ... |
+------------+-----------+----------+------------+-----+
| 552        | Jill      | Baker    | jbaker@    | ... |
+------------+-----------+----------+------------+-----+
| 553        | Stephen   | Jackson  | s.jackson@ | ... |
+------------+-----------+-----+----+------------+-----+
                               |
                               |
                              /|\  Computer
            +------------+-----+------+-----------------+-----+
            | Serial     | EmployeeID | Description     | ... |
            +------------+------------+-----------------+-----+
            | XP5435512  | 551        | Dell Laptop     | ... |
            +------------+------------+-----------------+-----+
            | XA5543231  | 551        | Apple MacBook   | ... | 
            +------------+------------+-----------------+-----+
            | WA2324451  | 552        | Acer Desktop    | ... |
            +------------+------------+-----------------+-----+
            | BC32345412 | 553        | MacBook Pro     | ... |
            +------------+------------+-----------------+-----+
            | ZZ87656    | 553        | HP Server       | ... |
            +------------+------------+-----------------+-----+
            | XX21321    | 553        | iPad3           | ... |
            +------------+------------+-----------------+-----+
                              (FK)
```

Separate the table by creating a computer table will create a one-to-many relationship between Employee table and Computer table. This effectively solves the problem.

There is no repeating values, and no repeating groups in either table. This would get us into first normal form. Solution to 1NF is to create a new table, and sometimes it requires one-to-many or other times many-to-many requiring a joining table.

## Applying Second Normal Form (2NF)

First you have to be in First Normal Form (1NF). You don't pick and choose between them, you go through this one, two, and three.

Second normal form and third normal form are all about the relationship between your columns that are your keys and your other columns are not your keys.

From description, Second normal form:
"Any non-key field should be dependent on the entire primary key."

The second normal form is only ever a problem when we are using a composite primary key. That is a primary key made of two or more columns.

```                    Events
+-----------------------+------+----------+-----------+-----+
| Course     | Date     | Room | Capacity | Available | ... |
+-----------------------+------+----------+-----------+-----+
| SQL101     | 3/1/2013 | 4A   | 12       | 4         |     |
+-----------------------+------+----------+-----------+-----+
| DB202      | 3/1/2013 | 7B   | 14       | 7         |     |
+-----------------------+------+----------+-----------+-----+
| SQL101     | 4/1/2013 | 7B   | 14       | 10        |     |
+-----------------------+------+----------+-----------+-----+
| SQL101     | 5/1/2013 | 12A  | 8        | 8         |     |
+-----------------------+------+----------+-----------+-----+
| CS200      | 4/1/2012 | 4A   | 12       | 11        |     |
+-----+-----------------+------+----------+-----------+-----+
      |
      |
     /|\      Course
+-----+-------------------------+-----+
| CourseID   | Title            | ... |
+-------------------------------+-----+
| SQL101     | SQL Fundamentals |     |
+-------------------------------+-----+
| DB202      | Database Design  |     |
+-------------------------------+-----+
| CS200      | C Programming    |     |
+-------------------------------+-----+
```

If we had a composite key from Event table that is made of two columns: "Course" and "Title", it would violate 2NF, because either course name or title are exposed to the risk of being changed. Since title is not related in any way with the date, it should be separated out to a new table like the above example.

Moving that event table means that everything in that table is now based on the entire key. Particular course at a particular date which may have a different room, or different capacity, different number of available seats.

Here is the great thing. If you are not using composite keys, second normal form is not even a concern. You can step ahead and go right through second normal form and into the next one. Third normal form.

## Applying Third Normal Form (3NF)

Third normal form:
"No non-key field is dependent on any other non-key field."

It is in a way similar to second normal form. Second normal form asks, "Can I figure out any of the values in this row from just part of the composite key." Third normal form asks "Can I figure any of the values in this row from any of the other values in this row and I shouldn't be able to do that."

 ```                    Events
+-----------------------+-----------------------+-----------+-----+
| Course     | Date     | Room                  | Available | ... |
+-----------------------+-----------------------+-----------+-----+
| SQL101     | 3/1/2013 |       4A              | 4         |     |
+-----------------------+-----------------------+-----------+-----+
| DB202      | 3/1/2013 |       7B              | 7         |     |
+-----------------------+-----------------------+-----------+-----+
| SQL101     | 4/1/2013 |       7B              | 10        |     |
+-----------------------+-----------------------+-----------+-----+
| SQL101     | 5/1/2013 |       12A             | 8         |     |
+-----------------------+-----------------------+-----------+-----+
| CS200      | 4/1/2012 |       4A              | 11        |     |
+-----+-----------------+--------------------+--+-----------+-----+
      |                                      |
      |                                      |
     /|\      Course                        /|\  Room
+-----+-------------------------+-----+   +--+---+----------+
| CourseID   | Title            | ... |   | Room | Capacity |
+-------------------------------+-----+   +------+----------+
| SQL101     | SQL Fundamentals |     |   | 4A   | 12       |
+-------------------------------+-----+   +------+----------+
| DB202      | Database Design  |     |   | 7A   | 14       |
+-------------------------------+-----+   +------+----------+
| CS200      | C Programming    |     |   | 12A  | 8        |
+-------------------------------+-----+   +------+----------+
```
If we always have same a capacity for the same room, we are repeating data. This is violating the 3NF. We can solve this problem similarly to how we solved the problem with 2NF. We would create a new table and put the repeated column in this new table. This will create another one-to-many relationship between Events and Room.

It is all about the redundancy of the information. This is what we are trying to do with normalization.

## Database Denormalization

We should always take our database design through:

```
first normal form -> second normal form -> third normal form
      (1NF)                 (2NF)                (3NF)


```

In practice, we would break our rules. It is called denormalization decision. You are consciously making the choice something could be normalized in another table. You could follow the official rules but for convenience and/or for performance, you are not going to.

```
first normal form     ->     second normal form      ->      third normal form
      (1NF)                         (2NF)                          (3NF)
no repeating values,     no non-key values based on      no mnon-key values based on
no repeating groups      just part of a composite key    other non-key values

```

Taking these three steps will vastly improve the quality of your data.

## Creating Queries in SQL

### SQL keywords

* SELECT - Question (Query)
* FROM
* WHERE
* ORDER BY
* GROUP BY
* JOIN
* INSERT INTO
* UPDATE
* DELETE
* HAVING
* IN

### Usage

```
SELECT columns
FROM table

SELECT FirstName
FROM Employee;

SELECT FirstName,LastName
FROM Employee;

SELECT *                  // means all
FROM Employee;
WHERE LastName = 'Green'; //condition

WHERE EmployeeID = 474;

WHERE Salary > 50000;
```

SQL is not case-sensitive generally speaking. SELECT can be written as select. But by long convention over many years, most developers will write the SQL keywords all upper case. It makes the statement easier to read. Your table names and column names on the other hand should just match however they were named in the database. Many DBMS will not care about case-sensitivity. Line breaks also don't matter. SQL is not sensitive to white space.

```
SELECT *
FROM HumanResources.Employee // databaseName.tableName
WHERE Salary > 50000;
```

## Creating the WHERE Clause

Writing an WHERE clause is similar to writing an if-statement in other programming languages.

```
SELECT *
FROM Employee
WHERE LastName = 'Green'; // true or false

String values in SQL uses a single quote ('')

>
<
>=
<=
<> // not equal

SELECT *
FROM Employee
WHERE Salary > 50000
      AND Department = 'Sales';

SELECT *
FROM Employee
WHERE Department = 'Marketing'
      OR Department = 'Sales';

SELECT *
FROM Employee
WHERE Department IN
      ('Marketing','Sales');

SELECT *
FROM Employee
WHERE LastName LIKE 'Green%'; // % is the wildcard in SQL

SELECT *
FROM Employee
WHERE LastName LIKE 'Sm_th'; // _ is the one character wildcard in SQL

SELECT *
FROM Employee
WHERE MiddleInitial IS NULL; // better than using '='

SELECT *
FROM Employee
WHERE MiddleInitial IS NOT NULL;
```

## Sorting Your Results

```
SELECT Description,
        ListPrice, Color
FROM Product;

// Most expensive first, cheapest last

SELECT Description,
        ListPrice, Color
FROM Product
ORDER BY ListPrice // default ascending order

SELECT Description,
        ListPrice, Color
FROM Product
ORDER BY ListPrice DESC; // set it to descending order

SELECT *
FROM Employee
WHERE Salary > 50000
ORDER BY LastName, FirstName; // Sort by LastName first, then FirstName
```
## Using Aggregate Functions

It means it does some calculation on data and give a single value.

```
SELECT COUNT (*) // Count rows
FROM Employee

+--------+
| result |
+--------+
| 547    |
+--------+

SELECT COUNT (*) // Count with a condition
FROM Employee
WHERE Salary > 50000

+--------+
| result |
+--------+
| 132    |
+--------+

SELECT *
FROM Product
ORDER BY ListPrice DESC;

SELECT MAX(ListPrice) // Finding the max value
FROM Product;

+--------+
| result |
+--------+
| 699.00 |
+--------+

SELECT MIN(ListPrice) // Gives the minimum value
FROM Product;

SELECT AVG(ListPrice) // Gives the average value
FROM Product;

SELECT SUM(TotalDue) // Gives a total sum value
FROM Order
WHERE CustomerID = 854;

+---------+
| result  |
+---------+
| 2742.75 |
+---------+

SELECT COUNT(*) // Get the number of rows
FROM Product
WHERE Color = 'Red';

SELECT COUNT(*) , Color // Will give all the counts for each color
FROM Product
GROUP BY Color // You would only use GROUP BY with Aggregate Functions

+--------+--------+
| result | Color  |
+--------+--------+
| 47     | Black  |
+--------+--------+
| 32     | Silver |
+--------+--------+
| 8      | White  |
+--------+--------+
| 86     | Clear  |
+--------+--------+
| ...    | ...    |
+--------+--------+
```

## Joining Tables

```
SELECT FirstName, LastName, HireDate, // All these columns are from Employee
   Employee.DepartmentID, Name, Location // Name and Location columns are from Department
FROM Employee JOIN Department // JOIN keyword joins two tables together for the query
ON Employee.DepartmentID = Department.DepartmentID
```
Since DepartmentID column name is shared for both tables, we can set it explicitly by writing it as `Employee.DepartmentID` instead of just `DepartmentID`

If there is no match, that row will not be returned in the result table.

```
SELECT FirstName, LastName, HireDate,
    Employee.DepartmentID, Name, Location
FROM Employee LEFT OUTER JOIN Department
ON Employee.DepartmentID = Department.DepartmentID // include all rows in the left table

SELECT FirstName, LastName, HireDate,
    Employee.DepartmentID, Name, Location
FROM Employee RIGHT OUTER JOIN Department
ON Employee.DepartmentID = Department.DepartmentID // include all rows in the right table
```

## Inserting, Updating and Deleting

We have several different keywords in SQL for inserting, updating and deleting information. How this goes back to the idea that any computer system not just databases that deals with storing data needs to provide four fundamental functions. The ability to create, read, update, and delete.

```
Function   In SQL
-----------------
Create     INSERT
Read       SELECT
Update     UPDATE
Delete     DELETE

INSERT INTO table
    (column1, column2...)
    VALUES (value1, value2...)


INSERT INTO Employee
    (FirstName, LastName, Department, Salary)
    VALUES (value1, value2...)


INSERT INTO Employee
    (FirstName, LastName, Department, Salary) // columns and
    VALUES ('Joe', 'Allen', 'Sales', '45000') // values and their types should match

```

We don't have to write manual INSERT statements for every new row in our database. It is much more likely that this process will be done programmatically that people will be using more pleasant user interface to enter data. But this is the kind of INSERT statement that is going on behind the scenes.

```
UPDATE table
SET column = value
WHERE condition

UPDATE Employee
SET Email = 'joea@twothreesoliveoil.com'
WHERE EmployeeID = 734

```

Delete is the simplest because it all about the WHERE. We don't have to name any column because DELETE just works on rows.

```
DELETE FROM table
WHERE condition

DELETE FROM Employee
WHERE EmployeeID = 734
```

A good practice when working with the DELETE and also when working with UPDATE is to create it first as a SELECT statement so in this case, so in this case:

```
SELECT *
FROM Employee
WHERE EmployeeID = 734
```

And just confirm that the result I would expect back in this case one row, that is what we'd also affect if I was doing an UPDATE and that is what affect if I was doing a DELETE.

```
SELECT *
FROM Employee
WHERE EmployeeID = 734

DELETE
FROM Employee
WHERE EmployeeID = 734
```

Will ensure that you are doing it correctly.

## Using Data Definition Language

### SQL statement types

```

   data manipulation                 data definition                   data control
+---------------------+          +---------------------+          +---------------------+
|       SELECT        |          |        CREATE       |          |        GRANT        |
|       INSERT        |          |        ALTER        |          |        REVOKE       |
|       UPDATE        |          |        DROP         |          |                     |
|       DELETE        |          |                     |          |                     |
+---------------------+          +---------------------+          +---------------------+
most of the time developers       less time                        even lesser time
would spend time on
```

### Usage

```
CREATE table
(column definition)

CREATE Employee
(EmployeeID    INTEGER    PRIMARY KEY,
 FirstName     VARCHAR(35) NOT NULL,
 LastName      VARCHAR(100) NOT NULL,
 Department    VARCHAR(30) NULL,
 Salary        INTEGER
);


ALTER TABLE table

ALTER TABLE Employee
ADD Email VARCHAR(100);


DROP TABLE table

DROP TABLE Employee;
```

## Creating Indexes

Index in a database is like an index at the back of the textbook. It will help you find things in that book. Say if I have 500 page book on database management and I want to find the content dealing just with date columns. I can look in the back in the index for date. It tells me that is on page 124, and I turn directly to that page. Indexes are all about speed and access. I could have found that content by going through the book page by page, so index isn't adding any content, it is just helping me find it.

```
+------------+-----------+-----------+-----+              +-------------+------------+
| CustomerID | FirstName | LastName  | ... |              | LastName    | CustomerID |
+------------+-----------+-----------+-----+              +-------------+------------+
| 551        | Angela    | Smith     | ... |              | Allen       | 592        |
+------------+-----------+-----------+-----+              +-------------+------------+
| 561        | Lee       | Stout     | ... |              | Bailey      | 432        |
+------------+-----------+-----------+-----+              +-------------+------------+
| 584        | Michelle  | Blackwell | ... |              | Blackwell   | 584        |
+------------+-----------+-----------+-----+              +-------------+------------+
| 592        | Lynn      | Allen     | ... |              | Burns       | 122        |
+------------+-----------+-----------+-----+              +-------------+------------+
| ...        | ...       | ...       | ... |              | ...         | ...        |
+------------+-----------+-----------+-----+              +-------------+------------+
clustered index                                           | ...         | ...        |
                                                          +-------------+------------+
                                                     ---->| Smith       | 551        |
                                                          +-------------+------------+
                                                          | ...         | ...        |
                                                          +-------------+------------+
                                                          non-clustered index on LastName


SELECT * FROM Customer WHERE LastName = 'Smith';
```

We cannot make non-clustered index on every columns becasue every index has a cost. Indexes are benefit when reading data but they are deteriment when writing or changing because they must be maintained.

Say we have a clustered index on EmployeeID, and a non-clustered index on LastName and a non-clustered index on FirstName. If we insert a new row, we would need to insert three times for three different tables.

You only put them on the columns that you really need and use all the time. It is far better to do an occasional tables scan than have multiple indexes that you don't really use.

### Indexing

* Indexing is not just "up-front" work
* Indexing is a trade-off - faster reads, slower writes
* But it can be tweaked without breaking applications

## Conflicts and Isolation

* Atomic
* Consistent
* Isolated
* Durable

```
+--------+----------+---------+-----+
| ID     | Nickname | Balance | ... |
+--------+----------+---------+-----+
| 1      | Joint    | $10000  |     |
+--------+----------+---------+-----+
| 2      | Alice    | $50     |     |
+--------+----------+---------+-----+
| 3      | Bob      | $45     |     |
+--------+----------+---------+-----+
| ...    | ...      | ...     |     |
+--------+----------+---------+-----+

get balance of Joint account ($10000)
get balance of Alice account ($50)
update balance of Joint account ($10000) - $1000
update balance of Alice account ($50) + $1000
```

### Race Condition

It is a conflict where two people or two programming threads doing very similar steps in just getting a little bit ahead of each other. They are trying to affect the same data. When they are doing it together, you will end up with a very different outcome to what would have happened if they are done exactly same steps but Alice did hers first and Bob did his.

```
+--------+----------+---------+-----+
| ID     | Nickname | Balance | ... |
+--------+----------+---------+-----+
| 1      | Joint    | $9000   |     |
+--------+----------+---------+-----+
| 2      | Alice    | $1050   |     |
+--------+----------+---------+-----+
| 3      | Bob      | $1045   |     |
+--------+----------+---------+-----+
| ...    | ...      | ...     |     |
+--------+----------+---------+-----+

get balance of Joint account ($10000)                get balance of Joint account ($10000)
get balance of Alice account ($50)                   get balance of Bob account   ($45)
update balance of Joint account ($10000 - $1000)     update balance of Joint account ($10000 - $1000)
update balance of Alice account ($50 + $1000)        update balance of Bob account ($50 + $1000)
```

### Atomic

The first step to fixing this situation is we make these steps atomic. We are making these several actions group into one indivisible unit by making them transactions. And we do this by adding SQL keywords: at the start and end.

```
BEGIN TRANSACTION                                      BEGIN TRANSACTION
  get balance of Joint account ($10000)                  get balance of Joint account ($10000)
  get balance of Alice account ($50)                     get balance of Bob account   ($45)
  update balance of Joint account ($10000 - $1000)       update balance of Joint account ($10000 - $1000)
  update balance of Alice account ($50 + $1000)          update balance of Bob account ($50 + $1000)
COMMIT                                                 COMMIT
```

### Dirty Read

The issue is that Bob is being allowed to read from the same table that Alice is in the process of changing, but she hasn't finished changing it yet. This is often what is referred to as a dirty read.

There is a transaction going on that is part way through it is going to be changing this data but we are allowed to read from somewhere in the middle of that transaction. So often what happens is we don't want to just treat all as one unit just making them transaction is not good enough. We also want some kind of a locking to occur that we are prevented from simultaneously changing the same data, at least until the transaction is over.

### Pessemistic Locking

One way of doing this is what is referred to as **Pessimistic locking**. As soon as a transaction starts we are going to lock the data that is referring to, and only unlock it once the transaction commits. However, we need to be careful because not all transactions update.

### Optimistic locking

In this case, Bob would be allowed to read from the table on the transaction is going on because we are optimistic that there won't be a conflict.

```
               Alice                                                  Bob

BEGIN TRANSACTION                                      BEGIN TRANSACTION
  get balance of Joint account ($10000)                  get balance of Joint account ($10000)
  get balance of Alice account ($50)                     get balance of Bob account   ($45)
  update balance of Joint account ($10000 - $1000)       update balance of Joint account ($10000 - $1000)
  update balance of Alice account ($50 + $1000)          error - dirty read detected - rollback
COMMIT
```

## Stored Procedures

It is like creating a function or a method in the other programming languages, and it can be executed multiple times.

So here is the most basic way. We have some SQL we have written and we want to reuse.

```
SELECT * FROM Employee
WHERE Salary > 50000
ORDER BY LastName, FirstName

CREATE PROCEDURE HighlyPaid()
    SELECT * FROM Employee
    WHERE Salary > 50000
    ORDER BY LastName, FirstName
END;

CALL HighlyPaid();
```

You could call it from within database administration application, you could call it from an application you were writing yourself in some other programming language, more from reporting application. Now it is another area where the actual creation of a stored procedure is a little different accross the database management systems although there are core similarities.

### Stored procedures can have parameters

```
SELECT * FROM Employee
WHERE Department = 'Sales'
ORDER BY LastName, FirstName

CREATE PROCEDURE EmployeesInDept(IN dept VARCHAR(50))
    SELECT * FROM Employee
    WHERE Department = 'Sales'
    ORDER BY LastName, FirstName
END;

CALL EmployeesInDept('Accounting');
```

### SQL Injection

```
                 +-------------------------------+ +--------+
Customer Number: | ABC551                        | | Submit |
                 +-------------------------------+ +--------+

sqlString = "SELECT * FROM Orders WHERE CustomerID = '"
            + textbook.value
            + "'";

sqlString = "SELECT * FROM Orders WHERE CustomerID = 'ABC551';"
executeSQL(sqlString);


```

What happens when the user who sees this page as malicious and they enter something like this

```
                 +-------------------------------+ +--------+
Customer Number: | x'; SELECT * FROM Users; --   | | Submit |
                 +-------------------------------+ +--------+

sqlString = "SELECT * FROM Orders WHERE CustomerID = 'x'; SELECT * FROM Users; --'"
executeSQL(sqlString);

// What the above query actually do
SELECT * FROM Orders WHERE CustomerID = 'x';  // won't return any value
SELECT * FROM Users;                          // what we just injected into the system
--''                                          // counted as a comment
```

What someone can do with their malicious is they can wonder whether your website is liable or responsive to SQL injection attacks. If it is that usually means that this is going to be constructed in some kind of concatenated string.

```
                 +-------------------------------+ +--------+
Customer Number: | x'; DROP TABLE Orders; --     | | Submit |
                 +-------------------------------+ +--------+

sqlString = "SELECT * FROM Orders WHERE CustomerID = 'x'; DROP TABLE Orders; --'"
executeSQL(sqlString);

// What the above query actually do
SELECT * FROM Orders WHERE CustomerID = 'x';  // won't return any value
DROP TABLE Orders;                            // DDL. You've just lost an entire part of your database
--''                                          // counted as a comment

```

Really malicious here.

Allowing SQL injection can allow someone to log into your system as someone else even administrator without knowing a username or password.

One way around them is to use stored procedures with parameters rather than constructing your own strings as stored procedures inherently don't have this level of flexibility and want to passed into them. You can't dynamically break a stored procedure part into several statements.

## Desktop Database Systems

Some popular desktop softwares:

1. Microsoft Access
2. FileMaker
3. Apache OpenOffice Base
4. FileMaker Bento

```
            reasons + | reasons -
       simple install | many users
          easy to use | large data
    template starters | website database
database and UI tools | 
    reporting options |
                      |
                      |
```

## Relational Database Management Systems

If any database systems can be described as classic, it is these ones that relational database management systems or RDBMS that we have been focusing on this course. They all share the key features discussed.

They are made of:

* Tables with defined columns
* Multiple rows of data
* Primary keys and Foreign keys
* They support relationships, transactions and the ACID test
* Using SQL to talk to them

## XML and Object-Oriented Database Systems

There are a handful of database management systems oriented specifically around using XML as their internal structure rather than tables and columsn and rows.

### XML database systems

```
Name  | License     | QueryLanguage
------+-------------+--------------
BaseX | Open Source | XQuery
Sedna | Open Source | XQuery
eXist | Open Source | XQuery

```

### Object-Oriented Database Systems (OO DBS)

```
Name
---------------
Objectivity/DB
Versant
VelocityDB

```

### Object-Relational Mapping (ORM)

```
ORM Framework | Language
--------------+-----------------
Hibernate     | Java
Core Data     | Objective-C
ActiveRecord  | Ruby
NHibernate    | C# / VB.NET

```

## NoSQL Database Systems

NoSQL "Not only SQL"

You can't assume that they are all similar to each other. Unlike relational databases as a category, where the skills are broadly transferrable between, say Oracle and SQL Server, or DB2, or MySQL. In the NoSQL category, just because you know MongoDB doesn't mean you know Neo4J. They are very different each other.

There are no rules as to what makes a NoSQL database systems and that is kind of a point, because it is more about what they aren't. They are not traditional relational databases. They are getting away from those rules.

### Features of NoSQL databases may include:

* not using SQL
* not being table-based
* not relationship-oriented
* not ACID
* no formal schema
* oriented to web development
* oriented to large-scale deployment
* often open source

### Document Stores

* documents, not rows and columns
* examples: CouchDB, MongoDB

### Key-Value Stores

* everything stored as a key-value pair
* examples: MemcacheDB, Riak, Project Voldemort

### Graph Database

* everything stored as small connected nodes, with relations
* examples: Neo4J, AllegroGraph, DB2 NoSQL Graph Store

### Reasons to Choose a NoSQL Database

* Do you need a flexible schema?
* Do you have vast amounts of data?
* Do you value scaling over consistency?
