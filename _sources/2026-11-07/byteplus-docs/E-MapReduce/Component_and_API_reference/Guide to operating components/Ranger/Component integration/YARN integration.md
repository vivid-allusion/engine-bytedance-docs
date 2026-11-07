---
title: "YARN integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/YARN_integration"
---

This article introduces Ranger YARN integration and the related operations for configuring YARN user permissions.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. A cluster with E\-MapReduce (EMR) and the Ranger service has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For instructions on the Ranger UI login interface, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 


<span id="_2-启用-ranger-yarn-plugin"></span>
## 2 Enable the Ranger YARN Plugin


1. Cluster details \-\> Service list \-\> Ranger service details \-\> Service overview page, click the switch to enable the YARN Plugin.

2. The changes take effect after restarting the YARN service as prompted.


<span id="_3-新增policy"></span>
## **3 Add a policy**

The default YARN queue manager used by EMR is Capacity Scheduler. By default, Ranger grants the yarn user queue management permissions. For other permission configurations, refer to the following.


1. Cluster management interface \-\> Access link \-\> Click the access link for Ranger UI \-\> Enter the Ranger Admin UI interface.

2. Enter the login password for the Ranger Admin UI. For information on how to obtain the login password, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 

3. Go to Ranger admin \-\> Access Manager \-\> YARN \-\> Click default_yarn to enter the permission editing interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_718ba4867096f00a6389a7307d91ea1a.png) </span>

4. Add New Policy to grant the emr_admin user permission to Submit Job to root.default.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5da72958b55391e69f17221ddfac98c.png) </span>


<span id="_4-参数说明"></span>
## **4 Parameter note**


|Parameter |Semantic |
|---|---|
|Policy Name |Policy name, customizable |
|Queue |Queue name, for example, root.default |
|recursive |Whether sub\-queues inherit this permission |
|Select Group |Specify the user group to add this policy for |
|Select User |Specify the user to add this policy for |
|Permissions |Select the permissions to grant |
