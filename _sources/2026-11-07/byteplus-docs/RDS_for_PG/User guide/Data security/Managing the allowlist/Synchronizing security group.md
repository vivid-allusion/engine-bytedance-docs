---
title: "Synchronizing security group"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Synchronizing_security_group"
---

RDS for PostgreSQL supports associating ECS security groups. After binding the ECS security group, if the ECS security group is updated, it can be synchronized as an allowlist in RDS for PostgreSQL.

<span id="6Jfo8XjJ"></span>
## Prerequisites


* There is an allowlist associated with the ECS security group.

* If the target allowlist has an associated instance, the instance's status needs to be running.


<span id="NNni3JR2"></span>
## Precautions


* When synchronizing security groups, RDS for PostgreSQL automatically recognizes IP changes that exist in allowlist security groups and updates the IP information in the allowlist. Please confirm whether the removal of the IP from the associated security group from the allowlist will affect business.

* An allowlist can support up to 300 IPs or IP segments. If the associating security group involves an IP or the IP segment exceeds the limit, the synchronization will fail.


<span id="13rzNS6k"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click on **Instances** in the left navigation bar.

4. Click  **...**  \> **Sync security group** in the **Actions** column of the target allowlist, confirm the IP changes before and after synchronization in the pop\-up dialog box, and click **OK** after confirming that it is correct.
