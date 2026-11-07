---
title: "Change the PFS instance of a prepaid resource group"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Change_the_PFS_instance_of_a_prepaid_resource_group"
---

If you need to replace or unbind a PFS instance after creating a prepaid resource group, you can use this function to complete the resource group PFS instance change.

<span id="概念介绍"></span>
## Concept introduction


|concept |explain |Discription |
|---|---|---|
|PFS mount service |* When you add the first PFS instance to the Machine Learning Platform, the platform creates a mount service for the user and binds the PFS instance to that mount service.<br><br>* When you want to add a second PFS instance, if the VPC associated with the selected PFS instance is the same as the VPC of the created mount service, please directly click the operation item [Bind PFS Instance] of the PFS mount service to complete.<br><br>* If the second PFS instance you want to add is inconsistent with the VPC of the currently created mount service, click [Add Authorization] and select the PFS instance that needs authorization. At this point, the platform will create a second mount service for you.<br><br>* If you want to replace a PFS instance, first authorize the new PFS instance that needs to be mounted, and then unbind the old instance that is no longer in use. When the last PFS instance is unloaded, the platform automatically removes the PFS mount service. |* The platform currently supports creating a mount service by default. If you need to create multiple mount services, please contact BytePlus oncall to apply for clarification.<br><br>* Each mount service can bind up to two PFS instances. |


<span id="场景-1：更换相同挂载服务的-vepfs-实例"></span>
## Scenario 1: Replacing a PFS instance of the same mount service

<span id="使用场景"></span>
### Usage scenarios

If you want to replace the resource group bound PFS instance, that is, switch from PFS instance 1 to PFS instance 2, you can do it through the [Change PFS instance] operation.

<span id="前置条件"></span>
### precondition


1. The resource group is running

2. Permissions to operate resource groups and global configurations


<span id="操作步骤"></span>
### Procedure


|operation |Demo |Discription |
|---|---|---|
|1. Log in to the Machine Learning Platform and select Global Configuration \- PFS in the left navigation bar. |*  | |
|2. If you have authorized the PFS instance on the platform, please click [Bind PFS Instance] on the bound PFS mount service to enter the operation page, select the PFS instance with the same VPC as the current mount service, and click Confirm Submit. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/313d27ccaa964ca0b39de6a1daa0bdad~tplv-goo7wpa0wc-image.image) </span> | |
|3. In the left navigation bar, select Resource Group \- Resource Group Instance. |*  | |
|4. Select the resource group that needs to change the PFS instance, click the [Change PFS Instance] operation, and enter the operation page.<br><br>   1. Please check the PFS instance you want to use first<br><br>   2. Cancel a bound PFS instance<br><br>   3. Submit Form | |Please note that the VPC network of the selectable PFS instance needs to be consistent with the already bound VPC, otherwise the binding cannot be successful. If you need to change your storage network, please contact BytePlus oncall. |
|5. PFS instances that are no longer used in the global configuration [Unauthorization] |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb85692df7d04486b4386a1e28d5d82d~tplv-goo7wpa0wc-image.image) </span> |After canceling the authorization, the existing load tasks that are using PFS cannot access the instance. Please inform the users in the group before unbinding and do a good job of task migration. |


<span id="场景-2：取消授权-vepfs-实例"></span>
## Scenario 2: Unauthorizing the PFS instance

<span id="使用场景"></span>
### Usage scenarios

If you want to unbind a PFS instance that is already bound in the global configuration (including replacing the PFS mount service), you can refer to the following operations.

<span id="前置条件"></span>
### precondition


1. The resource group is running

2. Permissions to operate resource groups and global configurations


<span id="操作步骤"></span>
### Procedure


|operation |Demo |Discription |
|---|---|---|
|1. Log in to the Machine Learning Platform. |*  | |
|2. In the left navigation bar, select Resource Group \- Resource Group Instance. |*  | |
|2. Select the resource group that needs to unbind the PFS instance, click the [Change PFS Instance] operation, and enter the operation page.<br><br>   1. Delete the PFS instance and turn off the PFS function |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e11be04ccd64cbdb66c3a507cdf88c8~tplv-goo7wpa0wc-image.image) </span> | |
|3. The PFS instance that is no longer used in the global configuration [Unauthorization]. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eda16e2dd8d4594898c834525a28538~tplv-goo7wpa0wc-image.image) </span> |After canceling the authorization, the existing load tasks that are using PFS cannot access the instance. Please inform the users in the group before unbinding and do a good job of task migration. |
