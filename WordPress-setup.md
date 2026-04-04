# Installing and Configuring WordPress

## Week 12

### 2026-04-04

## Overview

This document records my process for installing and configuring WordPress on my Linux virtual machine. The goal of this lab was to verify that the server met the software requirements, install the required PHP modules, download and extract WordPress, create the WordPress database and user in MySQL, configure `wp-config.php`, troubleshoot the setup, and complete the browser-based installation.

## Environment

- VM Provider: Google Cloud
- OS: Ubuntu 24.04.4 LTS
- Web Server: Apache2
- PHP Version: 8.3.6
- MySQL Version: 8.0.45-0ubuntu0.24.04.1 for Linux on x86_64
- Tested From: Web browser using server IP address

## Files in This Repo

- `README.md` — repository overview and summary of the WordPress assignment
- `wordpress-install.md` — summary of the WordPress installation and configuration process
- other course documentation files as needed for related setup work

## Steps Completed (High-Level)

1. Verified the Ubuntu, PHP, and MySQL versions met the WordPress requirements.
2. Installed the additional PHP modules needed for WordPress.
3. Restarted Apache2 and MySQL after installing the PHP extensions.
4. Downloaded the latest WordPress package from WordPress.org.
5. Installed `unzip` after discovering it was not already available on the server.
6. Extracted WordPress into `/var/www/html/wordpress`.
7. Created the `wordpress` MySQL user and the `wordpress` database.
8. Granted the WordPress user privileges on the WordPress database.
9. Copied `wp-config-sample.php` to `wp-config.php`.
10. Updated the WordPress database configuration settings in `wp-config.php`.
11. Troubleshot the site when it would not load and found that the sample database placeholders had not been replaced.
12. Corrected the database configuration and completed the install script in the browser.
13. Confirmed that the WordPress site loaded successfully.

## Issues Encountered

- I first tried downloading WordPress without `sudo`, which caused a permissions error when writing `latest.zip`.
- The `unzip` command was not installed, so I had to install it before extracting the WordPress archive.
- I made a typo in the MySQL command by writing `indentified` instead of `identified`, which caused repeated SQL syntax errors.
- WordPress would not load at first because `wp-config.php` still contained the default sample value `database_name_here` instead of the real database information.
- I had to troubleshoot the site by checking the WordPress directory, Apache status, MySQL status, and Apache error log before identifying the real configuration problem.

## Reflection

This assignment was a good reminder that technical work depends on careful attention to detail. The overall WordPress process was not conceptually difficult, but several small mistakes slowed me down: forgetting `sudo`, not having `unzip` installed, making a typo in a MySQL command, and leaving the default sample values in `wp-config.php`. None of those problems were huge on their own, but each one prevented the installation from working until I found the exact cause.

What stood out most to me is that a working web application depends on multiple systems connecting correctly: Apache, PHP, MySQL, file permissions, and configuration files. Even after the software was downloaded and the services were running, WordPress still would not work until the configuration file was updated properly. This made the troubleshooting part just as important as the installation itself.

If I were repeating this process, I would still document the errors as they happen because that is where most of the learning takes place. The final result matters, but the mistakes and corrections are what made the process easier to understand.

## Result

The WordPress installation completed successfully, and the site loaded through the browser using the server IP address and the `/wordpress/` directory.
