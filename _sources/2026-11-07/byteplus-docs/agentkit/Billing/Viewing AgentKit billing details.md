---
title: "Viewing AgentKit billing details"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Viewing_AgentKit_billing_details"
---

By querying the bills of AgentKit and its associated cloud products, you can review charge details promptly and make better business decisions from a cost allocation perspective. This topic does not cover unit prices, discount rules, or billing settlement cycles. For related information, refer to the billing documentation of each product.

> **warning**

> **Stopping the runtime does not stop all related charges.** Resources such as model calls, logs and indexes, TOS, images, memory, and knowledge bases may be billed independently by other cloud products. To stop the related charges, use the product, billing item, and resource identifier shown in the bill to go to the corresponding product and stop or release the resources.

## Application scenarios

This topic applies to the following scenarios:

* View the charges and usage generated in AgentKit within a specified billing period.

* Locate billed resources by instance ID, split item ID, project, or tag.

* Troubleshoot why charges are still displayed after the runtime is stopped.

* Distinguish AgentKit native charges from charges of associated cloud products such as models, logs, and storage.

## Prerequisites

* The current account has permission to view bills in the Billing center.

* To query charges for an enterprise organization or other accounts, make sure the current account has view permission for the corresponding bill scope.

* To locate associated resources from a bill, make sure the current account has resource\-view permission for the corresponding cloud product.

## View AgentKit charges

This topic uses ** Billing item (recommended) ** dimension for filtering.

