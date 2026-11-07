---
title: "How does the expected number of nodes change?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How_does_the_expected_number_of_nodes_change"
---

The expected number of nodes refers to the number of nodes that a node pool needs to maintain. You can adjust the expected number of nodes to scale out or scale in the node pool.

For a node pool with an expected node count configured, the resulting behavior differs based on the operation performed, such as removing nodes and releasing the associated ECS instances. The following table displays the details.


|Operation side |Specific operations |Change in the number of nodes in the node pool |
|---|---|---|
|VKE |Adjust the **number of nodes** in the [VKE console](https://console.byteplus.com/vke). |VKE will scale out or scale in the nodes in the node pool until the expected number of nodes you set is reached. |
||Add existing nodes (existing ECS instances) to a node pool in the [VKE console](https://console.byteplus.com/vke). |VKE will add existing nodes to the specified node pool as required. The number of nodes in the node pool increases. |
||Add existing nodes to a node pool by using [CreateNodes](https://docs.byteplus.com/en/docs/vke/CreateNodes). ||
||Delete nodes in the [VKE console](https://console.byteplus.com/vke). |VKE will delete specified nodes from the node pool based on your requirements. The number of nodes in the node pool decreases. |
||Delete nodes by using the [DeleteNodes](https://docs.byteplus.com/en/docs/vke/DeleteNodes) API. ||
|ECS |Delete the ECS instance associated with a node in a VKE normal or managed node pool in the [ECS console](https://console.byteplus.com/ecs). |VKE will generate a new ECS instance based on the latest node pool configuration and add it to the node pool to reach the expected number of nodes. |
||Delete the ECS instance associated with a node in a VKE normal node pool or managed node pool by using the [DeleteInstance](https://docs.byteplus.com/en/docs/ecs/DeleteInstance) API or [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API. ||
||Subscription ECS instances are released upon expiration. ||
||After an existing ECS instance is added to a VKE normal or managed node pool, the ECS instance is deleted in ECS. ||
||After an existing ECS instance is added to the default VKE node pool, the ECS instance is deleted in ECS. |The number of nodes in the default node pool of VKE decreases. |
