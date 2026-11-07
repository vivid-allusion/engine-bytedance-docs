---
title: "Billing instructions"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Billing_items"
---

This topic describes the breakdown, unit prices, and calculation methods for each billing item in AgentKit to help you estimate costs before placing an order.

> **warning**

* > Starting from **August 31, 2026**, the previous gateway billing and agent runtime billing have been replaced by usage\-based billing for **gateway instances** (shared gateway and dedicated gateway), **agent runtimes**, **MCP** (MCP services and MCP toolsets),  .

* > When purchasing resources, make sure your BytePlus account has an available balance greater than **USD 5**. If the balance is insufficient, please go to the console to recharge before proceeding.

* > All prices in this topic are listed prices (pay\-as\-you\-go). The actual transaction price is subject to the order page in the console and the latest announcements.

## Billing overview

AgentKit fees are the sum of **resource usage fees** and **gateway instance fees**. Each item is metered and billed independently.

* **Resource usage fees**

   * **Agent runtime:**  An instance that hosts agent applications. Billed based on actual vCPU, memory, and public network traffic usage.

   * **Tool (Sandbox)** : Provides a secure code/command execution environment for agents. Billed based on actual vCPU, memory, and public network traffic usage.

   * **MCP (including MCP services and MCP toolsets)** : For backend tool integration and toolset management.

      * **MCP services in deployment mode**: Billed based on actual **vCPU, memory, and public network traffic** usage.

      * **Other integration methods and MCP toolsets**: No vCPU/memory resource usage fees. If semantic retrieval is enabled, tool indexing fees may be incurred.

* **Gateway instance fees**

   AgentKit supports two gateway types: **shared gateway** and **dedicated gateway**. The two types have non\-overlapping billing items. The gateway provides an access entry point for runtimes and MCP, handling authentication, routing, protocol conversion, access governance, and more. [Learn more.](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview)

   > **tip**

   > **The runtime gateway and MCP gateway are currently two separate gateway instances**. They are ordered and billed independently and do not share the same gateway instance.

   * **Shared gateway**: Gateway fee = **Instance fee + Data processing fee**

   * **Dedicated gateway**: Gateway fee = **Instance fee + Public network traffic fee + Data processing fee + Tool indexing fee (semantic retrieval scenarios only)**

## Resource usage

### Agent runtime

|**Billing items** |Billing unit |Description |**Billing granularity** |**Listed price (pay\-as\-you\-go)**  |
|---|---|---|---|---|
|Runtime CPU |runtimevcpu |Compute resources consumed by runtime instances. |USD/vCPU/second |0.000019 |
|Runtime memory |runtimemem |Memory resources consumed by runtime instances. |USD/GB/second |0.000003 |
|Runtime public network traffic |runtimetraffic |* When the associated gateway type is shared gateway, charges apply for public network client response traffic and platform\-initiated outbound public network traffic (if applicable).<br><br>* When the associated gateway type is dedicated gateway, charges apply for platform\-initiated outbound public network traffic (if applicable). Public network client response traffic is charged on the gateway instance side. |USD/GB |0.081 |

### Sandbox templates

|**Billing items** |Billing unit |Description |**Billing granularity** |**Listed price (pay\-as\-you\-go)**  |
|---|---|---|---|---|
|Sandbox template CPU |toolvcpu |Compute resources consumed by running sandbox templates. |USD/vCPU/second |0.00000975 |
|Sandbox template memory |toolmem |Memory resources consumed by running sandbox templates. |USD/GB/second |0.00000225 |
|Sandbox template public network traffic |tooltraffic |Outbound public network traffic fees incurred by sandbox templates. |USD/GB |0.081 |

### MCP (MCP services and MCP toolsets)

