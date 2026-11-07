---
title: "Billing overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Billing-overview"
---

This topic describes the billing items and methods associated with Elastic Compute Service (ECS) instances.

<span id=".6K6h6LS56aG5"></span>
## Billing items

Billing items refer to the resources that incur charges for an ECS instance. These include the instance type, images, volumes, and elastic IP addresses (EIPs). See the following for the details of the billing items:


|Billing item |Description |Supported billing method |
|---|---|---|
|[Instance type](https://docs.byteplus.com/en/docs/ecs/Instance-type-billing) |Costs of compute resources (vCPUs, GPU and memory) and local volumes (if applicable) are based on the selected instance type. |* Pay\-as\-you\-go<br><br>* Subscription<br><br>* Spot instance<br><br>* Pay\-as\-you\-go + Reserved Instances (RI) |
|[Image](https://docs.byteplus.com/en/docs/ecs/Imagebilling) |The cost of an image depends on its type and usage. |* Subscription<br><br>* Pay\-as\-you\-go |
|[Volume](https://docs.byteplus.com/en/docs/ecs/Volume-billing) |Volumes, including system volumes and data volumes, are charged based on the unit price, capacity, and duration. |* Subscription<br><br>* Pay\-as\-you\-go |
|[EIP ](https://docs.byteplus.com/en/docs/ecs/Elastic-IP-Address-billing) |Internet traffic fee is applicable when an ECS instance is associated with an EIP. |* Subscription<br><br>* Pay\-as\-you\-go<br><br>   * Pay\-by\-bandwidth<br><br>   * Pay\-by\-data\-transfer |


<span id=".6K6h6LS55pa55byP"></span>
## Billing methods

With ECS, you can choose a billing method based on your needs. The following table shows the applicable resources and benefits of each billing method.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Compute resources form the basic configurations of an instance. Even if a pay\-as\-you\-go ECS instance is not running any service, it will be continuously billed for use of compute resources throughout the billing cycle, except that you have enabled <a href="https://docs.byteplus.com/en/docs/ecs/Economical-mode-for-pay-as-you-go-instances">Economical Mode</a>.</div>


* <div data-tips="true" data-tips-type="tip">The local volume is associated with specific instance types and cannot be purchased separately. Its cost is included in the instance cost.</div>




|Billing method |Description |Applicable resources |Settlement cycle |Price characteristics |Applicable scenarios |
|---|---|---|---|---|---|
|[Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) |Pay\-as\-you\-go: Without paying for a large amount of resources in advance, you can provision and release resources on\-demand at any time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can purchase Reserved Instances (RIs) for cost savings. For more information, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Billing-overview#.5oyJ6YeP6K6h6LS55LyY5oOg5oq15omj">Preferential deduction for pay\-as\-you\-go billing method</a>.</div><br> |* Compute resources (vCPUs, GPUs, and memory)<br><br>* Local volumes<br><br>* Image<br><br>* Volumes (system volumes and data volumes)<br><br>* EIP  |Second\-level billing: Settlement is done on an hourly basis. |The hourly unit price is higher compared with other billing methods. |Short\-term business scenarios with significant growth, such as limited\-time shopping events. |
|[Subscription](https://docs.byteplus.com/en/docs/ecs/Subscription) |Pay in advance to maximize cost savings. |* Compute resources (vCPUs, GPUs, and memory)<br><br>* Local volumes<br><br>* Image<br><br>* Volumes (system volumes and data volumes)<br><br>* EIP  |Billing based on duration: Monthly or yearly subscription options are available. |Offers more favorable pricing compared to Pay\-as\-you\-go, with additional discounts for yearly subscriptions. |Stable long\-term businesses. |
|[Spot instance](https://docs.byteplus.com/en/docs/ecs/Spot_Instance) |A unique Pay\-as\-you\-go method that saves up to 80% of costs compared with standard Pay\-as\-you\-go. However, the price fluctuates based on market supply and demand in real time, and the resources purchased by this billing method may be reclaimed due to price or inventory considerations. |Compute resources (vCPU, GPU, and memory) of pay\-as\-you\-go instances |Second\-level billing: Settlement is done on an hourly basis. |Prices fluctuate with market supply and demand, and can be as low as 10% of the pay\-as\-you\-go price. |Stateless application scenarios, such as stateless web site services, image rendering, offline analysis, and large\-scale parallel computing. |
|[Elastic Scheduled Instances (ESI)](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances) |A pre\-scheduled, automatic delivery sales mode. For scenarios with elastic resource requirements, this method provides resource assurance, with cost\-effectiveness much higher than Pay\-as\-you\-go. |Compute resources (vCPU and memory) for pay\-as\-you\-go instances |Second\-level billing: Settlement is done on an hourly basis. If the duration is less than one hour, billing will be made for one hour. If the instance is used for more than one hour, billing will be based on actual consumption. |Offers more favorable pricing compared to Pay\-as\-you\-go, but slightly higher than the hourly price of monthly subscriptions. |Predictable one\-off, cyclical elastic scenarios, such as e\-commerce promotions, big data, online education/games, etc.; Elastic offline businesses that can wait, such as scientific computing and offline rendering. |


<span id=".5oyJ6YeP6K6h6LS55LyY5oOg5oq15omj"></span>
### Preferential deduction for pay\-as\-you\-go billing method

For the compute resources of pay\-as\-you\-go instances, you can deduct bills by using Reserved Instances. This helps you save costs for resource use. You can buy Reserved Instances based on your actual needs.


|**Deduction method** |**Description** |**Instance coupon payment method** |
|---|---|---|
|[Reserved Instances](https://docs.byteplus.com/en/docs/ecs/Reserved-instances) |A voucher that provides discounts and resource reservation, which can be used to deduct the bill for compute resources required by Pay\-as\-you\-go instances (excluding spot instances). You can also use it to reserve resources to ensure a stable supply.<br><br><br>* The cost depends on the selected region, instance type, valid period, number of instances, etc.<br><br>* The voucher can be used to deduct the cost of a pay\-as\-you\-go instance at the resource level (with a commitment to use the specified resources). The deduction can be done only when the voucher and instance match. |Full prepayment, with all fees paid in a one\-off purchase. |


<span id=".6L2s5o2i6K6h6LS55pa55byP"></span>
## Changing billing method

After you subscribe to ECS resources, if you find that the current billing method does not meet your business needs, you can change the billing method. The following table lists the resources for which you can change the billing method.


|ECS resource |Related documents |
|---|---|
|Instance |* [Change the billing method from Pay-as-you-go to Subscription](https://docs.byteplus.com/en/docs/ecs/Converting-from-pay-as-you-go-to-subscription)<br><br>* [Change the billing method from Subscription to Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-to-pay-as-you-go) |
|Image |When you change the billing method of an instance, the billing method of images is changed simultaneously. |
|Volume |* [Change from pay-as-you-go volumes to subscription volumes](https://docs.byteplus.com/en/docs/ecs/Changing-pay-as-you-go-volumes-to-subscription-volumes)<br><br>* [Change from subscription volumes to pay-as-you-go volumes](https://docs.byteplus.com/en/docs/ecs/Converting-from-subscription-volumes-to-pay-as-you-go) |
|EIP  |[Change billing method for EIPs](https://docs.byteplus.com/en/docs/eip/Billing-methods-change) |


<span id=".5Lu35qC86K-m5oOF"></span>
## Pricing

On the [Price calculator](https://www.byteplus.com/en/pricing?product=ECS&tab=2) page, you can see the instance price and configuration items (such as system volumes, data volumes, and EIPs). The price calculator provides reference prices. The actual costs are the fee results displayed when you order in the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-shanghai/instance).

<span id=".5p-l55yL6LS555So6LSm5Y2V"></span>
## Viewing bill

To view the billing and consumption details of your ECS instances, go to the billing center in the ECS console by clicking User avatar \> Billing. Then, the billing details page appears. For detailed steps, refer to [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-viewing-bill-details).

<span id=".57ut6LS55ZKM6YCA6K6i"></span>
## Renewal and unsubscription

Before subscription\-based instances [expire](https://docs.byteplus.com/en/docs/ecs/Expiration), you can [renew](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.57ut6LS56K-05piO) them within a specified period. This ensures continuous operation and use of your instances.

If you do not need a subscription\-based instance, submit an [unsubscription](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription#.6YCA6K6i6K-05piO) request. Then, you can manually delete the instance during the retention period. Instances that are not renewed will be automatically released.

<span id=".6LSm5oi35qyg6LS5"></span>
## Account arrears

Account arrears affect the normal operation of instances. Therefore, recharge in a timely manner. For more information, refer to [Arrear](https://docs.byteplus.com/en/docs/ecs/Arrears).
