---
title: "Add a risk scanning policy"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Add_a_risk_scanning_policy"
---

The skills, tools, and other dependencies required by the assistant at runtime are potential supply chain risk entry points—they may contain known vulnerabilities, malicious code, or insecure implementation logic, which can be triggered during the assistant's execution.

The risk scanning module addresses this threat surface by allowing administrators to configure security scanning policies for specified assistants or their associated skills, performing code audits and behavior analysis before the skills are actually invoked. Once a risky skill is identified by the scan, the result will be synchronized back to the console, and the preset action (such as interception) will be executed to control its invocation and prevent the risk from spreading at runtime.

<span id="0280f327"></span>
### Applicable scenarios


* **Third\-party skill security review**: Perform a security scan before introducing skills developed by third parties to assess whether they contain malicious behavior or security vulnerabilities.

* **Supply chain security assurance**: Regularly scan all skills in the AI assistant ecosystem to ensure the security of the entire supply chain and prevent vulnerabilities in any link from affecting the whole.

* **Compliance check**: Customize scanning policies according to internal enterprise security standards to check whether skills have non\-compliant API calls or data processing behaviors.

* **Proactive risk detection**: Identify and remediate potential security risks through proactive scanning before the AI assistant goes live or performs high\-risk tasks, rather than passively waiting for attacks to occur.


<span id="f5c53e25"></span>
### Prerequisites

You have integrated the assistant with the ClawSentry service. For integration methods, refer to [Enable security protection](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection?lang=en).

<span id="GEAQhwH1"></span>
## Procedure


1. Log in to [ArkClaw Enterprise Edition Console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation menu, select **Security management**.

3. Under the **Protection** tab, select **Risk scanning**.

4. Click **Add rule**, then configure the rule parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Rule name<br><br> |Required |Name the rule using the format "business line\-protection scenario" (for example: customer service assistant\-ID card information) to facilitate future retrieval. |
   |Rule description |Optional |Add the applicable context, exceptions, or basis for this rule to facilitate internal team collaboration and handover. |
   |Action |Required |Currently supports interception actions. The connection is directly severed, preventing the AI assistant from invoking the corresponding tool or returning results. This effectively blocks risks. |
   |Applicable assistants |Required |* All assistants: Applies to all added assistants and any assistants added in the future.<br><br>* Select assistants: Set the specific scope of assistants to which the policy applies. |
   

4. After confirming the information is correct, click **OK**.