1. Log in to the [BytePlus console](https://console.byteplus.com/home).

2. Go to [Billing center > Bill management > Bill details](https://console.byteplus.com/finance/bill/detail).

3. Select the "Bill details" tab.

4. Set **Billing cycle** and set **Product** to **AgentKit**.

5. Select the **configuration name** values based on your query target, and check the usage time, instance, usage, and amount due.

   |Configuration name |Description |
   |---|---|
   |**Runtime call** |Charges incurred during runtime usage. |
   |**Tool calling** |Charges for using sandbox templates. |
   |**MCP service call** |Charges for using MCP services. |
   |**MCP toolset call** |Charges for using MCP toolsets. |
   |**Shared gateway (by hour)**  |Charges incurred for using shared gateway resources. |
   |**Gateway instance (by hour)**  |Charges for using dedicated gateway resources. |

6. Record the instance ID, instance name, owner account, project, tags, and split item ID to locate the specific resource.

   > **tip**

   * > For further bill analysis, click Download in the upper\-right corner of the list to export the current bill locally.

   * > When using AgentKit involves calls to other cloud products, charges are billed independently on the corresponding cloud product side. When querying, switch the product filter according to the product actually used.

## View charges of associated cloud products

When AgentKit calls capabilities such as models, logs, storage, images, memory, or knowledge bases, charges are billed independently on the corresponding cloud product side. The following table lists common charge sources, such as model calls, logs and indexes, object and attachment storage, image storage, memory, and knowledge bases, to illustrate the troubleshooting approach. The table does not list all cloud products associated with AgentKit or all billing items. The actual scope depends on the models, tools, plugins, data sources, and other external services used by the agent. When querying, refer to the actual call path of your business and the product and configuration names shown on the bill. Filtering AgentKit only may not display all associated charges.

|**Charge source** |**Bill filter** |**Information to verify first** |
|---|---|---|
|Model call |Corresponding model product |Caller, model name, token usage, and consumption time. |
|Logs and indexes |Torch Log Service (TLS) |Log topic, index, storage amount, and retention time. |
|Object and attachment storage |Torch Object Storage (TOS) |Bucket, object, artifact, attachment, and split item ID. |
|Image storage |Container Registry (CR) |Instance count, image count, and image storage volume. |
|Memory or knowledge base |Corresponding product |The associated instances, compute resources, index, and storage data. |

## Description of key bill fields

The following data is used only to illustrate field meanings and does not represent real resources, usage, or charges. Product, instance, billing item, usage time, usage, and amount due together describe which resource generated how much cost for what usage at what time.

|**Field** |**Sample value** |**Explanation** |
|---|---|---|
|Billing cycle |2026\-09 |The settlement month to which this bill belongs. |
|Business billing period |2026\-09 |The business month in which the resource actually incurred consumption. |
|Product |AgentKit |The product that generated the charges. When a component is billed independently, the corresponding cloud product name is displayed. |
|Billing method |Pay\-as\-you\-go |Billed on a pay\-as\-you\-go basis according to actual usage. |
|Instance ID/Instance name |runtime\-xxxx |The identifier of the billing instance that generated the charges. |
|Billing items |Agent runtime CPU |Indicates which type of resource or operation generated the charges. |
|Consumption time |2026\-09\-24 10:00～11:00 |The time range during which the usage actually occurred or was collected. The actual time granularity is subject to what is displayed in the bill. |
|Usage/Unit |7200 vCPU·seconds (example) |The actual usage billed during the settlement period and its unit of measurement. |
|Original price |0.xx USD (example) |The pre\-discount amount calculated based on the list price and usage. |
|Discount amount |0.xx USD (example) |The amount deducted by contract discounts or promotional offers. |
|Payable amount |0.xx USD (example) |The amount payable after discounts are applied. |
|Payer account |Account A |The account responsible for payment and settlement. |
|Owner account |Account B |The account that actually uses the resource and owns this charge. |
|Project/Tags |project\-agent |Used for resource ownership and internal cost allocation. |
|Split item ID |ep\-xxxx / bucket\-xxxx |An identifier used in usage\-type products to locate finer\-grained resources. |

## Determine whether the resources continue to incur charges

A new record in the bill does not necessarily mean that a resource is still being charged after release. Some products have billing delays. After a resource is released, usage incurred before the release may still be displayed. You should also compare the usage time with the time the resource was stopped or released.

1. **Confirm bill time**: Record the usage time and compare it with the time the resource was stopped or released.

2. **Check resource status**: Confirm whether the runtime, tool instance, gateway instance, or task is still running.

3. **Check persistent resources**: Confirm whether logs, indexes, objects, images, memory, or knowledge bases are still retained.

4. **Check call chains**: Confirm whether the agent runtime, tools, and MCP services are still calling models, databases, or third\-party services.

5. **Check traffic and requests**: Confirm whether there is still public outbound traffic, requests, retrieval tasks, or model calls.

6. **Check bill ownership**: Verify that the owner account, project, and tag match the target resource.

7. **Release associated resources**: Based on the product and instance identifier in the bill, go to the corresponding product to stop or release resources that are no longer needed.

   > **warning**

   > **Confirm the impact scope before deletion.** Deleting logs, objects, images, memory, or knowledge bases may make data unrecoverable and may also affect agents or services that are still using these resources. Before performing deletion, confirm resource ownership, dependencies, and data retention requirements.

8. **Check subsequent bills**: Continue to check bills during an observation period that covers the billing delay. This is to confirm there is no unexpected new usage with usage time later than the resource release time.

## Common billing items and resource mapping

|**Billing items in the bill** |**Resources or operations to check first** |
|---|---|
|Agent runtime CPU or memory |Runtime status, instance specification, and minimum instance count configuration. |
|Tool CPU or memory |Whether the cloud tool instance is still running. |
|Gateway CPU or memory |Whether the gateway instance is still running. |
|Gateway service request count/Retrieval task count |Whether there are callers requesting the gateway or performing toolset retrieval. |
|Gateway tool index count |Whether the tool index still exists. |
|Public network traffic |Whether the runtime, tool, or gateway is still generating outbound traffic. |
|Model token |Whether the agent, tool, evaluator, or memory extraction process still involves model calling. |
|Log and index storage |Whether the log topic, index, and stored data in TLS still exist. |
|TOS capacity |Whether objects, artifacts, or attachments remain in the TOS bucket. |
|Image storage or instance |Whether the Container Registry (CR) instance and image data still exist. |
|Sessions, memory, or knowledge base resources |Whether only sessions or documents were deleted while the corresponding database resources were not. |

##
