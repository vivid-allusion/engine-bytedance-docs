---
title: "Quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ranger_quickstart"
---

This article introduces how to quickly get started with Ranger in Volcano Engine E\-MapReduce (EMR) clusters.

<span id="_1-使用前提"></span>
## 1 Prerequisites

An EMR cluster with the Ranger service has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-创建集群时选择-ranger"></span>
## 2 Select Ranger when creating a cluster

In Volcano Engine EMR, Ranger is an optional component. When you select the optional Ranger component during cluster creation, services for the HDFS and YARN components will be created by default after the cluster is successfully created, and default permission policies will be configured.

<span id="_3-元数据连接配置"></span>
## 3 Metadata connection configuration

To provide you with greater stability, the Ranger component in Volcano Engine EMR now supports HA (High Availability), and you can configure the metadata connection to use an external RDS. For detailed procedures, refer to [Metadata connections](https://docs.byteplus.com/docs/E-MapReduce/105464).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The same metadata connection cannot be reused by Ranger in multiple clusters.</div>


<span id="_4-ranger-使用流程"></span>
## 4 Ranger usage procedure

After the cluster is successfully created, you can use Ranger to manage the usage permissions of each component within the cluster. The following uses HDFS permission management as an example:

<span id="_4-1-开启对应组件的-ranger-插件"></span>
### 4.1 Enable the Ranger plugin for the corresponding component


1. On the **Cluster Details \-\> Service List \-\> Ranger Service Details \-\> Service Overview** page, click to enable the **HDFS Plugin** switch.

2. The changes take effect after restarting the HDFS service as prompted.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a66b52ac089df2516d8eaa20737ed060.png) </span>

<span id="_4-2-emr-门户控制台导入用户至-emr"></span>
### 4.2 Import users into EMR via the EMR portal console


* **Cluster Details \-\> User Management \-\> Add User**

   Depending on your needs, you can choose **IAM user import** or **manual user addition**. After successful import, Ranger Usersync will synchronize user information to Ranger. Once synchronization is complete, the account can be seen in both LDAP and Ranger WebUI.

   For details on how to add users, see [User management](https://docs.byteplus.com/docs/E-MapReduce/105426)  **.** 

   For verification methods, see [Ranger User Sync integration with LDAP](https://docs.byteplus.com/docs/undefined/69aa39c094abd605130590e9)  **.** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aeda46c2499e4c28b88f4dc1843449aa~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-ranger-admin-登录"></span>
### 4.3 Ranger Admin login


1. Open the Ranger WebUI link:

   * Resource Management Interface \-\> Access Link \-\> Click the Ranger UI access link \-\> Enter the Ranger Admin UI interface.

2. Obtain the Ranger admin password and log in:

   * Resource Management Interface \-\> Service Management \-\> Ranger \-\> Service Parameters \-\> Enter ranger_admin_password in the search box to search and obtain the admin login password.


For detailed operations, see [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411)  **.** 

After successful login, the Ranger WebUI appears as shown:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fda55c001943bc8d4b9f6c04bf41b73.png) </span>

<span id="_4-4-配置相关组件权限"></span>
### 4.4 Configure permissions for relevant components

HDFS permission settings: To grant an account full path permissions, directly edit the policy all\-path and add the account name in Select User.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8179fdcc7807d7f7a725ae94e3df785a.png) </span>

For more granular control, you can create a new policy. For details, see [HDFS integration](https://docs.byteplus.com/docs/E-MapReduce/109415).
