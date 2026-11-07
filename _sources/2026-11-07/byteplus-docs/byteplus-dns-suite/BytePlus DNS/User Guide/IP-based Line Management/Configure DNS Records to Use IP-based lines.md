---
title: "Configure DNS Records to Use IP-based lines"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-configure-dns-records-to-use-ip-based-lines"
---

This document describes how to associate a DNS record set with BytePlus DNS.

In order to route user traffic accurately based on their IP addresses, you need to set the line of the DNS record set to an IP\-based line. Subsequently, user traffic from the IP range of the IP\-based line will be routed to the corresponding IP addresses of the DNS record set.

<span id="d7b7c32c"></span>
## Steps

You need to go to the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns) and set the **Line** parameter of the DNS record set to **IP\-based line** and select the IP\-based line you created. Refer to [Create DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records).

<span id="ba02d12f"></span>
## Priority of IP\-based Lines


* If a user's IP address matches both an IP\-based line and other lines, only the DNS record set of the IP\-based line will take effect.

* If a user's IP address matches multiple IP\-based lines in different DNS record sets, only the DNS record set corresponding to the smallest CIDR address block will take effect. For example, if a user's IP address is 192.168.1.12 and matches two IP\-based lines with CIDR address blocks of `192.168.1.0/24` (`192.168.1.1` \- `192.168.1.254`) and `192.168.1.0/26` (`192.168.1.1` \- `192.168.1.62`), only the IP\-based line corresponding to the CIDR `192.168.1.0/26` (`192.168.1.1` \- `192.168.1.62`) will take effect.


Refer to [Priority in DNS Records](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-priority-in-dns-records) for more information on the line priority of BytePlus DNS.
