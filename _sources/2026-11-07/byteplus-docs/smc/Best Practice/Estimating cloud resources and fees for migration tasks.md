---
title: "Estimating cloud resources and fees for migration tasks"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Evaluate-the-number-of-cloud-resources-used-by-Migration-Jobs"
---

SMC creates temporary resources, such as relay instances, cloud disks, and key pairs, in the destination region to relay data from the source server. As part of this process, SMC performs checks on your account's available resource quota and balance to help prevent migration failures due to insufficient quotas or funds.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Ensure that your BytePlus account, source servers, and other related features meet SMC migration requirements. For details, see [Limits](https://docs.byteplus.com/en/docs/smc/Limits).

* SMC automatically releases all temporary resources created during migration after the task completes. Do not use these temporary resources for your own production workloads. You can also manually clear these resources. For details, see [Clearing task resources](https://docs.byteplus.com/en/docs/smc/Clean-up-task-resources).


<span id=".5q2l6aqk5LiA77ya6K-E5LywU01D5Yib5bu655qE6LWE5rqQ5pWw6YeP"></span>
## Step 1: Estimate SMC\-created resource quantity

This section helps you estimate the cloud resources required for SMC migration and understand their default quota limits when you migrate your source server data to either an ECS instance or an ECS image.

<span id=".6L-B56e76Iez5LqR5pyN5Yqh5Zmo5a6e5L6L"></span>
### Migrate to ECS instance


<Tabs>
<Tab zoneid="aKEjS48Zfm" title="Migrate to "Pay-as-you-go" instances">
<TabTitle>Migrate to "Pay-as-you-go" instances</TabTitle>

* **Involved resources**

   
   |**Cloud resource** |**SMC resource creation rule** |**Limit description** |**Default quota** |**Changeable** |**Chargeable** |
   |---|---|---|---|---|---|
   |**Storage** ||||||
   |Volume |   * Quantity: Same as the number of migration tasks<br><br>   * Type: Same as the system volume type of the target instance<br><br>   * Capacity: Same as the system volume size of the target instance |Maximum usage per volume type |   * ESSD PL0: Maximum usage of 64TiB for each main account in a region<br><br>   * ESSD FlexPL: Maximum usage of 10TiB for each main account in a region |Yes |Yes |
   |**Network and security** ||||||
   |Security group |Same as the number of migration tasks |Upper quota limit of security groups for an account in a region |300 |Yes |No |
   |Key pair ||Max. key pairs for an account in a region |500 |No |No |
   

* **Process overview**


Refer to the diagram in this section for an overview of the temporary resource usage when the migration target is a "Pay\-as\-you\-go" ECS instance.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a52390363bc91da174bbf1b80aacf9bd.png) </span>


</Tab>
<Tab zoneid="UZ3eSKVOhK" title="Migrate to "Subscription" instances">
<TabTitle>Migrate to "Subscription" instances</TabTitle>

* **Involved resources**

   
   |**Cloud resource** |**SMC resource creation rule** |**Limit description** |**Default quota** |**Changeable** |**Chargeable** |
   |---|---|---|---|---|---|
   |**Image** ||||||
   |Image |Same as the number of migration tasks |Upper quota limit of custom images for an account in a region |50 |Yes |No |
   |**Storage and snapshot** ||||||
   |Volume |   * Quantity: Same as the number of migration tasks<br><br>   * Type: Same as the system volume type of the target instance<br><br>   * Capacity: Same as the system volume size of the target instance |Maximum usage per volume type |   * ESSD PL0: Maximum usage of 64TiB for each main account in a region<br><br>   * ESSD FlexPL: Maximum usage of 10TiB for each main account in a region |Yes |Yes |
   |Snapshot |   * Quantity: Same as the number of migration tasks<br><br>   * Capacity: Same as the size of the relay data volume |Maximum number of manual Snapshots that can be created per volume |Up to 10 manual snapshots can be created for each volume |No |Yes |
   |**Network and security** ||||||
   |Security group |Same as the number of migration tasks |Upper quota limit of security groups for an account in a region |300 |Yes |No |
   |Key pair ||Max. key pairs for an account in a region |500 |No |No |
   

* **Process overview**


Refer to the diagram in this section for an overview of the temporary resource usage when the migration target is a "Subscription" ECS instance.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed35e2b7fb08c0c1c46b0c9cfd6b7f12.png) </span>


</Tab>
</Tabs>


<span id=".6L-B56e76Iez5LqR5pyN5Yqh5Zmo6ZWc5YOP"></span>
### Migrate to ECS image

This section mainly describes the amount of **cloud resources that SMC creates**, and their default quota limits when you migrate your source server data to an ECS image (which is a custom image).


<Tabs>
<Tab zoneid="WxByTISaZx" title="Transmit data through Public Network">
<TabTitle>Transmit data through Public Network</TabTitle>

