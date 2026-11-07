---
title: "Basic concepts"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-basic-concepts"
---

BytePlus Content Delivery Network (CDN) uses a specialized set of terms to describe how it accelerates content delivery globally. This document serves as a glossary, defining fundamental concepts such as cache hit, origin server, and Time to Live (TTL). Familiarizing yourself with this terminology is essential for configuring your CDN services and interpreting performance metrics.


* **cache hit**: Occurs when a client requests content from a cache and the cache can fulfill the request.

* **cache miss**: Occurs when a client requests content from a cache and the cache cannot fulfill the request.

* **cache node**: These are the nodes where the CDN stores copies of the origin server's content to reduce traffic to the origin server and accelerate content distribution. In the CDN architecture, cache nodes are divided into two levels: edge nodes, which are close to the user, and regional nodes, which are close to the origin server.

* **CNAME**: The canonical name. A CNAME record is a resource record type in the Domain Name System. It maps one domain name (an alias) to another (the canonical name).

* **DNS (Domain Name System)** : A naming system that translates a domain name (for example, www.byteplus.com) into a specific IP address (for example, 192.0.2.1).

* **hit ratio**: Calculated by dividing the number of cache hits by the total number of requests (the sum of hits and misses). It measures how effective a cache is at fulfilling requests for content.

* **origin fetch**: The process of transferring data from the origin server to edge locations.

* **origin server**: A computer running one or more programs that are designed to listen to and respond to incoming requests. In the context of a CDN, it serves content for a website or web page.

* **TTL (Time to Live)** : The length of time that data is stored in a caching system before it is discarded or refreshed.
