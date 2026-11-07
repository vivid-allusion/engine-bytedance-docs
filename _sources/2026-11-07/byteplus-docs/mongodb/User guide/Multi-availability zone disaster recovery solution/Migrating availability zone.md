---
title: "Migrating availability zone"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/migrate-az"
---

Document Database for MongoDB provides availability zone migration feature, supporting various availability zone migration scenarios to enhance instance disaster recovery capabilities and enable cross\-datacenter disaster recovery. This topic describes operations related to availability zone migration.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* The instance must not have any public network addresses. If public network addresses already exist in the instance, release all public network addresses before migrating availability zones. For specific procedures, refer to [Releasing public address](https://docs.byteplus.com/en/docs/mongodb/release-public-address).


<span id=".5pSv5oyB55qE6L-B56e75Zy65pmv"></span>
## Supported migration scenarios


|Supported migration scenarios |Scenario description |
|---|---|
|Migrate from a single availability zone to a single availability zone |Migrating a MongoDB instance to the availability zone to which the ECS instance belongs, and connecting ECS instance and MongoDB instances within the same availability zone through a private network to reduce network latency and optimally ensure security and performance. |
|Migrate from a single availability zone to a single availability zone |Enhance the disaster recovery capability of the instance to achieve cross\-data center disaster recovery. Single availability zone instances can withstand server and rack\-level failures, while multi\-availability zone instances can withstand datacenter\-level failures. For example, deploying nodes from a three\-node replica set in three different availability zones within the same region can withstand higher levels of disaster. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Currently, only availability zone migration within the same region is supported. Cross\-region availability zone migration is not yet supported.

* Migration from multiple availability zones to other multiple availability zones is only supported in regions with 4 or more availability zones. Currently, only China (Shanghai) supports 4 availability zones.

* To migrate from a single availability zone to multiple availability zones, ensure that the instance does not contain any read\-only nodes. If read\-only nodes already exist in the instance, delete all read\-only nodes before performing the availability zone migration. For specific procedures to delete read\-only nodes, refer to [Deleting read-only node](https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node#.5Yig6Zmk5Y-q6K-76IqC54K5).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The availability zone migration operation not only affects the performance of the primary node but is also influenced by various factors (such as network environment, task queue, data volume, and so on). **It is recommended to perform the operation during off\-peak business hours**.

* During the availability zone switch, **the instance may experience 1~2 temporary disconnections, each lasting within 30 seconds**. Proceed with caution and ensure the client is configured with the correct retry mechanism.

* During the availability zone switch, the instance will enter the **Migrating** status. At this time, you can only view instance information, and cannot perform any modification operations on the instance (such as changing instance configuration, modifying instance name, and so on). For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* Migrating availability zones may **result in changes to the VIP (Virtual IP address)** . If the business uses a VIP to connect to the instance, the corresponding connection will be disconnected.

* For optimal network performance, it is recommended to **change the instance's subnet to a subnet in the new primary availability zone when migrating availability zones**.

* Availability zone migration involves data migration, which may affect business operations and even lead to irreversible consequences. This is an **allowlist feature**. To use this feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to request enablement. Before applying, carefully assess the above risks and ensure your business is configured with a robust automatic reconnection mechanism.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. In the **Basic information** area under the **Summary** tab, click <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) </span> icon behind the availability zone.

6. In the **Migrate availability zone** dialog box, set the availability zone deployment plan for the instance according to service requirements.

   
   |Parameter |Description |
   |---|---|
   |Current availability zone |Confirm the current availability zone of the instance. |
   |Deployment plan |You can select a deployment plan based on the availability zone migration scenario:<br><br><br>* Migrate from a single availability zone to a single availability zone<br><br>   1. The **Deployment plan** is **Single availability zone deployment**; no configuration is required.<br><br>   2. Select the target availability zone on the right side of **Availability zone**.<br><br>* Migrate from a single availability zone to a single availability zone<br><br>   1. Select the **Deployment plan** as **Multiple availability zone deployment**.<br><br>   2. Select the target availability zones from the dropdown lists of **Primary availability zone** and two **Secondary availability zone**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The availability zones before and after migration cannot be the same.</div><br> |
   |Subnet |Select an available subnet in the current VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Subnets possess availability zone properties. The drop\-down list only displays subnets in the selected availability zone.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To avoid cross\-availability zone access for subnets, it is recommended selecting a new subnet associated with the primary availability zone to achieve optimal network performance.</div><br> |
   |Instructions for use |Carefully read and check the notice for migrating availability zones. For details about the availability zone migration feature, refer to [Precautions](https://docs.byteplus.com/en/docs/mongodb/migrate-az). |
   

7. click **OK**.
