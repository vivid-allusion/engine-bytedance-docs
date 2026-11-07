---
title: "Viewing the allowlists in the current region"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_the_allowlists_in_the_current_region"
---

This topic introduces the procedure for viewing the allowlists in the current region.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If instances in the current region have used the session management function provided by the Database Workshop (DBW) or MySQL instances have been operated on by the Database Transmission Service (DTS), the instances are added to system built\-in allowlists. System built\-in allowlists are also displayed in the allowlists list. The system IPs included in the system built\-in allowlist may change. To ensure business stability, do not rely on the system allowlist.

   * The system\-built\-in allowlist added by DBW for a MySQL instance is named `DBW_Sole_Group_Name_For_RDS`.

   * The system\-built\-in allowlist added by DTS for a MySQL instance is named `dts_internal_for_EndpointVolcMySQL`.

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the allowlist in the upper\-left corner of the top menu bar.

3. Click **Allowlists** in the left navigation bar to view the allowlists list under the current region.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the upper\-right corner of the allowlists, you can search for allowlists by allowlist name, allowlist ID, description, security group ID, or Internet protocol address.</div>


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) |Call the DescribeAllowLists API to view the allow list. |
