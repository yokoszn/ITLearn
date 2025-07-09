Structured query language (SQL) is a programming language for storing and processing information in a relational database. A relational database stores information in tabular form, with rows and columns representing different data attributes and the various relationships between the data values. You can use SQL statements to store, update, remove, search, and retrieve information from the database. You can also use SQL to maintain and optimize database performance.

---
### Learning Objectives

- Understand what databases are, as well as key terms and concepts
- Understand the different types of databases 
- Understand what SQL is
- Understand and be able to use SQL CRUD Operations
- Understand and be able to use SQL Clauses Operations
- Understand and be able to use SQL Operations
- Understand and be able to use SQL Operators
- Understand and be able to use SQL Functions

There are quite a few different types of databases that can be built, but for this introductory room, we are going to focus on the two primary types: **relational databases** (aka SQL) vs **non-relational databases** (aka NoSQL).
![[Pasted image 20241112140624.png]]
**Relational databases:** Store structured data, meaning the data inserted into this database follows a structure. For example, the data collected on a user consists of first_name, last_name, email_address, username and password. When a new user joins, an entry is made in the database following this structure. This structured data is stored in rows and columns in a table (all of which will be covered shortly); relationships can then be made between two or more tables (for example, user and order_history), hence the term relational databases.

**Non-relational databases:** Instead of storing data the above way, store data in a non-tabular format. For example, if documents are being scanned, which can contain varying types and quantities of data, and are stored in a database that calls for a non-tabular format. Here is an example of what that might look like:
```
 {
    _id: ObjectId("4556712cd2b2397ce1b47661"),
    name: { first: "Thomas", last: "Anderson" },
    date_of_birth: new Date('Sep 2, 1964'),
    occupation: [ "The One"],
    steps_taken : NumberLong(4738947387743977493)
}
```
In terms of what database should be chosen, it always comes down to the context in which the database is going to be used. Relational databases are often used when the data being stored is reliably going to be received in a consistent format, where accuracy is important, such as when processing e-commerce transactions. Non-relational databases, on the other hand, are better used when the data being received can vary greatly in its format but need to be collected and organised in the same place, such as social media platforms collecting user-generated content.
Tables, Rows and Columns

Now that we’ve defined the two primary types of databases, we’ll focus on relational databases. We’ll start by explaining tables, rows, and columns. All data stored in a relational database will be stored in a table; for example, a collection of books in stock at a bookstore might be stored in a table named “Books”. 
![[Pasted image 20241112142411.png]]
When creating this table, you would need to define what pieces of information are needed to define a book record, for example, “id”, “Name”, and “Published_date”. These would then be your **columns**; when these columns are being defined, you would also define what data type this column should contain; if an attempt is made to insert a record into a database where the data type does not match, it is rejected. The data types that can be defined can vary depending on what database you are using, but the core data types used by all include Strings (a collection of words and characters), Integers (numbers), floats/decimals (numbers with a decimal point) and Times/Dates. 

Once a table has been created with the columns defined, the first record would be inserted into the database, for example, a book named “Android Security Internals” with an id of “1” and a publication date of “2014-10-14”. Once inserted, this record would be represented as a **row**.

---

**Primary Keys**: A primary key is used to ensure that the data collected in a certain column is unique. That is, there needs to be a way to identify each record stored in a table, a value unique to that record and is not repeated by any other record in that table. Think about matriculation numbers in a university; these are numbers assigned to a student so they can be uniquely identified in records (as sometimes students can have the same name). A column has to be chosen in each table as a primary key; in our example, “id” would make the most sense as an id has been uniquely created for each book where, as books can have the same publication date or (in rarer cases) book title. Note that there can only be one primary key column in a table.

**Foreign Keys**: A foreign key is a column (or columns) in a table that also exists in another table within the database, and therefore provides a link between the two tables. In our example, think about adding an “author_id” field to our “Books” table; this would then act as a foreign key because the author_id in our Books table corresponds to the “id” column in the author table. Foreign keys are what allow the relationships between different tables in relational databases. Note that there can be more than one foreign key columns.

---
## CRUD

**CRUD** stands for **C**reate, **R**ead, **U**pdate, and **D**elete, which are considered the basic operations in any system that manages data.

Let's explore all these different operations when working with **MySQL**. In the next two tasks, we will be using the **books** table that is part of the database **thm_books**. We can access it with the statement `use thm_books;`.

### Create Operation (INSERT)

