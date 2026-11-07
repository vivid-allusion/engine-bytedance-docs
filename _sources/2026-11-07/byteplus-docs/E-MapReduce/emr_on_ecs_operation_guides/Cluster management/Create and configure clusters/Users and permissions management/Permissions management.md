---
title: "Permissions management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Permissions_management"
---

Volcano Engine E\-MapReduce (EMR) integrates the Apache® Ranger centralized permission management framework, providing fine\-grained access control for Hadoop ecosystem components.

> Apache Ranger, the names of other Apache projects, and the ASF logo are either registered trademarks or trademarks of the Apache Software Foundation in the United States and/or other countries.


Considering that permission control is not a mandatory feature, EMR is designed to give you significant autonomy, allowing you to choose whether to install the Ranger service. For clusters with the Ranger service installed, you can also choose whether to enable Ranger authentication for specific services. Additionally, we provide an interactive UI for permission control based on the Role\-Based Access Control (RBAC) permission model, making it easier and faster for ordinary users to configure permissions for EMR clusters.

<span id="_1-ranger-默认启用情况"></span>
## Default Ranger enablement

Permission management was introduced in the EMR 3.1.0 software stack version. The currently supported cluster types and services are shown in the table below:


|Analysis scenarios |Cluster types |Services |Ranger authorization enabled by default |
|---|---|---|---|
|Data lake |Hadoop |HDFS |✅ |
|||YARN |✅ |
|||Hive |✅ |
|||Spark |✅ |
|||Presto | |
|||Trino | |
|Real\-time computing |Kafka |Kafka |✅ |
|Interactive analytics |Presto |HDFS | |
|||Hive | |
|||Presto |✅ |
||Trino |HDFS | |
|||Hive | |
|||Trino |✅ |
|NoSQL database |HBase |HDFS | |
|||HBase |✅ |


<span id="_2-使用限制"></span>
## **Limits**


* To ensure proper functionality of the permission management module, you need to open port 8080 for the `100.64.0.0/10` IP range in the cluster's security group. For detailed steps, see [Add security group access rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

* Do not modify the Ranger administrator password, as this will render the permission management feature unavailable.


<span id="_3-权限管控启停"></span>
## Enable or disable permission control

EMR allows you to control whether to install the Ranger service for a cluster. For clusters with the Ranger service installed, you can also control whether to enable or disable Ranger authentication for specific services.

<span id="_3-1-ranger-服务安装"></span>
### Ranger service installation

You can choose whether to install the Ranger service during [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456), thereby controlling whether to enable the permission control feature.


* **Select Ranger service installation when creating a cluster**

   To enhance cluster data access security, select Ranger service installation in optional services when creating a cluster. Depending on the cluster type, EMR will enable Ranger authentication by default for the corresponding services. For details on the default Ranger authentication enablement, refer to the table above.

* **Do not select Ranger service installation when creating a cluster**


To quickly experience the EMR product, you can choose not to select Ranger service installation when creating a cluster. At this time, Ranger authorization is not enabled for any services that support Ranger authorization in the current version. You can still enable access control later during cluster operation by adding the Ranger service. For details, see [Add/restart services](https://docs.byteplus.com/docs/E-MapReduce/105409).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you enable permission control by adding the Ranger service after the cluster is running, Ranger authorization will not be automatically enabled for all services that support Ranger authorization in the current version. You need to manually enable Ranger authorization for the corresponding components on the Ranger service overview page. For details, see the <strong>Ranger authorization enable/disable</strong> subsection below).</div>


<span id="_3-2-ranger-鉴权启停"></span>
### Ranger authorization enable/disable

For clusters with the Ranger service installed, EMR allows you to control whether Ranger authorization is enabled or disabled for specific services. You can perform this operation on the Ranger service overview page.

Taking the HDFS service as an example, follow these steps:


1. Go to the **Cluster Details \> Service List \> Ranger \> Service Overview** page and turn on the HDFS Plugin switch.

2. Click Service, select the **HDFS** service from the dropdown list, go to the **Deployment Topology** tab, and restart the relevant HDFS service components.


To disable Ranger authorization for specific services, follow the same steps as above.

In addition to using Ranger authorization, the HDFS and YARN services also retain built\-in ACL authorization. The authorization process is shown in the following diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b46655b287f611787ec2024eec87e786.png) </span>

That is, authorization is granted if either the built\-in ACL or Ranger matches a permission\-allow policy; otherwise, the request is denied.

<span id="_4-权限配置管理"></span>
## Permission configuration management

The Ranger service provides a Web UI for configuring operation permissions for services. Considering that the Ranger Web UI may not be user\-friendly for ordinary users in terms of usability and interaction habits, EMR offers a management UI based on the RBAC permission model (hereafter referred to as the EMR permission control UI), which aims to provide a simpler and more intuitive way for ordinary users to configure permissions. For cluster types that support permission management, you can see the "**Permission Management**" entry in the cluster navigation bar.

At the same time, EMR also retains the native Ranger Web UI. You can choose based on your personal preferences. The two UIs are already interoperable at the underlying data layer. The following diagram illustrates the relationship between the EMR permission control UI and the Ranger Web UI:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acff728d674cf5cd0f56f847906da9b5.png) </span>

The current version of the EMR permission control RBAC permission model includes three dimensions: permissions, roles, and users. Each role can be associated with one or more permissions for one or more services, and a role can be granted to zero or more ordinary users who have been created or imported (users can be created or imported in EMR user management).

You can view the list of roles already created in the cluster on the **Permission Management** page, and you can also create, edit, or delete existing roles.

<span id="_4-1-创建角色"></span>
### Create roles

When creating a new role, you need to fill in the following information:


* **Role name (required)** : Must be unique within the cluster, limited to 30 characters, and cannot contain Chinese characters.

* **Associated users (optional)** : Select ordinary users created or imported in the user management module from the dropdown; multiple users can be associated.

* **Role description (optional)** : Used to describe the current role, limited to 255 characters, and can include Chinese characters.

* **Role permissions (optional)** : Set the permission information for specific services associated with the role. Click the "Add Permission" button to configure permission settings for each service.


<span id="_4-2-编辑角色"></span>
### Edit roles

You can click the **Edit** button to modify an existing role. Modifiable items include associated users, role description, and role permissions. Role name cannot be modified.

<span id="_4-3-删除角色"></span>
### Delete roles

You can click the **Delete** button to delete an existing role. Please assess the impact on the cluster before deletion.
