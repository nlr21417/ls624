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
- PHP Version: 8.3.6 
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


## Issues Encountered
- None during intallation and testing

## Reflection 
What clicked for me is that PHP isn’t executed in the browser like JavaScript. Apache runs the PHP on the server and sends back the resulting HTML.
Updating DirectoryIndex helped me understand how Apache decides what file to serve by default, and why index.php can “override” index.html when it appears first in the list. 
This repeats what was discussed earlier about order being important in the command line.
