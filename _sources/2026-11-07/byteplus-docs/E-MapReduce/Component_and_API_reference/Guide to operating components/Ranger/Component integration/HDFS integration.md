---
title: "HDFS integration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/HDFS_integration"
---

This article introduces Ranger HDFS integration related operations and access control configuration for HDFS data.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An E\-MapReduce (EMR) cluster with Ranger service has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For Ranger UI login interface operations, see:[Overview](https://docs.byteplus.com/docs/E-MapReduce/109411)  **.** 


<span id="_2-启用-ranger-hdfs-plugin"></span>
## 2 Enable Ranger HDFS Plugin


1. Cluster details \-\> Service list \-\> Ranger service details \-\> Service overview page, click the switch to enable HDFS Plugin.

2. Restart the HDFS service as prompted for the changes to take effect.


<span id="_3-新增policy"></span>
## **3 Add policy**


1. Cluster management interface \-\> Access link \-\> Click the Ranger UI access link \-\> Enter the Ranger Admin UI interface.

2. Enter the login password for Ranger Admin UI. For details on obtaining the login password, see: [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 

3. Go to Ranger admin \-\> Access Manager \-\> HDFS \-\> Click default_hadoop to enter the permission editing interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c7889cacd3d1c2ec87885cf8443edd0.png) </span>

4. Add New Policy. Grant the hive user read, write, and execute permissions for any path. Configure as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_769b77d44cca93153afe32c6fe9e0f38.png) </span>


<span id="_4-policy-验证"></span>
## **4 Policy verification**

```shell
# 切换到管理员账号
su hdfs hdfs dfs -mkdir /user/ranger_test
hdfs dfs -chmod 000 /user/ranger_test
# 切换账号到 hive,因为已经配置了 hive 任意目录到权限，所以可以访问 /user/ranger_test
su hive
hdfs dfs -ls /user/ranger_test
```


<span id="_5-参数说明"></span>
## **5 Parameter description**


|Parameter |Semantics |
|---|---|
|PolicyName |Policy name, customizable |
|Resoure Path |Resource path |
|recursive |Whether subdirectories or files inherit permissions |
|Select Group |Specify the user group to add to this policy |
|Select User |Specify the user to add to this policy |
|Permissions |Select the permissions to grant |
