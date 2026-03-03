# Apache + PHP Setup (Browser/OS Detector)
## Week 8
### 2026-03-03


## Overview
This repository documents my process installing and configuring PHP to work with the Apache web server on a Linux virtual machine.  
The goal was to verify PHP server-side execution using a `phpinfo()` test file and a browser/OS detection script (`index.php`).

## Environment
- VM Provider: Google Cloud
- OS: Ubuntu 24.04.4 LTS
- Web Server: Apache2
- PHP Version: PHP 8.3.6 (cli) (built: Jan  7 2026 08:40:32) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.3.6, Copyright (c) Zend Technologies
    with Zend OPcache v8.3.6, Copyright (c), by Zend Technologies
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
