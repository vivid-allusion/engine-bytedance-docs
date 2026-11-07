---
title: "HBase integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/HBase_integration"
---

This article introduces Ranger HBase integration and related operations, as well as access control configuration for HBase.

<span id="_1-使用前提"></span>
## **1 Prerequisites**


1. A cluster with E\-MapReduce (EMR) that includes the Ranger service has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For instructions on the Ranger UI login page, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411)


<span id="_2-启用-ranger-hbase-plugin"></span>
## **2 Enable Ranger HBase plugin**


1. Cluster details \-\> Service list \-\> Ranger service details \-\> Service overview page, click the switch to enable the HBase plugin.

2. The changes take effect after restarting the HBase service as prompted.


<span id="_3-新增-policy"></span>
## **3 Add policy**


1. Cluster management interface \-\> Access link \-\> Click the access link for Ranger UI \-\> Enter the Ranger Admin UI.

2. Enter the login password for Ranger Admin UI. For details on how to obtain the login password, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411).

3. Go to Ranger admin \-\> Access Manager \-\> HBASE \-\> Click default_hbase to enter the permission editing interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4530068a5a58c895fe5c23d490b38fc.png) </span>

4. Click the "**Add New Policy**" button in the upper right corner to add a new policy. The resource types for HBase include table, column\-family, and column. You can configure user permissions as needed.

   For example, to grant the ranger user Read permission to table: test001, configure as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_187e2e194caf170d9c2897d7c82af722.png) </span>

5. After configuration is complete, click the **Add** button at the bottom of the interface to finish adding the new permission policy.
