---
title: "Managing cluster events"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Manage_cluster_events"
---

Cluster event monitoring is used to record and notify events related to GPU instances in HPC clusters. When an instance triggers a system event (such as a system failure that leads to instance redeployment), you can promptly view the event details and take action.

<span id=".5LqL5Lu25qaC6L-w"></span>
## Event overview


* Event status: Displays the different stages or situations of an event in the lifecycle. For details, refer to the [Event overview](https://docs.byteplus.com/en/docs/ecs/Event-monitoring-overview#.5LqL5Lu254q25oCB).

* Naming rules for event types and event names: Event types and event names follow fixed naming rules. After understanding the naming rules, you can quickly learn what an event means based on the name. For details, refer to [Naming rules for event types and event names](https://docs.byteplus.com/en/docs/ecs/Event-monitoring-overview#.5LqL5Lu257G75Z6L5LiO5LqL5Lu25ZCN56ew5ZG95ZCN6KeE5YiZ).


<span id=".5LqL5Lu25rGH5oC7"></span>
## Event summary

Below are the types, statuses, names, and recommended actions for currently supported events.


|Category |Event type |Event name |Description |
|---|---|---|---|
|Scheduled O&M events |SystemMaintenance.Redeploy |Instance redeployment due to system maintenance |For event descriptions, impacts, recommended user operations, and other information, refer to [Scheduled O&M events](https://docs.byteplus.com/en/docs/ecs/Event-type-overview#.6K6h5YiS5YaF6L-Q57u05LqL5Lu2). |
||InfrastructureUpgrade.Redeploy |Instance redeployment due to infrastructure upgrade ||
|Unexpected O&M events |SystemFailure.Redeploy |Instance redeployment due to system failure |For event descriptions, impacts, recommended user operations, and other information, refer to [Unexpected O&M events](https://docs.byteplus.com/en/docs/ecs/Event-type-overview#.6Z2e6aKE5pyf6L-Q57u05LqL5Lu2). |
||GpuRiskDetected |GPU risk detected ||
||DiskErrorDetected |Hard disk exception ||


<span id=".5p-l6K-i5bm25aSE55CG5LqL5Lu2"></span>
## Query and handle events

You can query and handle events in the ECS console. To avoid impacting your business operations, please promptly view and address the issue upon receiving the event notification.


1. Log in to the [HPC Cluster console](https://console.byteplus.com/ecs/hpcCluster). 

2. In the left\-side navigation pane, select "Instances & Images \> HPC Cluster".

3. In the top menu bar, select the project and region of the resource that has triggered the event.

4. On the HPC Cluster page, click the target instance and the "Event list" tab in sequence.

5. You can view and handle events after clicking the "Pending" or "All" tabs. You can also filter the target events by time period, event ID, or other conditions. For more operation instructions, refer to [Query and handle events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events).

   * **Pending (default)** : Displays only the events requiring response in this cluster.

   * **All**: Displays all current O&M events for this cluster, including handled and pending events.


<span id=".6YWN572u5LqL5Lu255uR5o6n6YCa55-l"></span>
## Configure event monitoring notifications

When a GPU instance within an HPC cluster triggers a monitoring event, you can receive the event notification by subscribing to message center notifications, or [configuring Cloud Monitor notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#.5LqR55uR5o6n6YCa55-l).


> * Whether you have configured to receive event notifications or not, this does not affect events being displayed in the ECS console. For information about how to query and handle events in the console, refer to [Query and handle events](https://docs.byteplus.com/en/docs/gpu/Manage_cluster_events#.5p-l6K-i5bm25aSE55CG5LqL5Lu2)​.

> * You can receive event notifications via the message center and Cloud Monitor in a more timely and convenient manner than in the console.
