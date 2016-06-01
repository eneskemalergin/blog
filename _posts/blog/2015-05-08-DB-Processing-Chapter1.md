---
layout: post
title: Database Processing - Chapter 1
tags:
- Database
published: true
---

## Chapter 1 : Introduction
---
### The Characteristics of Databases
Purpose of database is to help people to keep track of things, most common way of using databases is using relational database.

- Relational databases store data in tables.
- Data are recorded facts and numbers
- Table has rows and matrices
- Each row contains data according to the column but all data in one row is related with some thing or somebody (__Known as records__)
- Each column contains some kind of data for different individuals (__Know as fields__)
- We know how to structure data to store data but a database is not complete unless it also shows the relationships among the rows of data
- Without pointing out who's data it is, the numbers or words are meaningless
- To be able to point out the classes and identify who's records we are dealing we use _primary key_. The values of these keys are used to create relationships between the tables

![figure-1.1](http://eneskemalergin.github.io/images/exampleOfPrimaryKey.png)

- If the numbers used in primary key columns such as StudentNumber and ClassNumber are automatically generated  and assigned in the database itself, then the key is also called a _surrogate key_.
- Foreign key provides the link between two tables

---
In order to make some decisions we need information, to define information we need databases:

- Knowledge derived from data
- Data presented in meaningful context
- Data processed by summing, ordering, averaging, grouping, comparing, or other similar operations, might get from the information

### Components of a Database Systems
Database system is defined to consist of four component:

- Users
- Database Application
- Database Management System (DBMS)
- Database

However SQL(Structured Query Language) is very popular bridge between database application and DBMS. SQL is used to enter, remove, filter, and get data from the database by connection all 4 components together.  

Here is the components of database systems in general.

![Database Systems](http://eneskemalergin.github.io/images/ComponentsOfDatabaseSystem.png)

Here is the components of databases systems with using SQL

![SQL Database Systesm](http://eneskemalergin.github.io/images/ComponentsOfDatabaseSystemSQL.png)

Database application is a set of one or more computer programs which serves as a bridge between users and DBMS. Users are last component of database systems which is doing everything read, enter, query the data.

#### Databases Application and SQL
First an application program creates and processes forms, then function of application programs is to process user queries.

- To be able to achieve that it creates a query request and send it to the DBMS. Then results are formatted and returned to user. They use SQL to accomplish these. Here is an example of how to call queries and use them with SQL.

```SQL
SELECT 		LastName, FirstName, EmailAddress
FROM		STUDENT
WHERE		StudentNumber > 2;
```
Here are the basic functions of application programs:

- Create and process form
- Process user queries
- Create and process reports
- Execute application logic
- Control the application itself.

As we've seen example above, SQL is query statement which ask DBMS to obtain specific data from a database. Another function of application is to create and process reports.

- Application first queries the DBMS for data using SQL then formats the query results as a report.

The last function of application is controlling the application this can be done in two ways.

1. Application needs to be written so that only logical options are presented to the user.
2. Application needs to control data activities with the DBMS

#### The DBMS
DBMS creates, processes, and administers the database. Microsoft Access, Oracle Database, and MySQL are only some example of DBMS.  Here are the basic functions of DBMS:

- Create database
- Create Tables
- Create supporting structures (like indexes)
- Modify(insert, update, or delete) database data
- Read database data
- Maintain database structures
- Enforce rules
- Control concurrency
- Perform backup and recovery

To make read, modify happens DBMS receives SQL and other requests and transforms those into actions on database files. DBMS are might be useful to change the format of a table or another supporting structure DBMS are also rule forcer. In case of invalid entry the disallow it by their rules.

#### Database
Database is a self-describing collection of integrated tables, which means table store both data and relationships among data. Database is self describing because it contains a description of itself.
> Database contains explanation of user data as well and they called __metadata__(Data about data)(Format or form may vary from DBMS to DBMS)

> Note: Because metadata is stored in tables, we can use SQL to query it, as just illustrated. To do that we just apply the SQL statements to metadata.

This is an example statement to handle the metadata.

```SQL
SELECT *
FROM SYSOBJECTS
WHERE [Name]='CLASS'
AND Type='U';
```

### Database Design
It is a process of creating of the proper structure of database tables, the proper relationships between table, appropriate data constraints, and other structural components of the database. Also keep that in mind design of a database is very important for efficiency and performance issues.

#### Database Design from Existing Data
In some cases you need to design existing data by creating new database with new design and transfer the old ones into new designed database.

![DesingDB from existing](http://eneskemalergin.github.io/images/DesignDBfromExisting.png)

Developers must determine the appropriate structure for the new database. Common issue is how the multiple files or tables in the new database should be related.

#### Database Design for New System Development
User requirements to design of database is often too big, that's why they cut it into two steps first team creates a data model from the requirements. You can think of a data model as  a blueprint that is used as a design model.

![s](http://eneskemalergin.github.io/images/ComponentsOfDatabaseSystem.png)

#### Database Redesign
It requires database which already designed we will transform them into new one. There are two common ways of redesigning a database.

1. First database flexible enough for changes and adaptions, we use database migration. In migration process tables can be created, modified, or removed; relationships can be altered and data constraints can be changed.
2. Second, more than one databases are integrating and making new design for them all united.

![Alt text](http://eneskemalergin.github.io/images/RedesignDB.png)
