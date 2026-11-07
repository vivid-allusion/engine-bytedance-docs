---
title: "Switching thinking mode"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Switching_thinking_mode_"
---

You can flexibly switch among Fast, Standard, and Expert thinking modes based on task complexity and response time requirements. This helps match scenarios on demand, reduce redundant thinking time, and improve conversation efficiency.

> Thinking mode: Preconfigured levels for the AI based on thinking depth, response speed, conversation capacity, and tool invocation capabilities to handle questions of varying difficulty. You can switch modes in real time and select flexibly based on your needs.


<span id="PeoX0ObC"></span>
## Supported thinking modes


* **Fast mode**: Provides quicker responses with simplified reasoning. It is suitable for lightweight tasks such as small talk, translation, simple queries, and basic Q&A.

* **Standard mode** (default) **:**  Balances response speed and thinking depth. It is suitable for most general tasks such as data analysis and recommendations, delivering both efficiency and accuracy.

* **Expert mode:**  Delivers thorough reasoning and rigorous logic. It is applicable for high\-demand scenarios such as complex analysis, professional questions, in\-depth creation, programming, deployment, and multi\-step automation.


<span id="MdEjnFAX"></span>
## Usage notes


* Switching thinking modes does not affect the current conversation. Chat history and context are preserved, and no new separate conversation will be created.

   * Standard mode and Expert mode support all ArkClaw tools. Fast mode supports only the following tools:

      * File operations: `read`, `write`, `edit`, `apply_patch`

      * Web search: `web_search`, `web_fetch`, `x_search` (X/Twitter search)

      * Conversation management: `session_status`


<span id="oh2ctvu8"></span>
## Switch on the ArkClaw page

On the ArkClaw conversation page, you can quickly switch thinking modes with one click based on your needs. This method is recommended for its simplicity and stability.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Switching thinking modes via commands is currently not supported.</div>



1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. Click the current mode name (e.g., Fast) in the chat input box.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">(Optional) If the switch button is disabled (grayed out) on your ArkClaw due to an outdated version, <a href="https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_">upgrade to the latest version</a> first, and then switch thinking modes using the visual button. Otherwise, skip this step. After the upgrade, you need to manually refresh the ArkClaw page to enable and experience the new features.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The mode name displayed in the chat input box indicates the currently active thinking mode. For example, if "Standard" is displayed, Standard mode is in use.   </div>
   

4. In the pop\-up window, select the desired thinking mode as needed. After the thinking mode is switched, new conversations will use the mode you selected.


<span id="dCYh0Z3b"></span>
## Switch on the message channel page

You can quickly switch thinking modes by entering and sending commands in a fixed format in the chat input box of message channels such as Lark and Slack.

> This method is suitable for users who are accustomed to command\-based operations or for quick switching in pure text interaction scenarios.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Compatibility issues or switching failures may occur in some scenarios when you switch thinking modes on the message channel page. For a more stable and smooth experience, we recommend that you preferentially switch thinking modes on the ArkClaw page.</div>


* <div data-tips="true" data-tips-type="default">Switching thinking modes is temporarily unavailable in Lark groups with <strong>Thread mode</strong> enabled.</div>


* <div data-tips="true" data-tips-type="default">Switching thinking modes is currently supported only on Lark and Slack, and is not yet compatible with DingTalk.</div>



<span id="4PS0OrhG"></span>
### Prerequisites

You have completed the relevant [message channel integration](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_message_channels__).

<span id="S5WSRuoq"></span>
### Procedure


1. Open the corresponding message channel (Feishu, Slack).

2. Enter the conversation window with the bot/assistant.

3. (Optional) Enter and send the `/mode status` command in the chat input box to view the currently available thinking modes.

4. Enter and send the following switching commands in the chat input box as needed to quickly switch to your desired thinking mode. After switching, subsequent conversations will automatically respond in the selected mode.

   * `/mode fast`: the Fast mode.

   * `/mode standard`: the Standard mode.

   * `/mode expert`: the Expert mode.

5. Verify whether the switching is successful:

   * After ArkClaw is switched to `/mode fast` (Fast mode), the prompt shows "Switched. Current mode: Fast".

   * After ArkClaw is switched to `/mode standard` (Standard mode), the prompt shows "Switched. Current mode: Standard".

   * After ArkClaw is switched to `/mode expert` (Expert mode), the prompt shows "Switched. Current mode: Expert".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the thinking mode switching does not deliver the expected results on your ArkClaw, complete the <a href="https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_">upgrade to the latest version</a> first, and then retry the switching steps above.   </div>
