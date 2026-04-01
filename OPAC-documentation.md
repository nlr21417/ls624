# Basic OPAC and Cataloging Module Documentation

## Introduction

An OPAC, or Online Public Access Catalog, is the public-facing part of a library system that allows users to search, view, and retrieve bibliographic records. In a real library environment, the OPAC is one part of a larger integrated library system (ILS), which also includes staff-side tools for cataloging, circulation, acquisitions, and account management. In this assignment, I worked with a bare bones OPAC and a basic cataloging module in order to better understand how bibliographic data moves between a relational database, server-side code, and a web interface.

This project used Apache, PHP, MySQL, and HTML on a Linux server. Even though the system was simple, it demonstrated the core relationship between data storage, server-side processing, and the web browser. The OPAC displayed data from the database, while the cataloging module made it possible to add records to that same database through a protected interface.

## Relational Database Structure

The database used in this project was MySQL. A relational database stores data in tables made up of rows and columns. In this case, bibliographic data was stored in a `books` table. Each row represented one record, and each column represented a field within that record, such as author, title, publisher, or copyright year.

One important part of the table structure was the `id` field, which functioned as the primary key. This meant each record had a unique identifier. The table also used specific data types, including `varchar` for text fields and `year` for the copyright field. These details are small, but they matter because the database depends on them to store, sort, and retrieve information correctly.

The relational database acts as the foundation of the system. The OPAC does not store records by itself. Instead, it retrieves information from the database when a user accesses the page. The cataloging module works with the same database, but instead of displaying records, it provides a way to add new ones. This helped me see that the public search interface and the staff data-entry interface are different parts of the same larger system.

## Step-by-Step Setup

## 1. Establishing the Database Connection

The PHP code connected to MySQL by loading credentials from a separate `login.php` file. This file stored the database hostname, database name, username, and password. It was kept outside the public web directory so that users on the web could not directly access it.

The PHP scripts used this information to create a connection to the MySQL database. Once the connection was established, PHP could send SQL queries to MySQL and receive results back. This was one of the most important concepts in the project because it showed how a web page becomes dynamic rather than static.

## 2. Structure of the Cataloging Module

The cataloging module functioned as a staff-side interface for entering records into the database. Instead of only viewing information, this side of the system allowed data to be added through a web form. The form sent information to a PHP script, and that script inserted the submitted values into the appropriate MySQL table.

This part of the assignment made it easier to understand how staff tools in library systems differ from public interfaces. The OPAC is designed for searching and viewing, while the cataloging module is designed for creating and maintaining records. Even though this version was very simple, it demonstrated the core logic of a cataloging workflow.

The cataloging module was also protected with Apache authentication. This was important because cataloging tools should not be publicly editable. Requiring a username and password introduced the basic idea of restricting administrative access.

## 3. Search and Retrieval in the Bare Bones OPAC

The OPAC worked by sending SQL queries from PHP to MySQL and then displaying the returned records in HTML. In the simplest version, PHP queried the `books` table and printed out the results to the page. In the more interactive version, a search form allowed users to enter search terms and retrieve matching records.

This made the role of SQL much clearer to me. SQL queries were what allowed the system to retrieve only the needed data. For example, SQL could select all records, retrieve specific fields, filter results, sort records, or match certain values. The OPAC page itself was really the visible output of database queries being processed on the server side.

## 4. Configuration Steps

Several configuration steps were necessary for the system to work correctly:

- Apache had to be installed and running as the web server.
- PHP had to be installed so Apache could process PHP scripts.
- MySQL had to be installed and configured.
- PHP support for MySQL had to be installed so PHP could communicate with the database.
- A database user, database, and table had to be created in MySQL.
- The `login.php` file had to be stored outside the public web directory and assigned the correct permissions.
- Apache authentication had to be configured for the cataloging module.
- Files had to be placed in the correct locations under `/var/www` and `/var/www/html`.

These configuration steps showed that the system depends on multiple layers working together. The code alone is not enough if permissions, authentication, dependencies, or file locations are incorrect.

