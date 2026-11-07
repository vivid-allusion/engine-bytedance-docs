---
title: "Updating model configuration"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_model_configuration"
---

This topic describes how to update the model configuration of an agent runtime.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Updating a model may affect the output style, capability boundaries, response latency, and call costs. After the release, we recommend that you verify key use cases first and continuously monitor core metrics, such as latency and call costs, during an observation period. The platform supports the <a href="https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes">grey release</a> feature. We recommend that you first complete verification and observe stability within a small scope, and then gradually expand the scope of impact.</div>


<span id="oc1DA5Vw"></span>
## Usage notes


* **Version requirement**: In preview mode, you can update the configuration only for the Latest version. In non\-preview mode, you do not need to specify a version and can update directly.

* **Effective conditions**: After you update the model, the new configuration takes effect only after ** republishing**, and a new version is generated simultaneously. Once published, the latest version is automatically used for subsequent agent runtime calls. [View release history](https://docs.byteplus.com/en/docs/agentkit/Viewing_release_history).


<span id="NpscBVNc"></span>
## Procedure


1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the agent runtime list, click the name of the target agent runtime.

4. In the "Model configuration" section of the **Configuration information** tab, click the "Edit" button.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In preview mode, configuration updates are supported only for the Latest version. Switch the version to Latest before you perform the operation.   </div>
   

5. In the dialog box that appears, configure the model as needed. 

   * **Model service:** 

      1. In the **Model selection** drop\-down list, switch to the **Model service** tab, select the corresponding Proxy API Key name, and then select the required model.

      2. After selecting the model, skip API Key configuration and click "Confirm".

   * **ModelArk:** 

      1. In the **Model selection** drop\-down list, switch to the **ModelArk** tab and select the required model.

      2. In the **API Key** drop\-down list, select the corresponding **API Key**, and then click the "Confirm" button.

6.  Publish the agent runtime to apply the new configuration:

   * Preview mode: Click "Save" to save the configuration. After you save the configuration, you can test the Latest version or[ publish it as an official version](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes).

   * Non\-preview mode: After updating the configuration, click "Release" in the upper\-right corner of the page. The new configuration takes effect only after republishing.
