---
title: "Configuring models for my agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_models_for_my_agents"
---

After adding sub\-agents from Agent Gallery or custom sub\-agents to ArkClaw, you can specify an inference model for each sub\-agent. This allows you to flexibly select the most suitable model based on agent roles and task characteristics to configure differentiated inference capabilities. This topic describes how to configure independent models for **sub\-agents**. For information about configuring ** the model for the primary agent**, see[ Adjusting inference models](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__?lang=en).

<span id="r8SPOvz3"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page, and select "Agent Center" in the left\-side navigation pane.

3. On the "My agents" page, click "View details" on the target agent card.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent whose Agent ID is <strong>main</strong> is the <strong>primary agent</strong>.   </div>
   

4. In the "Model" area, select the target model from the drop\-down list.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you configure custom models for different sub\-agents, note that model pools that contain API Key–required models are subject to a <strong>global uniqueness constraint</strong>:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Two or more </strong>model pools that contain API Key–required models: Only <strong>one</strong> model pool can take effect at a time (the most recently configured one prevails). Sub\-agents associated with the model pools that do not take effect will fail to run. We recommend that you associate all sub\-agents with the same model pool that contains the API Key–required models.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>At most one</strong> model pool that contains API Key–required models: This pool coexists with any pools that contain no API Key–required models, without affecting one another.   </div>
   

   5. After the configuration, click the "Update" button for the configuration to take effect.
