# Installing and Configuring MySQL
## Week 9
### 2026-03-11


## Overview
This document records my process for installing and configuring MySQL as part of completing the LAMP stack on my Linux virtual machine.  
The goal of this lab is to install MySQL, secure it, create a database and regular user, create and test a table, connect MySQL with PHP, and verify that the database content displays correctly in the browser.


## Environment
- VM Provider: Google Cloud
- OS: Ubuntu 24.04.4 LTS
- Hostname:
- MySQL Version: 8.0.45-0ubuntu0.24.04.1 for Linux on x86_64
- Public IP Address:
- Tested From: Google Chrome

## Files in This Repo
- `php-setup.md` — step-by-step installation/configuration notes (commands + config edits)
- `README.md` — overview + what was accomplished

## Steps Completed (High-Level)
1. Installed PHP and the Apache PHP module.
2. Restarted/reloaded Apache and verified service status.
3. Created and tested `info.php` (then removed it for security).
4. Updated Apache `DirectoryIndex` to prioritize `index.php`.
5. Created `index.php`.


[Nancy Roberts' Webpage](http://35.192.178.142/)

## Issues Encountered
- None during intallation and testing

## Reflection 
What clicked for me is that PHP isn’t executed in the browser like JavaScript. Apache runs the PHP on the server and sends back the resulting HTML.
Updating DirectoryIndex helped me understand how Apache decides what file to serve by default, and why index.php can “override” index.html when it appears first in the list. 
This repeats what was discussed earlier about order being important in the command line.
