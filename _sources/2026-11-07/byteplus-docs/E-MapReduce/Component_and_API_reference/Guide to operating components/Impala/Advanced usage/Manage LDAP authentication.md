---
title: "Manage LDAP authentication"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/impala_Manage_LDAP_authentication"
---

Volcano Engine E\-MapReduce (EMR) integrates the OpenLDAP service by default. You can use OpenLDAP to manage usernames and passwords for Impala.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An EMR cluster has been created with **Impala, OpenLDAP** component services. For details, see [创建集群](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92).

2. Currently, the Impala component is available through an allowlist. You can apply for access via [Manage LDAP authentication](https://docs.byteplus.com/docs/E-MapReduce/109297).


<span id="_2-查看用户名-密码"></span>
## 2 View usernames/passwords


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, select and go to the **Cluster List \> Cluster Name \> User Management** page.

3. On the User Management page, view the information of users that have been added. You can also add users who connect to Impala by **importing IAM users** or **adding manually**. For details on how to add users, see [User management](https://docs.byteplus.com/docs/E-MapReduce/105426).


<span id="_3-开启-impala-的-openldap-认证"></span>
## 3 Enable OpenLDAP authentication for Impala

The following describes how to manually enable OpenLDAP authentication for Impala.


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, select and go to the **Cluster List \> Cluster Name \> Service List \> Impala** page.

3. On the Impala details page, switch to the **Service Parameters** tab.

4. On the Service Parameters page, search for the **enable_ldap_auth** parameter.

5. Change the value of the enable_ldap_auth parameter to **true**, then in the upper right **Service Actions**, **restart** impalad to enable OpenLDAP authentication. To disable OpenLDAP authentication, set this parameter to false and restart.
