---
title: "Create custom topology clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/create_custom_topology_clusters"
---

This article describes how to create custom topology clusters in EMR. It is suitable for scenarios where node groups and service deployments need to be flexibly planned based on business requirements. The article focuses on prerequisites, project and configuration processes, as well as the custom topology capabilities, deployment limitations, and adjustment rules supported by each service component, helping you complete cluster planning and setup.

<span id="3006af0c"></span>
# **Prerequisites**


1. The primary Volcano Engine account has been registered, and all cloud resource access authorizations for the service account have been completed. The system default policy named “**ServiceRoleForEMR**” has been granted to the EMR service account.

   You can use the upper right corner **User** \> **Access control** \> **Role Management** interface, search for the keyword "EMR" in the search bar at the top right of the interface, and confirm whether the “**ServiceRoleForEMR**” role is effective.

2. When a sub\-user performs cluster creation, the primary account must grant EMRFullAccess permission to the sub\-user in the **Access control**  **\> User** interface. For details, see [Role authorization](https://docs.byteplus.com/docs/E-MapReduce/ecs_role_authorization).


For account activation and permission operations, see [Preparation](https://docs.byteplus.com/docs/E-MapReduce/Preparation_sq).

<span id="62566711"></span>
# Limits

Please pay attention to the restrictions of **Set deployment topology**:


* **Custom deployment**Only clusters with **service high availability** enabled are supported.

* **Custom deployment**Subject to restrictions on the number of nodes, node groups, and service roles. If the conditions are not met, the page options will be grayed out and cannot be adjusted.


<span id="_2-操作步骤"></span>
## **Procedure**


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the top menu bar, select the region and project space from the dropdown according to your actual scenario:

   * Region: The created cluster and corresponding resources will be deployed in the selected region and cannot be changed.

   * Project space: The system has automatically created a default project named **default**. You can create your own project space using the following path:

      * In the upper right corner of the interface, go to **User \>Access control \> Resources \> Project** to enter the project interface.

      * Click the Create projectbutton, enter the project name, display name, remarks, and other information to complete the creation of a new project.

         For details, see [Project configuration](https://docs.byteplus.com/docs/E-MapReduce/ecs-project_configuration).

3. In the overview interface, click the Create resourcebutton to enter the cluster creation interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/973147d5df694555b881e47f020db530~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-自定义配置集群"></span>
## Configure custom cluster


1. In the **software settings** step, select the Data Lake \- **Hadoop cluster** type or **custom cluster** type, and complete parameter configuration for the remaining components and metadata information. For more configuration notes, see [Create clusters](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

2. After **Software settings** selection is complete, click the **Next** button to enter the **Hardware settings** page, and fill in configuration parameters such as Payment settings, available regions, Network configuration, Instance Settings, and more. For more hardware setting notes, see [Create clusters](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

   1. In the **Instance Settings** process, click the **Custom deployment** button in the upper left corner;

   2. In **Deployment topology** below, click the **SettingsDeployment topology** button to enter the deployment topology settings interface;

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4e59bf37f224c3ca1f61394964686e1~tplv-goo7wpa0wc-image.image) </span>

   3. Complete custom topology adjustments for HDFS, YARN, Hive, Zookeeper, and more. For details, see [Custom topology adjustment notes](https://docs.byteplus.com/docs/E-MapReduce/create_custom_topology_clusters#_4-%E8%87%AA%E5%AE%9A%E4%B9%89%E6%8B%93%E6%89%91%E8%B0%83%E6%95%B4%E8%AF%B4%E6%98%8E) below.

   4. After completing the deployment topology settings, click the **Confirm** button in the lower right corner to save the deployment topology plan.

3. After completing topology adjustments and hardware settings, click the **Next** button to enter the **other settings** page, and fill in the cluster name and key pair information. For more setting notes, see [Create clusters](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later).

4. After completing other settings, click the **Next** button to enter the overall **Cluster Preview** confirmation page. Once confirmed, check **I agree to the EMR Service Terms** at the bottom of the page, and click the **Create Now** button to complete cluster creation.

5. You can then go to the cluster list to view the cluster creation progress and wait for it to finish.


<span id="_4-自定义拓扑调整说明"></span>
## **Custom topology adjustment notes**


|**Service name** |**Component name** |**Supported custom topology for node/node group scenarios** |
|---|---|---|
|HDFS |Namenode |Master node group<br><br>Supported number of instances: multiples of 2, and cannot exceed the number of master nodes<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Federation feature can be enabled to specify multiple NameService groups.</div><br><br><br><div data-tips="true" data-tips-type="tip">For each NameNode group, the user must enter a NameService name, which can contain only letters, numbers, and underscores.</div><br> |
||Datanode |Core node group |
|YARN |ResourceManager |Master node group<br><br>Supported number of instances: 2 |
||NodeManager |Core/Task node group |
|Hive |MetaStore |Master node group<br><br>Supported number of instances: 2 or more, cannot exceed the number of master nodes |
||HiveServer2 |Master node group<br><br>Number of instances: 2 or more, cannot exceed the number of master nodes |
|ZooKeeper |ZooKeeper |Master node group<br><br>Can be set to 3, 5, or 7, but cannot exceed the maximum number of master nodes<br><br>The number of ZooKeeper instances only affects the number of fault\-tolerant nodes and does not affect ZooKeeper metadata storage capacity. |
|Doris |FE |Not supported |
||BE |Core node group |
|StarRocks |FE |Not supported |
||BE |Core node group |
||CN |Core/Task node group |
|Presto |Coordinator |Not supported |
||Worker |Core/Task node group |
|Trino |Coordinator |Not supported |
||Worker |Core/Task node group |
|Celeborn |Master |Master node (supported only in EMR\-4.0.0 and later versions)<br><br>Can be set to 3, 5, or 7, but cannot exceed the number of master nodes |
||Worker |Core/Task node group |
|DolphinScheduler |Master Server |Master node group (supported only in EMR\-4.0.0 and later versions) |
||Alert Server |Master node group (supported only in EMR\-4.0.0 and later versions) |
|Ranger |Ranger Usersync |Master node group (supported only in EMR\-4.0.0 and later versions) |
|Airflow |Airflow Celery Flower |Master node group (supported only in EMR\-4.0.0 and later versions) |
||Airflow WebServer |Master node group (supported only in EMR\-4.0.0 and later versions) |
||Redis Server |Master node group (supported only in EMR\-4.0.0 and later versions) |
||Airflow Scheduler |Core node group (supported only in EMR\-4.0.0 and later versions) |
||Airflow Celery Worker |Core node group (supported only in EMR\-4.0.0 and later versions) |
