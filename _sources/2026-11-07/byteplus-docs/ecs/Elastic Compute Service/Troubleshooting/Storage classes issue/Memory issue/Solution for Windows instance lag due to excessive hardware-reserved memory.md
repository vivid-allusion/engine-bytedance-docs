---
title: "Solution for Windows instance lag due to excessive hardware-reserved memory"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_Windows_instance_sluggishness_due_to_excessive_hardware_reserved_memory"
---

This topic describes how to resolve issues of instance lag and slow system response caused by excessive hardware\-reserved memory on Windows instances.

> You can [log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Overview-1) and then view the hardware\-reserved memory by selecting "Task Manager \> Performance \> Memory".


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The copyright of the official Microsoft links cited in this topic belongs to Microsoft. The BytePlus platform assumes no responsibility for the scope of operating systems applicable to this topic, or issues that may arise from Microsoft Windows product iterations or delayed document updates.</div>


* <div data-tips="true" data-tips-type="tip">This topic may contain information about third\-party products. Related information is provided for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.</div>



<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

Due to abnormalities such as incorrect configurations of the license in the Windows Registry, and abnormal changes to instance specifications (sudden increase or decrease in memory size), an instance may not be activated normally. This causes a large amount of memory to be locked or reserved (excessive hardware\-reserved memory), thereby causing high memory load and slow system response or even lag.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

We recommend [creating a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) first to back up instance data. This improves your fault tolerance and ensures data security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Fix this issue by resetting the activation status of Key Management Service (KMS).


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

2. Open the Command Prompt (cmd) with an administrator account.

3. Clear the activation information of KMS.

   1. Clear the server address.

      1. Execute the following command to clear the server address.

         ```Plain Text
         slmgr.vbs /ckms
         ```
         

      2. Click the "Confirm" button.

   2. Detach service key.

      1. Execute the following command to detach the service key.

         ```Plain Text
         slmgr.vbs -upk
         ```
         

      2. Click the "Confirm" button.

   3. Reset the authorization status of the computer.

      1. Execute the following command to reset the authorization status of the computer.

         ```Plain Text
         slmgr.vbs -rearm
         
         ```
         

      2. Click the "Confirm" button.

   4. Restart the Windows instance to make the changes take effect. For detailed operations, refer to[ Restarting instances](https://docs.byteplus.com/en/docs/ecs/Restarting-instances).

4. Reactivate the KMS service.

   1. Query the KMS key corresponding to the operating system version of the instance. About [KMS keys](https://docs.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys?spm=a2c9r.14518950.0.0.143d772bVTGsXX).

   2. Execute the following commands to reactivate KMS.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Make sure that a legitimate KMS server address is used. Using unauthorized or untrusted KMS server addresses may cause activation failure, system instability, or even legal risks.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">For individual users, since personal editions of Windows are typically activated via legitimate methods, such as purchasing genuine keys, we generally do not recommend that they use KMS activation.      </div>
      

      ```Plain Text
      slmgr.vbs /ipk your_kms_key
      slmgr -skms cloudkms.ivolces.com
      slmgr.vbs /ato
      ```
      

      * Replace "your_kms_key" with the actual KMS key.

      * Replace "cloudkms.ivolces.com" with the actual address of your KMS server on the BytePlus platform.

   3. Wait for the system prompt indicating successful product activation, and then [restart the instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances) to complete the system update.
