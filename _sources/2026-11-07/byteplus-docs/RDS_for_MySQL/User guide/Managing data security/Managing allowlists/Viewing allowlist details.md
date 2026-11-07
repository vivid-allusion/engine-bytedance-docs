---
title: "Viewing allowlist details"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_allowlist_details"
---

An allowlist is a security control for database connections. Only IP addresses added to the allowlist can access an RDS for MySQL instance. To ensure the security of database connections, maintain allowlists regularly to remove IP addresses that no longer need to access the database. This topic describes the procedure for viewing the details of RDS for MySQL allowlists.

<span id="abCksUUI"></span>
## Precautions

To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the allowlist in the upper\-left corner of the top menu bar.

3. Click **Allowlists** in the left navigation bar to view the allowlists list under the current region.

4. In the list of allowlists, click the name of the target allowlist to view its details. The details include the following:

   
   |Project |Description |
   |---|---|
   |Allowlist information |Includes the name, description, **all IPs**, and whether it is a default allowlist.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">"All IPs" includes the internet protocol addresses in the allowlist and its associated security groups.</div><br> |
   |Associated security groups |A list of security groups associated with the allowlist. |
   |Associated instances |A list of instances associated with the allowlist. |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlistdetail1) |Call the DescribeAllowListDetail API to view the details of an allowlist. |
