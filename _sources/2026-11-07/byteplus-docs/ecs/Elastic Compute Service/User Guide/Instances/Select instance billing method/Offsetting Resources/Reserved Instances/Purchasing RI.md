---
title: "Purchasing RI"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Buying-Reserved-instances"
---

This topic describes how to purchase Reserved Instances (RI) in the console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* The following table lists the instance families that you can purchase with RI. For more information on instance types, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

   
   |**Type** | |**Instance families** |
   |---|---|---|
   |x86 Compute |General\-purpose |g3i, g2i |
   ||Compute\-optimized |c3i, c2i |
   ||Memory\-optimized |r3i, r2i |
   ||Local SSD |i2 |
   ||Big Data |d2 |
   ||Burstable instance |t2 |
   ||Shared |s2, e |
   |EBM |General\-purpose EBM |ebmg3id |
   ||Compute\-optimized EBM |ebmc3id |
   

* Some instance types have corresponding RIs that do not allow you to change instance type ([Reserved Instances (RI) that do not support changing instance type](https://docs.byteplus.com/en/docs/ecs/Change-Reserved-instances#.5rOo5oSP5LqL6aG5)). For deduction or reservation for these instance types, you can only purchase zonal RIs.

* The number of instances that can be deducted or reserved by RI is determined by the number of vCPUs of the instance. By default, in a single availability zone, the total number of vCPUs that can be offset by all RIs owned by an account is no more than 200. To increase your vCPU quota, go to the Quota center. [Learn more](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management)


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Offsetting resources console](https://console.byteplus.com/ecs/ri).

2. In the top menu bar, select the region and project of your business.

3. Click the "Create Offsetting Resources" button to enter the purchase page.

4. Refer to the table below to complete the related settings.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region for offsetting resources.  |China (Beijing） |
   |**RI** |||
   |Purchase Reserved Instances (RI) |Check this option to purchase RI. |\- |
   |Resource scope |Select RI type:<br><br><br>* Zonal RIs (reserved) can only offset pay\-as\-you\-go instances of the same instance type and size as the RIs in the same availability zone. Zonal RIs support resource reservation.<br><br>* Regional RI (not reserved) can deduct all pay\-as\-you\-go instances in the same region that belong to the same instance family. Regional RIs do not support resource reservation.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Regional RI is currently in Beta. If you need a trial, contact the account manager to apply.   </div><br>    |Zonal RI (reserved) |
   |Availability zone |When you purchase zonal RIs, specify the availability zone where your business is located. When you purchase regional RIs, the system defaults to "All zones". |Availability zone A |
   |Name |Enter the RI name. |ReservedInstanceName |
   |Instance type |Select an instance type that meets your business needs. For instance families that support RIs, refer to [Precautions](https://docs.byteplus.com/en/docs/ecs/Buying-Reserved-instances#.5rOo5oSP5LqL6aG5). |General\-purpose g2i ecs.g2i.2xlarge |
   |Instance quantity |Instance number that can be deducted or reserved by RIs.<br><br>For example, if you have a zonal RI for the ecs.g2i.2xlarge instance type and set the instance count to 2, this RI can match 2 pay\-as\-you\-go instances of the same type at the same time. |1 |
   |Project |(Optional) After associating the RI with a project, you can classify the RI under this account into the project for unified management.<br><br><br>* If you select a specific project in the top navigation bar and enter the create page for RI, the newly created RI can only be associated with that project. To associate it to another project, change the project in the top navigation bar to either "All Resources" or the target project.<br><br>* RIs support cross\-project deduction of pay\-as\-you\-go instance bills. This means the RI and the pay\-as\-you\-go instances it deducts can belong to different projects.<br><br>* For more information on projects, refer to [Managing projects](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |Project A |
   |Tag |(Optional) Click the "<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span>Add tags" button to add tags to RI. For more information, please refer to [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |k1:v1 |
   |Automatic renewal |Set whether to "Enable auto\-renewal" for RI. After you enable auto\-renewal, the platform automatically deducts the renewal expenses before the expiration of RI. You don't need to manually renew it. |\- |
   |Purchase duration |Select the subscription duration term for offsetting resources. |1 year |
   

6. On the purchase page, confirm the configuration details on the right side. Then, review and confirm the relevant agreements as the console instructions.

7. Click the "Buy now" button, and then confirm the order information, such as configurations, payment method, subscription duration, quantity, and amount. After you confirm configuration is correct, click the "Next" button.

   > If you have available coupons, you can select coupons to deduct your payment.   
   

8. After you complete your payment, click the "Go to the console" button to the RI list to view the newly created order.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operation

You can view the purchased RIs on the RI list page. The RIs automatically match your pay\-as\-you\-go instances and offset the bills.

<span id=".55u45YWz5paH5qGj"></span>
## Related document

[PurchaseReservedInstances - Purchases Reserved Instances](https://docs.byteplus.com/en/docs/ecs/PurchaseReservedInstances)
