---
title: "Vertical scaling overview"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Overview-of-vertical-scaling"
---

You can use the vertical scaling feature to change the instance type (including vCPU and memory) of pay\-as\-you\-go instances. Upgrade and downgrade operations are supported. When an instance type cannot meet or exceeds application requirements, the instance type can be automatically upgraded or downgraded via the vertical scaling feature to meet your diverse needs.

When a vertical scaling task is executed, the instance needs to be restarted. During this process, the instance is stopped, the instance type is modified, and then restarted. As the instance is temporarily stopped, the high availability of your business services may be impacted.

<span id=".5bqU55So5Zy65pmv"></span>
## Scenarios

Currently, only scheduled vertical scaling tasks are supported. For predictable business fluctuations, such as traffic surges every weekend or activities that need to be carried out at a specified time, you can create scheduled vertical scaling tasks to upgrade or downgrade instance types before or after specific time points. This allows your business requirements to be met automatically.

For small\-scale businesses with no strict high availability requirements, we recommend using this feature to adjust the instance type, rather than creating or removing instances to reduce costs.

<span id=".5Yqf6IO95LyY5Yq_"></span>
## Advantages


* Vertical scaling adjusts instance type configuration. Compared to instance count adjustments, it eliminates resource consumption due to repeated instance creation/release. Additionally, it reduces repetitive configuration work for custom business scenarios.

* When a vertical scaling task is executed, the target instance is stopped, the instance type is modified, and then restarted automatically, requiring no manual operations.


<span id=".5Lu75Yqh57G75Z6L"></span>
## Task type

Vertical scaling tasks support immediate, scheduled, or periodic execution. Select an appropriate type based on your needs.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The maximum number of vertical scaling tasks one root user can create in one region is 100.

* You can only select one instance for one vertical scaling task.

* You can change the instance type only for [pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) instances (excluding [spot instances](https://docs.byteplus.com/en/docs/ecs/Spot_Instance)) via the vertical scaling feature.
