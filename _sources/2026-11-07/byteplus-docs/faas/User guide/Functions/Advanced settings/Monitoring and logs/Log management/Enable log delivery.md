---
title: "Enable log delivery"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Enable_log_delivery"
---

The Function Service (FaaS) connects to [Torch Log Service](https://docs.byteplus.com/en/docs/tls/What_is_TLS), providing log management features. You only need to enable the log feature when creating a function to query the function running logs in the Function Service console. This article introduces how to enable log delivery.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please be cautious when switching the delivered log project and log topic! After the switch, you will no longer be able to query the historical logs delivered to the original project and topic from the Function Service side.</div>


<span id="prerequisites"></span>
## Prerequisites

If you need to use a custom log set to deliver function logs, please ensure that the Torch Log Service is activated, and a log set has been created. For detailed actions, refer to [Manage a project](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Manage a topic](https://docs.byteplus.com/en/docs/tls/Managing_topics).

<span id="procedure"></span>
## Procedure

Supports the following two methods to enable log delivery:


* Function not created

   When creating a function, in the **Advanced Settings** area, enable the logging feature to deliver the function's call logs to TLS. For specific actions, refer to [Create Function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection).

* Function created (logging not enabled)

   1. Log in to the [Function Service console](https://console.byteplus.com/vefaas), and on the top navigation bar, select the region your business is located in.

   2. In the function list, click the target function name to enter the current function configuration page.

   3. In the function configuration area, click **Edit**. On the Edit Function Configuration page, enable the logging feature to deliver the function's call logs to TLS.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">veFaaS offers two log delivery methods: default log set and custom log set.</div>



* <div data-tips="true" data-tips-type="tip">Default log set</div>


   <div data-tips="true" data-tips-type="tip">Select the default log set, and the logs will be delivered to the specific log project <code>tls-vefaas</code> under the log topic <code>tls-vefaas-logstore</code>.   </div>
   

* <div data-tips="true" data-tips-type="tip">Custom log set</div>


   <div data-tips="true" data-tips-type="tip">Select a custom log set to direct logs to a log topic within a log project specified by the user.   </div>
