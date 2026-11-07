---
title: "Add a high-risk operation blocking policy"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Add_a_high-risk_operation_blocking_policy"
---

In enterprise\-level AI applications, if an assistant has excessive permissions, it is very easy for malicious users to exploit it to execute high\-risk commands, such as reading sensitive server files, tampering with backend databases, executing malicious system commands, and more.

With the "high\-risk operation interception" feature, security administrators can define clear operational boundaries for different AI assistants and specify which sensitive actions are strictly prohibited, thereby preventing unauthorized operations and malicious damage, and ensuring that AI business activities remain transparent and controllable.

The system will, by default, create a high\-risk operation interception policy that applies to all newly added assistants. To create a corresponding policy, refer to the instructions in this document.

<span id="a0ef3b52"></span>
## Applicable scenarios


* **Tool invocation execution boundary control**: When an AI assistant needs to call internal APIs or tools, precisely control the range of callable functions and parameters to prevent the execution of dangerous operations.

* **Batch deletion and modification operation protection**: For actions where an AI assistant may perform batch deletion or modification of database records or files, set up pre\-approval or interception to avoid large\-scale data corruption.

* **External system write protection**: When an AI assistant needs to write data to external systems, perform security verification to prevent malicious or erroneous data from contaminating critical business systems.


<span id="a5dff9df"></span>
## Prerequisites

You have already connected the assistant to the ClawSentry service. For connection methods, refer to [Enable security protection](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection?lang=en).

<span id="PXciD2uK"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation menu, select **Security management**.

3. Under the **Protection** tab, select **High\-risk operation interception**.

4. Click **Add rule**, then configure the rule parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Rule name<br><br>  |Required |For rule naming, it is recommended to use the format "Business Line\-Protection Scenario" (for example: Customer Service Assistant\-System Command Injection Prevention) to facilitate future retrieval. |
   |Rule description |Optional |Provide additional information about the applicable context, exceptions, or basis for this rule to facilitate internal team collaboration and handover. |
   |High\-risk operation |Required |Select the types of high\-risk behaviors that this rule should detect and control from the dropdown list (multiple selections supported), or configure custom high\-risk operations according to the prompts on the interface (available in Advanced Edition only). |
   |Action to execute |Required |Set how ClawSentry handles the above high\-risk operations when detected:<br><br><br>* Block: Immediately terminate the connection to prevent the AI assistant from invoking the corresponding tool or returning results, strongly blocking the risk.<br><br>* Alert: Only triggers a security alert record without interrupting the current interaction. It is recommended to use this mode for observation during the initial rollout of the rule. |
   |Applicable assistants |Required |* All assistants: Applies to all added assistants and any assistants added in the future.<br><br>* Select assistants: Specify the scope of assistants to which this rule applies. |
   

5. After confirming the information is correct, click **OK**.
