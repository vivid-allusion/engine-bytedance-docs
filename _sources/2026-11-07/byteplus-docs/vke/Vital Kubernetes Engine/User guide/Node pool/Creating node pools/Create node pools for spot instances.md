---
title: "Create node pools for spot instances"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Preemptible_instance_node_pool"
---

This topic describes the capabilities and policies of spot instance node pools in Vital Kubernetes Engine (VKE).

<span id=".5oqi5Y2g5byP5a6e5L6L5LuL57uN"></span>
## Brief introduction

Spot instances are a type of instance offered by BytePlus Cloud Service (ECS) under a postpaid model. The Elastic Compute Service instances purchased under this model are available at a significant discount compared to **pay\-as\-you\-go**, with performance equivalent to standard ECS instances. However, when inventory is insufficient, the system will automatically release the resources of these instances. We recommend that you back up your data in advance. For details, see [Spot instances](https://docs.byteplus.com/en/docs/ecs/Spot_Instance).

VKE allows you to select spot instances as the billing model in both normal node pools and managed node pools.

<span id=".5Yib5bu65oqi5Y2g5byP5a6e5L6L6IqC54K55rGg"></span>
## Create spot instance node pools

When [creating a normal node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) or [creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool), configure the following parameters as described. Configure the remaining parameters as needed.


|Parameter |Description |
|---|---|
|**Node pool settings** ||
|Billing method |Select **Spot instance**. |
|**Advanced settings** ||
|Spot instance compensation |You can choose whether to enable this feature. If enabled, see the **Configure node pools for spot instances** section below for details on the policy. |
|Supplement preemptive capacity by pay\-as\-you\-go instances ||
|Node distribution ratio policy ||


<span id=".5oqi5Y2g5byP5a6e5L6L6KGl5YG_"></span>
## Configure node pools for spot instances

<span id="JdE0RWpA"></span>
### Spot instance compensation

Spot instance compensation supplements resources before spot instances expire and are reclaimed:


* **Enable**: The system proactively creates new instances for replacement about 5 minutes before spot instances are reclaimed. As a result, the number of nodes in the node pool may temporarily exceed the expected number. Additionally, when spot nodes are about to be reclaimed in 5 minutes, the system will cordon and drain the old nodes, and then take them offline and remove them. By doing that, the interruption caused by instance reclaim can be avoided.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Updating this configuration for an existing spot instance node pool does not affect the lifecycle of existing nodes in the node pool. The update only affects subsequent instance supplementation policies.    </div>
   

* **Disable**: will create new spot instances when spot instances are reclaimed upon expiration.


This capability is particularly useful for node pools that use subnets across multiple availability zones. Reclamation of a spot instance usually indicates insufficient inventory of the relevant instance type in the availability zone where the instance resides. In that case, a node pool working on a **subnet that spans multiple availability zones** and has this feature enabled can obtain replacements from other availability zones before spot instances are reclaimed.

<span id=".5oyJ6YeP5a6e5L6L6KGl5YWF5oqi5Y2g5byP5a656YeP"></span>
### Supplement spot capacity with pay\-as\-you\-go instances

This feature is to use pay\-as\-you\-go ECS instances as replacements when spot instances are not available.


* **Enable**: When spot instances are unavailable due to insufficient inventory or other reasons, pay\-as\-you\-go instances are used as supplements in scenarios such as manual scale\-out, Cluster Autoscaler, and compensation for spot instance reclamation. Supplemental pay\-as\-you\-go instances are not replaced even if spot instances become available again. These pay\-as\-you\-go instances are released first only during node scale\-in. 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you enable this feature, ensure the selected node specification supports both the <strong>Pay\-as\-you\-go</strong> and <strong>Spot instance</strong> billing models.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If both the <strong>Node distribution ratio policy</strong> and <strong>Supplement preemptive capacity by pay\-as\-you\-go instances</strong> are enabled in the current node pool, the percentage of pay\-as\-you\-go instances in the node pool may exceed the configured value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Updating this configuration for an existing spot instance node pool does not affect the lifecycle of existing nodes in the node pool. The update only affects subsequent instance supplementation policies.    </div>
   

* **Disable**: will not use pay\-as\-you\-go instances as replacements. Other policies you have set will apply.


<span id=".6IqC54K55YiG5biD5q-U5L6L562W55Wl"></span>
### Node distribution ratio policy

If enabled, you can configure the percentage of pay\-as\-you\-go and spot instances for the node pool. The configurable parameters are as follows:


|Parameter |Description |
|---|---|
|Baseline capacity of pay\-as\-you\-go instances |The minimum number of pay\-as\-you\-go instances required in the current node pool. When the actual count falls below this value, pay\-as\-you\-go instances will be the first option to be created.<br><br><br>* Default value: 0.<br><br>* Value range: It varies depending on whether the **Autoscaling** feature is enabled for your node pool. However, the maximum value cannot exceed 500. Details are as follows:<br><br>   * If **Autoscaling** is disabled, the value ranges from 0 to the expected number of nodes in the node pool.<br><br>      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2d5b89401f9a9313a278865b0d654d0.png) </span><br><br>   * If **Autoscaling** is enabled, the value ranges from 0 to the minimum number of nodes configured for autoscaling.<br><br>      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bdc96ad9cf0bd036d44a699196772203.png) </span> |
|Ratio of pay\-as\-you\-go instances |Percentage of pay\-as\-you\-go instances in the node pool. The sum of percentages of pay\-as\-you\-go and preemptible instances is 100%. The result calculated based on the percentage you set will be rounded up to the nearest integer before it is applied.<br><br><br>* Value range: 0–100.<br><br>* Unit: %. |


After you enable **Node distribution ratio policy** and finish the configuration of the related parameters, the system will calculate based on the number of pay\-as\-you\-go instances and the non\-expired spot instances in the node pool, and then apply the following policies to perform resource compensation when the spot instances are about to be reclaimed:


1. Create supplementary pay\-as\-you\-go instances if the current number of pay\-as\-you\-go instances does not meet the requirement of **Baseline capacity of pay\-as\-you\-go instances**.

2. If the **Baseline capacity of pay\-as\-you\-go instances** is met, the system then checks whether the **ratio of pay\-as\-you\-go instances** is met. If the ratio is not met, **pay\-as\-you\-go instances** are created as supplements. If the ratio is met, spot instances are created as supplements.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Updating this configuration for an existing spot instance node pool does not affect the lifecycle of existing nodes in the node pool. The update only affects subsequent instance supplementation policies. </div>
