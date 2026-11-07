---
title: "Using connectors"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Using_connectors"
---

Connectors are core components in the AI agent system, used for connecting agents with external systems or platforms. This way, the agents can perform practical operations. By adding different connectors to ArkClaw, you can flexibly expand its capabilities. This allows your ArkClaw to directly operate various external tools, read external data, or call external services.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic describes how to use connectors from the quick access toolbar in the ArkClaw chat box. You can also go to the "Plugins" tab on the ArkClaw details page to view and configure existing connectors, and create custom connectors as needed to introduce third\-party or self\-hosted services. <a href="https://docs.volcengine.com/docs/87732/2597517">Learn more</a></div>


<span id="BhdhrvP4"></span>
## Preset connectors

The following table lists the preset connectors in ArkClaw. If the preset connectors do not meet your requirements, you can add and use third\-party or self\-hosted connectors. [Learn more](https://docs.volcengine.com/docs/87732/2596227#UN8hlPwf)


|Term |Description |
|---|---|
|Feishu |Feishu CLI is a command\-line tool officially provided by Feishu. Through the rich commands and AI Agent Skills provided by Feishu CLI, ArkClaw helps you manage and operate Feishu more conveniently. It covers core business domains such as Feishu Messenger, Docs, Bases, Spreadsheets, Slides, Calendar, Email, Tasks, Meetings, and Markdown. [Learn more](https://www.feishu.cn/feishu-cli)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Authorization has a time limit. Upon expiration, Feishu CLI will display a pop\-up window in your conversation with the Feishu bot, prompting you to re\-authorize.</div><br> |


<span id="H53MslH3"></span>
## Procedure

<span id="pejAipAv"></span>
### Step 1: Enable a connector


1. Open a browser, enter the ArkClaw login link in the address bar, and press the "Enter" key.

2. Switch to the target ArkClaw page.

3. If your ArkClaw has multiple agents, switch to the target agent. You can configure separate connectors for each agent.

4. At the bottom of the chat box, click "+ \> Connector". Then, click the "Connect" button on the right side of the target connector as needed and [complete the authorization as prompted](https://docs.volcengine.com/docs/87732/2586821#6XbjMgGa).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the pop\-up window prompts "System upgrade required", please follow the instructions to complete the ArkClaw system and component upgrade.   </div>
   

<span id="y2fajIVu"></span>
### Step 2: Complete authorization configuration

Complete authorization as prompted to connect to the corresponding connector. This section uses a preset Feishu connector as an example to walk you through the authorization configuration process.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the authentication method selected for the connector is <strong>No authentication required</strong>, the connector can be used immediately after being enabled, with no authorization configuration required. <a href="https://docs.volcengine.com/docs/87732/2597517#xVIkGPpO">Learn more</a></div>



1. Configure the Feishu message channel.

   1. If your ArkClaw has not been configured with a Feishu bot yet, scan the QR code in the Feishu application to configure it. Otherwise, skip this step.

   2. Enter the name of the Feishu bot and click the "Create now" button to start the creation process.

   3. Once the bot is created, ArkClaw will automatically configure the new bot information for you.

2. Grant the permission to connect to Feishu CLI.

   1. Click the "Open authorization page" button.

   2. On the authorization page, confirm the permission information and click the "Activate and authorize" button.

   3. When "Activated and authorized" is displayed on the page, it means your ArkClaw has been linked to Feishu CLI.


<span id="paak50mj"></span>
### Step 3: Use a connector


1. You can enable or disable a connector from the quick access toolbar in the target ArkClaw chat box.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Disabling a connector will prevent ArkClaw from accessing the corresponding platform or using the platform's related capabilities through that connector. Proceed with caution.   </div>
   

3. Once a connector is enabled, you can add a usage instruction before a task that requires the connector (for example: Use **xx** to handle this task) to assign the task to the connector.

   * **Sample ** **prompt** **:** 

      Help me use Feishu to handle the current task: generate today's AI consultation digest and summarize the content into a Feishu document.

   * **Sample result:** 


<span id="6XbjMgGa"></span>
## Related operation

You can also go to the "Plugins" tab on the ArkClaw details page to view and configure existing connectors, and create custom connectors as needed to introduce third\-party or self\-hosted services. [Learn more](https://docs.volcengine.com/docs/87732/2597517)
