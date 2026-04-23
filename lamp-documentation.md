# Module 4: LAMP Documentation and Reflection

## Overview

A LAMP stack is a common web server setup made up of **Linux, Apache, MySQL, and PHP**. Linux is the operating system, Apache is the web server, MySQL is the database system, and PHP is the server-side scripting language. Together, they are often used to host dynamic websites and database-driven web applications.

This document records my process setting up a LAMP stack on an Ubuntu virtual machine hosted on Google Cloud. I followed Sean Burns’ *Systems Librarianship* text and completed the Apache, PHP, and MySQL sections in sequence. The goal was to install and configure each part of the stack, verify that each component worked correctly, and confirm that PHP and MySQL could work together through a webpage.

---

## Environment

- **VM Provider:** Google Cloud
- **OS:** Ubuntu 24.04.4 LTS
- **Web Server:** Apache2
- **PHP Version:** 8.3.6
- **MySQL Version:** 8.0.45-0ubuntu0.24.04.1 for Linux on x86_64
- **Tested From:** Google Chrome

---

## Source Used

I followed Sean Burns’ *Systems Librarianship* materials for this setup:

- [Installing the Apache Web Server](https://cseanburns.github.io/systems-librarianship/4a-installing-the-apache-web-server.html)
- [Installing and Configuring PHP](https://cseanburns.github.io/systems-librarianship/4b-installing-configuring-php.html)
- [Installing and Configuring MySQL](https://cseanburns.github.io/systems-librarianship/4c-installing-configuring-mysql.html)

---

## Apache Installation and Configuration

I began by installing and configuring Apache on my Ubuntu VM. A web server is a program that runs on a machine and responds to HTTP requests from a client such as Chrome, Safari, or Firefox. Apache serves files from a document root, which acts as the public directory for the site.

### Commands Used

```bash
sudo apt update
sudo apt upgrade
sudo apt install apache2
systemctl status apache2
````

### What I Did

After updating the system, I installed Apache and checked its status with `systemctl status apache2` to confirm that it was running. I then tested the server in the browser by visiting the public IP address of the VM. When the default Apache page loaded, that confirmed Apache was working correctly and serving pages over HTTP.

### Verification

* Apache installed without major errors
* `systemctl status apache2` showed the service as active
* The default Apache page loaded in the browser from the server’s public IP

---

## PHP Installation and Configuration

Next, I installed PHP so Apache could process server-side scripts. PHP is different from JavaScript because it runs on the server before anything reaches the browser. The browser only receives the finished output, usually HTML.

### Commands Used

```bash
sudo apt install php libapache2-mod-php php-cli
php -v
sudo systemctl restart apache2
```

### What I Did

I installed PHP and the Apache PHP module, then restarted Apache so it could process `.php` files. To verify the setup, I created an `info.php` file in the document root using `phpinfo()` and loaded it in the browser. This showed that PHP was installed and working correctly with Apache.

I also edited Apache’s `DirectoryIndex` settings so that `index.php` would be prioritized over `index.html`. That made the PHP page the default page served when I visited the root of the site.

### Configuration Changes

I edited Apache’s directory index configuration so that `index.php` would load first. This reinforced how much system behavior depends on order and configuration rules.

### Verification

* `php -v` confirmed PHP was installed
* `info.php` loaded correctly in the browser
* Apache served `index.php` after I changed the `DirectoryIndex` order
* I also tested the detector page from another device and browser, and it correctly identified the browser and operating system


---

## MySQL Installation and Configuration

The final part of the stack was installing and configuring MySQL. MySQL provides the database layer of the LAMP stack and stores structured data that PHP can retrieve and display.

### Commands Used

```bash
sudo apt update
sudo apt upgrade
sudo apt autoremove
sudo apt clean
sudo apt install mysql-server
mysql --version
systemctl status mysql
sudo mysql_secure_installation
sudo mysql -u root
```

### What I Did

After installing MySQL, I checked the version and confirmed that the service was running. I then ran `mysql_secure_installation` to apply the basic security recommendations. After that, I logged into MySQL as the root user and created a regular user account and a practice database.

### Creating the User and Database

Inside MySQL, I created a new user and a database for practice work:

```sql
create user 'opacuser'@'localhost' identified by 'YOUR_PASSWORD';
create database opacdb default character set utf8mb4 collate utf8mb4_0900_ai_ci;
grant all privileges on opacdb.* to 'opacuser'@'localhost';
show databases;
```

This created a regular MySQL user and a database called `opacdb`, which I used for the rest of the lab.

### Creating and Testing the Table

After logging in as the regular MySQL user, I created a `books` table:

```sql
create table books (
    id int unsigned not null auto_increment,
    author varchar(150) not null,
    title varchar(150) not null,
    copyright year not null,
    primary key (id)
);
```

I then inserted records and practiced common SQL commands such as:

```sql
insert into books (author, title, copyright) values
('Jennifer Egan', 'The Candy House', '2022'),
('Imbolo Mbue', 'How Beautiful We Were', '2021'),
('Lydia Millet', 'A Children\'s Bible', '2020'),
('Julia Phillips', 'Disappearing Earth', '2019');

select * from books;
select author from books;
select author, title from books;
alter table books add publisher varchar(75) after title;
update books set publisher='Simon & Schuster' where id='1';
delete from books where author='Julia Phillips';
```

This let me practice selecting, altering, updating, deleting, and inserting records in the database.

### Connecting PHP and MySQL

To connect PHP to MySQL, I installed PHP support for MySQL:

```bash
sudo apt install php-mysql
sudo systemctl restart apache2
sudo systemctl restart mysql
```

Then I created a `login.php` file in `/var/www` rather than in the public web directory. This file stored the database credentials:

```php
<?php // login.php
$db_hostname = "localhost";
$db_database = "opacdb";
$db_username = "opacuser";
$db_password = "YOUR_PASSWORD";
?>
```

I set the file permissions so Apache could read it without making it publicly accessible:

```bash
cd /var/www
sudo touch login.php
sudo chmod 640 login.php
sudo chown :www-data login.php
ls -l login.php
```

After that, I created `opac.php` in `/var/www/html` to connect to the database, run queries, and display the results in the browser.

### Verification

I tested the PHP files from the command line:

```bash
sudo php -f /var/www/login.php
sudo php -f /var/www/html/opac.php
```

Then I opened the page in the browser and confirmed that the records from the `books` table displayed correctly.

### Link to Site



---

## How I Verified the Full LAMP Stack

I verified the stack in stages:

1. **Apache** worked when the server responded in the browser and served the default page.
2. **PHP** worked when `phpinfo()` displayed correctly and `index.php` rendered through Apache.
3. **MySQL** worked when I could log in, create users and databases, and run SQL commands successfully.
4. **PHP and MySQL together** worked when `opac.php` connected to the database, queried the `books` table, and displayed the results in the browser.

This step-by-step verification helped me confirm not only that each component worked on its own, but that they also worked together as one system.

---

## Challenges Encountered

I did not run into major installation errors, but I did have a few smaller issues.

One challenge was catching typos in commands. In a few cases, I could only get commands to work after pasting them into a Word document and comparing them more carefully. I could not always immediately spot whether I had missed a space or typed the wrong character.

Another issue came from using the wrong editor earlier in the course. I meant to use Nano, but I accidentally opened `vi`, got stuck, and had to recover from that mistake. That taught me to pay closer attention to which editor I was using and also showed me the value of opening a second SSH session if I need to check help pages while working.

The main MySQL-specific mistake I made was in `login.php`, where I forgot to replace the placeholder text with my actual password. Once I fixed that, the connection worked the way it was supposed to. That mistake was helpful because it forced me to troubleshoot the problem and understand the connection process more clearly.

---

## Reflection on the Experience

Several aspects of the setup process felt straightforward by the time I reached MySQL because the earlier labs had already helped me get more comfortable with the command line and with the general structure of the server. Installing packages, checking service status, restarting services, and testing in the browser all started to feel more familiar through repetition. Typing the commands myself also helped. By working through them step by step, I could feel the process becoming more natural, and that made the lab feel less intimidating than some of the earlier assignments.

The main challenges I faced were not major technical failures, but smaller issues involving attention to detail. One recurring problem was finding typos in commands. Sometimes I knew I had entered something incorrectly, but I could not immediately tell whether the problem was a missing space, an extra character, or something else small. Comparing the commands more carefully helped me fix those mistakes. Another challenge came from my earlier experience of accidentally opening `vi` instead of Nano. That taught me to slow down and pay closer attention to the tools I am using. In the MySQL part of the lab, my main mistake was forgetting to replace the placeholder password in `login.php` with the actual password I had created. Once I corrected that, the PHP page connected to the database properly.

This exercise connects to real-world systems librarianship because library systems depend on web servers, databases, authentication systems, and well-documented infrastructure. A systems librarian may need to support online catalogs, digital collections, proxy services, user authentication, and other web-based tools. Understanding how Apache, PHP, and MySQL work together makes it easier to understand how those services are built and maintained. It also reinforces the value of careful documentation, troubleshooting, and reproducibility. This assignment showed me that even when the individual parts seem simple, the real skill is understanding how they connect into a working system.

---

## Links

* **GitHub Repo:** [ls624](https://github.com/nlr21417/ls624)

```
```
