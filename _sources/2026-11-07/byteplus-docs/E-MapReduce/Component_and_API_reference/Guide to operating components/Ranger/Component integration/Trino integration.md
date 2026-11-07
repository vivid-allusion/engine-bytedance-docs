---
title: "Trino integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Trino_integration"
---

This article introduces the operations related to integrating Ranger with Trino and the configuration of access control for Trino.

<span id="_1-使用前提"></span>
## **Prerequisites**


1. A cluster with E\-MapReduce (EMR) and the Ranger service has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For instructions on the Ranger UI login interface, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 


<span id="_2-启用-ranger-trino-plugin"></span>
## **Enable Ranger Trino Plugin**


1. Cluster details \-\> Service list \-\> Ranger service details \-\> Service overview page, click the switch to enable the Trino Plugin.

2. The changes take effect after restarting the Trino service as prompted.


<span id="_3-新增policy"></span>
## **Add policy**


1. Cluster management interface \-\> Access link \-\> Click the access link for Ranger UI \-\> Enter the Ranger Admin UI.

2. Enter the login password for the Ranger Admin UI. For instructions on obtaining the login password, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411)  **.** 

3. Go to Ranger admin \-\> Access Manager \-\> TRINO \-\> Click trino to enter the permission editing interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d358c5d64e4ad8228102f3c9aee469a9.png) </span>

4. Add New Policy。 Trino resource types include catalog, schema, table, and column, each corresponding to permission control at the respective level. User permissions can be configured as needed.

   For example, to grant the user named "ranger" select permission on table: test001, configure as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7183a13fb414b8c26da9de34472ccaca.png) </span>
