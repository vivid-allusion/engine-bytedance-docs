---
title: "Deleting an allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_an_allowlist"
---

An allowlist is a security control for database connections. Only IP addresses added to the allowlist can access an RDS for MySQL instance. To ensure the security of database connections, maintain allowlists regularly to remove IP addresses that no longer need to access the database. This topic describes how to delete allowlists to manage IP addresses.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Existing allowlist.

* It has been confirmed that all IP addresses in the allowlist to be deleted no longer require access to the database.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Allowlists that are associated with an instance cannot be deleted. To delete it, first disassociate the instance. For more information, refer to [Disassociating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociating_an_instance_from_an_allowlist).

* You cannot delete the default allowlist. To delete it, you must first modify the default allowlist to a standard allowlist and remove its association with the instance. For more information about modifying allowlists, refer to [Modifying allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_an_allowlist).

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. Click **Actions** in the target allowlist’s  **...**  column \> **Delete**, then click **OK** in the popped\-up dialog.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DeleteAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleteallowlist1) |Call the DeleteAllowList API to delete the target allowlist. |
