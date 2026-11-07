---
title: "Updating execution timeout"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/update-execution-timeout"
---

By configuring the execution timeout appropriately, you can achieve a balance between the success rate of long\-running requests and the resource release efficiency for abnormal requests. This topic describes how to adjust the maximum execution duration for a single synchronous request in the AgentKit agent runtime.

## Typical scenarios

|**Scenarios** |**Typical signals** |**Recommendation** |
|---|---|---|
|Increase the execution timeout |* The business logic includes complex workflows or multi\-turn tool calls.<br><br>* Requests need to perform large\-scale knowledge base retrieval or long text generation.<br><br>* Normal business requests are occasionally interrupted because they reach the timeout duration. |When you increase the timeout, we recommend that you also monitor instance resource usage and the timeout limits of downstream models, tools, or retrieval services. When you increase the timeout, we recommend that you also monitor instance resource usage and the timeout limits of downstream models, tools, or retrieval services. |
|Decrease the execution timeout |* Some requests enter an abnormal infinite loop or remain blocked for an extended period.<br><br>* You want failed requests to return sooner and instance resources to be released in a timely manner.<br><br>* Typically, business requests are completed quickly, so a long wait time is not required. |You can decrease the execution timeout as appropriate to terminate abnormal requests in a timely manner and release resources. Before decreasing the timeout, we recommend that you confirm the P99 execution duration of normal business requests to avoid terminating valid requests by mistake. |

## Usage notes

* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. Switch the version to Latest before you perform the operation.

* **Effective condition**: After you modify the execution timeout, the new configuration takes effect only after republishing, and a new version is generated simultaneously. Once published, the latest version is automatically used for subsequent agent runtime calls.

## Prerequisites

[You have created an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the "Basic information" section of the **Configuration information ** tab, locate **Execution timeout** and click ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png).

   > **warning**

   > In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.

5. In the dialog box that appears, enter a new value for the execution timeout duration (ranging from 1 to 3600).

   > For related configuration information, see [Creating runtimes (console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

6. Click "Confirm" to save the draft configuration.

7. Publish the agent runtime to apply the configuration.

   * Preview mode: Click "Save" to save the configuration. After you save the configuration, you can test the Latest version or [publish it as an official version](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes).

   * Non\-preview mode: After updating the configuration, click "Release" in the upper\-right corner of the page. The new configuration takes effect only after republishing.

## What to do next

* After publishing, you can view the new version record generated in "**Version management" \> "Release history"** , and confirm whether new calls use the latest version.

* To roll back, switch to a historical version in "**Version management**".
