---
title: "Masking observability data"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Masking_observability_data"
---

To ensure data security in scenarios such as the protection of sensitive employee information, observability data does not include Input and Output information by default. If such information is required for troubleshooting or debugging, you can configure the observability data masking policy globally or ‌adjust it manually. This topic describes how to configure observability data masking policies.

<span id="bTWzgFSc"></span>
## Background

The system enables ‌observability data masking by default and allows you to configure the observability data masking policy globally or modify the policy manually. The specific policies are as follows:


* **Enable:**  Data is masked. Input and Output information in logs will be masked to protect sensitive employee information.

* **Disable: ** Data is not masked. You can view complete Input and Output information, which facilitates debugging and troubleshooting.


<span id="yvOdSaOD"></span>
## Limits


* After you manually enable or disable the observability data masking policy for an ArkClaw instance, the gateway automatically restarts. The service is interrupted for about 1 minute during the restart. To prevent normal business operations from being affected, we recommend performing the modification during off‑peak hours.

* After you enable data masking, the collection of Input and Output information is prohibited. Even if you disable data masking later, historical data still does not include Input and Output information.

* Restoring the ArkClaw instance to factory settings resets the observability data masking status to its initial state. If the data masking status does not meet your expectations, you need to manually modify it again.


<span id="6wdI1Ie3"></span>
## Procedure

The observability data masking policy is enabled by default. To view complete Input and Output information, perform the following steps to modify the observability data masking policy.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Status in the Observability data masking column:</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The “Enable/Disable” state indicates that the system has accurately obtained the masking policy for observability data.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">For existing ArkClaw instances for which the observability data masking policy cannot be obtained, “Settings” is displayed in the Observability data masking column. After you click “Settings” and reconfigure the data masking policy, the “Enable/Disable” state will be displayed.</div>




<Tabs>
<Tab zoneid="Cmlm088pAT" title="Configure a global observability data masking policy">
<TabTitle>Configure a global observability data masking policy</TabTitle>

You can adjust the observability data masking policy for new ArkClaw instances by using a global configuration. When in effect, the global configuration applies to new ArkClaw instances.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This global configuration applies only to new Claw instances of employees. It does not affect shared or existing Claw instances.</div>



1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **Claws**. In the upper\-right corner of the ArkClaw instance page, click **Global configuration** to go to the global configuration management page.

3. In the data masking section, click the status toggle for **Employee Claw observability data masking** to adjust the observability data masking policy for new ArkClaw instances.


</Tab>
<Tab zoneid="v8V5kw0oJR" title="Configure an observability data masking policy for a single ArkClaw instance">
<TabTitle>Configure an observability data masking policy for a single ArkClaw instance</TabTitle>

You can manually modify the observability data masking policy for existing ArkClaw instances one by one.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **Claws** to go to the ArkClaw instance management list.

3. Find the target ArkClaw instance and click Settings or the switch in the **Observability data masking** column.

4. Select an observability data masking policy based on your business scenario. Then, click **Confirm**. After the gateway is restarted, the new data masking policy will be applied.





</Tab>
<Tab zoneid="c0m7xsF8Qu" title="Configure an observability data masking policy for multiple ArkClaw instances">
<TabTitle>Configure an observability data masking policy for multiple ArkClaw instances</TabTitle>

You can manually modify the observability data masking policy for multiple existing ArkClaw instances at a time.


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, click **Claws** to go to the ArkClaw instance management list.

3. In the instance list, select the ArkClaw instances for which you want to set the observability data masking policy simultaneously.

4. In the lower\-left corner, click `...` \> **Set data masking policy**.

5. Select an observability data masking policy based on your business scenario. Then, click **Confirm**. After the gateway is restarted, the new data masking policy will be applied.





</Tab>
</Tabs>


<span id="l74OOL2m"></span>
## Result verification

If you set the observability data masking policy to **Enable**, you can verify the configuration result by using the following scenarios.


* Click the name of the target ArkClaw instance to go to the ArkClaw instance details page and view the configured observability data masking policy.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">On the ArkClaw instance details page, you can also configure the observability data masking policy. Click <strong>Settings</strong> to adjust the observability data masking policy based on your business scenarios.   </div>
   

* Go to the details page of the target session. Input and Output information will no longer be displayed. For a detailed description of session management, see [Viewing ArkClaw sessions](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_sessions).

* Go to the details page of the target Trace. The LLM data tab will no longer display Input and Output information. For a detailed description of Trace analysis, see [Viewing ArkClaw Trace analysis](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_traces).
