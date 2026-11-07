---
title: "Add a prompt injection protection policy"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Add_a_prompt_injection_protection_policy"
---

Prompt injection protection specifically addresses input\-level risks faced by large language models during conversational interactions—users may craft prompts to guide the model to ignore system settings, bypass content policies, or hijack its role and behavioral boundaries. This feature performs real\-time detection before requests reach the large model, intercepting malicious guidance, jailbreaks, rule bypasses, and Role\-playing hijacking attacks, ensuring the model's output always operates within the expected range.

The system will automatically create a prompt injection protection policy, which applies to all newly added assistants. To create a corresponding policy, refer to the instructions in this document.

<span id="Okz8oCVN"></span>
## Applicable scenarios


* Open interaction scenarios: In ToC applications targeting the public, prevent malicious users from injecting prompts to induce the model to make inappropriate statements or engage in other malicious behaviors, protecting brand reputation.

* Strict directive scenarios: When an AI assistant is designed to strictly follow specific instruction formats or workflows, prevent users from bypassing preset rules by methods such as "ignore previous instructions," ensuring tasks are executed as intended.

* Prevent system prompt leakage: Prevent attackers from crafting specific questions to trick the model into revealing system\-level prompts (System Prompt), avoiding theft of core instructions and capability settings.


<span id="e061d00d"></span>
## Prerequisites

You have integrated the assistant with the ClawSentry service. For integration methods, refer to [Enable security protection](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection?lang=en).

<span id="6ff600ff"></span>
## Operation steps


1. Log in to [ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left menu bar, select **Security management**.

3. Under the **Protection** tab, select **Prompt injection protection**.

4. Click **Add rule**, then configure the rule parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Rule name<br><br>  |Required |Name the rule. It is recommended to use the format "Business line–Protection scenario" (for example: Customer service assistant–Prompt injection) for easier retrieval later. |
   |Rule description |Optional |Add the applicable context, exceptions, or basis for formulating this rule to facilitate internal team collaboration and handover. |
   |Protection type |Required |Select the types of prompt injection attacks to protect against for this rule from the dropdown list (multiple selections supported). |
   |Action to execute |Required |Set the handling method when ClawSentry detects the above sensitive information:<br><br><br>* Block: Immediately disconnects the link, preventing the AI assistant from invoking the corresponding tool or returning results, forcefully blocking risks.<br><br>* Alert: Only triggers a security alert record without interrupting the current interaction. It is recommended to use this for canary release observation in the early stage of rule deployment. |
   |Applicable assistants |Required |* All assistants: Applies to all existing assistants and any assistants added in the future.<br><br>* Select assistants: Set the specific range of assistants to which this applies. |
   

5. After confirming the information is correct, click **Confirm**.
