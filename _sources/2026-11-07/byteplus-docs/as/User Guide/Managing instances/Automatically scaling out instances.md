---
title: "Automatically scaling out instances"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Adding-instances-automatically"
---

The **scaling rule** and **instance count check** features in [adjustment types](https://docs.byteplus.com/en/docs/as/Adjustment-types) can help you monitor the instances in a scaling group and automatically trigger scale\-out activities. This topic describes how to select the automatic scale\-out policy for instances in a scaling group.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To avoid scaling failure, check whether there is sufficient quota in the Quota Center based on the amount of resources (such as instances and EIPs) you need.</div>


* <div data-tips="true" data-tips-type="warning">The balance requirement is applicable only when Pay\-as\-you\-go instances in a scaling group are automatically scaled out. Please refer to <a href="https://docs.byteplus.com/en/docs/Billing-and-Cost/bill-details">Bill details</a> to make sure that the total value of the cash balance and coupons is ≥ 100 RMB. Otherwise, instance scale\-out may fail. </div>



<span id=".5omp5a65562W55Wl57G75Z6L"></span>
## Scale\-out policy types

Currently, only [MultiAZ policies](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically#.5omp57yp5a65562W55Wl6K-05piO), and [scaling modes](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically#KN4gZ7Yo) are supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When both types coexist, the execution priority is: scaling mode \> MultiAZ policy.</div>


<span id="6tBDZsxn"></span>
## Explanation of scale\-out policies

Before learning about the scaling policy, you need to understand the following content:


* Availability zone usage scenarios:

   An availability zone refers to a physically isolated area with independent power supply and network within the same region. In the same VPC, each subnet corresponds to one availability zone, and the internal networks between availability zones are interconnected by default.

   * To meet high availability and disaster recovery requirements, we recommend that you select different subnets and deploy instances in different availability zones.

   * To meet low latency requirements, we recommend that you select a single subnet and deploy instances in the same availability zone.

* [Adjustment types](https://docs.byteplus.com/en/docs/as/Adjustment-types)

   The scale\-out policy varies slightly based on the adjustment type.

* Billing type for scaled out instances:

   You can specify the minimum Pay\-as\-you\-go instance count or capacity for a [scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group). You can also specify the percentage of Pay\-as\-you\-go instances for a scaling group. When [spot instances](https://docs.byteplus.com/en/docs/ecs/Spot_Instance) are sold out, you can create Pay\-as\-you\-go instances of the same type to meet the scale\-out requirements.

   In this scenario, if a scaling\-out task is triggered, the scaling group will first follow the policies described in the following table and attempt to create spot instances sequentially across all availability zones. When spot instances cannot be created in all availability zones, the scaling group will revert to the policies in the following table to create Pay\-as\-you\-go instances.

* Scenarios in which multiple instance types are required

   You can select multiple instance types and configure priorities in a single [scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources). We recommend that you select instance types similar in configuration, price, and performance. This helps reduce the risk of scale\-out failures due to insufficient stock and improve fault tolerance.

   Upon meeting the [scaling policy](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically#.5omp57yp5a65562W55Wl6K-05piO) requirements, if the higher\-priority instance type in the specified availability zone fails to be used to create instances, a lower\-priority instance type will automatically be used to create instances.


<span id="KN4gZ7Yo"></span>
### Description of the scaling mode

The scaling group supports being configured into "release mode" and "stop reclaim mode" based on different instance resource reclamation situations. For more resource reclamation scenarios, please refer to [Instance removal resource reclaim policy](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.5a6e5L6L56e75Ye65ZCO6LWE5rqQ5Zue5pS2562W55Wl).

When configured to "stop reclaim mode," it will affect the scaling up logic of instances in the scaling group:


* During scaling out, the scaling group prioritizes starting instances in the "Disabled" state before creating new instances. Instances that were stopped earlier are started first.

* If an instance starts successfully, its joining time to the scaling group will be automatically updated.

* If an instance fails to start, it will remain in the "Disable" state.


<span id=".5omp57yp5a65562W55Wl6K-05piO"></span>
### Scaling policy description

As described in the following table:


|Adjustment type |Scale\-out policy |Description | |
|---|---|---|---|
|Scaling rule |Priority policy |The scaling group sorts the availability zones by the order in which you select subnets. The availability zone corresponding to the first selected subnet has the highest priority. When the scaling group scales out, instances are preferentially deployed in availability zones with higher priority. |If instances cannot be scaled out in the target availability zone, other availability zones are selected in order of priority. |
||Balanced policy |Instances are randomly deployed to ensure that instances in the scaling group are as evenly distributed as possible across all availability zones. |If instances cannot be scaled out in the target availability zone, instances are deployed in other availability zones in a balanced manner. |
|Health Check |Priority policy |Instances are replaced preferentially in the original availability zones. |If instances cannot be scaled out in the original availability zone, other availability zones are selected in sequence. |
||Balanced policy ||If instances cannot be scaled out in the original availability zone, other availability zones are randomly selected. |


<span id=".5aaC5L2V6K6-572u5omp5a65562W55Wl"></span>
## How to configure the scale\-out policy

After a scaling group is created, you can [modify the scaling policy of the scaling group](https://docs.byteplus.com/en/docs/as/Modifying-the-multiAZ-policy-of-a-scaling-group). Modifications will not affect existing instances and will only apply to instances created or removed in subsequent adjustments.

<span id=".5a6e5L6L5omp5a655ZCO6LWE5rqQ5oyC6L29562W55Wl"></span>
## Resource mounting policy after instance scale\-out


* When the instance reclaim policy is set to "release mode": Instances are automatically added to the load balancer and RDS database instances associated with the scaling group. EIPs are automatically purchased and assigned based on the network configuration of the scaling configuration. You can log in to the Load Balancer, EIP, and other consoles to view the new instances.

* When the scaling mode is set to "Stop and Reclaim Mode", instances are automatically added to the load balancer associated with the scaling group, and the EIPs already associated with the instances are retained.
