---
title: "Automatically scaling in instances"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Removing-instances-manually"
---

The **scaling rule** and **instance count check** features in [adjustment types](https://docs.byteplus.com/en/docs/as/Adjustment-types) can help you detect anomalies in a scaling group, which will automatically trigger scale\-in activities. This topic describes how to select the removal policy when a scaling group automatically scales in.

<span id=".56e75Ye6562W55Wl57G75Z6L"></span>
## Removal policy types

Currently, the following removal policy types are supported: [instance reclaim mode](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#HSIc97qU), [scaling policy](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.5omp57yp5a65562W55Wl6K-05piO), and [instance removal policy](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.5a6e5L6L56e75Ye6562W55Wl6K-05piO). You can combine these types based on your specific needs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When three types coexist, the execution priority is as follows: instance reclaim mode \> scaling policy \> instance removal policy.</div>


<span id=".56e75Ye6562W55Wl6K-05piO"></span>
## Removal policy description

Before you learn how to configure a removal policy, you need to understand the following content:


* Instance billing type:

   You can specify the minimum Pay\-as\-you\-go instance count or capacity for a [scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group). You can also specify the percentage of Pay\-as\-you\-go instances for a scaling group. When [spot instances](https://docs.byteplus.com/en/docs/ecs/Spot_Instance) are sold out, you can create Pay\-as\-you\-go instances of the same type to meet the scale\-out requirements.

* Scenarios in which multiple instance types are required:

   You can select multiple instance types and configure priorities in a single [scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources). We recommend that you select instance types similar in configuration, price, and performance. This helps reduce the risk of scale\-out failures due to insufficient stock and improve fault tolerance. When a scaling group removes instances in an availability zone, instance types with lower priority are removed first.

   When both the [scaling policy](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.5omp57yp5a65562W55Wl6K-05piO) and the [instance removal policy](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.5a6e5L6L56e75Ye6562W55Wl6K-05piO) apply, the priority is as follows: scaling policy \> multiple instance type priority \> instance removal policy.

* [Instance sources](https://docs.byteplus.com/en/docs/as/Instance-lifecycle#.5a6e5L6L5p2l5rqQ) of the scaling group: Instances from different sources in a scaling group have different removal policies.

   * Automatically created instances: Instances automatically created by the scaling group during a scale\-out activity based on the scaling configuration source.

   * Manually added instances: Instances manually added to the scaling group after the instances are created in the ECS console.

* Instances in [vertical scaling](https://docs.byteplus.com/en/docs/as/Overview-of-vertical-scaling) cannot be removed


<span id="HSIc97qU"></span>
### Description of instance reclaim mode

Depending on how instance resources are reclaimed, the scaling group supports two instance reclaim modes: "Release Mode" and "Stop\-and\-Reclaim Mode". For more information, see [Resource reclaim policy after instance removal](https://docs.byteplus.com/en/docs/as/Removing-instances-manually#.5a6e5L6L56e75Ye65ZCO6LWE5rqQ5Zue5pS2562W55Wl).

When configured to "stop\-and\-reclaim mode," it affects the scaling down logic for instances in the scaling group:


* During scaling down, instances will first be turned to the Disable status.

* Disabled instances are not counted towards the desired instance count but are included in the maximum instance count.

* During scaling down, instances in the Disable status are removed first, with older disabled instances being released earlier.


<span id=".5omp57yp5a65562W55Wl6K-05piO"></span>
### Scaling policy description

Before learning about the scaling policy, you need to understand the following content:


* Availability zone usage scenarios:

   An availability zone refers to a physically isolated area with independent power supply and network within the same region. In the same VPC, each subnet corresponds to one availability zone, and the internal networks between availability zones are interconnected by default.

   * To meet high availability and disaster recovery requirements, we recommend that you select different subnets and deploy instances in different availability zones.

   * To meet low latency requirements, we recommend that you select a single subnet and deploy instances in the same availability zone.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This policy takes effect only when you select multiple subnets in different availability zones.   </div>
   

When a scaling group scales in, instances that do not belong to the availability zone of the scaling group are removed first. The policy then proceeds as described in the following table:


|Scaling policy |Description | |
|---|---|---|
|Priority policy |The scaling group sorts the availability zones by the order in which you select subnets. The availability zone corresponding to the first selected subnet has the highest priority. When the scaling group scales in, instances are preferentially removed from availability zones with lower priority. |If instances cannot be removed in the target availability zone, other availability zones are selected in order of priority. |
|Balanced policy |Instances are removed randomly to ensure that the remaining instances are distributed as evenly as possible across all availability zones. |If instances cannot be removed in the target availability zone, other availability zones are randomly selected. |


<span id=".5a6e5L6L56e75Ye6562W55Wl6K-05piO"></span>
### Description of the instance removal policy

As described in the following table:


|Policy |Description |Applicable scenario |
|---|---|---|
|Earliest instance created from earliest scaling configuration |Among instances **automatically created** by the scaling group based on earlier\-created scaling configuration sources, those created earlier are removed first. |This policy is applicable to scenarios where instances created based on the old scaling configuration need to be gradually replaced after the scaling configuration source is updated. |
|Most recent instance created from earliest scaling configuration |Among instances **automatically created** by the scaling group based on earlier\-created scaling configuration sources, those created later are removed first. ||
|Earliest instances |Instances created earlier (**including automatically created and manually added**) are removed first. |This policy is applicable to scenarios where all instances in the scaling group need to be upgraded as a whole. |
|Most recent instances |Instances most recently created in the scaling group (**including automatically created and manually added**) are removed first. |This policy is applicable to scenarios where new instances are used only for testing and do not need to provide external services. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When "Earliest instance created from earliest scaling configuration" is selected and all relevant instances are removed, if more instances need to be removed, manually added instances will then be removed sequentially in the order of "Most recent Instances".</div>


<span id=".5aaC5L2V6K6-572u56e75Ye6562W55Wl"></span>
## How to configure the removal policy

After a scaling group is created, you can [modify the scaling policy of the scaling group](https://docs.byteplus.com/en/docs/as/Modifying-the-multiAZ-policy-of-a-scaling-group). Modifications will not affect existing instances and will only apply to instances created or removed in subsequent adjustments.

<span id=".5a6e5L6L56e75Ye65ZCO6LWE5rqQ5Zue5pS2562W55Wl"></span>
## Resource reclaim policy after instance removal

After instances are removed from the scaling group, the Auto Scaling console will no longer display the instances. However, whether the resources of the removed instances are retained depends on the [lifecycle management](https://docs.byteplus.com/en/docs/as/Instance-lifecycle#.5a6e5L6L55Sf5ZG95ZGo5pyf566h55CG) method in the scaling group. Specifically:


* Instances whose lifecycle is managed by the scaling group:

   * When the instance reclaim policy is set to "release mode": Instances will be automatically deleted upon removal, along with associated resources such as EIPs, volumes, and network interfaces. The instances will be removed from the associated load balancer and RDS database instances.

      > Since EBS Volume involves the security of your business data, only the System Volume and Data Volumes specified to be released with the instance in the [scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources) are released.      
      

         * When the instance reclaim policy is set to "billing stop mode": Instances remain in the scaling group but are [converted to disabled status](https://docs.byteplus.com/en/docs/as/Change_the_instance_to_the_Disable_status). Compute resources (vCPU, GPU, and memory) of the instances are reclaimed and removed from Load Balancer instances while volumes, images, EIPs, bandwidth (fixed bandwidth mode), and RDS databases are retained.

* Instances whose lifecycle is **not managed** by the scaling group: After the instances are removed, the instance, associated resources, and resource association status will be retained. You can still log in to the corresponding consoles to view the resources.

* Instances enabled with "instance protection": Not affected by the removal policy.