## 5. What Would Be Needed for a More Real-World System

The bare bones OPAC and cataloging module were useful for learning, but they would need many additional features to function like a real library system. A more realistic OPAC would need better search options, field-specific searching, better metadata structure, item availability, user accounts, and improved interface design. A real cataloging module would need stronger authentication, record editing, deletion controls, validation, and support for standardized metadata formats such as MARC or Dublin Core.

A real system would also need stronger security, better error handling, more normalized tables, and probably multiple related tables instead of a single simple `books` table. Even so, the project was effective because it showed the core relationship among the database, the code, and the web interface.

## Key Details

Several small details were crucial to making the system work:

- The `id` field needed to be a primary key and auto-incrementing so each record would be unique.
- Text fields needed appropriate data types like `varchar`.
- The copyright field used the `year` type, which matched the kind of data being stored.
- The MySQL database, username, and password in `login.php` had to exactly match the values created in MySQL.
- The `login.php` file needed restricted permissions so Apache could read it without exposing it publicly.
- File permissions on web files mattered. A 403 error occurred when the permissions on `mylibrary.html` prevented Apache from reading the file.
- The cataloging module required authentication because administrative tools should not be open to all users.

This assignment showed that attention to detail is essential in technical work. Even when the code is correct, a small mistake in permissions, file path, credentials, or syntax can prevent the entire system from working.

## Using Documentation

To understand the code and setup process, I relied on the course textbook pages and instructions as my primary documentation. I used those materials to follow the database setup, understand how the PHP scripts connected to MySQL, and see how the OPAC and cataloging module were structured.

When typing and reviewing the PHP and MySQL code, I also had to pay attention to the purpose of individual parts of the syntax. For example, I needed to understand what the connection variables were doing, how SQL commands were structured, and why file placement and permissions mattered. In places where the provided material did not fully explain a problem I encountered, I had to troubleshoot based on the behavior of the system. For example, permission errors required me to look more closely at file ownership and file modes. That process showed me that documentation is not only something you produce, but also something you actively use to understand and debug systems.

One gap in the materials was that the general logic of the system was clear, but some of the small troubleshooting details were easier to understand only after encountering errors directly. Working through those gaps helped reinforce the importance of careful reading, testing, and documenting what happens.

## Links to Site

- OPAC Page: http://34.173.94.120/mylibrary.html
- Cataloging Module: http://34.173.94.120/cataloging/index.html

## Reflection

Working through the OPAC and cataloging module chapters helped me better understand how a simple library system is built from connected parts rather than isolated technologies. The clearest and most intuitive part for me was seeing the general relationship among MySQL, PHP, Apache, and the browser. Once I understood that MySQL stores the bibliographic data, PHP sends queries and processes results, Apache serves the files, and the browser displays the output, the overall structure of the assignment made much more sense. It was also helpful to see how the OPAC and the cataloging module were really two different interfaces working with the same database.

The parts that required more troubleshooting were the configuration details and file permissions. It was one thing to understand the code conceptually, but another to make everything work correctly on the server. For example, permission errors and path issues showed me how easy it is for a small technical detail to stop the entire system from functioning. I also had to pay close attention to credentials, file placement, and database structure. Those parts were less intuitive at first, but they became clearer through testing and correction.

This assignment reinforced why attention to detail is so important when working with databases, software code, and documentation. A missed semicolon, an incorrect file permission, a wrong path, or a mismatch between database credentials can break the system even if the overall design is correct. Good documentation helps reduce that risk because it makes the setup process easier to follow, repeat, and troubleshoot.

Even though this project only used bare bones versions of an OPAC and cataloging module, it connects closely to real-world library systems. Real systems are much more complex, but they still depend on the same underlying ideas: structured bibliographic data, controlled staff access, searchable public records, and well-maintained server-side systems. This assignment helped me see how those larger systems are built on smaller technical relationships and why maintaining them requires both technical skill and careful documentation.
