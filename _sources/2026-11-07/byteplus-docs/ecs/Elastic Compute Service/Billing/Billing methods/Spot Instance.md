---
title: "Spot Instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Spot_Instance"
---

Spot Instance is a unique Pay\-as\-you\-go method. Compared with standard [Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go), the compute resources for spot instances can be purchased with a certain discount. The price changes in real time with market demand and supply. When you purchase a spot instance, you need to set the maximum price you are willing to pay for the instance. It only represents your purchasing intention. The settlement is still based on the market price. For details, please refer to [Fee settlement example](https://docs.byteplus.com/en/docs/ecs/Spot_Instance#.6LS555So57uT566X56S65L6L).

ECS instances purchased with this billing method have the same performance as regular servers. However, when the inventory is insufficient, or the market price exceeds the maximum price you set, the system will automatically release instance resources and reclaim the discounted ECS instances. For the reclaim mechanism, please refer to [Reclaiming spot instance](https://docs.byteplus.com/en/docs/ecs/Reclaiming_spot_instance).

For details on the spot strategy of spot instances, please refer to [Purchasing spot instance](https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance).

<span id=".5Lu35qC85ZKM6K6h6LS56KeE5YiZ"></span>
## Pricing and billing rules

<span id=".5Lu35qC8"></span>
### Pricing


* Spot instances are sold at a steep discount under the Pay\-as\-you\-go billing method, i.e., Spot instance price = Price of a Pay\-as\-you\-go instance with the same specification × Discount. This billing method can save up to around 80% of the cost compared with Pay\-as\-you\-go.

* The prices and discounts of spot instances vary based on specification. Please refer to the prices displayed on the spot instance purchase page in the ECS console.

* The discount only applies to the compute resources (vCPUs, GPU, and memory) of the instance. Other resources such as system volume, data volume, and Elastic IP (EIP) are still billed based on pay\-as\-you\-go rules as below:

   * For billing rules for system volume and data volume, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go).

   * For billing rules of EIP, refer to [EIP pay-as-you-go](https://docs.byteplus.com/en/docs/eip/Pay-as-you-go).


<span id=".6K6h6LS55ZGo5pyf"></span>
### Billing cycle


* Second\-level billing, with bills generated on an hourly basis. The market price of the instance at the time of creation is the hourly price. By dividing it by 3600, you can get the per\-second price.

* Fees are accurate to two decimal places, and cumulative fees less than 0.01 USD are not charged.


<span id=".6K6h6LS55pe26ZW_"></span>
### Billing duration

Spot instances are billed based on the actual duration of use, which is the duration from instance creation to release. Billing ends after the instance is released. If you stop an instance in the [ECS console](https://docs.byteplus.com/en/docs/ecs/StopInstance) or by calling the StopInstance API operation, the billing continues.

<span id=".6LS555So57uT566X56S65L6L"></span>
## Fee settlement example

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b7f8bf7b5470762441db9ed58daff959.png) </span>

**Example 1: When the market price \> the maximum price offered by the user, the spot instance is released.** 

When the inventory of spot instances is sufficient and the market price is higher than the maximum price offered by the user, the instance is released, as shown in the figure above (left). The settlement is based on the actual usage duration (accurate to second) and the unit price (the market price at the time of the transaction).

8:00 market price was 0.2 USD/hour. One user offered a maximum price of 0.7 USD/hour and purchased a spot instance.

8:30 market price was 0.5 USD/hour.

9:30 market price was 0.3 USD/hour.

10:00 market price was 0.8 USD/hour, higher than the maximum price offered by the user. Therefore, the user received a notification of the upcoming instance release.

During this period, 3 billing cycles were generated, with the actual cost details as follows:

8:00–8:30 usage for 30 minutes, i.e., 30 \* 60 \* (0.2/3600)= 0.1 USD.

8:30–9:30 usage for 60 minutes, i.e., 60 \* 60 \* (0.5/3600)= 0.5 USD.

9:30–10:00 usage for 30 minutes, i.e., 30 \* 60 \* (0.3/3600)= 0.15 USD.

The actual usage duration was 2 hours. The total fee was 0.75 USD.

**Example 2: Spot instance is released due to insufficient inventory.** 

When the inventory of spot instances is insufficient and the market price is lower than the maximum price offered by the user, the instance is released, as shown in the above figure (right).

8:00 market price was 0.2 USD/hour. One user offered a maximum price of 0.7 USD/hour and purchased a spot instance.

8:30 market price was 0.5 USD/hour.

9:30 market price was 0.3 USD/hour.

10:00 market price was 0.6USD/hour, lower than the maximum price offered by the user. However, due to insufficient inventory, the user received a notification of the upcoming instance release.

During this period, 3 billing cycles were generated, with the actual cost details as follows:

8:00–8:30 usage for 30 minutes, i.e., 30 \* 60 \* (0.2/3600) = 0.1 USD.

8:30–9:30 usage for 60 minutes, i.e., 60 \* 60 \* (0.5/3600)= 0.5 USD.

9:30–10:00 usage for 30 minutes, i.e., 30 \* 60 \* (0.3/3600) = 0.15 USD.

The actual usage duration was 2 hours. The total fee was 0.75 USD.
