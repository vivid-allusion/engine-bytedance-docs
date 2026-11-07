---
title: "Viewing ArkClaw status and usage"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_status_and_usage_"
---

On the "Status and usage" page, you can view the current ArkClaw basic information, token usage statistics, usage trend, and resource allocation for the instance.

<span id="51ySjzUq"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw).

2. Switch to the target ArkClaw page. In the upper\-right corner of the page, click the details icon.

3. Select the "Status and Usage" tab. You can view monitoring information such as ArkClaw basic information, token usage, and usage trends on this page, and perform management operations.

   * **Basic information**

      
      |Metric |Description |
      |---|---|
      |Basic information |Current ArkClaw version, model source, configuration, and other related information. |
      |Related operation |In this module, you can change the ArkClaw avatar, name, and perform the following management operations:<br><br><br>* **Edit the ArkClaw name**: Click the edit button next to the ArkClaw name. Enter the name in the pop\-up dialog box, and click the "Confirm" button to complete the operation.<br><br>* **Upgrade specification**: Upgrade the current ArkClaw to a higher configuration for greater computing power, larger storage capacity, and more features. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_specification_).<br><br>* **Renew**: Extend the expiration time of your ArkClaw to ensure continuous use. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Renewing_ArkClaw).<br><br>* **Unsubscribe**: To avoid unnecessary fees, unsubscribe from ArkClaw if you no longer need it. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Unsubscribing_from_ArkClaw).<br><br>* **Auto healing:**  When your ArkClaw becomes unavailable due to tasks, setting adjustments, or other reasons, you can use the auto healing feature to attempt to restore it to the latest available state.<br><br>* **More configurations:** <br><br>   * **Restart:**  You can manually restart ArkClaw when you need to load new ArkClaw configuration or when ArkClaw responds slowly.<br><br>   * **View terminal**: You can access ArkClaw from terminals and use Shell commands to perform various operations (such as viewing directories and files in the current path, creating tasks, and so on). **This is suitable for technical developers who require advanced usage of ArkClaw.**  [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Accessing_ArkClaw_from_terminals_-).<br><br>   * **Restore factory settings:**  You can reinitialize the ArkClaw service and reset it to the initial available state when your ArkClaw configuration is corrupted and causes a service crash, or when system failures or abnormal states occur and cannot be recovered.<br><br>* **Adjust model configuration:**  ArkClaw supports models from **Agent Plan/Coding Plan subscription package** and **ModelArk "Foundation models"** . You can also integrate custom large model services provided by third\-party vendors (such as DeepSeek). You can adjust as needed. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_configuring_inference_models). |
      

   * **Usage** ** statistics**

      
      |Metric |Description |
      |---|---|
      |Running time |The runtime duration of the ArkClaw gateway service. |
      |Agents |The number of agents in the current ArkClaw team, including the primary agent and added members (agents). |
      |Token usage trend |The current ArkClaw trial token usage details.<br><br><br>* The trial quota is calculated on a **calendar\-month basis**. It is automatically reset at the beginning of each month, and the unused quota will not be carried over to the next month.<br><br>* When the trial quota is exhausted, you may [upgrade to Agent Plan](https://console.byteplus.com/ark/region:ark+cn-beijing/openManagement?LLM=%7B%7D&_vtm_=a106466.b106468.0_0.0_0.0.366_7613594367911118351&advancedActiveKey=agentPlan) or [modify the model configuration](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_configuring_inference_models) to obtain more exclusive quota and higher configuration. |
      |Coding Plan/Agent Plan remaining days |The expiration time of the Coding Plan/Agent Plan package subscribed by the current account.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This metric information is available only when you have subscribed to and are using ModelArk Coding Plan.</div><br> |
      |Coding Plan/Agent Plan usage |The usage percentage (%) of the Coding Plan/Agent Plan package subscribed by the current account.<br><br>You can also select the package usage card to view detailed usage and quota information for the Coding Plan/Agent Plan package in the pop\-up window.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only users who have subscribed to and are using the ModelArk Coding Plan or Agent Plan can view this metric information.</div><br> |
      |Storage usage (GB) |The used storage capacity and total storage capacity of the current ArkClaw. Supported operations:<br><br><br>* Viewing of the storage breakdown of used space by file category, including system files, cached data, plugins, skills, and more.<br><br>* [One-click cache data cleanup](https://docs.byteplus.com/en/docs/ArkClaw/Clearing_ArkClaw_storage_cache_data0?lang=en) |
      

   * **Usage** ** trend**

      
      |Metric |Description |
      |---|---|
      |Number of processed messages |The total number of messages processed by ArkClaw  compared with the previous period. |
      |Token consumption |The total number of tokens used by ArkClaw within the selected period . If the current period has , and the previous period has  compared with the previous period. |
      |Message processing trend |Message quantity change trend of the ArkClaw within the selected period. |
      |Token usage trend |Token usage trend of the ArkClaw within the selected period. |
