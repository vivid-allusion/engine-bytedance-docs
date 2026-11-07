---
title: "Configuring independent message channels for agents in teams"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_independent_message_channels_for_agents_in_teams"
---

If you have created an agent team for ArkClaw, in addition to configuring message channels (such as Feishu and DingTalk) for the primary agent, you can also **configure independent message channels ** for other agents in the team. After the configuration, you can communicate with different channel bots to send messages to the corresponding agents. Additionally, you can enable or disable the message synchronization feature to choose whether to sync and display the chat history from third\-party message channels to the ArkClaw console (web). This allows you to centrally manage all conversations within the console.

<span id="Ruy9txLp"></span>
## Usage notes


* Do not configure the same message channel bot for multiple agents. Otherwise, the messages you send may not be delivered to the target agent as expected.

* If you have configured a message channel bot for your agent, message channel bot reconfiguration will overwrite existing settings. As a result, the original message channel bot cannot send or receive messages. Proceed with caution.


<span id="E257VQZj"></span>
## Prerequisites

Currently, the "Sync messages to web" feature is available only for ArkClaws with an agent team plugin version of` ark-26.5.21` ** or later**. You can check your ArkClaw version and perform upgrades on the "Status and usage" tab of the ArkClaw details page. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_status_and_usage_).

<span id="boV4bQC4"></span>
## Usage notes

When you sync chat messages from third\-party message channels (such as Feishu and DingTalk) to the ArkClaw console, the following rules apply:


|Rule |Description |
|---|---|
|Synchronization switch control |* **Enabled**: After you turn on the "Sync messages to web" switch, new messages generated in the associated third\-party channel are synced to the console in real time.<br><br>* **Disabled** (default): After you turn off the "Sync messages to web" switch, synchronization of new messages stops. The historical channel conversations that have been synced are automatically hidden in the console. |
|One\-way synchronization mechanism |The synchronization is one\-way (**third\-party channel → console**).<br><br>After synchronization, you can view the records and continue conversations in the console. However, new messages and assistant replies sent from the console are not synced back to the corresponding third\-party channel. |
|Conversation operation limit |You cannot delete third\-party channel conversations that are synced to the console. Manually delete related content in the corresponding third\-party channel. You can also hide them temporarily by turning off the "Sync messages to web" switch. |


<span id="5fgpfPIL"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Switch to the target ArkClaw page and click the Claw details page icon in the upper\-right corner.

3. Select the "Agent team" tab.

4. Select the target agent from the agent list on the left.

5. In the "Channel" module, click the "Associate with xx +" button to associate with the target channel.

6. Scan the QR code or enter bot details to complete configuration. For more information, see [Configuring message channels](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels_1).

7. After configuration, you can send messages to the corresponding agent via the configured message channel bot. Each agent processes tasks independently and sends responses with no mutual interference.

8.  **(Optional) Enable or disable channel message synchronization**

   To centrally manage conversations in ArkClaw, you can enable message synchronization to sync conversation records from third\-party channels (such as Feishu and DingTalk) to the ArkClaw console. You can also disable this feature to hide the synced conversation content.

   * **Enable "Sync messages to web"** : Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1360bcbba661062971b0d8fdeb175ee6.png) </span> toggle to sync messages to the console.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you have not associated a message channel for the current agent or have dissociated the channel, messages from the corresponding channel will automatically stop being synchronized to the console.      </div>
      

   * **Disable "Sync messages to web"** : Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_551f97d5464d9781a3eda54351d51ddf.png) </span> toggle to hide synced conversations and stop synchronization of new conversations.

   * **View synced conversations:**  After synchronization is enabled, conversations from third\-party channels appear in the "My tasks" list. Conversations are displayed as independent chat records by channel and sorted chronologically.
