---
title: "Creating ESI order with the same configuration"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Purchase_reservation_orders_of_the_same_configuration"
---

This topic describes how to use the configuration information of an existing ESI order to quickly create a new one with the same configuration. Therefore, you can improve the efficiency of horizontal scaling in specific scenarios.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Elastic Scheduled Instances console](https://console.byteplus.com/ecs/esi).

2. In the top menu bar, select the region and project of your business.

3. Select any of the following methods to access the buy page.

   * On the ESI order list page, click the "Purchase the same configuration reservation" button in the "Actions" column on the right side of the target reservation order.

   * Click the target ESI order name to enter the details page. Then, click the "Purchase the same configuration reservation" button in the upper right corner.

   * In the left\-side navigation pane, select "Instances & Images \> Instances" to enter the instances page. Then, click the "Purchase the same configuration reservation" button in the "Actions" column on the right of the console.

4. The system will automatically fill in configurations of the original order and redirect you to the "Confirm" page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The filling logic for the <strong>Basic configuration</strong>, <strong>Network configuration</strong>, and <strong>Custom configuration</strong> of an instance is the same as that for purchasing an instance with the same configuration. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration">Purchasing an ECS instance with the same configuration</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the resource delivery time is automatically set to the same time slot of today/another day. You can also select a different time lot based on your needs.   </div>
   

5. Follow the console guidance to review and confirm the agreements.

6. Click "Buy now". On the order confirmation page, review the order information and complete the payment.

   > If you have available coupons, ​select them for fee deduction.   
   

7. After you make the payment, click the "Go to Console" button to be redirected to the ESI page. Here, you can view the order.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After you create an ESI order with the same configuration, the system automatically creates a "Pay\-as\-you\-go `ESI`" within the new resource delivery time slot based on the configuration of that order.

After you create an ESI, you can also quickly create another one with the same configurations by "Buy the same configuration instances " feature. For specific actions, refer to [Purchasing an instance with the same configuration](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration).