* **Involved resources**

   
   |**Cloud resource** |**SMC resource creation rule** |**Limit description** |**Default quota** |**Changeable** |**Chargeable** |
   |---|---|---|---|---|---|
   |**Instances and images** ||||| |
   |Instance |Same as the number of migration tasks |Max. ECS instances that can be created at one time |100 |Yes |Yes |
   |Image ||Upper quota limit of custom images for an account in a region |50 |Yes |No |
   |**Storage and snapshot** ||||| |
   |Volume |   * System volume:<br><br>      * Quantity: Same as the number of migration tasks<br><br>      * Type: ESSD PL0<br><br>      * Capacity: Same as the system volume size of the source server<br><br>   * Data Volume:<br><br>      * Quantity: Number of source server data disks to be migrated + 1<br><br>      * Type: ESSD PL0<br><br>      * Capacity: Matches the system disk and data disks of the source server to be migrated on a one\-to\-one basis, with the same sizing. |Maximum usage per volume type |Maximum usage of 64TiB for each main account in a region |Yes |Yes |
   |Snapshot consistency group |   * Quantity: Same as the number of migration tasks<br><br>   * Capacity: Same as the volume size of the relay instance |Maximum number of manual Snapshots that can be created per volume |Up to 10 manual snapshots can be created for each volume |No |Yes |
   |**Network and security** ||||||
   |Security group |Same as the number of migration tasks |Upper quota limit of security groups for an account in a region |300 |Yes |No |
   |Key pair ||Max. key pairs for an account in a region |500 |No |No |
   |EIP ||Max. EIPs that can be applied for an account in a region |20 |Yes |No |
   |Virtual Private Cloud ||Number of VPCs (including the default VPC) that can be created per account per region |10 |Yes |No |
   

* **Process overview**


Refer to the diagram in this section for an overview of the temporary resource usage when migrating to an ECS image over the public network.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cedfbc2c636cc062859ef3acc463b83b.png) </span>


</Tab>
<Tab zoneid="m3KfPw2SBN" title="Transmit data through Internal Network">
<TabTitle>Transmit data through Internal Network</TabTitle>

* **Involved resources**

   
   |**Cloud resource** |SMC resource creation rule |**Limit description** |**Default quota** |**Changeable** |**Chargeable** |
   |---|---|---|---|---|---|
   |**Instances and images** ||||||
   |Instance |Same as the number of migration tasks |Max. ECS instances that can be created at one time |100 |Yes |Yes |
   |Image ||Upper quota limit of custom images for an account in a region |50 |Yes |No |
   |**Storage and snapshot** ||||||
   |Volume |   * System volume:<br><br>      * Quantity: Same as the number of migration tasks<br><br>      * Type: ESSD PL0<br><br>      * Capacity: Same as the system volume size of the source server<br><br>   * Data Volume:<br><br>      * Quantity: Number of source server data disks to be migrated + 1<br><br>      * Type: ESSD PL0<br><br>      * Capacity: Matches the system disk and data disks of the source server to be migrated on a one\-to\-one basis, with the same sizing. |Maximum usage per volume type |Maximum usage of 64TiB for each main account in a region |Yes |Yes |
   |Snapshot consistency group |   * Quantity: Same as the number of migration tasks<br><br>   * Capacity: Same as the volume size of the relay instance |Maximum number of manual Snapshots that can be created per volume |Up to 10 manual snapshots can be created for each volume |No |Yes |
   |**Network and security** ||||||
   |Security group |Same as the number of migration tasks |Upper quota limit of security groups for an account in a region |300 |Yes |No |
   |Key pair ||Max. key pairs for an account in a region |500 |No |No |
   

* **Process overview**


Refer to the diagram in this section for an overview of the temporary resource usage when migrating to an ECS image over the private network.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b71bb5c489f5b5df9507436d331610a.png) </span>


</Tab>
</Tabs>


<span id=".5q2l6aqk5LqM77ya5p-l55yL5bey5pyJ6LWE5rqQ5pWw6YeP"></span>
## Step 2: View existing resource quantity

You can view information about existing resources under your account in the BytePlus console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For volumes, quota limits apply only to disk capacity. Therefore, you only need to calculate the capacity required based on the provided rule. You do not need to check the quantity details.</div>


* <div data-tips="true" data-tips-type="tip">SMC creates temporary resources in the region where the target instance or image is located. Therefore, you need to confirm the resource quantity of the corresponding region.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/dashboard?projectName=default).

2. In the left\-side navigation pane, select "Network and Security \> Security Group".

3. In the top menu bar, select the region where the target instance/image is located.

4. View the statistics in the lower right corner of the security group list page.

   The figure below shows that there are currently `98` security groups in the selected region. You can calculate the number of additional security groups that can be created as follows: **300 (quota limit)**  \- **98 (current number)**  = **202**. This means up to 202 more security groups can be created in this region.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7761bd54f43d8128cd742b8323504c40.png) </span>

5. Similarly, please confirm the existing quantity of the resource in the corresponding console of temporary resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The temporary resources created by SMC vary depending on the migration destination type and the network transmission mode. For details, see <a href="https://docs.byteplus.com/en/docs/smc/Evaluate-the-number-of-cloud-resources-used-by-Migration-Jobs#.5q2l6aqk5LiA77ya6K-E5LywU01D5Yib5bu655qE6LWE5rqQ5pWw6YeP">Estimating SMC\-created resource quantity</a>.   </div>
   

