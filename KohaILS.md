# Installing and Configuring Koha ILS

## Week 13
### 2026-04-20

## Overview

This project involved installing **Koha** as the final major part of the library website project. In earlier assignments, I installed **WordPress** as the main public-facing website and **Omeka Classic** as a digital library platform. In this final stage, I installed **Koha** to add a library catalog and integrated library system (ILS) component.

Koha is different from WordPress and Omeka because it is not just a content platform. It is a library system that supports catalog searching, staff-side administration, and the structure needed for a working OPAC. The goal of this assignment was to install Koha on a Linux server, complete the initial web-based setup, and connect the final result back to the larger library website project.

## Environment

- VM Provider: Google Cloud
- OS: Ubuntu 24.04.4 LTS
- Web Server: Apache2
- Database Server: MariaDB
- Library System: Koha ILS
- Staff Interface Port: 8080
- OPAC Port: 8081

## Files in This Repo

- `README.md` — repository overview and summary of completed course work
- `KohaILS.md` — summary of the Koha installation and configuration process
- previous documentation files for WordPress, Omeka, MySQL, PHP, and OPAC work

## Steps Completed (High-Level)

1. Created and prepared a new Ubuntu virtual machine for the Koha installation.
2. Updated the package lists, upgraded installed software, and cleaned unused packages.
3. Installed missing tools on the minimized Ubuntu image, including `tmux` and `nano`, when needed.
4. Added the Koha package repository and signing key.
5. Fixed a key file naming issue so the Koha repository could be verified by `apt`.
6. Installed MariaDB as the database backend for Koha.
7. Confirmed that the `koha-common` package was available from the repository.
8. Installed `koha-common` and its large set of dependencies.
9. Edited `/etc/koha/koha-sites.conf` to use port `8080` for the staff interface and `8081` for the OPAC.
10. Enabled required Apache modules, including `rewrite` and `cgi`.
11. Created the Koha instance with `sudo koha-create --create-db bibliolib`.
12. Disabled Apache’s default site and confirmed the `bibliolib` site was enabled.
13. Updated Apache so it would listen on ports `8080` and `8081`.
14. Retrieved the Koha installer credentials with `sudo koha-passwd bibliolib`.
15. Completed the browser-based Koha setup and loaded the required system data.
16. Verified that the Koha staff and public interfaces could load in the browser.
17. Updated the WordPress site so it could serve as the public-facing homepage linking out to Omeka and the Koha OPAC.

## Important Configuration Details

Several small configuration details were necessary for the Koha install to work correctly:

- The Koha repository key had to match the exact path listed in the `Signed-By` field.
- The repository file path had to be `/etc/apt/sources.list.d/koha.sources`, not `/etc/apt/source.list.d/koha.sources`.
- The Apache modules `rewrite` and `cgi` had to be enabled before `koha-create` would complete.
- `/etc/koha/koha-sites.conf` had to be updated so the instance used:
  - `INTRAPORT="8080"`
  - `OPACPORT="8081"`
- Apache’s `/etc/apache2/ports.conf` had to be updated so it would listen on ports `8080` and `8081`, not just port `80`.
- The Koha instance was created with the name `bibliolib`, which also affected the site configuration and installer credentials.

These details were important because the Koha installation depended on the package repository, Apache, MariaDB, Koha configuration files, and browser-based installer all matching correctly.

## Issues Encountered

The Koha installation involved more troubleshooting than some of the earlier web application assignments because the new VM was a minimized Ubuntu image and did not include several basic tools by default.

One early issue was that `tmux` was not installed. I installed it successfully, but the minimized system still did not include the full man page setup. Since that was not required to continue, I moved on with the Koha installation.

Another issue was that `nano` was not installed, which prevented me from editing `/etc/koha/koha-sites.conf` at first. Installing `nano` fixed that problem.

I also ran into a repository verification error because the Koha signing key file name did not match the path expected by the `Signed-By` line in the repository configuration. Renaming the key file corrected that problem and allowed `apt update` to complete successfully.

When I created the Koha instance, the process stopped twice because Apache required additional modules. First I had to enable `mod_rewrite`, and then I had to enable `mod_cgi`. After restarting Apache and rerunning the command, the Koha instance was created successfully.

