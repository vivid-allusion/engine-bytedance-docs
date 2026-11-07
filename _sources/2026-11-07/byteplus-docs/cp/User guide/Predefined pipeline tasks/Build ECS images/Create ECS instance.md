---
title: "Create ECS instance"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_ECS_instance"
---

Support adding a built\-in task for creating ECS instances in the pipeline. This article describes how to configure the built\-in task for creating ECS instances.

<span id="xVWyui6K"></span>
## Prerequisites


* Created VPC, for details refer to [Create VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Created subnet, for details refer to [Create subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* Created security group, for details refer to [Create security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).


<span id="VigSts9D"></span>
## Considerations

Some configuration items not shown in the built\-in task use the following default configuration and cannot be modified.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For detailed explanations of configuration items, refer to the official documentation for <a href="https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances">ECS instance</a> and <a href="https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP">Elastic IP Address</a>.</div>



|Product |Parameter |Description |
|---|---|---|
|ECS |Billing method |Pay\-as\-you\-go Billing |
||Whether to install cloud assistant |Yes |
||Data volume capacity |200 GiB |
|Elastic IP Address |Billing method |Pay\-as\-you\-go Billing |
||Thread type |BGP (multi\-line) |
||Bandwidth limit |50 Mbps |
||Release settings |Release with instance |


<span id="zdwlmNs5"></span>
## Add task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select **Others \> ECS instance creation** as the task template.

<span id="ck4ggJ0V"></span>
## Parameter description

The following describes the parameters for this built\-in task.


* **Task name**

   Custom task name.

* **Upstream task**

   Show the name of the upstream serial task for the current task. If there is no upstream task, `-` is displayed.

* **Task configuration**

   
   |Parameter |Description |
   |---|---|
   |Region |Select the region for creating the ECS instance. |
   |Availability zone |Choose the availability zone for ECS instance creation. |
   |Instance Name |Custom instance name. |
   |Instance specification |Select the instance type. |
   |ECS image |Select the image for creating the instance. Currently supports **Public images**, **Custom images ** , and **Shared images **  types. For details, refer to [Image overview](https://docs.byteplus.com/en/docs/ecs/Image-overview). |
   |Private network |Select the created VPC. |
   |Subnet |Select the created subnet. |
   |Security group |Select the created security group. |
   |Enable public network access |Select whether to enable public network access rights for the instance. After enabling, an EIP will be automatically created and associated with the created ECS instance. |
   

* **Task output**

   Show the ID of the ECS instance to be created.

* **Advanced settings**

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Support pushing task\-level messages via Webhook and Larkbot, helping you stay informed about task status in a timely manner.
