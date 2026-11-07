---
title: "Viewing the allowlists in the current region"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Viewing_the_allowlists_in_the_current_region"
---

This topic introduces the procedure for viewing the allowlists in the current region.

<span id="dACOsIt9"></span>
## Precautions

If instances in the current region have used the session management function provided by the Database Workshop (DBW) or have been operated on by the Database Transfer Service (DTS), the instances will be added to system built\-in allowlists. The system built\-in allowlists are also displayed in the allowlists but do not support operations. The system IP addresses contained in the system built\-in allowlists may change. To ensure business stability, do not rely on system allowlists.


* The system built\-in allowlist names added by DBW for PostgreSQL instances are `DBW_Sole_Group_Name_For_RDS` and dbw\-`sole_v1_group_name`.

* The system built\-in allowlist names added by DTS for PostgreSQL instances begin with `dts_internal_for_` or `dts_internal_for_`.


<span id="cTOkYFbi"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** in the left navigation bar to view the allowlists list under the current region.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the upper\-right corner of the allowlists, you can search for allowlists by allowlist name, allowlist ID, description, security group ID, or Internet protocol address.   </div>
   

<span id="elWrZqqJ"></span>
## Related APIs


|**API** |**Note** |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/RDS_for_PG/describeallowlists) |Call DescribeAllowLists API to query the allowlists list in a specifc region. |
