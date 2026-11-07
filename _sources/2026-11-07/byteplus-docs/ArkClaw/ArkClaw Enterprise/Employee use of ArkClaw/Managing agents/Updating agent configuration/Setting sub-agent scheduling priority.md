---
title: "Setting sub-agent scheduling priority"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Setting_sub-agent_scheduling_priority"
---

You can control whether sessions initiated by the **primary agent** prioritize sub\-agent scheduling. This setting clarifies task execution priority and ensures stable, reliable multi\-agent handoffs. By default, prioritized sub\-agent processing is disabled. If your business has strict requirements for task distribution chains, we recommend that you enable this feature to improve the stability of sub\-agent calls.


* **Prioritized sub\-agent processing enabled**

   The primary agent will first attempt to distribute the task to a sub\-agent:

   * Matching sub\-agent found: The corresponding sub\-agent handles and responds to the session.

   * No matching sub\-agent: The task is still handled and responded to by the primary agent.

* **Prioritized sub\-agent processing disabled (default)** 

   The primary agent handles tasks in the original manner, rather than prioritizing the search for a matching sub\-agent. Task handling is determined by the primary agent's [Agent.md](https://docs.byteplus.com/en/docs/ArkClaw/Configuring_md_files__?lang=en) and [memory management](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Enterprise_memory_management__?lang=en) configurations, which decide whether the primary agent or a sub\-agent handles the task.


<span id="78VxsHfi"></span>
## Limits

This feature can only be configured on the primary agent. Sub\-agents do not support this configuration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The agent with the agent ID <strong>main</strong> is the <strong>primary agent</strong>. For details about how to view the agent ID, see the procedure below<strong>.</strong></div>


<span id="RQoEXWJB"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page, and select "Agent Center" in the left\-side navigation pane.

3. On the "My agents" page, click "View details" on the primary agent card.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agent with the agent ID <strong>main</strong> is the <strong>primary agent</strong>.   </div>
   

4. Enable or disable the prioritized sub\-agent processing feature as needed.

   * **Enable:** 

      1. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da9457636e0cc34d989dbd808f0fa430.png) </span> icon.

      2. (Optional) If a dialog box appears prompting you to upgrade the plugin, click "Upgrade now" to upgrade the plugin.

      3. After the upgrade is complete, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da9457636e0cc34d989dbd808f0fa430.png) </span> button again to enable the prioritized sub\-agent processing feature.

   * **Disable**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d40d00071cd81a7840c651423a39724.png) </span> icon to disable the prioritized sub\-agent processing feature.
