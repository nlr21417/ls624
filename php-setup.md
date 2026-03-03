# Apache + PHP Setup (Browser/OS Detector)
## Week 8
### 2026-03-03


## Overview
This repository documents my process installing and configuring PHP to work with the Apache web server on a Linux virtual machine.  
The goal was to verify PHP server-side execution using a `phpinfo()` test file and a browser/OS detection script (`index.php`).

## Environment
- VM Provider: <!-- ex: Google Cloud / AWS / VirtualBox / etc. -->
- OS: <!-- ex: Ubuntu 22.04 LTS -->
- Web Server: Apache <!-- add version if you know it -->
- PHP Version: <!-- paste from `php -v` -->
- Tested From: <!-- ex: Firefox on Windows, Safari on iPhone, etc. -->

## Files in This Repo
- `php-setup.md` — step-by-step installation/configuration notes (commands + config edits)
- `README.md` — overview + what was accomplished

## Steps Completed (High-Level)
1. Installed PHP and the Apache PHP module.
2. Restarted/reloaded Apache and verified service status.
3. Created and tested `info.php` (then removed it for security).
4. Updated Apache `DirectoryIndex` to prioritize `index.php`.
5. Created `index
