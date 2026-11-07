---
title: "Configuring models for my agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_models_for_my_agents_01"
---

ArkClaw supports model configurations for the **primary agent ** and for **the other agents.**  The primary agent model serves as the global default and is automatically inherited by other agents. After you build an agent team for ArkClaw, you can independently configure inference models for each of the other agents. This allows you to flexibly select the most suitable model based on agent roles and task characteristics to configure differentiated inference capabilities.

This topic describes how to configure **independent models for the other agents.**  For the configuration details of the **primary agent's model**, see [Adjusting/configuring inference models](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_configuring_inference_models).

<span id="xHiUNdyC"></span>
## Operation instructions

If the other agents have inference models independently configured, those inference models take precedence when the target agent handles tasks, and the inference model of the primary agent does not apply to that agent. If no independent inference model is configured, the agent automatically inherits and uses the inference model of the primary agent.

<span id="jTqZf7pP"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page.

3. In the left\-side navigation pane, click "Agent Center".

4. Click the "My agents" tab.

5. Select the target agent and click the "View details" button.

6. In the "Model configuration" section, click "Edit".

7. On the pop\-up model configuration page, configure the corresponding model. For details, refer to [Adjusting/configuring inference models](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_configuring_inference_models).

8. Click the "Confirm" button to complete the operation.
