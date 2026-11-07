---
title: "Setting read local node only"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/read-local-node-only"
---

Cache for Redis supports close\-by access for multi\-availability zone instances. Once this feature is enabled, read requests will be directed to the node in the availability zone closest to the requesting client, reducing the latency of accessing Redis services. This topic describes how to use the close\-by access feature.

## Prerequisite

**Primary\-secondary** instances with multiple availability zones have been deployed. For details about multi\-availability zone deployment solution, refer to [Deploying in multiple availability zones](https://docs.byteplus.com/en/docs/redis/deploy-multi-az).

> **tip**

> Single node instances do not support multi\-availability zone deployment, and therefore do not support the close\-by access feature. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Feature introduction

> **tip**

* > For more information about the parameters `read_local_node_only` and `read_request_distribution_strategy`, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).

* > The descriptions in this topic are based on the single\-shard read request distribution strategy in the instance. The read request submission policies for other shards are consistent with those specified in this topic.

Cache for Redis supports enabling or disabling the close\-by access feature for multi\-availability zone instances via the `read_local_node_only` parameter. Redis jointly determines the read request distribution strategy in conjunction with the read/write splitting parameter (that is, `read_request_distribution_strategy`). Among them:

* When the close\-by access feature is enabled (that is, the value of `read_local_node_only` is `yes`), the read request distribution strategy varies depending on the read/write splitting strategy. The specific details are shown in the table below.

   |Read/write splitting strategy |Read request distribution strategy |Diagram |
   |---|---|---|
   |`read_primary_node_only` |Close\-by access is enabled but not taking effect. In this scenario, the read request distribution strategy in different availability zones is shown as follows:<br><br><br>* **Availability zone with the primary node**<br><br>   All read requests are sent only to the primary node.<br><br>* **Availability zones without the primary node**<br><br>   Read requests are sent across availability zones to the primary node. |![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_92ae6983fe58ebcc40b920b2b64f284e.png) |
   |`read_secondary_nodes_only` |With the close\-by access feature enabled, the read request distribution strategy across different availability zones is as follows:<br><br><br>* **Availability zone with the primary node**<br><br>   Read requests are sent to all secondary nodes in the current availability zone, which are evenly distributed.<br><br>   > **tip**<br>   <br><br>   > If there is only 1 primary node and no other secondary nodes in the availability zone where the primary node resides, all read requests will be sent to the primary node.<br>   <br><br>* **Availability zones without the primary node**<br><br>   Read requests are sent to all secondary nodes in the availability zone closest to the requesting client, which are evenly distributed. |![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82ff1c7df28bfaf20f8706a7e4ee4641.png) |
   |`read_primary_node_and_secondary_nodes` |With the close\-by access feature enabled, the read request distribution strategy across different availability zones is as follows:<br><br><br>* **Availability zone with the primary node**<br><br>   Read requests are sent to the primary node and all secondary nodes in the current availability zone, which are evenly distributed.<br><br>   > **tip**<br>   <br><br>   > If there is only 1 primary node and no other secondary nodes in the availability zone where the primary node resides, all read requests will be sent to the primary node.<br>   <br><br>* **Availability zones without the primary node**<br><br>   Read requests are sent to all secondary nodes in the availability zone closest to the requesting client, which are evenly distributed. |![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_113f140d56cad021c6e418f134677748.png) |

* When the close\-by access feature is disabled (that is, the value of `read_local_node_only` is `no`), the read request distribution strategy is determined solely by the value of the read/write splitting parameter. The specific strategies are as follows:

   * `read_primary_node_only`: Read requests are only sent to the primary node.

   * `read_secondary_nodes_only`: Read requests are randomly distributed across all secondary nodes.

   * `read_primary_node_and_secondary_nodes`: Read requests are randomly distributed across the primary node and all secondary nodes.

## Precautions

After modifying the `read_local_node_only`, clients may briefly encounter request failure\-related error reports. It is recommended to perform parameter modification operations during off\-peak business hours and ensure that the client is configured with the correct retry mechanism.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find the `read_local_node_only` parameter in the parameter list, and modify its value according to business requirements.

   You can enter the parameter name in the search bar on the right to filter.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the configuration parameters of a specified Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the configuration parameters of a specified Redis instance. |
