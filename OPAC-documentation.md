# Basic OPAC and Cataloging Module Documentation

## Introduction

An OPAC, or Online Public Access Catalog, is the public-facing part of a library system that allows users to search, view, and retrieve bibliographic records. In a real library environment, the OPAC is one part of a larger integrated library system (ILS), which also includes staff-side tools for cataloging, circulation, acquisitions, and account management. In this assignment, I worked with a bare bones OPAC and a basic cataloging module in order to better understand how bibliographic data moves between a relational database, server-side code, and a web interface.

This project used Apache, PHP, MySQL, and HTML on a Linux server. Even though the system was simple, it demonstrated the core relationship between data storage, server-side processing, and the web browser. The OPAC displayed data from the database, while the cataloging module made it possible to add records to that same database through a protected interface.

## Relational Database Structure

The database used in this project was MySQL. A relational database stores data in tables made up of rows and columns. In this case, bibliographic data was stored in a `books` table. Each row represented one record, and each column represented a field within that record, such as author, title, publisher, or copyright year.

One important part of the table structure was the `id` field, which functioned as the primary key. This meant each record had a unique identifier. The table also used specific data types, including `varchar` for text fields and `year` for the copyright field. These details are small, but they matter because the database depends on them to store, sort, and retrieve information correctly.

The relational database acts as the foundation of the system. The OPAC does not store records by itself. Instead, it retrieves information from the database when a user accesses the page. The cataloging module works with the same database, but instead of displaying records, it provides a way to add new ones. This helped me see that the public search interface and the staff data-entry interface are different parts of the same larger system.

## Step-by-Step Overview

### 1. Building the Database Foundation

The project began with setting up MySQL as the database layer of the system. This was important because both the OPAC and the cataloging module depend on a structured place to store bibliographic data. A database user, a database, and a table all had to be created before the web pages could do anything meaningful. This step made it clear that the web interface is only the visible layer of the system and that the real data lives in the relational database underneath it.

### 2. Creating the `books` Table and Sample Records

After the database was created, the next step was defining the structure of the `books` table. This table stored the bibliographic records used by the OPAC and cataloging module. Fields such as `id`, `author`, `title`, `publisher`, and `copyright` determined what information could be stored for each record. The `id` field served as the primary key, which ensured that each record remained unique. Once the table existed, sample records were inserted so that the OPAC would have something to display and search.

This part of the assignment helped me understand that relational databases are not just collections of data. They depend on careful planning of fields, data types, and keys so that the records can be managed consistently.

### 3. Connecting PHP to MySQL

Once the database structure was in place, PHP was used to connect the web pages to MySQL. The connection information was stored in a separate `login.php` file containing the hostname, database name, username, and password. This file was stored outside the public web directory so that it could be used by the server without being directly exposed to web users.

This step clarified how PHP acts as the middle layer between the database and the browser. Instead of storing information itself, PHP connects to MySQL, sends SQL queries, receives results, and then turns those results into HTML that Apache can serve to the browser.

### 4. Building the OPAC Interface

The OPAC functioned as the public-facing side of the system. In the bare bones version, PHP queried the `books` table and displayed the results in a web page. In the searchable version, a form allowed a user to enter search terms, and PHP used those inputs to retrieve matching records from the database.

This part helped me see how SQL works in practice. The OPAC depended on SQL queries to retrieve all records, pull specific fields, and limit results based on user input. The OPAC page itself was therefore a display layer built on top of the database and query system.

### 5. Building the Cataloging Module

The cataloging module served as the staff-side interface of the same system. Instead of searching and displaying records, it provided a form for entering new bibliographic data into the database. When a user submitted the form, PHP processed the input and inserted the data into the `books` table.

This made the division between public and staff functions much clearer. The OPAC was designed for retrieval, while the cataloging module was designed for record creation. Even though both relied on the same database, they served different purposes within the system.

### 6. Protecting the Cataloging Module

Because the cataloging module changes data, it needed to be protected. Apache authentication was used so that only authorized users could access the cataloging area. This introduced the idea that staff tools should not be openly available to the public, even in a simple learning environment.

This was also a good reminder that systems are not only about code and databases. Access control and permissions are part of making a system function safely and appropriately.

### 7. What Would Make This More Like a Real ILS

A real integrated library system would need much more than this bare bones version. The OPAC would need improved searching, better metadata, item availability, circulation functions, and a more polished interface. The cataloging module would need stronger validation, editing tools, deletion controls, better authentication, and support for standardized schemas such as MARC or Dublin Core.

A real system would also likely use multiple related tables rather than one simple `books` table. Even so, this project was useful because it showed the basic structure behind a library system: a database stores records, PHP processes requests, Apache serves the pages, and the browser displays the result.

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

## GitHub Repository

- GitHub Repo: https://github.com/nlr21417/ls624


## Reflection

Working through the OPAC and cataloging module chapters helped me better understand how a simple library system is built from connected parts rather than isolated technologies. The clearest and most intuitive part for me was seeing the general relationship among MySQL, PHP, Apache, and the browser. Once I understood that MySQL stores the bibliographic data, PHP sends queries and processes results, Apache serves the files, and the browser displays the output, the overall structure of the assignment made much more sense. It was also helpful to see how the OPAC and the cataloging module were really two different interfaces working with the same database.

The parts that required more troubleshooting were the configuration details and file permissions. It was one thing to understand the code conceptually, but another to make everything work correctly on the server. For example, permission errors and path issues showed me how easy it is for a small technical detail to stop the entire system from functioning. I also had to pay close attention to credentials, file placement, and database structure. Those parts were less intuitive at first, but they became clearer through testing and correction.

This assignment reinforced why attention to detail is so important when working with databases, software code, and documentation. A missed semicolon, an incorrect file permission, a wrong path, or a mismatch between database credentials can break the system even if the overall design is correct. Good documentation helps reduce that risk because it makes the setup process easier to follow, repeat, and troubleshoot.

Even though this project only used bare bones versions of an OPAC and cataloging module, it connects closely to real-world library systems. Real systems are much more complex, but they still depend on the same underlying ideas: structured bibliographic data, controlled staff access, searchable public records, and well-maintained server-side systems. This assignment helped me see how those larger systems are built on smaller technical relationships and why maintaining them requires both technical skill and careful documentation.
