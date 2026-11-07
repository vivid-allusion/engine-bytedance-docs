---
title: "Copying snapshots"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Copy_Snapshot"
---

EBS lets you create a copy of a snapshot in a different region, which makes backing up your data across regions easier. In the event of data loss or failure, you can use the snapshot copy to restore lost data. This topic provides notes and steps for manually and automatically copying snapshots across regions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The snapshot copying feature is currently in closed beta and free of charge. The beta phase ends on July 1, 2026, Beijing Time. After that, it will become a paid service.</div>


* <div data-tips="true" data-tips-type="tip">You will be charged based on the size of the snapshots being copied when copying snapshots across regions. For more information, see <a href="https://www.byteplus.com/en/pricing?product=volume&tab=1">Pricing details</a>.</div>



<span id=".5L2_55So5Zy65pmv"></span>
## Use cases


* Cross\-region backup

   In the event of a natural disaster or equipment failure, you can use snapshot copies to restore your business systems in another region. This improves the reliability and resilience of your services.

* Cross\-region migration

   You can copy your local data to different regions to support launching the same business in multiple areas. One example is releasing a game in multiple regions.


<span id="Qyvkijnj"></span>
## Snapshot copies

When you copy a snapshot, its tags are copied as well. The snapshot copy receives a new ID and is classified as a **Copied snapshot**. Snapshot copies are easy to find on the **Snapshots** page by checking the **Type** column.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


|Category |Considerations |
|---|---|
|Unsupported operations |You cannot roll back the volume from which a snapshot was created while the snapshot is being copied. |
|Constraints and limitations |* A single source snapshot cannot exceed 2,048 GB in size.<br><br>* A snapshot can only be copied to one region at a time.<br><br>* No more than 10 concurrent snapshot copy operations are allowed for a single BytePlus account in the same region. |


<span id=".5aSN5Yi25b-r54Wn"></span>
## Manually copying a snapshot

EBS allows you to manually copy a snapshot to another region. You must initiate the copy process yourself, and you can only copy one snapshot at a time.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can perform the copy operation only when the snapshot status is "Available" or "Rolling back".</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the snapshot resides.

4. On the "Snapshots" tab, click "Copy snapshot" in the "Actions" column of the snapshot.

5. In the "Copy snapshot" dialog, select the "Target Region", enter a "Snapshot name", and click "Copy snapshot".

   On the "Snapshots" tab, you can view the "Status" of the snapshots. The copy is successful when the status of the new snapshot changes from "Creating" to "Available" and the snapshot appears in the target region.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The project of the copy is the same as the snapshot by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot set a description when copying a snapshot. Instead, the description for the copy is automatically set to <strong>Copied from [region] snapshot [snapshot ID]</strong>, which helps you identify the source.   </div>
   


<span id="6Kk6SPvk"></span>
## Related operations

Although you cannot cancel an ongoing copy operation, you can delete the new snapshot created through the copying process. Follow these steps to do so:

On the "Snapshots" page, select the region where the new snapshot is located from the top menu bar. In the "Actions" column of the snapshot, click "... \> Delete snapshot". In the box that appears, confirm the deletion by clicking "Delete snapshot".

<span id="NQv5E8Ng"></span>
## Automatically copying snapshots

EBS allows you to create policies to automatically copy snapshots of one or more volumes to a specified region. This enables automatic, cross\-region data synchronization.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the snapshots reside.

4. On the "Snapshots" page, click the "Auto Snapshot Policies" tab.

5. On the "Auto Snapshot Policies" tab, click "Create policy". In the box that appears, set the policy parameters.

   The table below outlines parameters related to snapshot copying. For more information about other parameters, see [Creating an auto snapshot policy](https://docs.byteplus.com/en/docs/ecs/Create-an-auto-snapshot-policy).

&nbsp;

   
   |Parameter |Description |
   |---|---|
   |Enable |Select whether to enable cross\-region copying. When this option is enabled, snapshots created by the auto snapshot policy will be copied to the specified region.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">By default, snapshots created through cross\-region copying are placed in the "default" project.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Snapshots created through cross\-region copying are automatically named "Copied from {source snapshot ID}".</div><br> |
   |Target Region |Select the region to which the snapshots will be copied. |
   |Retention time |Specify how long the snapshot copies should be retained. The default retention period is 30 days.<br><br><br>* Custom retention: 1 to 65,536 days.<br><br>* It will be permanently retained and will not be automatically deleted until the number of automatic snapshots reaches the upper limit: The system automatically deletes the oldest snapshot when the number of automatic snapshots reaches the upper limit. |
   

6. Once you have finished configuring, click "Create policy".


**Related operations**

To cancel the automatic snapshot copy, click "Modify policy" in the "Actions" column of the desired auto snapshot policy on the "Auto Snapshot Policies" tab. Toggle off the "Enable" switch and click "Modify policy". Snapshots created by the policy will no longer be copied.

<span id="n9vPRpas"></span>
## Important notes on cross\-region and cross\-border data transfer

When copying snapshots, confirm that you retain full control of your business data and assume full responsibility for the transfer. Make sure your data transfer complies with all applicable laws. This includes using adequate data security technologies and strategies and meeting legal obligations, such as obtaining explicit consent from individuals, performing security checks, and filing paperwork. You also warrant that your business data does not contain any content that is restricted from transmission or disclosure by applicable laws.

Failure to comply with these statements and warranties will result in legal consequences. You will be held liable for any losses incurred by BytePlus or its affiliates.

<span id="39zunONB"></span>
## What is cross\-border data transfer

A cross\-border data transfer occurs when data collected, generated, or processed within a specific jurisdiction (e.g., the Chinese mainland) is transmitted or stored on servers or by institutions outside that jurisdiction via networks.

Using the snapshot copy feature to synchronize data across regions in different sovereign countries or independent jurisdictions will transfer and store your business data across borders.

This includes transfers from your own country to another country and the following typical scenarios:


* Transfer across sovereign countries: Copying data from a region in the Chinese mainland (e.g., Beijing) to an overseas region (e.g., Singapore); or synchronizing data between regions in different overseas countries (e.g., from a US East region to a European region).

* Transfer across independent jurisdictions: Copying data from a region in the Chinese mainland to a region in a Special Administrative Region such as Hong Kong or Macau.


&nbsp;
