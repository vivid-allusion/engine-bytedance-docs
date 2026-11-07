---
title: "Billing items"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Billing_items"
---

This section introduces the billing items and pricing details related to message queue for RabbitMQ.

<span id=".6K6h6LS56aG5"></span>
## Billing items

The billing items for message queue for RabbitMQ include charges for compute specifications and storage specifications.


|**Billing items** |**Description** |
|---|---|
|Computing specifications |Provides compute specifications with varying performance based on the peak traffic supported by the business. Billing method includes subscription or pay\-as\-you\-go subscription. |
|Storage specifications |Cost of storage space for message queue for RabbitMQ instance. Billing method includes subscription or pay\-as\-you\-go subscription. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For information, please refer to <a href="https://docs.byteplus.com/en/docs/rabbitmq/Pay_as_you_go">Billing method</a>.</div>


<span id=".5a6e5L6L5Lu35qC8"></span>
## Instance prices

The RabbitMQ instances support multiple specification configurations and are billed based on compute and storage specifications.

<span id=".6K6h566X6KeE5qC8"></span>
### Computing specifications

Prices vary according to different computing specifications. For detailed information about subscription and pay\-as\-you\-go billing, please refer to [Pricing details](https://www.byteplus.com/en/pricing?product=Message_Queue_for_RabbitMQ&tab=1).

<span id=".5a2Y5YKo6KeE5qC8"></span>
### Storage specifications

After selecting the computing specifications, you also need to configure the storage for each instance. Different computing specifications correspond to varying ranges of optional storage. For specific information, please refer to the instance creation page. For pricing information on storage space under subscription and pay\-as\-you\-go models, please refer to [Pricing Details](https://www.byteplus.com/en/pricing?product=Message_Queue_for_RabbitMQ&tab=1).

<span id=".5Lu35qC86K6h566X5YWs5byP"></span>
## Pricing formula


* Pay\-as\-you\-go:

   Hourly price = (unit price of computing specifications + unit price of storage specifications × storage size) × number of instances

* Subscription:

   One\-time prepaid price = (unit price of computing specifications + unit price of storage specifications × storage size) × number of instances × number of months

    &nbsp;


<span id=".6LSt5Lmw56S65L6L"></span>
## Purchase example

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example, set in North China 2 (Beijing), is for illustration purposes only, and the estimated results are for reference. We recommend that you use <a href="https://www.byteplus.com/en/pricing?product=Message_Queue_for_RabbitMQ&tab=2">Price calculator</a> to estimate costs.</div>


<span id=".5YyF5bm05YyF5pyI"></span>
### Subscription


* **Application scenario**: Subscription duration is 1 month, quantity is 1, the compute specification is **rabbitmq.n1.x2.medium**, and the storage specification is 1800GiB instance.

* **One\-time prepaid prices**: (541 Yuan/month + 1 Yuan/GiB/month × 1800GiB) *one instance* for 1 month = 2341 Yuan

    &nbsp;


<span id=".5oyJ6YeP6K6h6LS5"></span>
### Pay\-as\-you\-go billing


* **Application scenario**: Subscribe quantity of 1, compute specification of **rabbitmq.n1.x2.medium**, storage specification of 1800GiB instance, used on\-demand.

* **Price per hour**: (1.13 Yuan/hour + 0.0025 Yuan/GiB/hour × 1800GiB) × 1 instance = 5.63 Yuan/hour
