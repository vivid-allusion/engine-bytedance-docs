---
title: "Viewing shared gateway information"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_shared_gateway_information"
---

When you select the **shared gateway mode ** for the first time in a region to create an agent runtime, model service, MCP service, or MCP toolset, the system automatically places an order for one shared gateway for each resource type. This topic describes how to view shared gateway information.

## Billing

A free quota is provided for shared gateways ** per account and per region**. If the number of resources associated with a shared gateway exceeds a specific quantity, fees are incurred. For more information about billing rules, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_method).

* Agent runtime: **2 ** free runtimes per account per region. Additional agent runtimes are billed at the shared gateway instance rate.

* MCP services and MCP toolsets: ** 2 free in total ** per account per region. Additional resources are billed at the shared gateway instance rate.

* Existing resources:

   * Existing resources (created before August 31, 2026) are upgraded to shared gateway mode by default, but **no shared gateway order is created automatically**. No fees are incurred immediately, even if the free quota has already been exceeded.

   * The system automatically places an order for a shared gateway instance only when you ** create ** a resource (an MCP service, MCP toolset, or runtime) in the region. Billing for resources that exceed the free quota starts at that point.

## Description

In shared gateway mode, QPS, traffic, and other usage metrics are limited. This mode is recommended only for proof\-of\-concept (PoC), development, and testing scenarios, where you can quickly evaluate capabilities and try out the service at low cost. For production environments, we recommend dedicated gateway mode. For more information, see [Creating dedicated gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Gateway \> Gateway overview". On the Shared gateway tab, view information about shared gateways, such as the ID, number of internal services, and current billing status.

3. Hover over the number of internal services for a gateway to view the internal service resources.
