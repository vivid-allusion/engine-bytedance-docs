---
title: "Synchronizing security group"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/sync_security_group"
---

RDS for MySQL allowlists now support associating with ECS security groups. After associating an ECS security group, if the security group is updated, you can synchronize the allowlist in RDS for MySQL.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* There is an allowlist associated with the ECS security group.

* If the target allowlist has associated instances, the state of the instances needs to be Running.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you synchronize the security group, RDS for MySQL automatically identifies IP changes in the security group associated with the allowlist and updates the IP information in the allowlist. Please confirm whether the removal of the IP from the associated security group from the allowlist will affect business.

* An allowlist can support up to 300 IPs or IP segments. If the associating security group involves an IP or the IP segment exceeds the limit, the synchronization will fail.

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click on **Instances** in the left navigation bar.

4. Click  **…**  \> **Sync security group** in the **Actions** column of the target allowlist, confirm the IP changes before and after synchronization in the pop\-up dialog box, and click **OK** after confirmation.
