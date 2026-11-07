---
title: "Disassociating with allowlists"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_an_allowlist"
---

This topic describes the procedure for disassociating with allowlists.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

RDS for PostgreSQL provides two disassociating entry points. You can choose freely according to your business scenario.


* [Disassociate an allowlist from an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_an_allowlist#.5LuO5a6e5L6L6Kej57uR55m95ZCN5Y2V): Operate within the instance to quickly disassociate multiple allowlists from one instance.

* [Disassociate an instance from an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_an_allowlist#.5LuO55m95ZCN5Y2V6Kej57uR5a6e5L6L): Operate within the allowlist to quickly disassociate one allowlist from multiple instances.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After disassociating an allowlist, the instance will no longer be accessible from the IP addresses or IP address ranges listed in the allowlist. Exercise caution when performing this operation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

the allowlist has associated instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5LuO55m95ZCN5Y2V6Kej57uR5a6e5L6L"></span>
### Disassociate an instance with an allowlist


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. on the **Allowlists** page, click the name of the target allowlist. in the pop\-up page, you can see the list of instances associated with the allowlist.

5. Click the **Disassociate with an allowlist** button. On the popped\-up **Disassociate with an allowlist** page, in the **Associated instances list**, click **Disassociate instance** in the **Actions** column of the target instance to disassociate the instance from the allowlist.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">repeat this operation to disassociate multiple instances from the allowlist.   </div>
   

<span id=".5LuO5a6e5L6L6Kej57uR55m95ZCN5Y2V"></span>
### Disassociate an allowlist with an instance


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click the **Security** tab at the top of the page.

6. Under the **Security** tab, locate the allowlist to be disassociated in the **Allowlists** subtab’s **Associated allowlists** list.

7. Click **Disassociate with an allowlist**, and then click **OK** in the pop\-up dialog box.


<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociateallowlist) |Call DisassociateAllowList API to disassociates an allowlist. |


&nbsp;
