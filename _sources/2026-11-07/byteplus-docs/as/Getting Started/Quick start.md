---
title: "Quick start"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Preparations"
---

You can refer to the quick start documentation to quickly experience the process of performing adjustments via Load Balancer and AS. This topic describes the preparations required before you get started.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

<span id=".5YeG5aSH6LSf6L295Z2H6KGh"></span>
### Prepare Load Balancer

You can associate the Load Balancer with a scaling group. This allows the target instances to be automatically synchronized to the server group specified by Load Balancer when the scaling group executes adjustment jobs. With the Load Balancer service enabled, incoming traffic is automatically distributed across instances in the scaling group.

To associate Load Balancer, confirm that you have a Load Balancer instance deployed in the same VPC as the scaling group and in **Active** status. Refer to [CLB quick start](https://docs.byteplus.com/en/docs/clb/Getting-Started) or [ALB quick start](https://docs.byteplus.com/en/docs/clb/ALB-quick-start-Overview) to complete the initialization of the corresponding Load Balancer instance.

<span id=".5YeG5aSH5a6e5L6L"></span>
### Prepare instance

When scaling jobs are being executed via AS, instances are purchased or released automatically. [Prepare the ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances#.5q2l6aqk5LiA77ya5YeG5aSH6LSm5Y-3) to complete the pre\-purchase operations.

<span id=".5YeG5aSH6LWE5rqQ6YWN6aKd"></span>
## Prepare resource quota

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To avoid scaling failure, check whether there is sufficient quota in the Quota Center based on the amount of resources (such as instances and EIPs) you need.</div>
