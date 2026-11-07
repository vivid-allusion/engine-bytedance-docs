---
title: "Purchase Reserved Storage Capacity (RSC)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Purchase-a-reserved-storage-capacity"
---

This article describes how to purchase Reserved Storage Capacity (RSC) in the Elastic Compute Service (ECS) console.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Category |Limits |
|---|---|
|Volume billing |Only charges for pay\-as\-you\-go\-based volumes can be offset with RSC. |
|Region |RSC can only be used to deduct volumes in the same region and availability zone. |
|Volume specification |It can only offset volumes with specifications matching the reserved capacity. For example, the RSC of ESSD PL0 specifications cannot be used to offset the billing for volumes of ESSD FlexPL specifications. |


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure ** 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Offsetting resources".

3. On the "Offsetting resources" page, click "Create offsetting resources".

4. On the "Create offsetting resources" page, configure the following parameters.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Region |A specified region is required. |China (Beijing) |
   |RI |Whether to purchase Reserved Instances (RI).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For parameter description of Reserved Instances (RI), please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Buying-Reserved-instances">Reserved Instances (RI)</a>.</div><br> |\- |
   |**RSC** |||
   |Purchase Reserved Instances (RI) |Select "Purchase Reserved Storage Capacity (RSC)". |\- |
   |Resource type |Only 'Zonal level (reserved)' is supported. This means it can only offset capacity charges for volumes with identical specifications within the same availability zone and supports resource reservation. |\- |
   |Availability zone |Availability zone must be specified for RSC. |Availability Zone A |
   |Term |Enter the name of the reserved block storage capacity. |rsctest |
   |Volume specification |Select the reserved volume specification as needed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details on volume performance, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Volume-specifications">Volume specification</a>.</div><br> |ESSD PL0 (maximum IOPS per volume: 10,000) |
   |Reserved capacity |Select the reserved volume capacity per hour.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For reserved capacity deduction rules, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Reserved-storage-capacity#.5oq15omj6K-05piO">Deduction description</a>.</div><br> |20 |
   |Associated project |(Optional) After you associate the RSC with a project, you can categorize the RSC under the account to the project for unified management.<br><br><br>* When you enter the create page, if you have selected a specific project in the top navigation bar, the newly created RSC can only be associated with that project. To associate it with another project, change the project in the top navigation bar to either "All Resources" or the target project.<br><br>* The RSC supports cross\-project deduction against pay\-as\-you\-go instance bills. This means the RSC and the pay\-as\-you\-go instances it deducts from can belong to different projects.<br><br>* For more information about projects, see [Managing projects](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |projectA |
   |Tag |(Optional) Click "<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span>Add tags" to add tags to the RSC. For more information, refer to [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |k1:v1 |
   |Subscription duration |Select the validity period of the reserved storage capacity package. Valid options are 1–9 months, 1 year, 2 years, 3 years, 4 years, and 5 years. |1 month |
   

5. On the right side of the purchase page, review and confirm the relevant agreements as guided by the console, select "I have read and agree to the Elastic Compute Service (ECS) Terms of Service", then click "Buy now".

6. After confirming the order details are correct, click "Next".

   After completing the payment, you can click "Go to console" to view the purchased reserved block storage capacity.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also call the PurchaseReservedStorageCapacity interface to purchase RSC. For specific steps, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Purchasereservedstoragecapacity">PurchaseReservedStorageCapacity</a>.   </div>
