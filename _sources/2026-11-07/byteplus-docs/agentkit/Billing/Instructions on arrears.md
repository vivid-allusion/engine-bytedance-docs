---
title: "Instructions on arrears"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Instructions_on_arrears"
---

This topic describes the impact of arrears on instances and associated resources, as well as the procedures for handling arrears, to help you manage your resources. 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When your account is in arrears, the platform sends a notification by SMS, email, or internal message based on the <a href="https://console.byteplus.com/message/setting">notification method</a> you specify to remind you of the unpaid fees.</div>


<span id="T6Es8wFS"></span>
## Impact of arrears

When your account is in arrears, your resources will enter a retention period, with usage being limited. Once the retention period expires, your resources will be forcibly reclaimed and cannot be recovered. To ensure uninterrupted use of AgentKit resources,[ settle overdue bills](https://docs.byteplus.com/en/docs/347/118713#awVXtoPc) within the specified period (before the resources are forcibly reclaimed).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">While your account is in arrears, you cannot create agent runtimes, tool instances, or MCP services.</div>


Once your account is in arrears, the running and billing status of AgentKit is shown in the chart below.

**Instructions on resource release due to arrears**


* Shutdown time: 24 hours after your account is in arrears.

* Release time: 168 hours (7 days) after your account is in arrears.


Regardless of whether your instance resources are suspended or released, you are required to pay the generated outstanding bills.

**Instructions on resource status during arrears**


|Resource type |Within 24 hours after arrears |Within 24 to 168 hours after arrears |7 days (168 hours) after arrears |
|---|---|---|---|
|Agent Runtime |Instance resources are retained, and billing continues. |The instance is stopped, the resources are retained, but service is no longer provided. |The resources will be forcibly released, and all associated configurations and data will be permanently deleted and cannot be recovered. |
|Tool ||||
|Gateway ||||


<span id="B6HNN1Iw"></span>
## Viewing outstanding amount

Go to the [Billing center - Overview](https://console.byteplus.com/finance/account-overview/) page to view the overdue amount. On this page, you can also enable the "Available balance alert". After you do this, the system will send a notification when the available balance is less than the alert threshold. 

<span id="awVXtoPc"></span>
## Bill settlement

If your account is in arrears, your instance may be stopped. To avoid interruption to your services, please recharge and settle overdue bills in a timely manner. 

After you settle overdue bills, the running status of instances will be as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Whether you renew before or after the suspension caused by arrears (24 hours after your account is in arrears), the instance status after settlement will be the same as before the arrears.</div>



|No arrears |Upon arrears |Stopped due to arrears |After recharge |
|---|---|---|---|
|In service |In service |Stopped |In service |