The most important troubleshooting step came when the Koha staff page would not load on port `8080`. The problem turned out to be that Apache was only listening on port `80`, even though Koha had already been configured to use `8080` and `8081`. Updating `/etc/apache2/ports.conf` to include those ports fixed the connection problem and allowed the site to load in the browser.

## What I Learned

This project helped me understand how much more complex a full library system is than a general website or digital exhibit platform. WordPress and Omeka mainly focused on web publishing, but Koha required more detailed coordination among the package repository, Apache modules, MariaDB, Koha configuration files, ports, and the browser installer.

It also reinforced the idea that web applications do not fail only because of bad code. Small configuration issues—such as a file path typo, a missing Apache module, or Apache not listening on the correct port—can stop the entire system from working even when the main software is installed correctly.

Another thing that became clearer is how the three systems now fit together as part of a broader library web environment:

- **WordPress** serves as the public-facing homepage.
- **Omeka** serves as the digital library.
- **Koha** serves as the OPAC and integrated library system.

That made this final project feel much closer to a real systems librarianship workflow, where different web tools are installed separately but need to work together as one public service environment.

## Live Links

- [WordPress Site:](http://34.173.94.120/wordpress/)
- [Koha OPAC:](http://34.45.17.203:8081/)

## Reflection

This was the most systems-focused installation in the project because it required attention to the operating system, package repositories, Apache modules, Apache ports, database setup, instance creation, and browser-based configuration all at the same time. Earlier assignments helped build the background for that, but Koha made the relationships among those layers much more visible.

What stood out most to me is that a working installation depended on details that were easy to overlook. A missing text editor, a mismatch in the repository key filename, disabled Apache modules, or Apache listening on the wrong port could all stop progress. None of those were especially large problems by themselves, but each one mattered. That reinforced why careful documentation is so important in this course. The process is not just about reaching a working result. It is also about recording the steps clearly enough that I could repeat them later or understand where something broke.

This project also helped me see the final library website as a connected system rather than a series of separate assignments. WordPress, Omeka, and Koha each serve a different purpose, but together they form a more complete library web presence. That made this installation feel like the final piece of the larger course project rather than just another isolated software setup.

## Return

## Apache Restart Fix
### 2026-04-20

When completing the the documentation for [Library-Web-Architecture](https://github.com/nlr21417/ls624/blob/main/Library-Web-Architecture.md) I could no longer get my [Koha ILS](http://34.45.17.203:8081/), to open so I went back through: the first check showed that nothing was listening on ports `8080` or `8081`. Apache was also in a failed state even though the configuration syntax tested as valid.

Using the Apache error log, I found that the failure was related to the Apache accept mutex:

### 1. Check whether Apache is listening on the Koha ports
sudo ss -tlnp | grep -E ':8080|:8081'

### 2. Check Apache service status
sudo systemctl status apache2

### 3. Check what ports Apache is configured to listen on
grep -E '^Listen' /etc/apache2/ports.conf

### 4. Test Apache configuration syntax
sudo apachectl configtest

### 5. Read recent Apache service logs
sudo journalctl -u apache2 -n 50 --no-pager

### 6. Read the Apache error log
sudo tail -n 50 /var/log/apache2/error.log

- `couldn't grab the accept mutex`
- `MPM run failed, exiting`

*(learned what mutex means - please get a chuckle out of this, also how did people code before there was internet and group think???)*

### 7. Check for an existing Mutex directive
sudo grep -R '^Mutex' /etc/apache2 2>/dev/null

### 8. Edit Apache config to add the mutex fix
sudo nano /etc/apache2/apache2.conf

Because there was no existing `Mutex` directive in the Apache configuration, I added the following line to `/etc/apache2/apache2.conf`:

#### added this line:
```apache
Mutex file:/var/lock/apache2 mpm-accept
```
### 9. Re-test configuration after editing
sudo apachectl configtest

### 10. Restart Apache
sudo systemctl restart apache2

### 11. Confirm Apache is running again
sudo systemctl status apache2

### 12. Confirm Apache is listening again on 8080 and 8081
sudo ss -tlnp | grep -E ':8080|:8081'

# Yay and finally *WHEW*




