---
title: "Viewing the allowlists of an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_the_allowlists_of_an_instance"
---

This topic describes the steps to view the allowlists of an RDS for MySQL instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If you have previously used the session management feature provided by the Database Workshop (DBW) or operated the MySQL instance using the Database Transmission Service (DTS), the instance will be added to the system\-built\-in allowlist. The system\-built\-in allowlist is also displayed in the Allowlists. The system IPs included in the system built\-in allowlist may change. To ensure business stability, do not rely on the system allowlist.

   * The system\-built\-in allowlist added by DBW for a MySQL instance is named `DBW_Sole_Group_Name_For_RDS`.

   * The system\-built\-in allowlist added by DTS for a MySQL instance is named `dts_internal_for_EndpointVolcMySQL`.

* RDS for MySQL allowlist feature has been upgraded to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar. If an instance is associated with allowlists from a project for which you do not have privileges, you can only view the allowlists but cannot modify or delete them.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click the **Security** tab at the top of the page.

6. Under the **Allowlists** sub\-tab, you can view the allowlists currently associated with the instance.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeallowlists1) |Call the DescribeAllowLists API to view the allow list. |
