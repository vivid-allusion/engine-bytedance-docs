---
title: "Presto integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Presto_integration"
---

This article introduces operations related to Ranger Presto integration and the configuration of access control for Presto.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An E\-MapReduce (EMR) cluster that includes the Ranger service has already been created. For details on the operation, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For operations on the Ranger UI login interface, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 


<span id="_2-启用-ranger-presto-plugin"></span>
## 2 Enable Ranger Presto plugin


1. Cluster details \-\> Service list \-\> Ranger service details \-\> Service overview page, click the switch to enable the Presto plugin.

2. It takes effect after restarting the Presto service as prompted.


<span id="_3-权限配置"></span>
## 3 Permission configuration

After Presto is installed, some user permissions are preset by default, such as Hive user permissions. To add new users and permissions, you can add new permission policies in the Ranger Admin interface. For details, refer to the [User guide](https://docs.byteplus.com/docs/E-MapReduce/109366) section of the Presto documentation.
