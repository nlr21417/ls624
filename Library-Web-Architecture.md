# Library Website Architecture

## Overview

My library website is built as a small ecosystem of three connected platforms: **WordPress**, **Omeka Classic**, and **Koha**. Instead of trying to make one platform do everything, each system handles the part of the library web presence it is best suited for. WordPress serves as the public-facing homepage, Omeka provides the digital library and exhibit space, and Koha provides the catalog through its public OPAC. Together, these platforms create a clearer separation of functions while still presenting users with a unified library website.

In this setup, **WordPress** acts as the main entry point. It is the first site a visitor sees and works as the central navigation layer. From WordPress, users can move to the Omeka digital library or to the Koha catalog. This makes WordPress function like the “front desk” of the web presence: it introduces the library, explains what the site offers, and directs people to the correct tool depending on what they want to do.

**Omeka Classic** supports the library’s digital collections. Its role is different from the catalog because it is designed for curated digital objects, online exhibits, and more media-rich presentation. In a real-world library, this would be useful for photographs, archival scans, local history materials, and themed digital exhibits. Omeka is not the main homepage because it is more specialized. Instead, it fits best as a linked destination from the public site.

**Koha** provides the OPAC, which is the search and access point for catalog records. In this project, Koha represents the more traditional integrated library system side of library work. While WordPress explains the library and Omeka presents digital collections, Koha supports catalog searching and the structure of a real library system. This separation is important because users looking for books or bibliographic records need a different interface than users browsing exhibits or general website information.

The navigation is organized around this division of purpose. The homepage in WordPress includes links to the digital library and to the catalog so that users can move between systems without needing to know which software is running underneath. This is an intentional architectural decision. Rather than blending all functions into one interface, the design keeps each platform focused on its strengths while making the transitions between them simple and visible.

This architecture would be useful in a real-world library context because many libraries already rely on multiple systems rather than a single all-in-one platform. Public and academic libraries often use a CMS for the main website, a separate catalog or discovery layer, and another platform for digital collections. My setup mirrors that pattern on a smaller scale. It is also easier to maintain because each platform has a distinct role: WordPress for communication and navigation, Omeka for digital collections, and Koha for the catalog. A colleague maintaining this system would need to understand that the overall web presence depends not on one application, but on the connections among all three.

## Diagram

```mermaid
flowchart TD
    A[Library User] --> B[WordPress Main Website]
    B --> C[Omeka Classic Digital Library]
    B --> D[Koha OPAC / Catalog]

    B --> E[General Library Information]
    C --> F[Digital Collections and Exhibits]
    D --> G[Catalog Search and Bibliographic Records]
