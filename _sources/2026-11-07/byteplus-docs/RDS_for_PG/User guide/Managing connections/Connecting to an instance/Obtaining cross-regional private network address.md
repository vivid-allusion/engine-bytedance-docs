---
title: "Obtaining cross-regional private network address"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Obtaining_cross-regional_private_network_address"
---

This topic introduces the procedure for obtaining an instance's cross\-regional private network address.

<span id="f8MG24KI"></span>
## Background information

Starting October 13, 2025, RDS for PostgreSQL provides cross\-regional accessible private network addresses and has upgraded the connectivity addresses.


* **Cross\-regional accessible private network connectivity address**

   The private network connectivity address supports cross\-region access.

* **Connectivity address upgrade**

   The instance's connectivity address has been upgraded by adding region information to the connectivity address. The differences between the address before and after the upgrade are shown in the table below.

   
   | |Private network address |Public network address |
   |---|---|---|
   |Before upgrade |postgres5b9918bc\*\*\*\*.rds\-pg.ivolces.com |postgres\-5b9918bc\*\*\*\*\-public.rds\-pg.volces.com |
   |After finished |postgres\-5b9918bc\*\*\*\*\-private.rds\-pg.cn\-beijing.ivolces.com |postgres\-5b9918bc\*\*\*\*\-public.rds\-pg.cn\-beijing.volces.com |
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is an invited test feature. If you need to use them, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to apply.</div>


If the creation times of connection endpoints differ, ** the effective methods of the private network address that supports cross\-region access** and **the Upgrade connection address differ.** 


* Private network address:

   * After enabling this feature, existing connection endpoints need to manually enable cross\-region address. Once enabled, a new private network address containing region information will be assigned.

   * After enabling this feature, the private network addresses of newly created connection endpoints support cross\-region access and include region information by default.

* Public network address:

   * After enabling this feature, existing connection endpoints will not include region information in the public network address even after manually enabling the cross\-region address. You need to disable public network access and then re\-enable it. The public network address will then include region information.

   * After enabling this feature, new connection endpoints support cross\-region access in their public network addresses by default once public network access is enabled, and these addresses include region information.


<span id="Ti7KEfuq"></span>
## Prerequisites

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id="PgbzJ31F"></span>
## Procedure


1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Go to the **Instances** page and click on the target instance name to open the **Summary** page.

4. Click the **Connectivity** tab at the top of the page.

5. In the **Connectivity** tab's **Instance topology** area, point the mouse cursor to the target endpoint card, and click **Enable** to the right of the **Cross\-region address** in the private network address area of the endpoint card. Point the mouse cursor to the target endpoint card again to retrieve the cross\-region accessible private network address of this connection endpoint to the right of the **Cross\-region address** in the Private network Address area of the endpoint card.