The **Create** operation will create new records in a table. In MySQL, this can be achieved by using the statement `INSERT INTO`, as shown below.  

Terminal

```shell-session
mysql> INSERT INTO books (id, name, published_date, description)
    VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");

Query OK, 1 row affected (0.01 sec)
```

  

As we can observe, the `INSERT INTO` statement specifies a table, in this case, **books**, where you can add a new record; the columns **id**, **name**, **published_date**, and **description** are the records in the table. In this example, a new record with an **id** of  **1**, a **name** of **"Android Security Internals**", a **published_date** of "**2014-10-14**", and a **description** stating "**Android Security Internals provides a complete understanding of the security internals of Android devices**" was added.

**Note:** This operation already exists in the database so there is no need to run the query.

### Read Operation (SELECT)

The **Read** operation, as the name suggests, is used to read or retrieve information from a table. We can fetch a column or all columns from a table with the `SELECT` statement, as shown in the next example.  

Terminal

```shell-session
mysql> SELECT * FROM books;
+----+----------------------------+----------------+------------------------------------------------------+
| id | name                       | published_date | description                                          |
+----+----------------------------+----------------+------------------------------------------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture |
+----+----------------------------+----------------+------------------------------------------------------+

1 row in set (0.00 sec)         
```

  

The above output `SELECT` statement is followed by an `*` symbol indicating that all columns should be retrieved, followed by the `FROM` clause and the table name, in this case, **books**.

If we want to select a specific column like the **name** and **description**, we should specify them instead of the `*` symbol, as shown below.  

Terminal

```shell-session
mysql> SELECT name, description FROM books;
+----------------------------+------------------------------------------------------+
| name                       | description                                          |
+----------------------------+------------------------------------------------------+
| Android Security Internals | An In-Depth Guide to Android's Security Architecture |
+----------------------------+------------------------------------------------------+

1 row in set (0.00 sec)         
```

  

### Update Operation (UPDATE)

The **Update** operation modifies an existing record within a table, and the same statement, `UPDATE`, can be used for this.  

Terminal

```shell-session
mysql> UPDATE books
    SET description = "An In-Depth Guide to Android's Security Architecture."
    WHERE id = 1;

Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0     
```

  

The `UPDATE` statement specifies the table, in this case, **books**, and then we can use `SET` followed by the column name we will update. The `WHERE` clause specifies which row to update when the clause is met, in this case, the one with **id 1**.

### Delete Operation (DELETE)

The **delete** operation removes records from a table. We can achieve this with the `DELETE` statement.

**Note:** There is no need to run the query. Deleting this entry will affect the rest of the examples in the upcoming tasks.

Terminal

```shell-session
mysql> DELETE FROM books WHERE id = 1;

Query OK, 1 row affected (0.00 sec)    
```

  

Above, we can observe the `DELETE` statement followed by the `FROM` clause, which allows us to specify the table where the record will be removed, in this case, **books**, followed by the `WHERE` clause that indicates that it should be the one where the **id** is **1**.

### Summary

In summary, **CRUD** operations results are fundamental for data operations and when interacting with databases. The statements associated with them are listed below.

- **Create (INSERT statement)** - Adds a new record to the table.
- **Read (SELECT statement)** - Retrieves record from the table.
- **Update (UPDATE statement)** - Modifies existing data in the table.
- **Delete (DELETE statement)** - Removes record from the table.

These operations enable us to effectively manage and manipulate data within a database.




----



## CRUD

**CRUD** stands for **C**reate, **R**ead, **U**pdate, and **D**elete, which are considered the basic operations in any system that manages data.

Let's explore all these different operations when working with **MySQL**. In the next two tasks, we will be using the **books** table that is part of the database **thm_books**. We can access it with the statement `use thm_books;`.

### Create Operation (INSERT)

The **Create** operation will create new records in a table. In MySQL, this can be achieved by using the statement `INSERT INTO`, as shown below.  

Terminal

```shell-session
mysql> INSERT INTO books (id, name, published_date, description)
    VALUES (1, "Android Security Internals", "2014-10-14", "An In-Depth Guide to Android's Security Architecture");

Query OK, 1 row affected (0.01 sec)
```

  

As we can observe, the `INSERT INTO` statement specifies a table, in this case, **books**, where you can add a new record; the columns **id**, **name**, **published_date**, and **description** are the records in the table. In this example, a new record with an **id** of  **1**, a **name** of **"Android Security Internals**", a **published_date** of "**2014-10-14**", and a **description** stating "**Android Security Internals provides a complete understanding of the security internals of Android devices**" was added.

