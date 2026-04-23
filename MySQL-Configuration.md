# Installing and Configuring MySQL
## Week 9
### 2026-03-11 & 2026-03-12


## Overview
This document records my process for installing and configuring MySQL as part of completing the LAMP stack on my Linux virtual machine.  
The goal of this lab is to install MySQL, secure it, create a database and regular user, create and test a table, connect MySQL with PHP, and verify that the database content displays correctly in the browser.


## Environment
- VM Provider: Google Cloud
- OS: Ubuntu 24.04.4 LTS
- MySQL Version: 8.0.45-0ubuntu0.24.04.1 for Linux on x86_64
- Tested From: Google Chrome

## Files in This Repo
- `mysql-install.md` — step-by-step notes for installing and configuring MySQL, creating a database and user, and testing SQL commands
- `README.md` — repository overview and summary of what was completed

## Steps Completed (High-Level)
1. Updated the Ubuntu system packages.
2. Installed MySQL server.
3. Verified the MySQL version and service status.
4. Ran `mysql_secure_installation` to apply basic security settings.
5. Logged in as the MySQL root user.
6. Created a regular MySQL user and a practice database.
7. Created the `books` table and inserted test records.
8. Ran `select`, `update`, `delete`, `insert`, and `alter table` commands.
9. Installed PHP support for MySQL.
10. Created `login.php` with database credentials and set secure permissions.
11. Created `opac.php` to retrieve and display database records.
12. Tested PHP syntax and verified the page in the browser.



## Issues Encountered
- I did not run into major installation errors, but I could only get some of the commands to work if I pasted them from your guide into a word document. I couldn't personally find my typos, so I'm sure it was a space or lack of space issue. I just couldn't determine what actual character area I was messing up. 
- The `login.php` file location and permissions was the only hiccup, I got an error because I didn't put in the actual password. 

## Reflection 
By typing in each command I felt my fingers become more familiar with the process. I actually liked the additional commands and repetition. We had done something similar in an earlier assignment that ended up confusing me, but I can see with this round that it is becoming easier. 
