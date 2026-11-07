---
title: "Overview of BytePlus CDN"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview-of-byteplus-cdn"
---

BytePlus CDN is a content delivery network service that accelerates the delivery of your web and mobile content to users worldwide. By caching content on a global network of over 3,500 nodes with a bandwidth capacity of over 150 Tbps, it reduces latency and significantly improves website performance and user experience. This document introduces how the CDN works and details its key benefits, including improved performance, enhanced security, and robust monitoring.

CDN aims to provide accelerated and more reliable web content delivery by effectively reducing the distance between data sources and end users. Supported protocols include HTTP, HTTPS, WebSocket, QUIC, HLS, DASH, HDS, and more. This network architecture is crucial for improving website loading times, enhancing video streaming quality, and reducing file download times. These capabilities are essential for meeting the demands of today's data\-intensive online environment.

## How it works

When your domain is connected to the CDN, the CDN will handle user requests. If the requested file is not cached by the CDN, the CDN will first request the file from the origin server. After receiving the file from the origin server, the CDN will cache the file. This reduces the traffic to the origin server, thereby lowering the bandwidth costs and the risk of server failures.

Assume a user requests a file on your site. The URL of the file is `https://www.example.com/file`. The request process is as follows:

1. The user enters `https://www.example.com/file` in the browser's address bar.

2. Based on the DNS resolution of `www.example.com`, the browser obtains the IP address of a CDN cache node. This cache node is the closest to the user.

3. The browser requests the file from this cache node.

   > **说明**

   * > If the cache node does not have a cached copy of the file, it requests the file from the origin server and then caches it.

4. The CDN sends the cached file to the user.

## How it benefits

The benefits of using BytePlus CDN to deliver content include:

* **Improved user experience**

   BytePlus CDN supports modern protocols, including HTTP/HTTPS and QUIC, and utilizes self\-developed cache software to improve site performance for web and mobile users. Based on its multilevel cache organization, BytePlus CDN delivers data, such as large files, static images, and streaming media, more quickly.

* **Stable performance with high flexibility**

   With its self\-developed resource planning system and real\-time resource scheduling and allocation system, it distributes user requests and serves content intelligently and reliably.

* **Effective balance of speed and security**

   BytePlus CDN uses HTTPS to implement end\-to\-end data encryption, ensuring secure data transmission and protecting your site from hotlinking and session hijacking. It allows you to configure access controls by offering options for a Referer blocklist and allowlist, IP blocklist and allowlist, and URL authentication.

* **Multi\-dimensional monitoring**

   BytePlus CDN is tightly integrated with monitoring, providing detailed daily, weekly, and monthly metrics for data transferred, bandwidth, and requests.

* **Support for dynamic resource transfer acceleration**

   For dynamic resources, the CDN uses path probing technology to select the optimal path for forwarding requests to the origin server, enabling clients to quickly obtain dynamic resources.
