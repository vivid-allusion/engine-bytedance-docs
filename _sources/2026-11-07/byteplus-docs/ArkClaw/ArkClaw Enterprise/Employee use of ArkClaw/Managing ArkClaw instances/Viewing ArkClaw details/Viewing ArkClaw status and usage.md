---
title: "Viewing ArkClaw status and usage"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_status_and_usage"
---

You can view the current ArkClaw health status, token usage statistics, usage trend, and resource allocation for the instance.

<span id="RVhJRBp5"></span>
## Procedure


<Tabs>
<Tab zoneid="AMtxr2CKkg" title="View the status and token usage of a single ArkClaw instance">
<TabTitle>View the status and token usage of a single ArkClaw instance</TabTitle>

On the "Status and usage" page of the target ArkClaw, you can view the current ArkClaw health status, token usage statistics, usage trend, and resource allocation.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. Select the "Status and usage" tab to view ArkClaw basic information and perform management operations. You can also view monitoring information for your ArkClaw, such as token usage, usage trend, and other metrics.

   * **Basic information**

      
      |Metric |Description |
      |---|---|
      |Basic information |Current ArkClaw version, model source, configuration, and other related information. |
      |Related operation |In this module, you can change the ArkClaw avatar, name, and perform the following management operations:<br><br><br>* **Edit the ArkClaw name**: Click the edit button next to the ArkClaw name. Enter the name in the pop\-up dialog box, and click the "Confirm" button to complete the operation.<br><br>* **Check for updates: ** Upgrade versions of the ArkClaw system and core components, such as "Message channel" and "Memory management", to ensure stable running of your ArkClaw. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Upgrading_ArkClaw_version_?lang=en).<br><br>* **One\-click diagnosis: ** ArkClaw can be triggered to automatically run the diagnostic script and check the running status and configuration information of ArkClaw. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/One-click_diagnosis_of_ArkClaw__?lang=en).<br><br>* **Auto healing: ** When your ArkClaw becomes unavailable due to tasks, setting adjustments, or other reasons, you can use the auto healing feature to attempt to restore it to the latest available state.<br><br>* **More configurations:** <br><br>   * **Restart:**  You can manually restart ArkClaw when you need to load a new ArkClaw configuration or when ArkClaw responds slowly. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Restarting_ArkClaw__?lang=en).<br><br>   * **View terminal**: You can access ArkClaw from terminals and use Shell commands to perform various operations (such as viewing directories and files in the current path, creating tasks, and so on). **This is suitable for technical developers who require advanced usage of ArkClaw.**  [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Accessing_ArkClaw_from_terminals_?lang=en).<br><br>   * **Restore factory settings: ** You can reinitialize the ArkClaw service and reset it to the initial available state when your ArkClaw configuration is corrupted and causes a service crash, or when system failures or abnormal states occur and cannot be recovered. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Restoring_ArkClaw_to_factory_settings__?lang=en).<br><br>* **Adjust model configuration:**  After the administrator configures multiple models, you can change the inference model used by ArkClaw based on actual business scenarios **.**  [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__?lang=en). |
      

   * **Basic statistics**

      
      |Metric |Description |
      |---|---|
      |Running time |The runtime duration of the ArkClaw gateway service. |
      |Agent count |The number of agents in the current ArkClaw instance, including the primary agent and added members (agents). |
      

   * **Usage trend**

      
      |Metric |Description |
      |---|---|
      |Number of processed messages |The total number of messages processed by ArkClaw.  compared with the previous period. |
      |Token |The total number of tokens used by ArkClaw within the selected period . If the current period has , and the previous period has  compared with the previous period. |
      |Storage usage (GB) |The used storage capacity and total storage capacity of the current ArkClaw. Supported operations:<br><br><br>* Viewing of the storage breakdown of used space by file category, including system files, cached data, plugins, skills, and more.<br><br>* [One-click cache data cleanup](https://docs.byteplus.com/en/docs/ArkClaw/Clearing_ArkClaw_storage_cache_data__?lang=en) |
      |Message processing trend |Message quantity change trend of the ArkClaw within the selected period. |
      |Token usage trend |Token usage trend of the ArkClaw within the selected period. |
      





</Tab>
<Tab zoneid="M7gqpYQUQq" title="View the token usage of all ArkClaw instances">
<TabTitle>View the token usage of all ArkClaw instances</TabTitle>

You can also view the summary data and trend of token usage for all ArkClaw instances under the current account.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. After switching to the target ArkClaw, in the lower\-left corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59698c698f1e49c07e0f26b331238337.png) </span>.

3.  to view aggregated monitoring information for all ArkClaw instances under the current account, such as token usage and usage trends.

   
   |Metric |Description |
   |---|---|
   |Number of processed messages |The total number of messages processed by all ArkClaw instances owned by the current user within the selected period. You can view:<br><br><br>* The total number of messages processed by all ArkClaw instances and the period\-over\-period change rate compared with the previous period. For example: Select **Last 7 days**. If the current period has `120` conversation times, and the previous period has `96` times, the system shows an increase of `25%` compared with the previous period.<br><br>* The ranking of the total number of messages processed by all ArkClaw instances among all users within the current enterprise. The ranking result is displayed as a title, such as "AI efficiency expert". |
   |Token usage |The total number of tokens consumed by all ArkClaw instances owned by the current user within the selected period. You can view:<br><br><br>* The total number of tokens consumed by all ArkClaw instances and the period\-over\-period change rate compared with the previous period. For example: Select **Last 7 days**. If the current period has `8055 K` tokens consumed, and the previous period has `6444 K` tokens consumed, the system shows an increase of `25%` compared with the previous period.<br><br>* The ranking of the total number of tokens consumed by all ArkClaw instances among all users within the current enterprise. The ranking result is displayed as a title, such as "AI efficiency expert". |
   |Number of processed messages |The message count trend for all ArkClaw instances owned by the current user within the selected period. |
   |Token usage trend |Token usage trend for all ArkClaw instances owned by the current user within the selected period. |
   





</Tab>
</Tabs>
