---
title: "Instance Specifications and Pricing"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing"
---

At present, the Machine Learning Platform only charges for computing resources, and the instance is the basic unit of computing resources. When a user executes a task, he can select an instance of a certain specification under a certain queue to obtain the corresponding CPU, memory, and GPU. The specific specifications and pricing are listed below.

<span id="023c2926"></span>
# Instance spec list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instance creation can have varying amounts of CPU and memory consumption depending on the type of workload. For example, if a user creates Dev boxes and custom tasks with the same instance specification, the actual amount of CPU and memory obtained may be inconsistent.</div>


<span id="4b827370"></span>
## Generic Instance


> * General purpose g3a

>    * Adopt the fourth generation AMD EPYC (TM) Genoa processor, the main frequency is 2.6GHz, and the turbo frequency is 3.7GHz.

>    * The processor to memory ratio is 1:4.

>    * Maximum support 192 vCPU, 768GiB

> * General purpose g3i

>    * Using the 4th generation Intel (®) Xeon (®) Scalable Processor (Sapphire Rapids) or the 5th generation Intel (®) Xeon (®) Scalable Processor (Emerald Rapids), the main frequency is 2.6GHz, and the full\-core turbo frequency is up to 3.1GHz.

>    * The processor to memory ratio is 1:4.

>    * Maximum support 192 vCPU, 768GiB



|instance specification |vCPU<br><br>（Core） |Memory (GiB) |Network base bandwidth (Gbit/s) |Cloud disk IOPS (million) |Cloud disk bandwidth<br><br>（Gbit/s) |Pay\-as\-you\-go (USD/hour) |Prepaid package days (USD/day) |Prepaid monthly subscription (USD/month) |
|---|---|---|---|---|---|---|---|---|
|ml.g3i.8xlarge |32 |128 |24 |10 |6 |1.8031 |43.2744 |956.08 |
|ml.g3i.12xlarge |48 |192 |36 |15 |8 |2.7047 |64.9128 |1,434.12 |
|ml.g3i.16xlarge |64 |256 |42 |20 |10 |3.6063 |86.5512 |1,912.16 |
|ml.g3i.24xlarge |96 |384 |64 |30 |16 |5.4094 |129.8256 |2,868.24 |
|ml.g3i.48xlarge |192 |768 |96 |60 |32 |10.8188 |259.6512 |5,736.48 |
|ml.g3a.8xlarge |32 |128 |12 |5 |5 |1.6464 |37.277885 |745.5577 |
|ml.g3a.12xlarge |48 |192 |16 |8 |6 |2.4697 |55.91683 |1,118.34 |
|ml.g3a.16xlarge |64 |256 |20 |10 |7 |3.2929 |74.55577 |1,491.12 |
|ml.g3a.24xlarge |96 |384 |32 |15 |10 |4.9393 |111.83366 |2,236.67 |
|ml.g3a.32xlarge |128 |512 |40 |20 |13 |6.5858 |149.111545 |2,982.23 |
|ml.g3a.48xlarge |192 |768 |64 |30 |20 |9.8786 |223.667315 |4,473.35 |


<span id="1af523f3"></span>
## GPU instance


|instance specification |vCPU（Core） |Memory (GiB) |GPU |GPU Memory (GiB) |Internet bandwidth (Gbit/s) |Cloud disk IOPS (million) |Cloud Disk Bandwidth (Gbit/s) |Pay\-as\-you\-go (USD/hour) |Prepaid package days (USD/day) |Prepaid monthly subscription (USD/month) |
|---|---|---|---|---|---|---|---|---|---|---|
|ml.gni3cl.11xlarge |44 |240 |L3c |48GB |40 |10 |6 |5.21 |125.00 |2,500.00 |
|ml.gni3cl.22xlarge |90 |480 |L3c |48GB |80 |20 |12 |10.42 |250.00 |5,000.00 |
|ml.gni3cl.45xlarge |180 |960 |L3c |48GB |160 |40 |24 |20.84 |500.00 |10,000.00 |


<span id="dbad4c2f"></span>
# Billing and settlement rules

<span id="bee999eb"></span>
## Prepaid

Machine Learning Platform offers prepaid billing. Pre\-payment is a billing method that pays first and then uses. Through the annual package, you can reserve resources in advance and enjoy greater price discounts, which will help you save more money.

You can place an order by creating a prepaid resource group. After the order is successfully placed, the countdown to the use time will be entered immediately.


* year and month

   * The service will be deducted at the time of subscription and will take effect upon successful subscription.

   * If the fee is not renewed/additional purchased in time, the corresponding prepaid service cannot continue to be used when the service expires.

   * When the monthly prepaid order expires, we will keep the order instance for 360 hours (15 days) from the expiration time. During this period, new tasks cannot be submitted, existing tasks will be stopped, and the Dev boxes cloud disk data will still be retained (please refer to the billing terms of the corresponding product for the data stored in TOS, NAS, and PFS).

      * The order instance will not be truly shut down until 12 hours after the expiration date (12 noon the next day). Before that, the resources can still be used normally, but the resource group cannot be reconfigured.

      * Within 360 hours, because the platform reserves resources for users, a fee for this period will be charged when renewing, and the resources will return to normal availability after renewal.

      * After more than 360 hours, it is considered that you have voluntarily given up the prepaid service of the Machine Learning Platform, and the relevant instances, existing tasks, and data will be released, and the released resources and data cannot be recovered.

* Bao Tian

   * After the prepaid order expires, we will keep the order instance for you for 48 hours. During this period, new tasks cannot be submitted, existing tasks will be stopped, and the Dev boxes cloud disk data will still be retained (please refer to the billing terms of the corresponding product for the data stored by TOS, NAS, and PFS).

      * The order instance will not be truly shut down until 12 hours after the expiration date (12 noon the next day). Before that, the resources can still be used normally, but the resource group cannot be reconfigured.

      * Within 48 hours, because the platform reserves resources for users, a fee for this period will be charged when renewing, and the resources will return to normal availability after renewal.

      * After more than 48 hours, it is considered that you have voluntarily given up the prepaid service of the Machine Learning Platform, and the relevant instances and existing tasks will be released, and the released resources and data cannot be recovered.


<span id="f10d7ad8"></span>
## Configuration change


* Support up\-allocation, down\-allocation, specific rules see the [resource change billing rules description](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules).

* The actual amount to be paid when matching is subject to the amount displayed on the matching interface.


<span id="a4f3df89"></span>
## Unsubscribe


* Pre\-paid billing supports non\-7\-day no\-reason unsubscribe methods. For specific rules, please refer to the [unsubscribe management expense center - BytePlus ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

* The actual amount payable when unsubscribing is subject to the amount displayed on the unsubscribing interface.