**Note:** This operation already exists in the database so there is no need to run the query.

### Read Operation (SELECT)

The **Read** operation, as the name suggests, is used to read or retrieve information from a table. We can fetch a column or all columns from a table with the `SELECT` statement, as shown in the next example.  

Terminal

```shell-session
mysql> SELECT * FROM books;
+----+----------------------------+----------------+------------------------------------------------------+
| id | name                       | published_date | description                                          |
+----+----------------------------+----------------+------------------------------------------------------+
|  1 | Android Security Internals | 2014-10-14     | An In-Depth Guide to Android's Security Architecture |
+----+----------------------------+----------------+------------------------------------------------------+

1 row in set (0.00 sec)         
```

  

The above output `SELECT` statement is followed by an `*` symbol indicating that all columns should be retrieved, followed by the `FROM` clause and the table name, in this case, **books**.

If we want to select a specific column like the **name** and **description**, we should specify them instead of the `*` symbol, as shown below.  

Terminal

```shell-session
mysql> SELECT name, description FROM books;
+----------------------------+------------------------------------------------------+
| name                       | description                                          |
+----------------------------+------------------------------------------------------+
| Android Security Internals | An In-Depth Guide to Android's Security Architecture |
+----------------------------+------------------------------------------------------+

1 row in set (0.00 sec)         
```

  

### Update Operation (UPDATE)

The **Update** operation modifies an existing record within a table, and the same statement, `UPDATE`, can be used for this.  

Terminal

```shell-session
mysql> UPDATE books
    SET description = "An In-Depth Guide to Android's Security Architecture."
    WHERE id = 1;

Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0     
```

  

The `UPDATE` statement specifies the table, in this case, **books**, and then we can use `SET` followed by the column name we will update. The `WHERE` clause specifies which row to update when the clause is met, in this case, the one with **id 1**.

### Delete Operation (DELETE)

The **delete** operation removes records from a table. We can achieve this with the `DELETE` statement.

**Note:** There is no need to run the query. Deleting this entry will affect the rest of the examples in the upcoming tasks.

Terminal

```shell-session
mysql> DELETE FROM books WHERE id = 1;

Query OK, 1 row affected (0.00 sec)    
```

  

Above, we can observe the `DELETE` statement followed by the `FROM` clause, which allows us to specify the table where the record will be removed, in this case, **books**, followed by the `WHERE` clause that indicates that it should be the one where the **id** is **1**.

### Summary

In summary, **CRUD** operations results are fundamental for data operations and when interacting with databases. The statements associated with them are listed below.

- **Create (INSERT statement)** - Adds a new record to the table.
- **Read (SELECT statement)** - Retrieves record from the table.
- **Update (UPDATE statement)** - Modifies existing data in the table.
- **Delete (DELETE statement)** - Removes record from the table.

These operations enable us to effectively manage and manipulate data within a database.

---
Using the `tools_db` database, which tool falls under the **Multi-tool** category and is useful for **pentesters** and **geeks**?  

Using the `tools_db` database, what is the category of tools with an amount **greater than** or **equal** to **300**?  

Using the `tools_db` database, which tool falls under the **Network intelligence** category with an amount **less than 100**?

Using the `tools_db` database, what is the tool with the longest name based on character length?  

Using the `tools_db` database, what is the total sum of all tools?  

Using the `tools_db` database, what are the tool names where the amount does not end in **0**, and **group** the tool names **concatenated** by " & ".

- **Databases** are collections of organised data or information that are easily accessible and can be manipulated or analysed.
- The two primary types of databases are **relational databases** (used to store structured data) and **non-relational databases** (used to store data in a non-tabular format).
- Relational databases are made up of **Tables, columns and rows**. **Primary keys** can ensure a record is unique within a table, and **foreign keys** can allow for a relationship/connection to be made between two (or more) tables.
- **SQL** is an easy-to-learn programming language that can be used to interact with relational databases.
- **Database and Table statements** can be used to create/manipulate databases and tables.
- CRUD Operations (**INSERT, SELECT, UPDATE** and **DELETE**) can be used to manage data in a database.
- In SQL, we can use **clauses** to define how data should be retrieved, filtered, sorted, or grouped.
- The efficient use of **operators** and **functions** can help us filter and manipulate data in SQL.