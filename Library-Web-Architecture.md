# Library Website Architecture

## Overview

My library website is built as a small ecosystem of three connected platforms: [WordPress](http://34.173.94.120/wordpress/), [Omeka Classic](http://34.173.94.120/omeka/), and [Koha OPAC](http://34.45.17.203:8081/). Instead of forcing one platform to do every job, I used each one for the kind of work it handles best. WordPress serves as the public-facing homepage, Omeka supports the digital library, and Koha provides the catalog through its OPAC. Together, these platforms create a clearer division of roles while still functioning as one library web presence.

In this architecture, **WordPress** is the main entry point for users. It acts as the homepage and navigation layer, introducing the library and guiding visitors to the right service. From WordPress, users can move to the digital library in Omeka or to the catalog in Koha. I made this choice because WordPress is flexible and easy to use for general site content, announcements, and top-level navigation. It works well as the central “front door” of the system.

**Omeka Classic** supports the library’s digital collections and exhibits. Its role is more specialized than WordPress because it is designed for curated digital objects, media-rich collections, and exhibit-style presentation. In a real library context, Omeka would be useful for local history collections, scanned archival materials, photographs, or themed online exhibits. I linked Omeka from WordPress rather than making it the homepage because it works better as a destination for a specific type of content than as the main website itself.

**Koha** provides the public catalog through its OPAC. Its role is different from both WordPress and Omeka because it is focused on bibliographic records, catalog searching, and the structure of an integrated library system. This makes Koha the most library-specific part of the architecture. Users who want to search for books or records go to Koha, while users who want general library information stay in WordPress, and users who want digital collections move into Omeka.

The navigation is organized around that division of purpose. The WordPress homepage includes links out to the digital library and the catalog, so users do not need to understand the software structure behind the site. They only need to know where to go based on what they want to do. That is why I kept the public-facing architecture simple: one main site, with clear links to the specialized systems.

Compared with [Loudoun County Public Library](https://library.loudoun.gov/), my system is much smaller and designed for a single library environment rather than a county-wide system with many branches. Loudoun’s site currently includes branch navigation, catalog and account links, research tools, services, and a separate events calendar, which reflects the needs of a much larger organization. My setup is simpler, but the overall logic is similar: a main website handles navigation and public information, while specialized systems handle the catalog and other library services. In that way, my project mirrors real library practice on a smaller scale.

This setup would be useful in a real-world library because it keeps each system focused on its strengths. WordPress handles communication and navigation, Omeka handles digital collections, and Koha handles catalog access. That separation also makes the system easier to maintain, since each platform has a clear role in the larger ecosystem.

## Site Links

- Main Website: [WordPress](http://34.173.94.120/wordpress/)
- Digital Library: [Omeka Classic](http://34.173.94.120/omeka/)
- Catalog: [Koha OPAC](http://34.45.17.203:8081/)
- Comparison Site: [Loudoun County Public Library](https://library.loudoun.gov/)

## Diagram

```mermaid
flowchart TD
    A[Library User] --> B[WordPress Main Website]
    B --> C[Omeka Classic Digital Library]
    B --> D[Koha OPAC / Catalog]

    B --> E[General Library Information]
    C --> F[Digital Collections and Exhibits]
    D --> G[Catalog Search and Bibliographic Records]
