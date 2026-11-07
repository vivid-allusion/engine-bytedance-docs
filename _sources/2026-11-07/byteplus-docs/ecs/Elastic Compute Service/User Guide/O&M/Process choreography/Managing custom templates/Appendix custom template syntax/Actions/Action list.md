---
title: "Action list"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Action_list"
---

An action defines a specific operation and serves as the smallest operational unit. Each task specifies the particular action it will execute. Actions are defined and implemented by Orchestration, encompassing both atomic actions and cloud product actions.


* Atomic action: Refers to the smallest indivisible unit of action. For example, sending an HTTP request is an atomic action.

* Cloud product action: Refers to an action associated with a specific cloud service. For example, restarting instances in a batch is a cloud product action.



|**Action category** |**Action subcategory** |**Action name** |**Description** |
|---|---|---|---|
|Atomic action |API<br><br> |[VOS::ExecuteAPI](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#MmMl4rtc) |Call OpenAPI. |
|||[VOS::WaitFor](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#SyEiVueH) |Call OpenAPI to query a resource to check if it is in the expected status. |
|||[VOS::CheckFor](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#ox3Kxhaq) |Call OpenAPI to check the status of a resource. |
||Trigger |[VOS::PeriodicTrigger](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#gB60hwCL) |Time\-related trigger rules. Valid values:<br><br><br>* Fixed: trigger at a specific time point.<br><br>* Rate: trigger periodically. |
||Control<br><br> |[VOS::Choice](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#r3j6s3sl) |Select actions to be performed based on conditions. |
|||[VOS::SelectTargetInstances](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#vhvB5JWA) |Select resources to execute based on conditions. |
||Function execution |[VOS::InvokeInnerFunction](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#jFz0OeRt) |Execute built\-in functions. |
||Nesting |[VOS::InvokeTemplate](https://docs.byteplus.com/en/docs/ecs/Atomic_actions#s3lY77bY) |Execute other templates in a nested manner. |
|[Cloud product action](https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps) |ECS<br><br> |VOS::ECS::BulkyDeleteInstance |Delete multiple ECS instances at one time. |
|||VOS::ECS::BulkyModifyInstanceChargeType |Change the billing method of multiple instances from pay\-as\-you\-go to subscription at one time. |
|||VOS::ECS::BulkyModifyInstanceSpec |Change the types of multiple instances at one time. |
|||VOS::ECS::BulkyRebootInstances |Restart multiple instances at one time. |
|||VOS::ECS::BulkyReplaceOS |Change the operating system for multiple instances at one time. |
|||VOS::ECS::BulkyStartInstances |Start multiple instances at one time. |
|||VOS::ECS::BulkyStopInstances |Stop multiple instances at one time. |
|||VOS::ECS::CopyImage |Copy an image to the specified region. |
|||VOS::ECS::CopyImageToOtherReion |Copy a custom image across regions. |
|||VOS::ECS::CreateAndCopyImage |Create a custom image and distribute it. |
|||VOS::ECS::CreateImage |Create a custom image based on an ECS instance. |
|||VOS::ECS::CreateImageByInsatnce |Create a custom image based on an existing instance. |
|||VOS::ECS::CreateSnapshot |Create a snapshot. |
|||VOS::ECS::DownloadFile |Download files in an ECS instance. |
|||VOS::ECS::ExtendVolume |Scale up volumes. |
|||VOS::ECS::InvokeRunCommand |Deliver commands to an instance for execution. |
|||VOS::ECS::ModifyImageSharePermission |Share an image. |
|||VOS::ECS::ModifyInstanceAttribute |Modify the attributes of an ECS instance. |
|||VOS::ECS::ModifyInstanceChargeType |Change the billing method of an instance from pay\-as\-you\-go to subscription. |
|||VOS::ECS::ModifyInstanceSpec |Change the instance type. |
|||VOS::ECS::RebootInstance |Restart an ECS instance. |
|||VOS::ECS::RebootOneInstance |Restart the instance. |
|||VOS::ECS::ReplaceOS |Change the operating system. |
|||VOS::ECS::ReplaceSystemVolume |Change the operating system of an ECS instance. |
|||VOS::ECS::RunCommand |Execute commands on ECS instances. |
|||VOS::ECS::RunInstances |Create an instance. |
|||VOS::ECS::StartInstance |Start an ECS instance. |
|||VOS::ECS::StartOneInstance |Start an instance. |
|||VOS::ECS::StopInstance |Stop an ECS instance. |
|||VOS::ECS::StopOneInstance |Stop an instance. |
|||VSO::ECS::RunSameInstances |Create an instance with the same configuration as an existing instance. |
||VPC |VOS::VPC::AllocateEipAddress |Create an available EIP. |
|||VOS::VPC::AssociateEipAddress |Associate an EIP. |
|||VOS::VPC::BulkyAllocateEipAddress |Apply for multiple EIPs at one time. |
|||VOS::VPC::BulkyDisassociateEipAddress |Disassociate multiple EIPs at one time. |
|||VOS::VPC::BulkyModifyEipAddressAttributes |Modify the bandwidth for multiple EIPs at one time. |
|||VOS::VPC::BulkyReleaseEipAddress |Release multiple EIPs at one time. |
|||VOS::VPC::DisassociateEipAddress |Disassociate an EIP. |
|||VOS::VPC::ModifyEipAddressAttributes |Modify the EIP bandwidth. |
|||VOS::VPC::ReleaseEipAddress |Release an EIP. |
||AS |VOS::AS::UpdateLaunchTemplate |Update the image of a launch template. |
