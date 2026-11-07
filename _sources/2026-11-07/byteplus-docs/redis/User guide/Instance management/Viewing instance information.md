---
title: "Viewing instance information"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/view-instance"
---

You can view the basic information, configuration details, billing information, and topology architecture of instances on the Redis console. This topic describes how to view Redis instance information.

## Prerequisites

A Redis instance has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

   > **tip**

   * > If there are many instances in your list, you can quickly filter out the target instances that meet the criteria through the following methods:

      * > In the search box in the upper left corner of the list, filter by instance ID, instance name, private address/port, private network IP, or VPC ID filtering criteria.

      * > Each filtering criterion supports specifying multiple keywords. Multiple keywords are separated by English commas (,), and multiple keywords under the same filtering criterion are in an `OR` relationship.

      * > Combined search using multiple filtering criteria is supported. Multiple filtering criteria are in an `AND` relationship.

   * > For instances with a long name, you can adjust the list by dragging the right border of the **Instance name/ID** column.

   * > On the **Instances** page, in the **Monitoring** column of the target instance's row, click the monitoring icon ![](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b0600ba57c01153454e5799d64e610d.png). You can directly open the monitoring panel on the list page to view monitoring charts.

4. You can view the following information about the Redis instance under the **Summary** tab.

   |Information category |Description |
   |---|---|
   |Basic information |* You can view details such as instance ID, instance name, availability zone, creation time, network information (private network and subnet), maintenance period, host project, deletion protection status and number of associated tags.<br><br>* In this pane, you can also perform tasks such as modifying instance name, modifying availability zone, modifying private network or subnet, setting maintenance periods, enabling or disabling instance protection and editing tags. For specific procedures, refer to:<br><br>   * [Modifying availability zone](https://docs.byteplus.com/en/docs/redis/modify-az)<br><br>   * [Modifying VPC or subnet](https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet)<br><br>   * [Setting maintenance period](https://docs.byteplus.com/en/docs/redis/set-maintenance-period)<br><br>   * [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection)<br><br>   * [Editing tag](https://docs.byteplus.com/en/docs/redis/associate-tag#.5Li65Y2V5Liq5a6e5L6L57uR5a6a5oiW5re75Yqg5qCH562-) |
   |Configuration |* You can view details such as database version, memory usage, read/write bandwidth, maximum number of connections, instance specifications, and whether shard cluster is enabled.<br><br>* In this pane, you can also perform tasks such as upgrading major version, modifying maximum number of connections, changing instance configuration, and modifying bandwidth in this area. For specific procedures, refer to:<br><br>   * [Upgrading major versions using blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment)<br><br>      > **tip**<br>      <br><br>      > To use the major version upgrade feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to technical support to apply for usage.<br>      <br><br>   * [Modifying maximum connections](https://docs.byteplus.com/en/docs/redis/modify-max-conn-number)<br><br>   * [Changing instance configuration](https://docs.byteplus.com/en/docs/redis/solutions-for-spec-modification)<br><br>   * [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth) |
   |Billing information |You can view information about the instance billing method. For yearly or monthly subscription instances, you can also view the expiration time. You can manually renew the instance or enable automatic renewal before the instance expires. For specific procedures, refer to [Automatic or manual renewal](https://docs.byteplus.com/en/docs/redis/automatic-manual-renewal). |
   |Topology |Supports performing the following actions in the **Topology** area:<br><br><br>* Access layer<br><br>   View information including the total number of nodes, node ID, and start time of the access layer.<br><br>* Proxy<br><br>   * View information including the total number of nodes, node ID, and start time of the proxy.<br><br>   * Manually restart the Proxy node, which is used for real\-time disaster recovery drills, or to initiate active operation and maintenance when services are abnormal or latency is high. For specific procedures, refer to [Restarting proxy node](https://docs.byteplus.com/en/docs/redis/restart-proxy-node).<br><br>   * In the **Monitoring** column to the right of the node list, click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b07ac099f8b06c60eb508e5ba1e2d111.png) icon to view monitoring metric data for the corresponding node. For more information on indicator\-based monitoring, refer to[ Monitoring metrics](https://docs.byteplus.com/en/docs/redis/monitoring-metric).<br><br>* Server<br><br>   * View information including the total number of shards, shard ID, and the total number of server nodes per shard.<br><br>   * Click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cad27cf4c326d9892fb605720a944843.png) icon on the left of the shard ID to view information such as node ID, memory usage, maximum bandwidth, node role, availability zone, and startup time for each node under the current shard.<br><br>      > **tip**<br>      <br><br>      * > The maximum bandwidth displayed here refers to the maximum bandwidth of the current shard in a non\-read\-write separation scenario. The read and write bandwidths are both this value.<br>      <br><br>      * > If the bandwidth of an instance is modified, the maximum bandwidth here will display the modified maximum bandwidth of a single shard (that is, the default bandwidth of a single shard + the additional bandwidth of a single shard). For more details, refer to [Modifying bandwidth](https://docs.byteplus.com/en/docs/redis/modify-bandwidth).<br>      <br><br>   * In the **Monitoring** column to the right of the node list, click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b07ac099f8b06c60eb508e5ba1e2d111.png) icon to view monitoring metric data for the corresponding node. For more information on indicator\-based monitoring, refer to[ Monitoring metrics](https://docs.byteplus.com/en/docs/redis/monitoring-metric).<br><br>   * Click **Switch to primary node** in the **Actions** column on the right of **SecondaryNode** to manually switch between primary and secondary nodes. For details about failover, refer to [Executing failover manually](https://docs.byteplus.com/en/docs/redis/switch-primary-node-manually). |

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) |Call the DescribeDBInstances API to query the basic information of one or more Redis instances. |
|[DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) |Call the DescribeDBInstanceDetail API to query the details of a specified Redis instance. |