<span id=".5q2l6aqk5LiJ77ya55Sz6K-35Y-Y5pu06YWN6aKd"></span>
## Step 3: Apply for quota change

If your assessment indicates insufficient available quota in the destination region or that the maximum capacity per volume is insufficient for your needs, contact your account manager to request a quota increase.

<span id=".5q2l6aqk5Zub77ya6aKE5Lyw5LqR6LWE5rqQ6LS555So"></span>
## Step 4: Estimate cloud resource fees

SMC is a free service, but a small amount of costs may be incurred for consumed cloud resources during the migration process. Therefore, estimate the cost before starting a migration task to prevent task failure due to insufficient BytePlus account balance.

This section uses a data migration of a 40 GiB system volume as an example to illustrate how costs are calculated for different migration tasks **during migration**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The cloud resource prices used in the calculations are sample rates for illustration purposes only. Refer to the official pricing for actual rates.</div>


<span id=".6L-B56e76Iez5LqR5pyN5Yqh5Zmo5a6e5L6L"></span>
### Migrate to ECS instance


<Tabs>
<Tab zoneid="ii6s9Gl014" title="Migrate to "Pay-as-you-go" instances">
<TabTitle>Migrate to "Pay-as-you-go" instances</TabTitle>


|**Cloud resource** |**Billing method** |**Specifications** |**Migration duration (hour)**  |**Unit price** |**Calculation method** |**Migration process fee (** **USD** **)**  |
|---|---|---|---|---|---|---|
|Target instance |Pay\-as\-you\-go |ecs.g3i.large |10 |0.2254 USD/hour |Specification unit price \* billing duration |0.2254 \* 10 = 2.254 |
|Volume ||System volume:<br><br><br>* Capacity: 40 GiB<br><br>* Specification: ESSD_PL0 volume ||0.00025 USD/GiB/hour |Volume unit price \* volume capacity \* billing duration |0.00025 \* 40 \* 10 \* 2 = 0.200 |
|||Relay data volume:<br><br><br>* Capacity: 40 GiB<br><br>* Specification: ESSD_PL0 volume |||||
|Fees deducted during migration: 2.254 + 0.200 = **2.454** USD |||||||





</Tab>
<Tab zoneid="h0VExF2EQp" title="Migrate to "Subscription" instances">
<TabTitle>Migrate to "Subscription" instances</TabTitle>


|**Cloud resource** |**Billing method** |**Specifications** |**Migration duration (hour)**  |**Subscription duration (year)**  |**Unit price** |**Calculation method** |**Migration process fee (USD)**  |
|---|---|---|---|---|---|---|---|
|Target instance |Subscription |ecs.g3i.large |10 |1 |1434.120 USD |\- |No additional charges |
|Volume |Subscription |System volume:<br><br><br>* Capacity: 40 GiB<br><br>* Specification: ESSD_PL0 volume |||51.360 USD |\- |No additional charges |
||Pay\-as\-you\-go |Relay data volume:<br><br><br>* Capacity: 40 GiB<br><br>* Specification: ESSD_PL0 volume ||\- |0.00025 USD/GiB/hour |Volume unit price \* volume capacity \* billing duration |0.00025 \* 40 \* 10 = 0.100 |
|Snapshot |Pay\-as\-you\-go |Capacity: 40 GiB ||\- |\- |\- |Temporarily no billing |
|Fees deducted during the migration process: **0.100** USD ||||||||





</Tab>
</Tabs>


<span id=".6L-B56e76Iez5LqR5pyN5Yqh5Zmo6ZWc5YOP"></span>
### Migrate to ECS image


|Cloud resource |Billing method |Specifications |Migration duration (hour) |Unit price |Calculation method |Migration process fee (USD) |
|---|---|---|---|---|---|---|
|Relay instance |Pay\-as\-you\-go |ecs.g3i.large |10 |0.2254 USD/hour |Specification unit price \* billing duration |0.5192 \* 18 = 5.192 |
|Volume ||System volume:<br><br><br>* Capacity: 40 GiB<br><br>* Specification: ESSD_PL0 volume ||0.00025 USD/GiB/hour |Volume unit price \* volume capacity \* billing duration |0.00105 \* 40 \* 10 \* 2 = 0.840 |
|||Relay data volume:<br><br><br>* Capacity: 40 GiB<br><br>* Specification: ESSD_PL0 volume |||||
|Snapshot consistency group ||* System volume snapshot capacity: 40 GiB<br><br>* Relay data volume snapshot: 40 GiB ||\- |\- |Temporarily no billing |
|Fees deducted during the migration process: 2.254 + 0.200 = **2.454** USD |||||||


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The relay instance specification used in this example is for reference only. SMC automatically selects an available specification based on the actual specification inventory. The actual instance type that is provisioned prevails.</div>
