# Install Omeka 
### April 8, 2026
## Overview

For this project, I installed and configured **Omeka Classic** on my Ubuntu server and linked it as part of the larger library website environment I have been building throughout the course. The goal was to apply the same general process used in the earlier WordPress and bare bones OPAC assignments: creating a separate database, configuring application files, managing Apache settings, and completing the setup through a web interface.

## What I Built
I installed **Omeka Classic** in its own directory on the web server and configured it to use a separate MySQL database and user account. I also adjusted Apache settings so Omeka could use its rewrite rules correctly and complete the web-based installation.


## Main Technologies Used
- Linux / Ubuntu server
- Apache web server
- MySQL database
- PHP
- Omeka Classic
- ImageMagick
- Apache `mod_rewrite`

## What This Project Helped Me Understand
This project helped me better understand how similar the installation process is across different web applications. Even though Omeka is different from WordPress and the OPAC project, the overall workflow was familiar: verify dependencies, create a new database and user, download and extract the software, edit configuration files, adjust permissions, and complete the final setup in the browser.

It also gave me more practice troubleshooting Apache and application configuration issues. I had to work through how Omeka depends not only on the database connection in `db.ini`, but also on supporting configuration files like `config.ini` and `.htaccess`, as well as Apache settings that allow rewrite rules to function properly.

## Challenges and Troubleshooting
I ran into several issues during the installation. First, the original Omeka download shortcut returned a 404 error, so I had to download the current Omeka Classic release from GitHub instead. After that, Omeka reported configuration errors because the `db.ini` file was missing the required `[database]` section. Once that was fixed, I discovered that `config.ini` and `.htaccess` had not yet been created from their `.changeme` versions. This was where I realized that we should read the installation instructions first like you noted in the presentation last week. 

The final major problem involved Apache configuration. Omeka kept reporting that `mod_rewrite` was not enabled, even though the module itself was active. The actual issue was that Apache was not fully allowing the rewrite directives in Omeka’s `.htaccess` file. Fixing the directory settings in `apache2.conf` resolved the internal server error and allowed the installation page to load correctly.

## Reflection
This assignment showed me that installing a web platform is often less about following one exact set of commands and more about understanding the relationships between the application, the database, the web server, and configuration files. Omeka followed the same general pattern as earlier assignments, but it still required careful troubleshooting when small configuration details were wrong.

Overall, this project strengthened my confidence working in the server environment and reinforced the importance of reading error messages closely, checking file locations, and understanding how Apache settings affect web applications.
