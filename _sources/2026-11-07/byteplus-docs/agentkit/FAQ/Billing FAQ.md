---
title: "Billing FAQ"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Billing_FAQ"
---

This topic is for AgentKit users and provides answers to frequently asked questions about billing sources, bill queries, how to stop billing, refunds, and handling of overdue payments.

## Related entry points

* [Billing center > Bill details](https://console.byteplus.com/finance/bill/detail): Query hourly, daily, and monthly consumption details.

* [AgentKit console](https://console.byteplus.com/agentkit): Check agent runtime, tool, MCP, and gateway resources.

* [AgentKit billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items): View billing items, unit prices, and how fees are calculated.

* [AgentKit billing method](https://docs.byteplus.com/en/docs/agentkit/Billing_method): View the billing start and end times and the settlement cycle.

* [Submit an AgentKit ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000240): Request an account\-level billing review.

## Understand billing sources

By first confirming the AgentKit billing model and billing scope, you can quickly determine whether a bill originates from resources that are still running or retained.

### How is AgentKit billed?

**AgentKit uses the pay\-as\-you\-go (postpaid) billing model.**  The system aggregates the actual usage of each billing item on an hourly basis and automatically deducts the amount from your available account balance. At each hour mark, the usage of the previous hour is settled. You can view hourly, daily, or monthly details in [Billing center > Bill details](https://console.byteplus.com/finance/bill/detail). For instructions on querying bills, see [Bills and details](https://docs.byteplus.com/en/docs/agentkit/Billing_method).

### What are the main types of fees that AgentKit incurs?

**Fees mainly come from agent runtimes, tools, MCP services or MCP toolsets, model services, and gateway instances. Each resource is metered independently and billed separately.**  For the specific billing items and prices, see [Billing instructions](https://docs.byteplus.com/en/docs/agentkit/Billing_items).

### Why are vCPU or memory fees still incurred when no agent is called?

**As long as a billable instance remains running, resource fees may continue to be incurred.**  If the minimum number of instances for an agent runtime is greater than 0, the platform retains that number of instances continuously. Even if there is no request load, you are billed based on the actual retained vCPU and memory usage. First, confirm the instance ID in the bill details, then go to the [AgentKit agent runtime page](https://console.byteplus.com/agentkit) to find the target instance and check its status and minimum number of instances.

### Can Agent Plan, Coding Plan, or complimentary model call quotas be used to offset AgentKit fees?

**You cannot use these quotas to offset by default.**  Model call quotas (tokens) provided through Agent Plan, Coding Plan, or promotional activities are mainly used to offset the model call volume stipulated in the corresponding plan. AgentKit runtimes, tools, MCP services, and gateways are independent billing resources. Fees are offset according to the corresponding rules only when a plan or promotional activity explicitly includes covered AgentKit billing items.

### When a model is called in AgentKit, are the model fees calculated separately?

**Yes.**  AgentKit resource fees and model call fees are different billing items: the former covers resources such as runtimes, sandbox templates, MCP, and gateways, while the latter is settled according to the billing rules of the selected model. When you review bills, filter products related to AgentKit and model services separately.

## Locate deduction details

If you do not know what is being charged, first locate the product, billing item, and instance in the bill, and then decide whether to stop the resource or submit a review request.

### How can I confirm which service is continuously incurring deductions?

**Go to Billing center \> Bill details, filter by billing period, and view the product name, billing item, instance identifier (instance ID), and consumption time.**  If you first see the deduction in the[ revenue and expense](https://console.byteplus.com/finance/fund/income-expend) details, you can use the business transaction number to locate the bill. "Being billed" means the bill is still being settled. You can go to [Bill details ](https://console.byteplus.com/finance/bill/detail)to view it. After confirming the instance ID, go to the corresponding AgentKit resource page to verify the status.

### Does the "by day" date in the bill indicate when the service occurred?

 **"By day" is mainly a daily\-level aggregated view. To verify the actual usage time, check the hourly\-level details.**  AgentKit uses an hourly basic billing cycle and settles the usage of the previous hour at each hour mark. If the daily bill appears inconsistent with the resource operation time, switch to the hourly details to verify the consumption time and instance ID.

## Stop or reduce deductions

The key to stopping charges is to ensure that the actual billing resources enter the officially defined stopped billing state, rather than simply stopping calls.

### How do I stop AgentKit from continuing to incur fees?

**First, locate the billing resource in the bill details by instance ID, then follow the billing instructions for that resource to perform the stop billing operation.**

The conditions for stopping billing may differ by resource: resource\-type instances typically must be stopped or released, and dedicated gateways must be released. For shared gateways, refer to the description of the corresponding billing items. In the [AgentKit console](https://console.byteplus.com/agentkit), verify the actual status of agent runtimes, tools, MCP services, and gateways. After you complete the operation, check the hourly bill in the next billing cycle to confirm that no new usage has been incurred.

> **warning**

> **Deletion cannot be undone**. Before deletion, make sure that no tasks are running and back up any data, configurations, or images that must be retained. If you only need to reduce fees temporarily, first check whether the product supports stopping instances or setting the minimum number of instances to 0.

### Why is the bill still increasing when a resource has been shut down/deleted?

**First, compare the time of the last usage with the time the resource was stopped.**  AgentKit settles bills on an hourly basis. After you stop the operation, you may still see bills generated by prior usage; if the hourly details show that new usage continues to be generated after the stop time, you usually need to check for residual instances, unpublished configurations, and associated tools, MCP services, or gateway resources. When you submit a ticket, attach the resource ID, the time the resource was stopped, and the time of the last usage.

## Handle fee disputes and overdue payments

Fee disputes must be reviewed entry by entry against the account bill and resource records, while overdue payments can affect resource availability and data retention.

### Can AgentKit fees that were incurred unknowingly be refunded?

**Refunds are not processed automatically. Submit a ticket for review.**  The support team determines whether the request meets the processing criteria based on records of resource creation, running, usage, and notifications. The review result and the credit arrival time are subject to actual processing. First, stop the resources that are still incurring fees, and then submit the account ID, instance ID, disputed billing period, and bill details to prevent further fee accumulation.

### What do I need to provide when submitting a fee review ticket?

**At a minimum, provide the account ID, instance ID, disputed billing period, hourly bill screenshots or details, and the time the resource was stopped.**  If the issue involves "unclear how to activate the service" or "still charged after disabling", also state the resource creation source, the most recent configuration release time, and the last consumption time. Complete information helps reduce repeated confirmation.

### After an account becomes overdue, do AgentKit resources immediately stop being billed?

**No, they do not stop immediately.**  Within 24 hours after the account becomes overdue, instance resources are retained and continue to be billed. Within 24 to 168 hours, instances are shut down and stop serving requests. If the account remains overdue for 7 days, the resources are forcibly released, and the related configurations and data are permanently deleted. Issued bills still need to be settled based on actual usage. For details, see [Instructions on arrears](https://docs.byteplus.com/en/docs/agentkit/Instructions_on_arrears).