|**Billing items** |Billing unit |Description |**Billing granularity** |**Listed price (pay\-as\-you\-go)**  |
|---|---|---|---|---|
|CPU |gateway\-mcpservice\-deploy\-vcpu |Compute resource usage on the gateway side.<br><br>> **tip**<br><br><br>> Charged only when the MCP integration method is "Deploy MCP service". Other integration methods and MCP toolsets are not charged.<br> |USD/vCPU/second |0.000019 |
|Memory |gateway\-mcpservice\-deploy\-mem |Memory resource usage on the gateway side.<br><br>> **tip**<br><br><br>> Charged only when the MCP integration method is "Deploy MCP service". Other integration methods and MCP toolsets are not charged.<br> |USD/GB/second |0.000003 |
|Public network traffic |gateway\-traffic |* When the associated gateway type is shared gateway, charges apply for public network client response traffic and platform\-initiated outbound public network traffic (if applicable).<br><br>* When the associated gateway type is dedicated gateway, charges apply for platform\-initiated outbound public network traffic (if applicable). Public network client response traffic is charged on the gateway instance side. |USD/GB |0.081 |
|Tool indexing |gateway\-mcptoolset\-tool\-index |Charged only when semantic retrieval is used in the MCP toolset, billing is based on the maximum number of tool indexes within the hour.<br><br>> **tip**<br><br><br>> If the MCP toolset uses a dedicated gateway, this fee is charged on the dedicated gateway side.<br> |USD/10,000 indexes/hour |0.0027 |
|Gateway service request count |gateway\-mcpservice\-request |No longer charged if existing resources (MCP services or MCP toolsets) are connected to a shared gateway and a shared gateway instance order has been placed. Dedicated gateways are not involved. |USD/1,000 requests |0.005 |
|Number of retrieval tasks in the gateway toolset |gateway\-mcptoolset\-request |No longer charged if existing resources (MCP services or MCP toolsets) are connected to a shared gateway and a shared gateway instance order has been placed. Dedicated gateways are not involved. ||0.025 |

## Gateway instances

