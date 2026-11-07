---
title: "Node configuration changes"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Node_configuration_changes"
---

When the ECS instance specifications of a node group in a Volcano Engine E\-MapReduce (EMR) cluster do not meet or exceed application requirements, you can change the instance specifications (including vCPU and memory), supporting both upgrades and downgrades.

<span id="_1-使用限制"></span>
## Limits


1. EMR\-2.3.0, EMR\-3.3.0, or later cluster versions must be created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Upgrades and downgrades are supported for both Pay\-As\-You\-Go and Subscription instances.

3. Local and Big Data ECS instances do not support specification changes.

4. Cross\-specification configuration changes are supported. For the machine type configuration change table, refer to [Cloud Service Instance Specification Modification Overview](https://docs.byteplus.com/en/docs/ecs/Overview-2).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">The instance will be shut down during the configuration change process. Shutdown may affect normal cluster operations or even cause business interruption. Please carefully evaluate before making changes!</div>


2. <div data-tips="true" data-tips-type="warning">Do not perform other operations on the instance before the instance specification change operation is completed, as this may cause the change to fail.</div>


3. <div data-tips="true" data-tips-type="warning">After submitting the configuration change, the price will be automatically adjusted. Subscription nodes will automatically process payment or refunds.</div>


4. <div data-tips="true" data-tips-type="warning">Since version 3.8.0, StarRocks cluster FE node groups use rolling configuration changes by default, ensuring at least two FE nodes remain online during the change process and no business interruption occurs.</div>



<span id="_2-操作步骤"></span>
## procedure

<span id="_2-1-新建配置变更"></span>
### Create a new configuration change


1. Log in to the , , or [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?) as appropriate.

2. In the left navigation bar, click **Resource Management \> ECS \> Cluster Name** to enter the specific cluster details page.

3. On the cluster details page, click the **Nodes**tab to enter the node group list page.

4. On the node group list page, click the **Configuration changes**button in the operation column of the target node group to open the configuration change dialog box. In the **Change Configuration**window, you can filter the machine types that support changes for the current node group based on instance specification name, vCPU, and memory size, and select the machine types to change according to your requirements.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Refer to the console for supported upgradeable instance specifications.   </div>
   

5. Select **I agree to the E\-MapReduce Service Terms** and click the **Confirm** button to submit.

6. Select **I acknowledge the above information** and click the **Confirm** button to execute. Wait for the ECS instance in the node to start, after which the configuration change takes effect.


<span id="_2-2-配置变更重试"></span>
### Retry configuration change

Due to ECS inventory issues, node group configuration changes may not be delivered with all expected specifications. Undelivered nodes will continue to run with their original specifications, and business is not affected. There may be specification heterogeneity within the node group. It is recommended to retry the configuration change to ensure all nodes are changed to a unified specification.


1. On the **Cluster Details** page, click the **Node Management** tab to enter the node group list page.

2. On the node group list page, click **Retry Configuration Change** in the operation column of the target node group.

3. In the **configuration change retry** dialog box, click the **one\-click retry** button to retry and wait for the change to complete.
