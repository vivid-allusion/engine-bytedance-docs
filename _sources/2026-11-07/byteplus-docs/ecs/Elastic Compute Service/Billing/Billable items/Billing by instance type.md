---
title: "Billing by instance type"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-type-billing"
---

Billing by instance type refers to the charging of compute resources (vCPU, GPU, and memory) based on the selected instance type. This topic describes billing methods for different instance types and the characteristics of each method.

<span id=".6LSt5Lmw5a6e5L6L5Y-K5a6a5Lu3"></span>
## Purchasing instances and pricing


* Purchasing instances: [Subscribe to instances based on the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Pricing: Prices vary for the same instance type in different regions. For more information, refer to [Pricing](https://www.byteplus.com/en/pricing?product=ECS&tab=1).


<span id=".5a6e5L6L6KeE5qC86K6h6LS55pa55byP5a-55q-U"></span>
## Comparing billing methods based on instance type

Instances of different types are billed with the following methods. The following table shows comparison of them.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Compute resources form the basic configurations of an instance. Even if a pay\-as\-you\-go ECS instance is not running any service, it will be continuously billed for use of compute resources throughout the billing cycle, except that you have enabled <a href="https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances">Economical Mode</a>.</div>



|Billing method |[Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) |[Subscription](https://docs.byteplus.com/en/docs/ecs/Subscription) |[Spot Instance](https://docs.byteplus.com/en/docs/ecs/Spot_Instance) |[Elastic Scheduled Instances (ESI)](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances) |
|---|---|---|---|---|
|Payment |Without paying for resources in advance, you can provision and release resources on\-demand at any time.<br><br>You can purchase Reserved Instances (RIs) for cost deduction and saving. For more information, refer to [Preferential deduction for pay-as-you-go billing method](https://docs.byteplus.com/en/docs/ecs/Instance-type-billing#.5oyJ6YeP6K6h6LS55LyY5oOg5oq15omj). |Pay in advance to maximize cost savings; Applicable for scenarios where resources are required in a long term. |A unique Pay\-as\-you\-go method that saves up to 80% of costs compared with standard Pay\-as\-you\-go. However, the price fluctuates based on market supply and demand in real time, and this billing method may be reclaimed due to market price or inventory considerations. |A pre\-scheduled, automatic delivery sales mode. For scenarios with elastic resource requirements, this method provides resource assurance, with cost\-effectiveness much higher than Pay\-as\-you\-go. |
|Settlement cycle |Second\-level billing: Settlement is done on an hourly basis. |Billing based on duration: Monthly or yearly subscription options are available. |Second\-level billing: Settlement is done on an hourly basis. |Second\-level billing: Settlement is done on an hourly basis. If the duration is less than one hour, billing will be made for one hour. If the instance is used for more than one hour, billing will be based on actual consumption. |
|Price characteristics |The hourly unit price is higher compared with other billing methods. |Offers more favorable pricing compared to Pay\-as\-you\-go, with additional discounts for yearly subscriptions. |Prices fluctuate with market supply and demand, and can be as low as 10% of the pay\-as\-you\-go price. |Offers more favorable pricing compared to Pay\-as\-you\-go, but slightly higher than the hourly unit price of monthly subscriptions. |
|Applicable scenarios |Short\-term business scenarios with significant growth, such as limited\-time shopping events. |Stable long\-term businesses. |Stateless application scenarios, such as stateless web site services, image rendering, offline analysis, and large\-scale parallel computing. |Predictable one\-off, cyclical elastic scenarios, such as e\-commerce promotions, big data, online education/games, etc.; Elastic offline businesses that can wait, such as scientific computing and offline rendering. |
|Changing instance type |You can upgrade or downgrade instances. For more information, refer to [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Instance-type-change). |You can upgrade or downgrade instances. For more information, refer to [Changing instance type](https://docs.byteplus.com/en/docs/ecs/Instance-type-change). |Not supported. |Not supported. |
|Changing billing method |[Convert from pay-as-you-go to subscription](https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription). |[Changing billing method from Subscription to Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go). |Not supported. |Not supported. |
|Stopping instance |If you stop an instance but do not release the ECS resources, the instance continues to incur charges.<br><br>> Instances with the [Economical Mode](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances) enabled will not incur charges for compute resources after being stopped. |Billing continues even after the instance is stopped.<br><br>> The Economical Mode is not available. |If you stop an instance but do not release the ECS resources, the instance continues to incur charges.<br><br>> Instances with the [Economical Mode](https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances) enabled will not incur charges for compute resources after being stopped. |Charges continue even after the instance is stopped.<br><br>> The Economical Mode is not available. |
|Deleting instance |You can delete an instance at any time. |When a subscription instance [expires](https://docs.byteplus.com/en/docs/ecs/Expiration) or you [unsubscribe](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.6YCA6K6i6K-05piO) to it, you can manually delete the instance within the resource retention period. Instances that are not [renewed](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.57ut6LS56K-05piO) will be automatically released. |You can delete an instance at any time. The system may automatically release the instance due to market price changes or insufficient instance inventory. |You can delete an instance at any time. |


<span id=".5oyJ6YeP6K6h6LS55LyY5oOg5oq15omj"></span>
### Preferential deduction for pay\-as\-you\-go billing method

For the compute resources of pay\-as\-you\-go instances, you can deduct bills by using Reserved Instances. This helps you save costs for resource use. You can buy Reserved Instances based on your actual needs.


|**Deduction method** |**Description** |**Payment** |
|---|---|---|
|[Reserved Instances](https://docs.byteplus.com/en/docs/ecs/Reserved-instances) |A voucher with the ability to deduct and reserve, which can be used to deduct the bill for compute resources required by Pay\-as\-you\-go instances (excluding spot instances). You can also use it to reserve resources to ensure a stable supply.<br><br><br>* The cost depends on the selected region, instance type, valid period, number of instances, etc.<br><br>* The voucher can be used to deduct the cost of a pay\-as\-you\-go instance at the resource level (with a commitment to use the specified resources). The deduction can be done only when the voucher and instance match. |Full prepayment, with all fees paid in a one\-off purchase. |


<span id=".6K6h6LS55pa55byP5o6o6I2Q"></span>
## Recommended billing methods

For different business scenarios, you can consider the following suggestions to choose a billing method.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a18dca859dfeeb5bdc1d4caba339f0a3.png) </span>


|Business scenario type |Scenario characters |Scenario example |Recommended billing method |
|---|---|---|---|
|Stability |Businesses are not interconnected and are overall stable, with no significant traffic fluctuations. |For example, multiple cloud exhibition projects that are not interconnected. |* Subscription<br><br>* Pay\-as\-you\-go + Reserved Instances (RI)<br><br>* Elastic Scheduled Instances (ESI) |
|Interconnection |Businesses are interconnected, and as traffic increases, the resource demands of each business grow simultaneously. |Stable online businesses, such as internal OA systems. |Pay\-as\-you\-go + Reserved Instances (RI) |
|Surge |Businesses are not interconnected and short\-term burst activities are involved. |Scenarios such as hot events, limited\-time shopping, virtual concerts, and holiday celebrations, where there can be thousands or even tens of thousands of concurrent users. |* Pay\-as\-you\-go (Reserved Instances (RI) can be used for high\-frequency bursts)<br><br>* Spot Instance<br><br>* Elastic Scheduled Instances (ESI) |
|Hybrid deployment |Multiple businesses with different requirements for computing power and priorities at different times. |Blue\-green deployment, online/offline, and job\-based hybrid deployments. |* Pay\-as\-you\-go + Reserved Instances (RI)<br><br>* Elastic Scheduled Instances (ESI) |


&nbsp;
