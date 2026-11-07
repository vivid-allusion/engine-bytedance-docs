---
title: "Network connectivity solution"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/network_connectivity_solution"
---

Before using the data synchronization feature, you need to ensure network connectivity between the Data Integration Resource Group and the Database. You can select an appropriate network solution based on the database's network environment to establish connectivity. This article introduces network connectivity solutions available for databases in different network environments.

An Exclusive Data Integration Resource Group can establish network connectivity with data sources in public networks, private networks (VPC), and local IDCs. For connectivity solutions applicable to different scenarios, refer to the plans below:


|Applicable scenarios |Network connectivity plans |
|---|---|
|Database and Data Integration Resource Group in the same VPC network |* When the datasource is an RDS (MySQL or PostgreSQL) cloud database, you need to add the [IPv4 CIDR](https://console.byteplus.com/vpc/region:vpc+ap-southeast-1/vpc?) address in the VPC to the database allowlist.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5e8a723ad034a989b0b627df077ffca~tplv-goo7wpa0wc-image.image) </span><br><br>* Other types of datasources can be directly connected. |
|Self\-hosted public network databases |You need to enable public network access for the VPC bound to the Data Integration Resource Group. For detailed instructions, see [Enable public network for Resource Group VPC](https://docs.byteplus.com/docs/undefined/6895c4bb648481085833f711). |
|The datasource is in the local IDC. |Establish a dedicated, high\-speed, low\-latency, stable, and secure connection between the user's local data center (IDC) and the cloud private network (VPC) through Direct Connect. Interconnection between multiple local IDCs and multiple cloud VPCs is supported. For detailed instructions, see the [Direct Connect Getting Started Guide.](https://docs.byteplus.com/en/docs/directconnect/Quick-start)<br><br>By using the VPN connection feature, you can establish an IPsec tunnel between the cloud VPC and the local IDC, enabling a flexible hybrid cloud deployment solution. For detailed steps, see [Connecting a virtual private cloud to multiple data centers](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec8a6f1ff2b345aeaa11a74b219124c6~tplv-goo7wpa0wc-image.image) </span> |
