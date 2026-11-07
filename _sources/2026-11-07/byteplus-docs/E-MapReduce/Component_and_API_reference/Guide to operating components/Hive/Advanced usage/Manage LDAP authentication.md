---
title: "Manage LDAP authentication"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Manage_LDAP_authentication"
---

After enabling the LDAP authentication feature for the service, you must provide LDAP credentials (LDAP username and password) when accessing the service to enhance its security. The LDAP service used when enabling the LDAP feature is the OpenLDAP service included with E\-MapReduce (EMR). Enabling the LDAP authentication feature makes it easy to use LDAP authentication and avoids complex configuration.

<span id="_1-前提条件"></span>
## **1. Prerequisites**

The cluster has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-开启-ldap-认证"></span>
## **2. Enable LDAP authentication**

After the cluster is successfully created, LDAP authentication is enabled by default. You can check it as follows:


1. Go to the Hive page

   1. Log in to the [Volcano Engine E-MapReduce console](https://console.volcengine.com/emr/).

   2. In the top menu bar, select the region as needed.

   3. Click the **Cluster List** tab on the left.

   4. On the **Cluster List** page, click the corresponding **cluster name** to view the cluster details.

   5. Click the **Service List** tab and select **Hive**.

2. On the **Hive** page, modify the configuration

   1. Click the **Service Parameters** tab.

   2. Select the **Security** option from the categories on the left.

   3. If the value of the parameter hive.server2.authentication is LDAP, it means that LDAP authentication is enabled for the cluster.


<span id="_3-访问-hiveserver2"></span>
## 3. Access HiveServer2

After enabling LDAP authentication, you must provide LDAP credentials when accessing HiveServer2.


1. Use SSH to log in to the primary node of the cluster. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404)

2. You can access HiveServer2 in the following three ways.

* Beeline client:


```Plain
   beeline -u jdbc:hive2://<hive_server_ip>:10000 -n <user> -p <password>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>hive_server_ip</strong> is the machine where the HiveServer service is located, usually the primary node.</div>


<div data-tips="true" data-tips-type="tip"><strong>user</strong> is the LDAP username.</div>


<div data-tips="true" data-tips-type="tip"><strong>password</strong> is the LDAP password. After enabling LDAP authentication, you must provide the LDAP username and password to access HiveServer2. For information on how to obtain them, see <a href="https://docs.byteplus.com/docs/E-MapReduce/105426">User management</a>.</div>



* JDBC


```Plain
jdbc:hive2://<hive_server_ip>:10000/default;user=<user>;password=<password>
```



* If high availability is enabled, you can connect to HiveServer using ZK. For details, see [HiveServer2 load balancing](https://docs.byteplus.com/docs/E-MapReduce/109258).
