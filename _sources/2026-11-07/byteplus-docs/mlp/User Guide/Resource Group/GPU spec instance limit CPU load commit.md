---
title: "GPU spec instance limit CPU load commit"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/GPU_spec_instance_limit_CPU_load_commit"
---

<span id="使用前提"></span>
# Premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">There is an instance specification for the GPU model in the current resource group and the resource group status is <strong>running</strong> .</div>


2. <div data-tips="true" data-tips-type="tip">The flexible matching function is not enabled.</div>



<span id="操作步骤"></span>
# Procedure

When you have purchased an instance specification for any GPU model in a resource group, on the Resource Group Details \- Instance Specifications page, select Configure **GPU Specification instances to support scheduling pure CPU load** .

<span id="开启配置"></span>
## Enable configuration

When the configuration is turned on, the newly committed CPU load will support scheduling to the GPU spec instance, but the CPU load that was already **in the queue** before the configuration is turned on may still only be scheduled to the CPU spec instance, at which point you can choose to stop and resubmit.

> Running CPU loads on GPU spec instances is likely to cause GPU spec node fragmentation. If subsequent GPU load submissions are queued due to insufficient CPU resources, you can confirm and fragment them in "Node Load Details".


<span id="关闭配置"></span>
## Close configuration

After shutdown, deployed and running loads are not affected. The newly committed CPU load will not support scheduling to the GPU spec instance. CPU loads that were already **in the queue** before the configuration change may still be scheduled to the GPU spec instance. You can choose to stop and resubmit.

> After closing the configuration, if the current resource group is a mixed resource group of GPU instance specifications and CPU instance specifications, there may be CPU quotas in the queue at this time, but the CPU load is always **in the queue** state, because the GPU specification instance does not support submitting CPU load and at this time CPU specification instance resources have no remaining available quotas.


<span id="对存量负载影响说明"></span>
## Description of impact on inventory load

After the configuration is turned on or off, the impact on the stock load update operation is described as follows:


|stock load type |update operation |use configuration |
|---|---|---|
|Dev boxes |power on |Use creation\-time configuration |
| |shutdown |Use creation\-time configuration |
| |restart |Use creation\-time configuration |
|inference services |Editing Services/Deployment |Use creation\-time configuration |
| |update service |Use creation\-time configuration |
| |update deployment |Use the latest configuration |
| |Stop/start service/deployment |Use the latest configuration |
| |expansion |Use creation\-time configuration |
| |migration |Use creation\-time configuration |
| |Rollback |Use creation\-time configuration |
