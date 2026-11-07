---
title: "Viewing the allowlists of an instance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Viewing_the_allowlists_of_an_instance"
---

This topic describes the procedure to view the allowlists of RDS for PostgreSQL instances.

<span id="6tRiBDIV"></span>
## Precautions

If you have previously used the session management feature provided by the Database Workbench (DBW) or operated the instance using the Database Transmission Service (DTS), the instance will be added to the system built\-in allowlist. The system built\-in allowlist will also be displayed in the allowlists associated with the instance but cannot be disassociated. The system IPs included in the system built\-in allowlist may change. To ensure business stability, do not rely on the system allowlist.


* The system built\-in allowlist added by DBW for PostgreSQL instances is named `DBW_Sole_Group_Name_For_RDS`.

* The system built\-in allowlist added by DTS for PostgreSQL instances is named `dts_internal_for_EndpointVolcPG`.


<span id="X8yT6xtM"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

4. Click on **Instances** in the left navigation bar.

5. On the **Instances** page, click on the target instance name.

6. Click the **Security** tab at the top of the page.

7. Under the **Allowlists** sub\-tab, you can view the allowlists currently associated with the instance.


<span id="pREMK5oe"></span>
## Related APIs


|API |Note |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlists) |Call DescribeAllowLists API to query the allowlists list in a specifc region. |
