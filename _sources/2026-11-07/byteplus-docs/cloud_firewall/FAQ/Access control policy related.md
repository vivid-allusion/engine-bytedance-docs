---
title: "Access control policy related"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Access_control_policy_related"
---

<span id="f41317fc"></span>
### Configured internet boundary access control policy, why is it not effective? 

You must first enable the asset protection switch on the **firewall switch** \> **internet boundary** page for the traffic of relevant assets to pass through the cloud firewall, and the access control policy will be effective.

<span id="0eca768f"></span>
### Why is the domain access control not effective? \nDomain access control relies on the following two data sources:


* Host information in the HTTP protocol

* Server Name information in the Client Hello of HTTPS protocol packets\nIf these information are missing in the business traffic packets, the domain policy will not be effective.


<span id="c9249f1e"></span>
### Already configured the domain blocking policy, why can this domain be telnet accessible but not curl? 

The principle of domain access control policies is to match control based on the Host information in the HTTP protocol data and the Server Name information in the Client Hello of HTTPS protocol packets; only after the three\-way handshake is completed will packets with domain information be sent. Telnet itself is not an HTTP protocol and only provides remote terminal access, while curl sends HTTP requests; therefore, there can be cases where telnet works but curl does not.

<span id="badfdfcd"></span>
### When no strategy is configured, does the cloud firewall default rule allow or block? 

The cloud firewall defaults to allowing all traffic.

<span id="f9388919"></span>
### After configuring access control rules, how long does it take to take effect? 

After configuring the cloud firewall strategy, it takes about 1 minute to take effect.

<span id="223ba627"></span>
### How many firewall policies can be expanded to? 

The Internet boundary firewall, VPC boundary firewall, and NAT boundary firewall access control policies can be expanded to a maximum of 300,000 entries.
