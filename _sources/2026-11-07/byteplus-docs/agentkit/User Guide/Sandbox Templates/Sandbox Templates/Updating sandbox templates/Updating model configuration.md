---
title: "Updating model configuration"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Updating_model_configuration_tool"
---

The model configuration of a sandbox template determines the large language model used by agents within instances. You can perform this operation when you need to switch models (for example, from doubao\-seed\-2.0\-pro to another model version) to meet different inference capability requirements. This topic describes how to update the model configuration.

## Instructions

Only the following sandbox templates types support updating the model configuration. Other sandbox template types do not support this operation.

* **ArkClaw Sandbox**

* **Hermes Sandbox**

* **Skills Sandbox**

* **Code Sandbox**

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Templates".

3. In the "Sandbox templates" list, click the target template name. In the "Model and skill configuration" section of the "Configuration information" tab, find the "Agent model" setting and click its ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a5bf12c121e79c81297d621ca1c2dd4.png)****.

4. In the dialog box, select the target model and click "Confirm".

5. After a successful update, go to the "Configuration information" tab and confirm that the agent model has been updated to the target model in the **Model** **and skill ** **configuration** section. Model configuration updates do not apply to existing instances. Newly created instances will use the new model.
