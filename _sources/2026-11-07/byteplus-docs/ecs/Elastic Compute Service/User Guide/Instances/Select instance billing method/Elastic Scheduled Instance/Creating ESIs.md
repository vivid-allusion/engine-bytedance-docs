---
title: "Creating ESIs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_ESIs"
---

This document introduces how to create Elastic Scheduled Instances (ESIs) on the console. When you create an ESI, you need to complete a reservation first. After that, the system automatically generates an ESI order. During the resource delivery period specified in the order, it automatically creates your instance with the pay\-as\-you\-go billing method.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note


* Currently, only the following types of ESIs are available for purchase: General\-purpose, Compute\-optimized, Memory\-optimized, High Frequency General\-purpose hfg2, and Local SSD i3s/i2.

* For ESIs, a [minimum 1-hour consumption policy](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances#.6K6h6LS5) is implemented. Regardless of whether the instance is released within the first hour after creation, a one\-hour bill is issued and the fee is charged. Charges beyond the first hour are based on your actual usage of ESI.

* When you associate a project or tag with a newly created reservation order, all instances reserved successfully in this order are automatically associated with the corresponding tag or project.

* ESI does not support the deployment set feature.

* ESI can only be created from images based on snapshots:

   * Public images provided by the platform are all snapshot\-based and recommended for usage.

   * If you want to use a custom image to create an ESI, first enable the snapshot service and make sure the image has a corresponding snapshot.

   * If you want to use a shared image to create an ESI, make sure that the image has a corresponding snapshot.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic mainly introduces configurations when you create an ESI. For more details of instance configurations, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances">Purchasing an instance by following the wizard.</a></div>



1. Log in to [the ESI console](https://console.byteplus.com/ecs/esi).

2. In the top menu bar, select the region and project of your business.

3. Click the "Create Elastic Scheduled Instances" button to start purchasing an ESI. At this time, the billing method is "Elastic Scheduled Instances". Do not change this setting.

   You can also click the "Create instance" button on [ECS console](https://console.byteplus.com/ecs/instance), and select the billing method as "Elastic Scheduled Instances" for purchase.

4. Refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances), and then complete the instance **Basic configuration**, **Network configuration**, and **Custom configuration**.

5. Click the "Next" button to fill in the reservation information.

   Hover over the question mark next to the fee at the bottom of the page to view cost details and discount amounts, including fees for specifications, system volume, data volume, and EIP.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |ESI order name |Fill in the ESI order name. |ESI\-Name |
   |Quantity |You need to specify the number of instances to be reserved.<br><br><br>* By default, one account can use up to 300 vCPUs in an availability zone. To increase your vCPU quota, you can go to the [Quota center](https://console.byteplus.com/quota/ProductList/inParameterList?ProviderCode=ecs).[Learn more](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management)<br><br>* You can purchase a maximum of 500 instances in an order. |1 |
   |Delivery time interval |Select the instance delivery time period. For the China (Beijing) region, the time period is within 1 to 8 hours, and for the China (Shanghai) or China (Guangzhou) region, it is within 3 to 8 hours. The time period is precise to the minute, and each interval is 10 minutes. After you select the time, your instances will be delivered within this time period. Upon successful delivery, they will change to the **Running** state.<br><br>For example, if the current time is 17:42, the earliest delivery time period for the China (Beijing) region is 18:50–19:00 (one hour later). For the China (Shanghai) or China (Guangzhou) regions, the earliest period is 20:50–21:00 (three hours later). The latest delivery time period, 8 hours after the current time, is 01:40–01:50 (+1 day). |2024\-06\-12 21:50 \- 22:00 |
   |Tip on billing |ESIs have a [minimum 1-hour consumption policy](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances#.6K6h6LS5). Please confirm your understanding of this policy. |\- |
   |Agreement |Follow the console guidance to review and confirm the agreements. |\- |
   

6. After you confirm the information is correct, click "Buy now" to go to the application submission page and view whether your service is created.

7. Click the "Go to Console" button to be redirected to the ESI page to view the newly created order.

   At this point, the reservation order has been created. Once the resource delivery time is reached, the system automatically creates the ESI that meets your requirements on the order.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operation


<Tabs>
<Tab zoneid="TNfC4upWbc" title="View the instance delivery status">
<TabTitle>View the instance delivery status</TabTitle>

If your reservation is successful, you can view the details in the following ways:


* On the list page or details page, you can view the order name/ID, status, instance type, resource delivery time period, and delivery status. Click the value in the "Delivered quantity" column to jump to the instances page to view all delivered and unreleased instances.

* Click the order name to enter the details page, and select the "Delivery Instances" tab to view the delivered ESI. Click the instance name to jump to the instance details page to manage your instance.


</Tab>
<Tab zoneid="k82Bat17PR" title="Learn and use ECS instances">
<TabTitle>Learn and use ECS instances</TabTitle>

After delivery is complete, the Instances page displays an ECS instance whose billing method is "Pay\-as\-you\-go `ESI`".  You can then follow the guidance in [What to do next ](https://docs.byteplus.com/en/docs/ecs/What-to-do-next)to learn how to use the ECS instance.


</Tab>
<Tab zoneid="hObKEdZSzC" title="View elastic scheduled events or receive related notifications">
<TabTitle>View elastic scheduled events or receive related notifications</TabTitle>

Refer to [Viewing Elastic Scheduled events](https://docs.byteplus.com/en/docs/ecs/View_ESI_order_event).


</Tab>
<Tab zoneid="Y4zOd5Th4x" title="Cancel ESI order">
<TabTitle>Cancel ESI order</TabTitle>

You can cancel the reservation within 30 minutes after the ESI order is created. For detailed steps, see [Cancelling reservation](https://docs.byteplus.com/en/docs/ecs/Cancel_appointment).


</Tab>
<Tab zoneid="f0575w9G1F" title="Delete ESI">
<TabTitle>Delete ESI</TabTitle>

Refer to [Deleting Elastic Scheduled Instances](https://docs.byteplus.com/en/docs/ecs/Delete_Elastic_Scheduled_Instances).


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[CreateScheduledInstances - Creates ESIs](https://docs.byteplus.com/en/docs/ecs/CreateScheduledInstances)
