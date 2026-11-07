---
title: "What is BytePlus DNS"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-what-is-byteplus-dns"
---

BytePlus DNS provides authoritative DNS service for public domain names.

For example, if you have created a website, and the IP address of the website server on the internet is:


* IPv4 address: `203.0.113.0`

* IPv6 address: `2001:db8::`


Since IP addresses are difficult to remember, you want users to be able to easily remember your website. To achieve this, you can assign a domain name to the website, such as `www.example.com`. At the same time, you create two DNS records for the domain name, which resolve `www.example.com` to the IPv4 and IPv6 addresses of the website server. This way, users can access your website through the domain name.

<span id="feature-overview"></span>
## Feature overview

BytePlus DNS supports the following features.

<span id="dnssec"></span>
### DNSSEC

You can enable DNSSEC (DNS Security Extension) for your domain names.

<span id="intelligent-dns"></span>
### Intelligent DNS

BytePlus DNS returns appropriate IP addresses based on the source of user traffic. The source of user traffic can be ISPs, geolocations, cloud vendors, or IP address ranges.

<span id="load-balancing"></span>
### Load balancing

If a record set contains multiple record values, and each record value has a weight, BytePlus DNS calculates the sum of weights for all record values in the set and determines the weight proportion of each record value. Based on these proportions, BytePlus DNS returns the corresponding record value when responding to DNS queries of the same proportion.

<span id="subdomain-delegation"></span>
### Subdomain delegation

You can use the subdomain delegation feature to manage the DNS of one or multiple subdomains separately.

<span id="import-export-and-backup-of-dns-records"></span>
### Import, export, and backup of DNS Records

You can import external DNS records into BytePlus DNS, and export DNS records from BytePlus DNS to files. Additionally, you can backup DNS records.

<span id="view-dns-query-metrics"></span>
### View DNS query metrics

You can gather statistics on the number of DNS queries sent by recursive DNS servers to BytePlus DNS, categorized by DNS status, record type, ISP, cloud vendor, geolocation, and other dimensions.
