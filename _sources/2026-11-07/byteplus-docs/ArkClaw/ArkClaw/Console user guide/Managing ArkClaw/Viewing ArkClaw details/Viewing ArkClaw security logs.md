---
title: "Viewing ArkClaw security logs"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_security_logs_"
---

BytePlus has preset and enabled the AI security assistant for ArkClaw by default. You can enable or disable it as needed and view information about risk events it monitors and defends against.

<span id="qE0IWhDe"></span>
## Concepts

The AI security assistant acts as a professional "security steward" for your ArkClaw. Without affecting the normal operation of ArkClaw, it uses the built\-in LLM Application Firewall to provide real\-time monitoring and defense against the following three core risks.


* **Prompt injection:**  Attackers may hide malicious instructions in web pages, documents, or emails processed by ArkClaw, tricking it into performing unintended operations, such as stealing passwords or leaking data.

* **PII leakage:**  You may accidentally enter personal or corporate sensitive information (such as ID numbers, phone numbers, and API Keys) during your conversation with ArkClaw or document processing. This information could be sent to external large models, resulting in PII leakage.

* **Risky operations:**  When interpreting ambiguous instructions, ArkClaw may misinterpret instructions or be maliciously induced to call high\-privilege tools and execute dangerous commands. For example, misinterpreting "clean up the desktop" as deleting critical system files.


<span id="hNsmiX9O"></span>
## Procedure


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw).

2. Switch to the target ArkClaw page and click the Claw details page icon in the upper\-right corner.

3. Select the "Security and audit" tab.

4. Enable or disable the AI security assistant as needed.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We strongly recommend that you enable this feature to ensure the security of your ArkClaw. Otherwise, when responding to extreme or malicious queries, ArkClaw may output the sensitive information you configured, resulting in content risks.   </div>
   

5. After you enable the AI security assistant, you can view information about risk events it monitors and defends against.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The event logs do not record all your operations on ArkClaw. Only events related to these operations are logged: ArkClaw configuration changes (such as changes to model change/cloud disk/messaging channel), version upgrades, backups, and migrations.   </div>
