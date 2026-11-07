---
title: "Updating concurrent requests per instance"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_instance_configurations"
---

By properly configuring the concurrent requests per instance, you can balance instance throughput and backend resource load. This topic describes how to adjust the request concurrency for a single AgentKit agent runtime instance.

<span id="hdXKUdmQ"></span>
## Typical scenarios


|**Scenarios** |**Typical signals** |**Recommendation** |
|---|---|---|
|Concurrency increase |* Sessions are throttled and rejected during peak hours.<br><br>* Instance CPU and memory resources still have headroom.<br><br>* Agent tasks are mainly I/O\-bound, such as waiting on large models, knowledge bases, or tool calls. |You can increase the concurrency to improve per\-instance throughput and handle more concurrent sessions. |
|Concurrency decrease |* High instance memory load.<br><br>* Occasional process crashes.<br><br>* Downstream dependencies have a concurrency limit.<br><br>* Long\-running, compute\-intensive agent sessions are common. |You can decrease the concurrency to reduce per\-instance load, protect backend resources, and improve end\-to\-end stability. If the overall traffic is insufficient, we recommend that you [add instances](https://docs.byteplus.com/en/docs/agentkit/Updating_runtime_instance_count) ** for horizontal scaling** instead of continuing to increase the per\-instance concurrency. |


<span id="Wna1DrJv"></span>
## Usage notes


* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. Switch the version to Latest before you perform the operation.

* **Effective conditions**: After you modify the concurrent requests per instance, the new configuration takes effect only after ** republishing**, and a new version is generated simultaneously. Once published, the latest version is automatically used for subsequent agent runtime calls.

* **Value range**: The concurrent requests per instance range from 10 to 1000.


<span id="g1lNNuTi"></span>
## Prerequisites

You must have [created an agent runtime in the console](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

<span id="JicBqwdh"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the "Basic information" section of the **Configuration information** tab, locate **Concurrent requests per instance** and click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png) </span>****.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.   </div>
   

5. In the dialog box that appears, enter a new value for the concurrent requests per instance (ranging from 10 to 1000).

   > For related configuration information, see [Creating runtimes (console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).   
   

6. Click "Confirm" to save the draft configuration.

7. publish the agent runtime for the new configuration to take effect.

   * Preview mode: Click "Save" to save the configuration. After you save the configuration, you can test the Latest version or[ publish it as an official version](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes).

   * Non\-preview mode: After updating the configuration, click "Release" in the upper\-right corner of the page. The new configuration takes effect only after republishing.


<span id="13gqoVN5"></span>
## What to do next


* After publishing, you can view the new version record generated in "**Version management" \> "Release history"** , and confirm whether new calls use the latest version.

* To roll back, switch to a historical version in "**Version management**".
