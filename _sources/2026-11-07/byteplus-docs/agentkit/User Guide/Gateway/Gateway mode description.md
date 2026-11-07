---
title: "Gateway mode description"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Gateway_modes_and_MCP_request_counting_rules"
---

In AgentKit, you can centrally manage external access to MCP services through gateways. Based on your business scenarios and requirements, you can select the gateway mode to associate with resources. This topic describes the feature differences between the gateway modes.

## Gateway mode overview

Gateways are available in two modes: dedicated gateway and shared gateway.

* **Dedicated gateway: ** An instance has exclusive resource capacity and supports both public and private network access. The instance can connect to model services, MCP, and agent runtimes. This mode provides a unified entry point and stable performance for instances.

* **Shared gateway:**  This mode is suitable for scenarios such as quick validation and proof\-of\-concept (POC). Both the number of resources that you can create and the maximum performance are restricted.

### Shared gateway

A shared gateway is the gateway resource that the platform provides by default. You do not need to create it separately. The first time you use the shared gateway mode in a region to create an agent runtime, MCP service, or MCP toolset, the system automatically places an order for a shared gateway instance of the corresponding type. After the number of resources of the same type exceeds the free quota, fees are incurred. You can view the number of associated services and the billing status of each type of shared gateway in the current region. For more information, see[ Viewing shared gateway information](https://docs.byteplus.com/en/docs/agentkit/Viewing_shared_gateway_information).

### Dedicated gateway

A dedicated gateway provides a dedicated gateway instance for your resources. It is suitable for scenarios that require stricter network isolation, observability monitoring, or a higher QPS of the gateway specification. Before you use a dedicated gateway, first [create a dedicated gateway instance ](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances)and select the corresponding dedicated gateway when you create a resource.

**Key features**

* Exclusive resource capacity, stable performance, and isolation from other users

* Provides independent monitoring data at the gateway level, which allows you to view metrics such as the number of requests and QPS

* Supports configuring the maximum QPS of a gateway specification and provides multiple specifications to choose from

* Supports both public network access and private network access

**Gateway specification**

|**Specifications** |**QPS** |**Client connections** |The total number of MCP services and toolsets that can be associated |The total number of agent runtimes that can be associated |
|---|---|---|---|---|
|small_x1 |1,500 |20,000 |500 |500 |
|small_x2 |3,000 |40,000 |500 |500 |
|small_x4 |6,000 |80,000 |500 |500 |
|medium_x1 |12,000 |160,000 |1,000 |1,000 |
|medium_x2 |24,000 |320,000 |1,000 |1,000 |
|large_x1 |48,000 |640,000 |2,000 |2,000 |
|large_x2 |96,000 |1,280,000 |2,000 |2,000 |
|large_x4 |192,000 |2,560,000 |2,000 |2,000 |

## Recommendations for choosing a gateway mode

If your business requires unified management of access entry points, unified monitoring, or independent billing, we recommend that you choose the ** dedicated gateway**. If you only need to validate the integration process for a single tool or model, complete the quick start of the corresponding feature first, and then migrate to a gateway instance based on your production requirements.

* **For formal production or when there are requirements for resource isolation or dedicated capacity, ** choose ** dedicated gateway**.

* **For fast verification, development testing, or a lightweight trial, ** choose **shared gateway.**

|**Dimension** |**Dedicated gateway** |**Shared gateway** |
|---|---|---|
|Application scenarios |Core production businesses and scenarios with high concurrency, isolation, and stability requirements. |Proof of concept (PoC), development and testing, low\-traffic validation, and lightweight trials. |
|Resource type |Visible, manageable, and independent resource instances. |Platform\-shared resource. |
|Resource isolation |Dedicated resources with stronger isolation. |Shares underlying gateway resources with other tenants. |
|Performance assurance |Designed for production scenarios, it delivers higher performance guarantees and more explicit SLA commitments. |No production\-grade SLA commitment. |
|Quantity and performance limits |Runs at the capacity of the selected specification tier. Capacity planning can be performed based on request volume, the number of connections, and the number of resources. |Subject to platform\-preset limits on quantity, performance, and capabilities and not suitable for long\-term production workloads. |
|Billing rules |* As an independent billable item, it charges instance fees and data processing fees based on specifications and usage.<br><br>* **Billing formula**: Dedicated gateway fee = Instance fee + Data processing fee + Tool indexing fee + Public network traffic fee. For more information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items). |* Shared gateway\-related fees are charged.<br><br>* **Billing formula**: Shared gateway fees = Instance fee + Data processing fee. For more information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).<br><br>* **Free quota**<br><br>   * **Agent runtime**: 2 free runtimes per account per region. Additional agent runtimes are billed at the shared gateway instance rate.<br><br>   * **MCP services and MCP toolsets**: 2 free in total per account per region. Additional resources are billed at the shared gateway instance rate. |

> **warning**

> Existing resources (created before August 31, 2026) are upgraded to**shared gateway**mode by default, but no shared gateway order is created automatically. Even if the free quota is already exceeded, fees are not incurred immediately. The system automatically places an order for a shared gateway instance only when you create a resource (an MCP service, MCP toolset, or agent runtime) in the region. Billing for resources that exceed the free quota starts at that point.
