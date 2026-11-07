---
title: "Resource management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/resource-management"
---

ByteHouse Enterprise supports resource permission management and supports granting specified resource usage permissions to roles or users. This tutorial introduces the scope of permissions for resource management and explains how to configure resource management permissions.

<span id="0b4b523a"></span>
# Prerequisites

Only users with the SystemAdmin or ClusterAdmin role can use this feature.

<span id="d977fe43"></span>
# Function overview

ByteHouse Enterprise supports configuring resource usage permissions for the cluster management, data import, permission management, and diagnostic optimization modules. It also controls the visibility scope of each functional module in the ByteHouse Enterprise console. You can grant resource usage permissions for the corresponding functional modules to custom roles or users based on business needs. The resource permissions of default roles in ByteHouse Enterprise are built\-in to the system and cannot be modified.

The description of resource permissions currently supported by ByteHouse Enterprise is as follows:


|Primary function modules |Second\-level function modules |Permission description |
|---|---|---|
|Cluster management |Resize Cluster |Permission to modify cluster resource specifications allows adjustment of CPU, memory, and disk storage specifications. |
||Restart cluster |Permission to manually restart the cluster. |
||Modify cluster parameters |Permission to modify the global parameters of the cluster. After modification, the cluster must be restarted for the changes to take effect. When enabling this permission, it is recommended to also enable the permission to restart the cluster. |
||Version change |Permission to change the cluster version. |
||Modify cluster user parameters |Permission to modify user\-level cluster parameters. |
||Backup data |Permission to configure and manage cluster data backup strategies. |
||Reshard data |Permission to trigger data redistribution when resource specifications change. |
||Manage advanced features |Permission to enable advanced cluster features, including GIS spatiotemporal analysis, vector search, and full\-text search capabilities. |
||Manage workloads |Permission to query cluster load status and to create and manage resource groups. |
|Data import |Manage data loading tasks |Permissions for managing data sources and import tasks. |
||Manage data loading executions |Permission to manage the execution plan for import tasks. |
|Access control |Manage row policies/IP whitelist |* Permission to configure row\-level access policies and grant authorization for database tables in the cluster.<br><br>* Configure permissions for accessing the IP whitelist. |
||Manage resource privileges |Manage permissions for function modules of the cluster console to control the range of console features visible to different roles or users after login. |
|Diagnostic optimization |Manage table statistics |The triggering and management permissions for the collection of statistical information of database tables in the cluster. |
||Intelligent patrol |Permission to configure and manage cluster inspection policies. |
||Intelligent diagnosis |If you have permission to use the diagnostic analysis functionality, you can query the optimization recommendations provided by the diagnostic analysis functionality. |


Resource management is used to manage the display permissions of feature modules in the ByteHouse Enterprise console. To adjust fine\-grained permissions for non\-administrators, such as the ability to view the number of rows returned by data queries, download data, change account passwords, or create clusters, refer to [Non-admin user management](https://docs.byteplus.com/docs/bytehouse/non-admin-user-management).

<span id="e77e8489"></span>
# Steps


1. Log in to the ByteHouse Enterprise console. Click the top **Role\-based Access Control** tab, then click **Resource** to go to the feature page.

2. Select a cluster from the dropdown list, and click the **Edit** button for the resource permission row you want to adjust.

3. On the permission assignment page, switch to the **Role** or **User** tab, and click the button in the permissions column to enable or disable permissions for the role or user.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d2964002fec42ffbd5627459106f65f~tplv-goo7wpa0wc-image.image) </span>

4. After adjusting permissions, click **Confirm**. The changes will take effect immediately.
