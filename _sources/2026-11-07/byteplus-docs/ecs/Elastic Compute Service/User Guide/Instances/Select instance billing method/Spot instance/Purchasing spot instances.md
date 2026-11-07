---
title: "Purchasing spot instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance"
---

This topic describes how to purchase spot instances in the ECS console.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section describes the configurations related to spot instances. For more parameter configurations, see <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances">Purchasing an instance by following the wizard</a>.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. Click "Create instance" button to purchase an ECS instance.

3. Select the billing method as "Spot".

4. Refer to the table below to select the instance's spot strategy.

   
   |Spot strategy |Description |Purchase result ||
   |---|---|---|---|
   |Set maximum price |* You need to set a maximum price for the target instance. The maximum price only represents your purchasing intent, and the settlement is based on market price.<br><br>* This price must be between the current spot market price and the pay\-as\-you\-go instance price. The higher your bid, the greater the chance of purchasing or retaining the spot instance. By clicking "View historical prices", you can view historical prices. |Bid price ≥ market price **and ** sufficient inventory |The spot instance is purchased and enabled. Billing is charged based on the current market price. You can refer to the [Fee settlement example](https://docs.byteplus.com/en/docs/ecs/Spot_Instance#.6LS555So57uT566X56S65L6L). |
   |||Bid price < market price **or** insufficient inventory |Purchase fails. |
   |Automatic bid |The system automatically sets the upper limit as the pay\-as\-you\-go instance price, which reflects only the purchase intention. It signifies that you accept the real\-time market price for billing spot instances. If available resources are insufficient, instances are automatically released. Therefore, we recommend that you back up data in advance. |Purchase succeeds due to sufficient stock. ||
   |||Purchase fails due to insufficient stock. ||
   

5. (Optional) When you create a spot instance with data volume, we recommend that you do not check "Delete with instance" option. Therefore, when you delete instance, your data volume is automatically retained.

6. Configure remaining parameters to complete the purchase.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After you create the instance, an instance with the billing method "Pay\-as\-you\-go `Spot`" appears on the instance page. You can follow the [Subsequent operations](https://docs.byteplus.com/en/docs/ecs/What-to-do-next) to learn and use ECS instances.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [RunInstances - Creates instances](https://docs.byteplus.com/en/docs/ecs/RunInstances)

* [DescribeSpotPriceHistory - Querys historical prices of spot instances](https://docs.byteplus.com/en/docs/ecs/DescribeSpotPriceHistory)

* [DescribeSpotAdvice - Queries the average release rate of spot instances over the past 30 days](https://docs.byteplus.com/en/docs/ecs/DescribeSpotAdvice)
