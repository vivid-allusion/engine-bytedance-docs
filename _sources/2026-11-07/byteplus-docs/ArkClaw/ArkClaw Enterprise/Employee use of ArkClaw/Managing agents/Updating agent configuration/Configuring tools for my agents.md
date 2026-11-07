---
title: "Configuring tools for my agents"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring_tools_for_my_agents"
---

After adding sub\-agents from Agent Gallery or custom sub\-agents to ArkClaw, you can enable or disable tools for each sub\-agent independently and retain only the capabilities the sub\-agent actually needs for greater security and efficiency.


* **Enable a tool**

   After you enable a tool, ArkClaw can invoke the corresponding external capabilities during conversations and provide extended services based on the features.

* **Disable a tool**

   After you disable a tool, ArkClaw will no longer invoke the capabilities of this tool during conversations.


<span id="OjlxnsdB"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page, and select "Agent Center" in the left\-side navigation pane.

3. On the My agents page, click "View details" on the target agent card.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent whose Agent ID is <strong>main</strong> is the <strong>primary agent</strong>.   </div>
   

4. In the "Tools" module, click the "Edit all" button.

5. In the All tools dialog, enable or disable the tool capabilities for the target agent as needed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Disabling all tools of the Agent will trigger the system fallback mechanism and load redundant configurations, resulting in context contamination and call exceptions. We recommend that you keep at least one tool enabled.   </div>
   

   * **Enable/batch enable**:

      * Enable individually: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_036005a10ca27ca2322c30b2c2317f38.png) </span> icon to the right of the target tool to enable it.

      * Enable in batches: Select multiple tools, click "Batch enable", and then click "Enable" to complete the operation.

   * **Disable/batch disable**

      * Disable individually: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4e49b8d191341a5353e9a4be1685fc9d.png) </span> icon to the right of the target tool to disable it.

      * Disable in batches: Select multiple tools, click "Batch disable", and then click "Disable" to complete the operation.

6. After the configuration, click the "Update" button for the configuration to take effect.
