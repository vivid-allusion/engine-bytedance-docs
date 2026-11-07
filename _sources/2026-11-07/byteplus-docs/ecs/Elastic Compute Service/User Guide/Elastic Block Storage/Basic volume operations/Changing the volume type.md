---
title: "Changing the volume type"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modify-volume-type"
---

You can change the type of your volume if your business needs change to get the performance you need. This topic explains how to change the volume type.

<span id=".5Y-Y6YWN6K-05piO"></span>
## Before you begin


* EBS only allows you to change the following types of volumes: ESSD PL0, ESSD PL1, and ultral disk. For more information about volume types, see [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).

* Different volume types have different performance limits. Changing the volume type may affect your business. Make sure you understand the different types before changing to ensure they meet your requirements. We recommend changing the volume type during off\-peak hours.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


|Category |Description |
|---|---|
|Restrictions before change |* You can only change a volume's type when it is in the "Attached" or "Available" status.<br><br>* The corresponding ECS instance cannot expire and the account cannot be in arrears if the volume is in "Attached" status. Otherwise, it is not possible to change the volume's type. |
|Restrictions during change |You cannot perform the following operations when a volume is in the "Modifying" status:<br><br><br>* Extending, attaching, detaching, deleting, modifying, canceling, migrating, or rolling back a volume<br><br>* Changing the billing method from pay\-as\-you\-go to subscription<br><br>* Partitioning and formatting a volume<br><br>* Creating a snapshot<br><br>* Changing the operating system for the ECS instance, or resetting the system volume |
|Restricted operations |Once a volume type change is triggered, it cannot be canceled. |
|Billing |The billing rules for the volume will change once you have modified its type. For more information, see [Billing rules for resource changes](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change). |
|Backup |We recommend creating a snapshot to back up your data before changing a volume's type. For more information, see [Creating snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page:

   * To change the type of a single volume:

      1. Click "... \> Modify volume type" in the "Actions" column of the volume.

      2. On the "Modify volume type" page, select a "New volume type" and click "Modify volume type".

   * To change the type of volumes in batches:

      1. Select the desired volumes and click "... \> Modify volume type" at the bottom of the page.

      2. On the "Modify volume type" page, select a "New volume type" for each volume and click "Modify volume type".

   You can verify the volume type on the "Volumes" page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Changing the type will not affect the provisioned capacity or ID of your volume.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can change the type of up to 50 volumes at once.   </div>
