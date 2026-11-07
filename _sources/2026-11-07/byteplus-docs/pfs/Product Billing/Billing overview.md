---
title: "Billing overview"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Billing-overview"
---

This article provides a billing description for BytePlus Parallel File Storage(PFS), including billing cycle, billing type and price.

<span id="e5def165"></span>
## Billing method

Currently, PFS only supports pay\-as\-you\-go billing. It is a postpaid billing method, which means you use the service first and then pay for it. The cost is calculated by multiplying the selected instance capacity configuration by the billing cycle, and the charges are included in your bill. You can settle the fees after the bill is generated.

<span id="2ef8f5ff"></span>
## Billing cycle

PFS calculates the usage of all billing items on an hourly basis and generates bills based on the usage.

<span id="01db3beb"></span>
## Billing items and prices

This article provides the billing items and types for PFS. For detailed pricing information on the billing items, please refer to [BytePlus pricing](https://www.byteplus.com/en/pricing?product=vePFS&tab=1).


|Billing items |Product specifications |Billing method |
|---|---|---|
|Storage billing |100MB/s/TiB |pay\-as\-you\-go |
||Performance_Edition ||
||Intelligent_Computing_Edition ||


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">Storage capacity is calculated using binary units, for example, 1GiB = 1024MiB.</div>


<span id="fc3615b4"></span>
## Associated cost explanation

When creating a mount service, three pay\-as\-you\-go ECS instances will be created as client management nodes. These instances will incur ECS product fees. For detailed information on ECS instance billing, please refer to the [ECS Billing overview](https://docs.byteplus.com/en/docs/ecs/Billing-overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="tip">The supported ECS instance specifications are subject to the information displayed on the console.</div>


* <div data-tips="true" data-tips-type="tip">Before creating a mount service, please ensure that your account is eligible in the availability zone of the PFS instance and meets the requirements for purchasing the corresponding ECS instance specifications.</div>
