---
title: "Enabling logs"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Enabling_logs"
---

**AgentKit** is integrated with BytePlus [Torch Log Service (TLS) ](https://docs.byteplus.com/en/docs/tls/What_is_TLS)to provide unified log management capabilities. After you enable the log service, you can view the runtime logs of each resource directly in the ** AgentKit console**. Viewing these logs helps you locate call exceptions and supports troubleshooting and business operations analysis.

<span id="tXq01xva"></span>
## Billing

After you enable logs, the platform automatically activates TLS. The log service incurs charges based on the TLS billing rules. Make sure that you review the billing information before use. For details about the billing rules, refer to [TLS billing overview](https://docs.byteplus.com/en/docs/tls/billable_items?lang=en).

<span id="9PI7vvjW"></span>
## Usage notes

Resources that support the log service: agent runtimes, tools, MCP services, gateway instances, and model services.

<span id="GcFvpQQn"></span>
## Enable logs

<span id="5XBjVuyq"></span>
### Enable logs during resource creation

Configure the log service when you create a resource. Runtime logs are then generated and delivered after the resource goes online.


1. Log in the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select the target resource or component, for example, "Agent runtime".

3. Navigate to the creation page of the target resource and enable logs ("Observability service" or "Torch Log Service") as needed.

   
   |Resource item |How to enable |Related documents |
   |---|---|---|
   |Agent Runtime |When you create an ** agent runtime ** or **sandbox template**, in the ** Advanced configuration \- Observability service** section of the creation page, select the "Enable" checkbox to enable logs for the resource.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, the observability service (sandbox template logs) cannot be enabled when the sandbox template type is<strong> OpenClaw</strong>.</div><br> |[Creating agent runtimes](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console) |
   |Sandbox templates ||[Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) |
   |MCP service |When you create **an MCP service**, in the **Advanced configuration \- Torch Log Service** section of the creation page, select the "Enable" checkbox to enable logs for the resource.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For an MCP service, you can enable TLS only when the creation method is <strong>Deploy MCP service</strong>.</div><br> |[Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services) |
   |Gateway instances |When you create a gateway instance, in the **Observability configuration \- Torch Log Service** section of the creation page, select the "Enable" checkbox to enable logs for the resource.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Logs cannot be enabled directly for the <strong>model service</strong>. Instead, enable TLS for the<strong> gateway instance associated with the model service</strong>. After you enable TLS for the gateway instance, the model service runtime logs are collected.</div><br> |[Creating gateway instances](https://docs.byteplus.com/en/docs/agentkit/Creating_gateway_instances?lang=en) |
   |Model service |||
   


<span id="9oisZB2f"></span>
### Enable logs for existing resources (created without logs enabled)

For existing resources created ** without the "Observability service"**  or ** "Torch Log Service"**  enabled, you can enable the service manually on the resource details page.


1. Log in the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select the target resource or component, for example, "Agent runtime".

3. On the resource list page, click the name of the target resource to enter the details page, and then enable logs ("Observability service" or "Torch Log Service") as needed.

   
   |Resource item |How to enable |
   |---|---|
   |Agent Runtime |1. In the **Observability service** section on the configuration information page of the target **agent runtime ** or **sandbox template**, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png) </span>.<br><br>   2. Check "Enable" and then click "Confirm" to enable logs for the resource. |
   |Sandbox templates ||
   |MCP services |1. In the ** Torch Log Service** section on the basic information page of the target ** MCP service**, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png) </span>.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For an MCP service, you can enable TLS only when the creation method is <strong>Deploy MCP service</strong>.   </div><br>   <br><br>   2. Check "Enable" and then click "Confirm" to enable logs for the resource. |
   |Gateway instances |1. In the **Torch Log Service ** section on the configuration information page of the target **gateway instance**, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png) </span>.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Logs cannot be enabled directly for the <strong>model service</strong>. Instead, <strong>enable TLS for the gateway instance associated with the model service</strong>. After you enable TLS for the gateway instance, the model service runtime logs are collected.   </div><br>   <br><br>   2. Check "Enable", select the[ log project](https://docs.byteplus.com/en/docs/tls/Managing_projects?lang=en) to which logs are delivered, and then click "Confirm" to enable log delivery for the target resource.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no existing log project meets your business requirements, or if you have not created a log project, click "Create project" to create one. For details, refer to<a href="https://docs.byteplus.com/en/docs/tls/Managing_projects?lang=en"> Log projects</a>.   </div><br>    |
   |Model service ||
