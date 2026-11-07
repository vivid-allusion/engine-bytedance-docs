---
title: "Changing instance to the Disabled status"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Change_the_instance_to_the_Disable_status"
---

<span id="VoQAjO8n"></span>
## Scenario

You can manually change an instance to Disabled status so that only part of its resources are retained, which helps reduce costs.

<span id="LzltVn6c"></span>
## Prerequisites

Before disabling the instance, confirm the following items:


|**Project** |**Prerequisites** |
|---|---|
|Instance |The instance must be in the **Active** state and must have been automatically scaled out and managed by the scaling group. |
|Scaling group |The scaling group must be in **Active** or **CoolingDown** state, and the scaling mode configuration should be "shutdown reclaim mode". |


<span id="41lnBRla"></span>
## Usage notes


* After switching the instance to Disabled status, it will not be counted towards the desired number of instances but will be included in the maximum number of instances. When the maximum number of instances in the scaling group is smaller than the total number of instances in all states (including those in the process of being disabled), the scaling group will prioritize the reclaim of instances being disabled.

* Manually starting instances in the "Disabling" status is not supported. During subsequent automatic scaling up of the scaling group, instances in "Disabling" status will be prioritized for enabling.


<span id="41lnBRla"></span>
## Procedure


1. Log in to the [Scaling Group console](https://console.byteplus.com/as/group). 

2. In the top menu bar, select the project and region of your target resource.

3. Click the name of the scaling group and select the "Instance Management" tab.

4. Select one or more instances to be removed and click the "Disable" button.

5. Click the "OK" button to complete the operation.


<span id="INQ23ZDP"></span>
## Resource reclaim policy after disabling

When an instance is disabled, its computing resources (vCPU, GPU, and memory) will be reclaimed and removed from the Classic Load Balancer instance, but the Volume, image, Elastic IP (EIP), bandwidth (fixed bandwidth mode), and RDS database will still be retained. For a detailed introduction of Economical Mode, please refer to [instance stop modes](https://docs.byteplus.com/en/docs/ecs/Stopping-instances#.5YGc5q2i5qih5byP).
