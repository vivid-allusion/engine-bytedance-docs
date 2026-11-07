---
title: "What if an error occurs when connecting to an instance while creating a data transmission task?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/what_if_an_error"
---

If an error occurs when connecting to an instance, you can troubleshoot the problem according to the following prompts:


* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.

* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.

* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.

* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.

* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet.

* **Internal Service is timeout.**  **Pls Contact with Admin**: When this error occurs, you need to first check whether the network can be used normally and whether there is sufficient bandwidth.
