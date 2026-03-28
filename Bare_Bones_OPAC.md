# Bare Bones OPAC and Cataloging Module 
### March 28-29, 2026
## Overview

For this project, I built a very simple online public access catalog (OPAC) and a basic cataloging module using Apache, PHP, and MySQL on a Linux server. The goal was to better understand how these parts of the LAMP stack work together in a library-related web application.

The OPAC side of the project focused on displaying and searching bibliographic data stored in a MySQL database through a web interface. The cataloging side focused on creating a protected area where records could be added to the same database. Together, these exercises helped me see how a database-driven website works from both the public user side and the staff/admin side.

## What I Built

I created two connected parts:

- A toy OPAC that displays library-style book data through a web page
- A toy cataloging module that allows records to be managed through a separate interface

Live links:

- [OPAC](http://34.173.94.120/mylibrary.html)
- [Cataloging Module](http://34.173.94.120/cataloging/index.html)

## Main Technologies Used

- Linux / Ubuntu server
- Apache web server
- MySQL database
- PHP for server-side scripting
- HTML for the web interface
- Apache authentication for protecting the cataloging module

## What This Project Helped Me Understand

This project made the relationship between MySQL, PHP, Apache, and the browser much clearer. MySQL stores and organizes the data, PHP retrieves or inserts that data, Apache serves the pages, and the browser displays the results through the web interface.

Working through the database portion also helped me better understand relational databases and SQL. Creating tables, inserting records, updating data, deleting records, and running queries made the structure of a database feel much more concrete than just reading about it. I also got a better sense of how an OPAC depends on a database behind the scenes and how a cataloging module functions as a staff-facing way to add or maintain records.

## Challenges and Troubleshooting

One of the main issues I ran into was a 403 permission error on the OPAC page. This happened because the `mylibrary.html` file had incorrect permissions, which prevented the web server from reading it properly. Updating the file permissions fixed the issue and helped me better understand how Apache depends on Linux file ownership and permissions.

I also accidentally duplicated some book records in the database. Fixing that mistake gave me additional practice with SQL and showed me how easy it is to correct records directly in a table when testing.

## Reflection

Overall, this assignment helped me move beyond thinking of a website as just files in a browser. It showed me that the web interface is only one layer, and that the database, server configuration, PHP scripts, and permissions all have to work together. Building both the OPAC and the cataloging module made the system feel much more like a real, if simplified, integrated library system.
