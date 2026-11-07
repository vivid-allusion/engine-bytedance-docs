---
title: "Enabling/Disabling observability service"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Enabling_or_Disabling_observability_service"
---

After observability is enabled, integrated observability services such as metrics, traces, and logs will be provided, and an observability dashboard will be generated. This topic describes how to enable or disable the observability service.

<span id="x7ijReuo"></span>
## Usage notes


* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. In non\-preview mode, you do not need to specify a version and can update directly.

* **Effective conditions**: After you enable or disable the observability service, the new configuration takes effect only after **republishing**, and a new version is generated simultaneously. Once published, the latest version is automatically used for subsequent agent runtime calls.


<span id="3zpTkJvx"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the "Basic information" section of the **Configuration information** tab, locate **Observability service** and click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png) </span> **.** 

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.   </div>
   

5. In the displayed dialog box, enable or disable the Observability service.

6. Click the "Confirm" button.

8. Publish the agent runtime to apply the new configuration:

   * Preview mode: Click "Save" to save the configuration. After you save the configuration, you can test the Latest version or[ publish it as an official version](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes).

   * Non\-preview mode: After updating the configuration, click "Release" in the upper\-right corner of the page. The new configuration takes effect only after republishing.


<span id="ICkrU96f"></span>
## Related documents


* Once the observability service is enabled, you can monitor end\-to\-end key metrics from three dimensions: runtime, session, and Trace, providing real\-time insights into the performance, accuracy, and reliability of your agent. For details, refer to [Observability](https://docs.byteplus.com/en/docs/agentkit/Observability_overview).

* Once the observability service is enabled, the runtime logs of the agent are automatically delivered to the log topic `apmplus-server-log` under the AgentKit\-dedicated log project `apmplus-server`. You can query the runtime logs of each resource in real time. For details, refer to [Viewing logs](https://docs.byteplus.com/en/docs/agentkit/Viewing_logs).
