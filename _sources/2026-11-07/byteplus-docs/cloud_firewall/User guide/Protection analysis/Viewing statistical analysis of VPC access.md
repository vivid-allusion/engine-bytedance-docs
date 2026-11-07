---
title: "Viewing statistical analysis of VPC access"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Viewing_statistical_analysis_of_VPC_access"
---

Cloud Firewall's VPC access analysis presents real\-time information about the communication between VPCs. With this data, you can promptly identify and investigate malicious traffic, enabling you to discover attacks earlier. This topic introduces how to view trends in traffic between VPCs, accessed ports, and traffic rankings.

<span id="Prerequisites"></span>
## Prerequisites


* You have turned on the VPC firewall switch. For more information about how to turn on the VPC firewall switch, refer to [Enabling the VPC firewall](https://docs.byteplus.com/en/docs/99/1249438).

* You have configured VPC access control policies. For more information about how to configure an access control policy, refer to [Configuring a VPC firewall access policy](https://docs.byteplus.com/en/docs/99/1249446).


<span id="cb423beb"></span>
## Steps


1. Log in to the Cloud Firewall console.

2. On the left side of the page, click **Protection analysis** ＞ **VPC visit analysis**.

3. Select the relevant VPC firewall, the primary VPC, the peer VPC, and the time range.

   You can inquire about the details of all the peer VPCs corresponding to a primary VPC or those of an individual peer VPC.

4. View the details of communication between VPCs.

   * Main VPC traffic rate trend : Displays the inbound and outbound traffic trends and peaks of the primary VPC within the time range.

   * Ports accessed by the main VPC Top 5: Displays the top 5 most frequently accessed ports of the primary VPC.

   * Traffic TOP ranking: Displays the top 10, 20, or 50 assets in the VPC in terms of traffic either outbound or inbound and their VPC IP addresses, traffic volume, and access counts.

   * Opening ports: Displays the statistical data on the ports used for communication between VPCs, including the IP addresses, ports, traffic, and request counts of the primary VPC's assets.
