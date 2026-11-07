---
title: "Application Scenarios"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-application-scenarios"
---

This document introduces the main application scenarios of BytePlus DNS.

<span id="网站"></span>
## Websites

Website domain names can be resolved to the IP addresses of web servers through A records or AAAA records. Users can then use domain names in their browsers to access your sites and various web applications.

<span id="电子邮件"></span>
## Email

Based on the configuration provided by your email service provider, you can create MX records. Users can then use domain email addresses to send and receive emails.

<span id="cdn-services-or-load-balancing-services"></span>
## CDN services or load balancing services

You can create CNAME records to:


* Point your domain name to a CNAME provided by a CDN service provider. This way, your business can be accelerated through CDN.

* Point your domain name to a CNAME provided by a load balancing service provider. This way, your business can use load balancing services.


<span id="avoiding-cross-region-access"></span>
## Avoiding cross\-region access

For users distributed across different regions, BytePlus DNS can return IP addresses or domain names you specify according to your configuration, thereby avoiding issues such as cross\-region access.

<span id="load-balancing"></span>
## Load balancing

BytePlus DNS can return IP addresses or domain names you specify in response to DNS queries according to your load balancing configuration. This means:


* When a domain name corresponds to multiple servers, BytePlus DNS can distribute user requests to different servers proportionally.

* When a domain name corresponds to CNAMEs of multiple CDN services or load balancing services, BytePlus DNS can distribute user requests to different CDN services or load balancing services proportionally.