Gateway instance fees depend on the gateway type selected when you create resources (**shared gateway** or **dedicated gateway). The two types have non\-overlapping billing items.**  For differences in capabilities, isolation, and applicable scenarios, see [Gateway instance: dedicated vs. shared](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview?lang=en#PT93XYP3).

> **tip**

* > Shared gateways provide a free quota **per account per region**:

   * > Agent runtime: **2** free runtimes per account per region. Usage beyond the free quota is charged at the shared gateway instance rate.

   * > MCP services and MCP toolsets:**2 free in total**per account per region. Additional resources are billed at the shared gateway instance rate.

* > Existing resources:

   * > Existing resources (created before August 31, 2026) are upgraded to shared gateway mode by default, but **no shared gateway order is created automatically**. No fees are incurred immediately, even if the free quota has already been exceeded.

   * > The system automatically places an order for a shared gateway instance only when you **create** a resource (an MCP service, MCP toolset, runtime) in the region. Billing for resources that exceed the free quota starts at that point.

**Shared gateway**

The billing entity for a shared gateway is the shared gateway instance. **Shared gateway fee = Instance fee + Data processing fee.**

|**Billing items** |Billing unit |Description |**Billing granularity** |**Listed price (pay\-as\-you\-go)**  |
|---|---|---|---|---|
|Shared gateway instance |gateway\-instance |Charged based on the shared gateway order. Fees apply regardless of whether any calls are actually made. Usage beyond the free quota is charged based on actual usage duration. |USD/unit/hour |0.192 |
|Shared gateway data processing |gateway\-data\-processed |Charged based on the total amount of request and response data processed by the gateway per hour, including both public and private network traffic. |USD/GB |Currently free of charge |

**Dedicated gateway**

The billing entity for a dedicated gateway is the gateway instance. **Dedicated gateway fee = Instance fee + Data processing fee + Tool indexing fee + Public network traffic fee.**

|**Billing items** |Billing unit |Description |**Billing granularity** |**Listed price (pay\-as\-you\-go)**  |
|---|---|---|---|---|
|Dedicated gateway instance |gateway\-instance |Charged based on the selected dedicated gateway specification. A fixed fee that does not vary with actual request volume. |USD/unit/hour |For detailed listed prices, see "**Dedicated gateway instance pricing**" below. |
|Public network traffic |gateway\-traffic |Charged based on public network client response traffic. |USD/GB |0.081 |
|Data processing |gateway\-data\-processed |Charged based on the total amount of request and response data processed by the gateway per hour, including both public and private network traffic. |USD/GB |0.006 |
|Tool indexing |gateway\-mcptoolset\-tool\-index |Charged only when semantic retrieval is used in the MCP toolset. Billing is based on the maximum number of tool indexes within the hour. |USD/10,000 indexes/hour |0.0027 |

**Dedicated gateway instance pricing**

|**Specifications** |**QPS** |**Client connections** |**Pay\-as\-you\-go (USD/unit/hour)**  |
|---|---|---|---|
|small_x1 |1,500 |20,000 |1.51 |
|small_x2 |3,000 |40,000 |2.88 |
|small_x4 |6,000 |80,000 |5.47 |
|medium_x1 |12,000 |160,000 |10.71 |
|medium_x2 |24,000 |320,000 |21 |
|large_x1 |48,000 |640,000 |40.32 |
|large_x2 |96,000 |1,280,000 |80.64 |
|large_x4 |192,000 |2,560,000 |161.27 |

> **tip**

> When the MCP toolset invokes the associated MCP service, each tool call is counted once on the toolset side and once on the MCP service side. Therefore, in dedicated gateway mode, the request QPS on the gateway side is twice the tool call QPS. For example, if the tool call QPS is 10, the QPS counted by the dedicated gateway is 20. In addition, when the toolset periodically connects to the MCP service to obtain the latest tool information, the number of requests generated is also included in the corresponding MCP service usage. For detailed rules on MCP request counting, see[MCP request counting rules](https://docs.byteplus.com/en/docs/agentkit/MCP_request_counting_rules).

## Formula

The following formulas apply to the Pay\-as\-you\-go billing method.

* **vCPU/memory fee** = actual usage per second × unit price

* **Internet traffic fee** = downstream traffic (GB) × unit price

* **Shared gateway instance fee** = Usage hours × Unit price

* **Dedicated gateway instance fee** = Instance specification unit price × Usage duration (hours)

* **Data processing fee** = Data processed (GB) × Unit price

* **Tool indexing fee** = Index count (per 10,000) × Usage duration (hours) × Unit price

## Fee calculation example

### Example 1: Existing runtime resource, no gateway instance created

Mr. Wang created a runtime in shared gateway mode in the China (Beijing) region in June 2026, with a specification of 2 vCPU/4 GB. The runtime ran continuously for 24 hours with no public network traffic during this period.

The total fee for that day was **USD 4.32**. The billing breakdown is as follows:

|**Actions** |Billing items |**Unit price** |Metered usage |**Fee** |
|---|---|---|---|---|
|Created one agent runtime with a specification of 2 vCPU/4 GB |Runtime CPU |USD 0.000019/vCPU/second |2 vCPU |USD 3.2832 |
||Runtime memory |0.000003 USD/GB/second |4 GB |1.0368 USD |

### Example 2: Shared gateway (runtime)

Mr. Wang created a runtime in shared gateway mode in the China (Beijing) region in September 2026, with a specification of 2 vCPU/4 GB. The runtime ran continuously for 24 hours and generated approximately 5 GB of public network traffic that day.

The total fee for that day was **USD 18.65**. The billing breakdown is as follows:

|**Actions** |Billing items |**Unit price** |Metered usage |**Fee** |
|---|---|---|---|---|
|Created one agent runtime with a specification of 2 vCPU/4 GB |Runtime CPU |USD 0.000019/vCPU/second |2 vCPU |USD 3.2832 |
||Runtime memory |0.000003 USD/GB/second |4 GB |1.0368 USD |
|5 GB of runtime public network outbound traffic per hour |Public network traffic |USD 0.081/GB |5 GB |USD 9.72 |
|Created one runtime shared gateway instance |Shared gateway instance |USD 0.192/unit/hour |1 |USD 4.608 |
||Data processing fee |Currently free of charge |Not involved |USD 0 |

### Example 3: Dedicated gateway (runtime + MCP)

Mr. Wang created one **runtime dedicated gateway** and one **MCP dedicated gateway** in the China (Beijing) region in September 2026, both with a specification of **small_x1**. The runtime dedicated gateway hosted one runtime with a specification of **2 vCPU/4 GB**. The MCP dedicated gateway hosted one MCP service in deployment mode (**1 vCPU/2 GB**), associated with one MCP toolset with semantic retrieval enabled.

All of the above resources ran continuously for 24 hours. During this period, the runtime generated approximately 3 GB of public network client response traffic per hour; the MCP dedicated gateway generated approximately 5 GB of public network client response traffic per hour; the MCP gateway processed approximately 8 GB of request and response data per hour; and the peak tool index count for semantic retrieval was 100,000.

The total fee for that day was **USD 96.312**. The billing breakdown is as follows:

|**Actions** |**Related billing items** |**Unit price** |**Metered usage** |**Fee** |
|---|---|---|---|---|
|Created one small_x1 runtime dedicated gateway instance |Dedicated gateway instance |USD 1.51/unit/ hour |1 |USD 36.24 |
|Created one small_x1 MCP dedicated gateway instance |Dedicated gateway instance |USD 1.51/unit/ hour |1 |USD 36.24 |
|Created one agent runtime with a specification of 2 vCPU/4 GB |Runtime CPU |USD 0.000019/vCPU/second |2 vCPU |USD 3.2832 |
||Runtime memory |0.000003 USD/GB/second |4 GB |1.0368 USD |
|Created one MCP service (deployment mode) with a specification of 1 vCPU/2 GB |MCP CPU |USD 0.000019/vCPU/second |1 vCPU |USD 1.6416 |
||MCP memory |0.000003 USD/GB/second |2 GB |USD 0.5184 |
|3 GB of runtime public network client response traffic per hour |Public network traffic |USD 0.081/GB |3 GB |USD 5.832 |
|5 GB of gateway public network client response traffic per hour |Public network traffic |USD 0.081/GB |5 GB |USD 9.72 |
|8 GB of request and response data per hour |Data processing |USD 0.006/GB |8 GB |USD 1.152 |
|Peak tool index count of 100,000 per hour |Tool indexing |USD 0.0027/10,000 units/hour |100,000 |USD 0.648 |

## Related cloud services

Based on the actual scenario in which you build agent applications, the following cloud services may also be involved. These cloud services are independent of the core billing items of AgentKit and are billed based on their corresponding product pricing. For details, see the documentation for each product.

|**Cloud service** |**Document link** |
|---|---|
|ModelArk |[Model service billing instructions](https://ark.volcengine.com/region:cn-beijing/docs/ark/model-service-pricing?lang=zh) |
|Application Performance Management Plus |[APMPlus billing instructions](https://docs.byteplus.com/en/docs/apmplus/Product_billing) |
|Torch Log Service |[TLS billing instructions](https://docs.byteplus.com/en/docs/tls/billable_items) |
|Agent identity and permission management platform |[Billing instructions for agent identity and permission management platform](https://docs.byteplus.com/en/docs/identity/Billing?lang=en) |
|Viking memory |[Viking memory billing instructions](https://docs.byteplus.com/en/docs/VikingDB/Billing_of_VikingMem) |
|Viking knowledge base |[Viking knowledge base billing instructions](https://docs.byteplus.com/en/docs/RAG_Cloud/Knowledge_Base_Billing) |
|LLM Application Firewall |[LLM Application Firewall billing instructions](https://docs.byteplus.com/en/docs/LLM-Application-Firewall/billing_model_and_pricing_details) |
|Torch Object Storage |[TOS billing instructions](https://docs.byteplus.com/en/docs/tos/docs-product-billing?lang=en) |
|CR |[CR billing instructions](https://docs.byteplus.com/en/docs/cr/billing-overview) |
|Code Pipeline |[Code Pipeline billing instructions](https://docs.byteplus.com/en/docs/cp/Pipeline_run_duration?lang=en) |
