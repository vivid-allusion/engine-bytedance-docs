---
title: "What is BytePlus GTM"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/U-qFtN"
---

BytePlus Global Traffic Management (GTM) is a DNS\-based traffic management service.

Suppose your service is deployed across multiple data centers. The IP addresses of these data centers are distributed across different ISPs and geolocations. Users access your service through a domain name. When users access your domain name, you want:


* Users to obtain the available IP address with the lowest access latency.

* User requests to be reasonably distributed according to the capacity of each data center, achieving load balancing in terms of the number of user requests.

* When a data center becomes unavailable due to a failure, user requests to be switched to other available data centers.


To meet these requirements,BytePlus GTM resolves your domain name to an appropriate IP address based on the following factors:


* The user's ISP and geolocation

* The access latency between the user's geolocation and the data centers

* Load balancing parameters you configure for multiple data centers, such as the capacity of data centers

* Health check and disaster recovery switchover parameters you configure for multiple data centers, such as health check parameters to determine whether a data center is available, and disaster recovery switchover parameters between primary and backup data centers


<span id="feature-overview"></span>
## Feature overview

BytePlus GTM supports the following features.

<span id="address-management"></span>
### Address management

You can perform custom multi\-level grouping management of IP addresses for IDC data centers in BytePlus GTM, enabling flexible weight and capacity allocation mechanisms and disaster recovery switchover mechanisms.

<span id="routing-user-requests-based-on-their-origin"></span>
### Routing user requests based on their origin

In the basic routing mode, BytePlus GTM can determine attributes such as the ISP and geolocation of the user's IP address based on the DNS query sent by the user, and route user requests to matching data centers according to these attributes, avoiding increased access latency caused by users accessing data centers across ISPs or regions.

In the intelligent routing mode, BytePlus GTM can automatically detect the access latency from users to data centers based on attributes such as the ISP and geolocation of the user's IP address, and automatically route user requests to the data center with the lowest access latency.

<span id="routing-user-requests-based-on-load-balancing-configuration"></span>
### Routing user requests based on load balancing configuration

BytePlus GTM adjusts the proportion of user requests received by each data center based on the capacity of each data center.

<span id="routing-user-requests-based-on-health-check-and-disaster-recovery-configuration"></span>
### Routing user requests based on health check and disaster recovery configuration

BytePlus GTM regularly checks the availability of data centers based on health check configurations. If a data center is determined to be unavailable during a health check, user requests routed to that data center will be switched to other available data centers. You can use the address management feature to implement more flexible disaster recovery mechanisms.

<span id="traffic-routing-visualization-and-dns-query-statistics"></span>
### Traffic routing visualization and DNS query statistics

BytePlus GTM displays the routing of traffic through Sankey diagrams. You can view the expected traffic routing diagram before the configuration takes effect, and also view the actual traffic routing diagram after the configuration takes effect.

You can also view statistical data on the number of DNS queries in BytePlus GTM, grouped by DNS status, record type, ISP, and geolocation.
