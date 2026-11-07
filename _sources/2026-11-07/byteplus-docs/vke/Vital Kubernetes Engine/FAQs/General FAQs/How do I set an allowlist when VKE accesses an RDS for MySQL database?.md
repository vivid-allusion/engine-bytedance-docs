---
title: "How do I set an allowlist when VKE accesses an RDS for MySQL database?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-set-an-allowlist-for-VKE-to-access-an-RDS-for-MySQL-database"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

How do I add an allowlist when VKE accesses a BytePlus RDS for MySQL instance? Which IP address ranges need to be added?

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

For the method of adding an allowlist to an RDS for MySQL instance, see [Adding IP address allowlist groups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances).

When VKE accesses an RDS for MySQL instance, the following IP address ranges need to be added to the allowlist:


<Tabs>
<Tab zoneid="okntSiBbQT" title="Access the database over the internal network">
<TabTitle>Access the database over the internal network</TabTitle>

* The Flannel network model cluster: Add the IP address ranges of nodes to the allowlist.

* The VPC\-CNI network model cluster: Add the subnet IP address ranges or pod IP addresses to the allowlist.


</Tab>
<Tab zoneid="x4CbV5mbIN" title="Access the database over the public network">
<TabTitle>Access the database over the public network</TabTitle>

Add the NAT gateway that is created when public access is enabled for the cluster to the allowlist.


</Tab>
</Tabs>
