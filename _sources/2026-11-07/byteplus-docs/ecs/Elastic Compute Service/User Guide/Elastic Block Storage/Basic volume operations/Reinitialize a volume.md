---
title: "Reinitialize a volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Reinitialize-volume"
---

When the volume is corrupted or a serious error occurs, you may need to restore the volume to its original state. EBS supports a reinitialization feature that allows you to restore the volume to the state it was created in. This article provides background information, prerequisites, cautions, and operational steps for reinitializing a volume.

<span id="background-information"></span>
## Background Information

After reinitializing the volume, the volume ID remains unchanged. Description as follows: Different creation methods of volumes result in different initial states after reinitialization, as detailed below:


* For volumes created from a snapshot: After reinitialization, it will revert to the snapshot state at the time of volume creation.

* For volumes not created from a snapshot: After reinitialization, all data in the volume will be erased.


It is recommended that you create a snapshot before reinitializing the volume to back up the volume data.

<span id="prerequisites"></span>
## Prerequisites

Before using the reinitialization function, make sure that the volume is mounted to the ECS instance and that the ECS instance is in the "stopped" state. For details, see [Stop instances](https://docs.byteplus.com/en/docs/ecs/Stopping-instances).

<span id="precautions"></span>
## Precautions


|**Category** |**Precautions** |
|---|---|
|Volume Type |Only data volumes support the reinitialization feature. |
|Snapshots |* For a volume created from a snapshot, if the snapshot is deleted, the volume will not support reinitialization.<br><br>* The volume where the snapshot is being created does not support reinitialization. |
|Automatic mounting at startup |If you have configured your system to automatically mount volumes at boot in the /etc/fstab file, and the volume is not created from a snapshot, automatic mounting will fail after reinitializing the volume, and you may encounter issues with ECS instance start\-up and usage. Therefore, you need to comment out the command for automatically mounting volumes at boot before reinitializing the volume. |
|Prohibited actions |If your volume is reinitializing, the following actions are not supported:<br><br><br>* All write operations of the volume<br><br>* Create custom images<br><br>* Boot ECS instance<br><br>* Restart the ECS instance<br><br>* Replace the operating system of the ECS instance |


<span id="operation-steps"></span>
## Operation Steps


1. Log in to the [ECS console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. In the left\-side navigation pane, click **Volumes**.

3. In the top menu bar, choose the project and the Region of the target volume.

4. On the **Volumes** page, click  **... \> Reinitialize** under the **Actions** column of the target volume.

5. In the pop\-up dialog box, after confirming the information is correct, select the **After I confirm that the Data Volume is reinitialized, the selected Volume will be restored to its original state when it was created** option, and click **Reinitialize Volume**.


<span id="subsequent-steps"></span>
## **Subsequent Steps**


* If the volume mounted on the ECS instance is a Linux operating system and the volume was not created from a snapshot, you will need to perform partition formatting operations on the volume after reinitialization to use it in the ECS instance. For details, see [Partition and format volumes](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume).

* If the volume is created from a snapshot, or if the mounted ECS instance runs a Windows operating system, there is no need to perform additional operations after reinitializing the volume to use it within the ECS instance.
