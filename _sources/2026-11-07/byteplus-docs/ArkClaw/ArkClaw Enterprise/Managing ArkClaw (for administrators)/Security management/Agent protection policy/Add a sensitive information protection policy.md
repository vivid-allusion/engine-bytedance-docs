---
title: "Add a sensitive information protection policy"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Add_a_sensitive_information_protection_policy"
---

When using an AI assistant to handle business tasks (such as customer service Q&A, internal knowledge base retrieval, or document summarization), user input (Prompt) or the output of large models (Response) may inadvertently contain users' personal privacy data (PII) or the company's core confidential information.

With the "Sensitive Information Protection" feature, you can add automated sensitive data identification rules to accurately intercept or alert on interactions involving privacy information such as ID cards or bank cards, effectively preventing unauthorized data leakage and ensuring compliance with enterprise data regulations (such as the Personal Information Protection Law).

The system will, by default, create a high\-risk operation interception policy that applies to all newly added assistants. To create a corresponding policy, refer to the instructions in this document.

<span id="3505fec2"></span>
## Prerequisites

You have already integrated the assistant with the ClawSentry service. For integration methods, see [Enable security protection](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection?lang=en).

<span id="zGaaYCNA"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **Security Management**.

3. Under the **Protection** tab, select **Sensitive Information Protection**.

4. Click **Add Rule**, and then configure the rule parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Rule name<br><br> |Required |Name the rule. It is recommended to use the naming format "business line\-protection scenario" (for example: Customer Service Assistant\-ID Card Information) for easier retrieval later. |
   |Rule description |Optional |Provide the applicable background, exceptions, or rationale for this rule to facilitate internal team collaboration and handover. |
   |Protected sensitive information |Required |Select the types of sensitive information that need to be protected by this rule from the drop\-down list (such as ID number and many other types; multiple selections are supported). |
   |Execute action |Required |Set the handling method when ClawSentry detects the above sensitive information:<br><br><br>* Block: Directly cut off the connection, preventing the AI assistant from invoking the corresponding tool or returning results, effectively block the risk.<br><br>* Alert: Only triggers a security alert, but does not block the current interaction. It is recommended to use this rule for observation during the initial canary release. |
   |Applicable assistants |Required |* All assistants: Applies to all existing and newly added assistants.<br><br>* Select assistants: Set the scope of assistants to which this applies. |
   

1. After confirming that the information is correct, click **OK**.
