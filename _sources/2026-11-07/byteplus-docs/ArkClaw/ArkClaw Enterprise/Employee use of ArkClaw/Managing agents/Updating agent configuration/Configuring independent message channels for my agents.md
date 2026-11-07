---
title: "Configuring independent message channels for my agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_independent_message_channels_for_my_agents"
---

After adding sub\-agents from Agent Gallery or custom sub\-agents to ArkClaw, in addition to configuring messaging channels (such as Feishu and DingTalk) for the primary agent, you can also ** configure message channels ** for each sub\-agent. After the configuration, you can communicate with different channel bots to send messages to the corresponding agents. Additionally, you can enable or disable the message synchronization feature to choose whether to sync and display the chat history from third\-party message channels to the ArkClaw console (web). This allows you to centrally manage all conversations within the console.

<span id="ypErvRzE"></span>
## Considerations


* Do not configure the same message channel bot for multiple agents. Otherwise, the messages you send may not be delivered to the target agent as expected.

* If you have configured a message channel bot for your agent, message channel bot reconfiguration will overwrite existing settings. As a result, the original message channel bot cannot send or receive messages. Proceed with caution.

* **The primary agent** supports the [Telegram](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__#ZUKitsVP), [Lark/Feishu](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__#pZU50Hfq), [Slack](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__#vYkph6hG), [WeCom](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__?lang=en#NKBf7zK7), [WeChat](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__?lang=en#zMNNQbdP), and [Microsoft Teams](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__?lang=en#f3RFpQ1n) message channels. **Sub\-agents** currently only support [Telegram](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__#ZUKitsVP), [Lark/Feishu](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__#pZU50Hfq), [Slack](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__#vYkph6hG), and [Microsoft Teams](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__?lang=en#f3RFpQ1n) message channels.


<span id="lIog6tWm"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page, and select "My agents" in the left\-side navigation pane.

3. On the My agents page, click "View details" on the target agent card.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent whose Agent ID is <strong>main</strong> is the <strong>primary agent</strong>.   </div>
   

4. In the "Channel" module, click the "Associate with xx +" button to associate with the target channel.

5. Scan the QR code or enter bot details to complete configuration. For more information, see [Configuring message channels](https://docs.volcengine.com/docs/87732/2430974?lang=zh).

6. After the configuration, click the "Update" button for the configuration to take effect. You can now send messages to the corresponding agent via the configured message channel bot. Each agent processes tasks independently and sends responses with no mutual interference.

7.  **(Optional) ** Enable or disable channel message synchronization

   To centrally manage conversations in ArkClaw, you can enable message synchronization to sync conversation records from third\-party channels (such as Feishu and DingTalk) to the ArkClaw console. You can also disable this feature to hide the synced conversation content.

   * **Enable "Sync messages to web"** : Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1360bcbba661062971b0d8fdeb175ee6.png) </span> to sync messages to the console.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you have not associated a message channel for the current agent or have dissociated the channel, messages from the corresponding channel will automatically stop being synchronized to the console.      </div>
      

   * **Disable "Sync messages to web"** : Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_551f97d5464d9781a3eda54351d51ddf.png) </span> to hide synced conversations and stop synchronization of new conversations.

   * **View synced conversations:**  After synchronization is enabled, conversations from third\-party channels appear in the "My tasks" list. Conversations are displayed as independent chat records by channel and sorted chronologically.
