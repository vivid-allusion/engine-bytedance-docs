---
title: "Slot distribution view"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Slot_distribution_view"
---

This topic describes the usage of the Slot distribution view feature.

## **Function**

The Slot distribution view is used to display the slot allocation of each shard in a Redis cluster instance. Redis clusters allocate 16384 hash slots to different shards to manage data. With this feature, you can:

* View a global Slot distribution overview to understand the slot range and quantity managed by each shard.

* Use the Key routing simulator (offline) to enter any Key and locate its corresponding shard and slot, assisting in shard planning and data distribution design.

## **Prerequisites**

* An instance has been created and its instance status is **Running**.

* The instance uses a Cluster architecture. Standard instances do not involve shard routing.

## **Procedure**

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Performance analysis** tab.

5. Click the **Slot distribution view** sub\-tab to access the Slot distribution view page. On the Slot distribution view page, you can use the Key routing simulator (offline) or view the global Slot distribution.

   * **Key routing simulator**

      The Key routing simulator is an offline simulation tool used to calculate the routing destination of a specified key, helping you understand which slot and shard the key will be routed to.

      **Usage:**

      1. Enter the Key to query in the input box of the **Key routing simulator (offline)**  area.

         * Supports entering regular Keys, e.g., user:1000:profile.

         * Supports entering Keys with Hash Tags, e.g., {user_id}:profile or {shop_id_42}:item_list.

      2. The system automatically parses the Key's effective Hash Tag, calculates the corresponding Slot number, and displays the shard information for that Slot.

   * **View global slot distribution**

      The global Slot distribution list displays the Slot range and ownership of each shard based on the instance's static sharding configuration. Table field descriptions are as follows:

      |**Field** |**Description** |**Example** |**Description** |
      |---|---|---|---|
      |Shard ID |Shard ID |0 |The unique identifier for this shard in the cluster. |
      |Number of segments |Number of slot segments |1 |The number of continuous slot segments managed by this shard. When slot distribution is discontinuous, the number of segments is \> 1. |
      |Total slots |Total number of slots under management |4096 |The total number of slots managed by this shard. |
      |Slot range |Slot Range |0 \- 4095 |The range of slot numbers managed by this shard. If there are multiple discontinuous segments, the slot range of each segment will be displayed separately as tags. |

   * **About the number of Slot segments**

      Normally, each shard manages a continuous range of Slots, with a segment count of 1. After a slot migration (e.g., scaling up or down), the slot distribution of some shards may become discontinuous. In this case, the number of segments will be greater than 1, and multiple slot ranges will be displayed as independent tags.
