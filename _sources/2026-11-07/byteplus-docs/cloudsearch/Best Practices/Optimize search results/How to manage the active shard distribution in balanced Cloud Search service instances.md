---
title: "How to manage the active shard distribution in balanced Cloud Search service instances"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/How_to_manage_the_active_shard_distribution_in_balanced_Cloud_Search_service_instances"
---

When creating a new index or changing the number of nodes (such as node restart or addition), Elasticsearch will adjust shard locations. Adding nodes or creating new indexes may cause imbalance in active shard numbers across nodes, resulting in uneven node load during peak writes and low overall cluster resource utilization. You can enable active shard balancing by configuring `active shard balancing` settings to evenly distribute active shards of different indices across all nodes, improving overall resource utilization.

## Precautions

* When multiple availability zones are used, `awareness` controls the distribution of active and replica shards, preventing them from residing in the same zone. This imposes certain limitations on active shard balancing during the `relocation` phase.

   * Existing indices may not support active shard balancing across availability zones when this feature is enabled.

   * New indices can still balance active shards across availability zones when assigning shards one by one.

* Currently, only Elasticsearch 7.10.2 instances created after December 2024 and OpenSearch 2.9.0 and 3.3.0 instances support enabling active shard balancing. You can try configuring it first; if you encounter an unrecognized parameter error, restarting the instance will activate this feature.

## Parameter description

You can set active shard balancing for indices with the following parameters.

|**Parameter** |**Description** |
|---|---|
|`cluster.routing.allocation.balance.prefer_primary` |Whether to turn on active shard balancing during `allocation`. The values are as follows:<br><br><br>* `true`: turn on active shard balancing.<br><br>* `false`: (default value) means turned off. |
|`cluster.routing.allocation.rebalance.primary.enable` |The values for turning on `rebalance` for active shard balancing are as follows:<br><br><br>* `true`: means turned on.<br><br>* `false`: (default value) means turned off. |
|`cluster.routing.allocation.rebalance.primary.buffer` |The allowed imbalance level during `rebalance`, ranging from 0 to 1, with a default value of 0.1.<br><br>0 means complete disallowance, specifically referring to how much the number of active shards on the current node exceeds the theoretically acceptable average per node. |
|`cluster.routing.allocation.move.primary_first` |Whether to migrate the active shard first when migrating shards. The values are as follows:<br><br><br>* `true`: migrate the active shard first when migrating shards.<br><br>* `false`: (default value) do not migrate the active shard first when migrating shards, and this does not affect active shard balancing. |
|`cluster.routing.allocation.primary_constraint.threshold` |Represents the increase in `weight` caused by violating the global active shard balance. Long type, default is 10.<br><br>> **tip**<br><br><br>> If this parameter value is too large, it may cause some nodes to have only active shards without replica shards in certain cases. Modify this parameter with caution.<br> |

## Usage example

The following uses the Kibana interface as an example to explain how to turn on active shard balancing.

1. Log in to Kibana. For the specific procedure, refer to [Log on to Kibana/Dashboards](https://docs.byteplus.com/en/docs/cloudsearch/logging-tool).

2. In the Kibana interface, enter the following command to turn on active shard balancing:

   ```JSON
   PUT _cluster/settings
   {
     "persistent": {
       "cluster": {
         "routing": {
           "allocation.balance.prefer_primary": true,
           "allocation.rebalance.primary.enable": true
         }
       }
     }
   }
   ```

   > **tip**

   > This parameter can only be modified when the instance health status is green. If the instance health status is orange, you also need to change `cluster.routing.allocation.allow_rebalance` from `indices_all_active` to `indices_primaries_active`. After balancing, revert it to the original configuration. For detailed actions, refer to [Viewing instance health overview](https://docs.byteplus.com/en/docs/cloudsearch/view-instance-health-overview).
