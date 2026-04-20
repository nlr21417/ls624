# Installing and Configuring Koha ILS

## Week 13

### 2026-04-20

## Overview

This project involved installing **Koha** as the final major piece of the library website project. In the earlier parts of the project, I installed **WordPress** as the main website and **Omeka Classic** as a digital library platform. For this final section, I installed **Koha**, an integrated library system (ILS), to add a more complete library management and OPAC component to the server. The course text frames this as the last part of the library web infrastructure project and describes Koha as the system that adds modules such as patron management, circulation, cataloging, serials, acquisitions, reports, and an OPAC. :contentReference[oaicite:0]{index=0}

## Environment

- VM Provider: Google Cloud
- OS: Ubuntu 24.04 LTS
- Web Server: Apache2
- Database: MariaDB
- Library System: Koha ILS
- Staff Interface Port: 8080
- OPAC Port: 8081

## Files in This Repo

- `README.md` — repository overview and summary of the Koha assignment
- `Koha-setup.md` — summary of the Koha installation and configuration process
- other course documentation files for the earlier WordPress, Omeka, and OPAC assignments

## Steps Completed (High-Level)

1. Created a new Google Cloud virtual machine with more memory and storage because Koha requires more resources than the earlier WordPress and Omeka installs.
2. Added the required Google Cloud firewall rules and network tags so the Koha staff interface and public OPAC could load on ports `8080` and `8081`.
3. Updated the server and cleaned unused packages before beginning the Koha installation.
4. Added the Koha package repository and signing key so the software could be installed through `apt`.
5. Installed MariaDB because the course setup uses MariaDB as the database backend for Koha.
6. Installed the `koha-common` package.
7. Edited `/etc/koha/koha-sites.conf` so the staff interface would use port `8080` and the public OPAC would use port `8081`.
8. Enabled the required Apache modules and updated Apache so it would listen on the Koha ports.
9. Created a Koha instance with `koha-create --create-db bibliolib`.
10. Disabled the default Apache site and enabled the Koha site configuration.
11. Retrieved the Koha installer username and password with `koha-passwd bibliolib`.
12. Completed the remaining setup through the Koha web installer.
13. Verified that the staff interface loaded on port `8080` and the public OPAC loaded on port `8081`. :contentReference[oaicite:1]{index=1}

## Issues Encountered

The biggest difference between Koha and the earlier installations was that Koha required a separate VM with more RAM and a more involved network setup. Unlike WordPress and Omeka, Koha also depended on separate ports for the staff side and public OPAC, so the Google Cloud firewall rules, network tags, Apache configuration, and Koha site configuration all had to match. The course notes specifically warn that if the site does not load, the most common causes are missing network tags, incorrect firewall rules, or Apache not listening on the correct ports. :contentReference[oaicite:2]{index=2}

Another thing that stood out is that Koha is more complex than the earlier applications because it is a full integrated library system rather than just a CMS or digital exhibit platform. That meant the installation involved more system configuration before the browser-based setup could begin. The course text also recommends using `tmux` during installation because the Koha package install can take a while and should continue even if the SSH session drops. :contentReference[oaicite:3]{index=3}

## What I Learned

This project helped me better understand how a full library system fits into the larger web environment I had already been building. WordPress served as the public-facing website, Omeka served as the digital library, and Koha added the more traditional ILS functions such as cataloging, circulation, patron records, and the OPAC. The course text presents this as the final step in connecting multiple library web services together, which made the overall project feel much closer to a real systems librarianship workflow. :contentReference[oaicite:4]{index=4}

I also learned that Koha installation depends on much more than just installing a package. The firewall rules, Apache modules, Apache ports, Koha configuration files, database backend, and web installer all have to line up correctly before the system works. That reinforced the same lesson from the earlier assignments: a working web application depends on multiple services and configuration files working together, not just the software being present on the server. :contentReference[oaicite:5]{index=5}

## Reflection

This installation felt like the most “systems” oriented part of the project because it required me to think about the server, the firewall, Apache, the database, package repositories, and the web interface all at the same time. Earlier assignments helped build the foundation for that, but Koha made the connections among those pieces much more obvious. It also made clear why documentation matters so much in this course. The class notes emphasize that documentation should be clear, reproducible, organized in Markdown, and honest about both the process and the problems, because a working system without documentation is incomplete. I approached this write-up in that same summary style so it fits the documentation pattern I have been using in the repo already. :contentReference[oaicite:6]{index=6} :contentReference[oaicite:7]{index=7}

## Live Access

- Staff Interface: `http://YOUR-IP-ADDRESS:8080`
- Public OPAC: `http://YOUR-IP-ADDRESS:8081`

## Notes

For GitHub, I would avoid posting any real Koha installer passwords or administrator credentials publicly. Earlier notes in this project also flagged that passwords should be replaced with placeholders before pushing documentation to a public repo. :contentReference[oaicite:8]{index=8}
