---
title: "Instance lifecycle"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Instance-lifecycle"
---

An instance in a scaling group is equivalent to an actual running cloud resource, that is, an ECS instance.

<span id=".5a6e5L6L5p2l5rqQ"></span>
## Instance sources

Depending on the sources of instances in a scaling group, instances are categorized as either "automatically created instances" or "manually added instances". The lifecycle management methods for different types of instances in a scaling group vary.


* Automatically created instances: instances that are automatically created based on the scaling configuration source when a scaling group is scaled out. Only pay\-as\-you\-go and spot instances are supported.

* Manually added instances: instances that are manually created in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance) and added to a scaling group. Pay\-as\-you\-go instances, subscription and spot instances are supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Currently, a scaling group cannot manage Elastic Bare Metal (EBM), GPU, and HPC\-optimized instances.</div>


* <div data-tips="true" data-tips-type="tip">The spot instance feature is currently in Beta. To request a trial, contact your account manager For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Spot_Instance">Spot instances</a>.</div>



<span id=".5a6e5L6L55Sf5ZG95ZGo5pyf566h55CG"></span>
## Instance lifecycle management

You can mark instances in a scaling group with the following attributes: "Managed by scaling group or not", "Instance protection enabled or not", and "Standby status enabled or not". These designations determine whether the scaling group manages the lifecycle of the instances.


* Mark as **Managed by scaling group**: When the scaling group scales in, the instances will be automatically deleted, along with associated resources, such as EIPs, volumes, and network interfaces. The instances will be removed from the associated load balancer and RDS databases.

* Mark as **Not managed by scaling group**: When the scaling group scales in, the instances will be automatically removed, while the instances themselves, their associated resources, and resource association status will be retained.

* Mark as **Instance protection**/**Standby status** enabled: The instances will not be affected by the automatic scale\-in and health check capabilities of the scaling group. You manually manage the lifecycle of the instances.


The following table describes the default lifecycle management status (whether instances are managed by the scaling group) and the default instance protection status for instances of different sources.


|Instance source |Managed status |Instance protection/Standby status |
|---|---|---|
|Automatically created instances |By default, the lifecycle of the instances is managed by the scaling group and you cannot change the lifecycle management status of the instances. |By default, the feature is disabled. You can enable the instance protection/standby feature at any time. |
|Manually added instances |Pay\-as\-you\-go instances (including spot instances): When an instance is added, the lifecycle of the instance is not managed by the scaling group by default. You can choose whether to enable the scaling group to manage the lifecycle of the instance based on your needs. If you enable the scaling group to manage the lifecycle of the instance, you cannot change the lifecycle management status of the instance. ||
||Subscription instances: By default, the lifecycle of the instances is not managed by the scaling group and you cannot enable the scaling group to manage the lifecycle of the instances. ||


<span id=".5a6e5L6L54q25oCB"></span>
## Instance state

The instance state here refers to the state of an instance within the scaling group, as shown in the following table. All states an instance undergoes from creation (purchase) to deletion (release and destruction) can be viewed in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance). For more information, see [Instance lifecycle overview](https://docs.byteplus.com/en/docs/ecs/Instance-lifecycle).


|State |State description |
|---|---|
|Initialization |The state of an instance before it is successfully created when provisioned automatically by a scaling group. |
|Adding |The instance is being added to the scaling group. |
|Pending addition |For a scaling group with lifecycle hooks configured for elastic scaling\-out activities, this is the state of an instance when it is suspended after being automatically provisioned. During the suspension, you can perform custom operations such as preinstalling software on the instance. |
|In service |The state of an instance when the instance runs as expected in the scaling group. |
|Removing |After an instance is manually or automatically removed or deleted from the scaling group, it enters the **Removing** state. |
|Pending removal |For a scaling group with lifecycle hooks configured for elastic scaling\-in activities, this is the state of an instance when it is suspended during the process of being automatically removed or deleted. When the instance is suspended, you can perform custom operations, such as downloading logs or backing up data, for the instance. |
|Disabled |After the instance has been disabled, it will be in the **Disabled** status. |
|Under protection |After instance protection is enabled for an instance, the instance will be in the **Under protection** state. |
|Standby |After instance protection is enabled for an instance, the instance will be in the **Standby** state. |
|Error |The state of an instance when it becomes abnormal due to certain reasons. |


<span id=".5a6e5L6L55u45YWz5pON5L2c"></span>
## Instance\-related operations

In the Auto Scaling console, only operations related to associating instances with a scaling group are supported. These operations include adding instances to a scaling group, enabling protection for instances, setting instances as standby, removing instances from a scaling group, and deleting instances. For regular operations such as modifying instance attributes and associating volumes/EIPs, there is no difference from instances created in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance). You can perform and manage these operations in the ECS console. For more information, see [ECS product documentation](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service).

<span id="dVeMdhL4"></span>
## Actions on instances in the ECS console affect the instances.


|Actions in the ECS console. |Impact on the scaling group. |
|---|---|
|Stop "In Service" instances in the scaling group |Regardless of whether the instances are managed by the scaling group, the scaling group removes the relevant instances from the scaling group (without triggering the lifecycle hook), retains the EIP, and then automatically scales out based on the scaling group's configuration policy. |
|Start the "Disabled" instance in the scaling group. |The scaling group synchronizes the startup status of the relevant instances but does not change the expected instance count. Automatic scale\-in occurs after the next health check. |
|Delete "In Service"/"Disabled" instances in the scaling group. |The scaling group removes the relevant instances from the scaling group and then automatically scales out based on the scaling group's configuration policy. |


&nbsp;
