---
title: "Deploying high-availability disaster recovery clusters"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Deploying-a-highly-available-and-disaster-tolerant-cluster"
---

This topic describes how to deploy a high\-availability disaster recovery cluster using Auto Scaling. It increases the success rate of scaling instances and enhances business high availability.

<span id=".6YOo572y5YmN6K-05piO"></span>
## Note before deployment

Auto Scaling provides the following methods to help you achieve high availability disaster recovery capabilities:


* Multiple availability zones: After you specify that instances in a scaling group are deployed across multiple availability zones, when resources are insufficient in one availability zone, the scaling group will automatically create instances in other availability zones. This ensures that scaling activities proceed smoothly. You can also specify that instances are preferentially deployed in higher\-priority availability zones, or that instances are deployed across availability zones in a balanced manner. For more information, see [Availability zones](https://docs.byteplus.com/en/docs/as/Regions-and-Availability-Zones#.5Y-v55So5Yy677yIQVrvvIk=).

* Multiple instance types: Select multiple instance types with similar performance, specifications, or prices as the instance configuration source in the same scaling configuration. When higher\-priority types cannot be used to create instances due to stockouts or other reasons, the next\-priority type will be automatically used to create instances. This increases fault tolerance during scale\-out and improves availability. It applies to scenarios requiring business continuity and high availability, without being restricted to a single instance type. For more information, see [Scaling configuration source](https://docs.byteplus.com/en/docs/as/Overview-of-scaling-configuration-sources).

* Integration with Load Balancer: Associate a Load Balancer instance with the scaling group so that when the scaling group scales in or out, the instances can be automatically synchronized to the backend server group of the Load Balancer instance. This ensures new instances handle client traffic immediately, released instances are promptly removed, and traffic is automatically distributed across all instances. It enhances business continuity and delivers reliable, enterprise\-grade stability. For more information, see [Load Balancer](https://docs.byteplus.com/en/docs/as/Related-cloud-services).

* Health check: The scaling group can regularly monitor the running status of instances. If an anomaly is detected, the scaling group will automatically add instances to replace unhealthy instances. This effectively prevents business disruptions caused by delayed detection of unhealthy instances. For more information, see [Classic Load Balancer (CLB)](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) and [Application Load Balancer (ALB)](https://docs.byteplus.com/en/docs/clb/Introduction).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have completed the preparations for deploying a high\-availability disaster recovery cluster:

<span id=".5YeG5aSH6LSf6L295Z2H6KGh"></span>
### Prepare Load Balancer

You can associate the Load Balancer with a scaling group. This allows the target instances to be automatically synchronized to the server group specified by Load Balancer when the scaling group executes adjustment jobs. With the Load Balancer service enabled, incoming traffic is automatically distributed across instances in the scaling group.

To associate a Load Balancer instance, confirm that you have a Load Balancer instance in the same subnet as the scaling group and in **Normal** status. Initialize the Load Balancer instance by referring to [Load Balancer quick start](https://docs.byteplus.com/en/docs/clb/Getting-Started).

<span id=".5YeG5aSH5a6e5L6L"></span>
### Prepare instance

When scaling jobs are being executed via AS, instances are purchased or released automatically. [Prepare the ECS instance](https://docs.byteplus.com/en/docs/ecs/Quick-start) to complete the pre\-purchase operations.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Create a scaling group](https://docs.byteplus.com/en/docs/as/Creating-a-scaling-group#.5pON5L2c5q2l6aqk): Select multiple subnets and specify the scaling policy.

   * For lower latency between your business systems, we recommend that you select "Priority policy". During scale\-out activities, instances are preferentially and as much as possible deployed in the availability zone with higher priority. During scale\-in activities, instances are preferentially removed from the availability zone with lower priority.

   * If your business requires disaster recovery capability, we recommend that you select "Balanced policy". When the scaling group scales out or in, instances are randomly deployed or removed to ensure that instances in the scaling group are as evenly distributed as possible across all availability zones.

2. [Configure multiple instance types for the scaling group](https://docs.byteplus.com/en/docs/as/Configuring-multiple-instance-types-for-a-scaling-group): Select the preferred instance type for scale\-out (that is, the type with the highest priority), and select several other instance types. Specify the priority by dragging the types.

   * You can select up to 10 instance types, including the preferred type.

   * We recommend that you select types with similar vCPU, memory, volume performance, network performance, and price.

3. [Enable the scaling group](https://docs.byteplus.com/en/docs/as/Enabling-a-scaling-group).

4. [Create scaling rules](https://docs.byteplus.com/en/docs/as/Creating-a-scheduled-scaling-policy).


<span id=".5omn6KGM57uT5p6c"></span>
## Execution results

This section describes the execution results through several typical scenarios. For details on the automatic scale\-out and scale\-in behaviors of instances, see [Automatically scaling out instances](https://docs.byteplus.com/en/docs/as/Adding-instances-automatically) and [Automatically scaling in instances](https://docs.byteplus.com/en/docs/as/Removing-instances-manually).


|Availability zone configuration |Instance type configuration |Execution result when the scaling group scales out by 5 instances |Execution result when the scaling group scales in by 2 instances |
|---|---|---|---|
|Availability zone A (highest priority), availability zone B and availability zone C (lowest priority), priority policy |4 instance types |Preferentially use the preferred instance type to deploy all 5 instances in availability zone A.<br><br><br>* If the preferred instance type in availability zone A cannot be used to create instances, use a lower\-priority instance type in availability zone A to create instances.<br><br>* If none of the 4 instance types in availability zone A can be used to create instances, preferentially use the preferred instance type in availability zone B to create instances. |Preferentially remove instances with the lowest\-priority specification from availability zone C.<br><br>If all instances in availability zone C are removed, continue to remove instances with lower\-priority type from availability zone B. |
|Availability zone A (highest priority), availability zone B and availability zone C (lowest priority), balanced policy |4 instance types |Preferentially use the preferred instance type to randomly deploy 5 instances across three availability zones, ensuring balanced distribution of instances in each availability zone after scale\-out.<br><br><br>* If the preferred instance type in the target availability zone cannot be used to create instances, use a lower\-priority instance type in that availability zone to create instances.<br><br>* If none of the 4 instance types in the target availability zone can be used to create instances, randomly select another availability zone and preferentially use the preferred instance type to create instances. |Remove instances while ensuring that the remaining instances are evenly distributed across all availability zones.<br><br>If instances cannot be removed from the target availability zone, randomly remove instances with a lower\-priority type from other availability zones. |
