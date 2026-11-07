---
title: "Viewing logs"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Viewing-logs"
---

All traffic that passes through Cloud Firewall will be recorded in logs, which can be divided into access control logs and traffic logs. You can audit network traffic in real time based on the log content to identify suspicious traffic.

<span id="background"></span>
## Background


* **Advanced mode**: Provides, among other features, syntax\-based retrieval and analysis, monitoring and alerting, and data visualization. It is suitable for data mining and analysis in complex scenarios.

* **Basic mode**: Provides basic retrieval and querying. It is suitable for log retrieval and analysis in simple scenarios.


<span id="viewing-access-control-logs"></span>
## Viewing access control logs

Access control logs record the traffic that passes through the internet firewall and matches any active control policy. You can view the details of these logs, such as policy hit time, source IP address, source port, destination IP address, protocol, policy ID, and action status.


1. Log in to the Cloud Firewall console.

2. On the left side of the page, select **Log**.

3. Click the **Access log** tab to view the logs of traffic that hit your access control policies.

   You can retrieve the logs you want by entering, above the access control log list, relevant information, such as source IP address, destination IP address, destination port, policy ID, or custom time range.


<span id="Traffic logs"></span>
## Viewing traffic logs

Traffic logs record all traffic to and from the internet. You can view the details of these logs, such as access time, source IP address, access destination, destination port, protocol, access traffic size, and number of packets.


1. Log in to the Cloud Firewall console.

2. On the left side of the page, select **Log**.

3. Click the **Traffic log** tab to view all the logs for traffic to and from the internet.

   You can retrieve the logs you want by entering, above the access control log list, relevant information, such as source IP address, destination IP address, destination port, or custom time range.
