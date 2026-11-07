---
title: "Hive integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_integration"
---

There are three ways to access Hive data: HiveServer2, Hive Client, and HDFS. For access permission control of HDFS, refer to [HDFS integration](https://docs.byteplus.com/docs/E-MapReduce/109415). The following introduces the configuration of Ranger access control for Hive data.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An E\-MapReduce (EMR) cluster with the Ranger service has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For operations on the Ranger UI login interface, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 


<span id="_2-启用-ranger-hive-plugin"></span>
## 2 Enable Ranger Hive Plugin


1. Cluster details \-\> Service list \-\> Ranger service details \-\> Service overview page, click the switch to enable the Hive Plugin.

2. Restart the Hive service as prompted for the changes to take effect.


<span id="_3-新增policy"></span>
## **3 Add Policy**


1. Cluster management interface \-\> Access link \-\> Click the Ranger UI access link \-\> Enter the Ranger Admin UI interface.

2. Enter the login password for the Ranger Admin UI. For details on obtaining the login password, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 

3. Go to Ranger admin \-\> Access Manager \-\> HADOOP SQL \-\> Click default_hive to enter the permission editing interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0eee448033812497adb8b188ddc2c0b0.png) </span>

4. Add New Policy: Grant the ranger user select permission on table test001. Configuration is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28f40d9ecb907a41e3b7015126cbf39a.png) </span>


<span id="_4-policy-验证"></span>
## **4 Policy verification**

<span id="_4-1-beeline-访问"></span>
### **4.1 beeline access**

For details on Hive access link operations, see: [Hive connection methods](https://docs.byteplus.com/docs/E-MapReduce/109265).

```shell
beeline -u jdbc:hive2://<HiveServer2地址>:10000 -n ${username} -p ${password}
```


Example

```shell
# beeline 链接到 HiveServer2
beeline -u jdbc:hive2://<HiveServer2地址>:10000 -n ranger -p ranger
# 测试ranger select test001 权限
select * from test001
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0527183a23bc94646d6cf338af38ae97.png) </span>

As shown in the figure above: If the ranger user is not configured, permission denied will occur. After configuration, queries can be performed normally.

<span id="_4-2-参数说明"></span>
### **4.2 Parameter description**


|Parameter |Semantics |
|---|---|
|Policy Name |Policy name, customizable. |
|database |Add a database in Hive, for example, testdb. |
|table |Add a table, for example, test. |
|Hive Column |Add column names. Entering an asterisk (\*) means all columns. |
|Select Group |Specify the user group to add to this policy. |
|Select User |Specify the user to add to this policy. |
|Permissions |Select the permissions to grant |
