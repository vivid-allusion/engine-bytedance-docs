---
title: "Instance lifecycle"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-lifecycle"
---

The lifecycle of an ECS instance refers to all the states it goes through from creation (purchase) to deletion (release or termination).

Planning and managing the instance lifecycle ensures that the applications running on the instance can provide services to users in a convenient, efficient, and cost\-effective manner.

The states can be divided into intermediate states and stable states. If an instance remains in an intermediate state for an extended period, this indicates an exception.

<span id=".5a6e5L6L54q25oCB"></span>
### Instance states

During the lifecycle, an instance has certain states, as shown in the table below.


|Status |State attribute |State description |
|---|---|---|
|Creating  |Intermediate status |The state of the instance after you create it and before it enters the **Running** state. |
|In service |Stable status |The state when the instance is running normally. In this state, the instance runs your business. |
|Stopping |Intermediate status |The status of the instance after you stop it in the console or by calling API operation and before the instance enters the **Stopped** state. |
|Stopped |Stable status |After the instance has been stopped, it will be in a **Stopped** state. |
|Migrating |Intermediate status |After you start migrating the instance to a deployment set, the instance status changes to **Migrating**. |
|Starting |Intermediate status |The state of the instance after you start it in the console or by calling API operation and before the instance enters the **Running** state. |
|Restarting |Intermediate status |The state of the instance after you restart it in the console or by calling API operation and before the instance enters the **Running** state. |
|Reinstalling |Intermediate status |The state of the instance after you change the operating system in the console or by calling API operation and before the instance enters the **Running** state. |
|Deleting  |Intermediate status |The state when the instance is being deleted. Once this state ends, the instance will automatically disappear from the console page. |
|Reconfiguring |Intermediate status |The state of the instance after you change the instance type in the console or by calling API operation and before the instance enters the **Running** state. |
|Maintaining |Intermediate status |The state when the instance is being evacuated, and the state remains unchanged after successful evacuation. For the instance under maintenance, you can not perform other actions. |
|Error  |Stable status |The state when the instance is being migrated due to failures. In this state, the instance cannot properly provide business services. Submit a support ticket. |
|Expired |Stable status |A subscription\-based instance enters the retention period due to account arrears or expiration of the instance, and the instance is in the **Expired** state. |


<span id=".5a6e5L6L5Yib5bu6"></span>
### [Instance creation](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances)


* After you initiate an instance creation action, the instance status changes to **Creating**. An ECS instance will be created based on the specified instance type and image.

* Once the instance is created, it changes to the **Running** state and provides users with connection and access services.


<span id=".5a6e5L6L5YGc5q2i"></span>
### [Instance stopping](https://docs.byteplus.com/en/docs/ecs/Stopping-instances)


* For instances, stopping is equivalent to shutdown. An instance that has been stopped no longer provides external services.

* The stop action does not cause the EIP address, private IP address, or volume data of the instance to change.


<span id=".5a6e5L6L6L-B56e7"></span>
### [Instance migration](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview)


* After you initiate an action of migrating the instance to a deployment set, the instance status changes to **Migrating**.

* Once the instance has been migrated to the deployment set, it changes to the "Stopped" state and must be manually started.


<span id=".5a6e5L6L5ZCv5Yqo"></span>
### [Instance start-up](https://docs.byteplus.com/en/docs/ecs/Starting-instances)


* After you initiate an instance start\-up action, the instance status changes to **Starting**.

* You need a few seconds or a few minutes to start an instance, depending on the configuration of the instance.


<span id=".5a6e5L6L6YeN5ZCv"></span>
### [Instance restart](https://docs.byteplus.com/en/docs/ecs/Restarting-instances)


* After you initiate a restart action, the instance status changes to **Restarting**.

* Restarting an instance is equivalent to rebooting the ECS service. The restart action does not cause the EIP address, private IP address, or volume data of the instance to change.

* You need a few seconds or a few minutes to restart an instance, depending on the configuration of the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the instance remains in the <strong>Restarting</strong> state for an extended period, the system will perform a forced restart. A forced restart is equivalent to a power\-off operation and will cause loss of all cached data not saved to storage devices. Therefore, we recommend that before restarting the instance, you should check whether all data is saved to volumes to avoid data loss.   </div>
   

<span id=".5a6e5L6L5pu05o2i57O757uf"></span>
### [Changing operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS)

Please exercise caution as changing the operating system of an instance will result in the loss of data on its system volume.

<span id=".5a6e5L6L5Y-Y5pu06KeE5qC8"></span>
### [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Overview-2)

Please exercise caution as when you change the instance type, the instance will immediately start. Please assess the impact on your business.

<span id=".5a6e5L6L5Yig6Zmk"></span>
### [Deleting instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances)


* Please exercise caution as deleting an instance will result in the loss of data on the data volumes if you have not enabled the option to retain the data volumes.

* An instance can not be restored once it is deleted.


<span id=".5a6e5L6L55aP5pWj"></span>
### Evacuating instance


* When you evacuate an instance, the instance status changes to **Maintaining**, and the status will remain unchanged after successful evacuation. For the instance under maintenance, you can not perform other actions.

* If the instance evacuation fails, the instance status changes to **Error**. Please carefully check the status after evacuation.


<span id=".5a6e5L6L6L-H5pyf"></span>
### [Instance expiration](https://docs.byteplus.com/en/docs/ecs/Expiration)


* If your account has unpaid bills or your subscription\-based instance expires because you do not timely settle the unpaid bills or renew your instance, the resources will enter a retention period, and the instance status will change to Expired. For more information, please refer to [Arrears](https://docs.byteplus.com/en/docs/ecs/Arrears) and [Expiration](https://docs.byteplus.com/en/docs/ecs/Expiration).

* After you timely settle the unpaid bills or renew your expired subscription\-based instance, the instance status automatically changes to Running.
