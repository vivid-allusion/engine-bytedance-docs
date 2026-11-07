---
title: "Adding message channels to ArkClaw Sandbox tool instances"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Adding_message_channels_to_ArkClaw_Sandbox_tool_instances"
---

ArkClaw Sandbox provides the built\-in ArkClaw instance feature. Sandbox instances created from a sandbox template of this type support configuring message channels (such as a Feishu bot). After you configure a channel, you can open the corresponding bot directly in Feishu and use natural language to handle daily tasks and lightweight office automation.

## Prerequisites

You have created a sandbox template of the **ArkClaw Sandbox ** type and created an instance in the sandbox template. For details, see [Creating sandbox templates](https://docs.byteplus.com/en/docs/agentkit/Creating_tools) and [Creating sandbox instances](https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances).

## Instructions

* After you configure a message channel for a sandbox instance, the channel can serve as an external entry point for reaching users. End users can talk to the agent behind the instance through the configured message channel.

* If snapshots are enabled for the sandbox template and you have configured a message channel for a sandbox instance, the channel association is preserved. After the instance lifecycle ends, when you restore the sandbox instance from a snapshot, the message channel associated with the instance is also restored.

> **warning**

* > A sandbox instance can be associated with only one bot. **If a bot is already associated with the instance, scanning the QR code for reassociation replaces the existing bot.**

* > We recommend that you enable this feature in scenarios where real users are involved, such as ArkClaw Sandbox. For testing or demo purposes, you can use the WebChat URL directly.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Sandbox Template".

3. In the list, click the name of the target tool whose tool type is "ArkClaw Sandbox".

4. On the Instance management tab, in the message channel column of the target sandbox instance, click "Connect Feishu" to add a message channel.

5. Click the "Generate QR code" button.

6. Use the Feishu app to scan the QR code and configure the Feishu app information as prompted.

7. After the configuration succeeds, open the corresponding bot in Feishu and send a message to trigger the agent. The bot replies with the instance's processing results in chat messages, including runtime logs and status information.
