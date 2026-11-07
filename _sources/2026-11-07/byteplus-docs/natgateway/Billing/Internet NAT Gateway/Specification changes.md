---
title: "Specification changes"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Specification-change"
---

After the Internet NAT Gateway instance is created successfully, you can change the Internet NAT Gateway specifications anytime based on actual business needs.

**Upgrade**: Increase the gateway specification. Upgrading​ does not affect running services but increases costs.

**Downgrade**: Decrease the gateway specification. If the downgraded specification is lower than the running service requires, it will affect the running service. Proceed with caution.

**Specification changes by billing method:** 


|Item |Pay\-by\-Specification |Subscription |
|---|---|---|
|Specification limits |Supports upgrade and downgrade. |Only upgrades are supported. |
|Formula |Internet NAT Gateway Spec Config fee (USD) for this billing cycle =<br><br>Unit price of the gateway specification before change (USD/hour) × Usage duration of gateway specification before change within the billing cycle (hours) + Unit price of the gateway specification after change (USD/hour) × Usage duration of gateway specification after change within the billing cycle (hours). |For more information, see [Changing Annual or Monthly Subscription Resource Specifications](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#.5LiA44CB5Y-Y5pu05YyF5bm05YyF5pyI6LWE5rqQ6KeE5qC8). |
|Effective time |Immediate activation ||
|Related documents |[Changing specification for Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Changing-the-specification-of-an-Internet-NAT-gateway). ||
