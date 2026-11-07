---
title: "Switch to yearly or monthly subscription"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/switching_to_subscription"
---

You can convert the billing method from pay\-as\-you\-go to yearly/monthly subscription for PostgreSQL instances at any time according to your business needs.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites 


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* The instance billing method is [Pay-as-you-go](https://docs.byteplus.com/en/docs/RDS_for_PG/pay_as_you_go).

* The instance cannot have unpaid orders for conversion to yearly/monthly subscription.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If an instance has unpaid orders for conversion to yearly/monthly subscription, upgrading the instance specification will invalidate those orders. You must cancel those orders on the order page first before proceeding with the conversion to yearly/monthly subscription again.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. Select the region for the instance in the upper\-left corner of the top menu bar.

3. On the **Instances** page, click **Switch to subscription** in the **Actions** column of the target instance.

4. Select the subscription duration and auto renewal options and click **Next step: Confirm order**.

5. On the Confirm order page, confirm the order details, read and check the Terms of Service, and then click **Submit**.
