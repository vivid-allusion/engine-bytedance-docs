---
title: "Billing items"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/billable-items"
---

This topic describes the billable items of Message Queue for Kafka.

<span id="计费项"></span>
## Billing items

The billable items of a Kafka instance include the instance type, storage specification, and number of partitions.


|**Billable Item** |**Description** |
|---|---|
|Instance type |It provides computing specifications with different performances according to the peak traffic supported by the business. The billing type is pay\-as\-you\-go. |
|Storage specification |The fee of the storage space of a Kafka instance. |
|Number of partitions |The fee of partitions that are used beyond the free partition quotas in a Kafka instance. |


For more information on the billing methods, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/kafka/pay-as-you-go).

<span id="实例价格"></span>
## Instance prices

Kafka instances support multiple combinations of instance specifications. They are charged by instance type, storage specification, and number of used partitions.

<span id="71e04a69"></span>
### Instance type

The prices vary among instance types.

<span id="8b8c245d"></span>
### Storage specification

You must specify a storage space for your instance after selecting an instance type. The storage space range you can specify varies depending on the selected instance type. Refer to the instance creation page for details. Message Queue for Kafka supports two types of disks: ESSD_FlexPL and ESSD_PL0. The former delivers higher input/output operations per second (IOPS) performance.

The unit price for storage space varies depending on the disk type.

<span id="39bd3e78"></span>
### Number of partitions

For each instance type, a certain number of partitions are offered free of charge. The partitions that are used beyond the free quota are charged as per the unit price.

<span id="价格计算公式"></span>
## Formula for calculating prices


* Pay\-as\-you\-go:


Post\-paid price per hour = [Unit price of the instance type + Unit price of storage specification × Storage space + Unit price of partitions × (Total number of partitions \- Number of free partitions offered by the instance type)] × Number of instances

<span id="6e65853c"></span>
## Examples

In the following examples, the China (Beijing) Region is used. The estimation of prices is for reference only.

<span id="按量计费"></span>
### Pay\-as\-you\-go

**Use scenario**: You buy one instance and select the pay\-as\-you\-go billing method. The instance type is kafka.n3.x2.small and the storage specification is 1,800 GiB.

**Price per hour**: (CNY 7.84/hour + CNY 0.0025/GiB/hour × 1,800 GiB) × 1 instance = CNY 12.34/hour
