---
title: "Viewing ArkClaw security logs"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_security_logs__"
---

ArkClaw comes with the built\-in AI security assistant enabled by default. You can view information about ArkClaw\-related risk events monitored and defended by this feature.

<span id="RJmr7OK6"></span>
## Concepts

The AI security assistant acts as a professional "security steward" for your ArkClaw. Without affecting the normal operation of ArkClaw, it uses the built\-in LLM Application Firewall to provide real\-time monitoring and defense against the following three core risks.


* **Prompt injection:**  Attackers may hide malicious instructions in web pages, documents, or emails processed by ArkClaw, tricking it into performing unintended operations, such as stealing passwords or leaking data.

* **PII leakage:**  You may accidentally enter personal or corporate sensitive information (such as ID numbers, phone numbers, and API Keys) during your conversation with ArkClaw or document processing. This information could be sent to external large models, resulting in PII leakage.

* **Risky operations:**  When interpreting ambiguous instructions, ArkClaw may misinterpret instructions or be maliciously induced to call high\-privilege tools and execute dangerous commands. For example, misinterpreting "clean up the desktop" as deleting critical system files.


<span id="Bwu2Jzhf"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw and click the details icon at the top.

3. On the ArkClaw details page, select the "Security and audit" tab.

4. View information about risk events monitored and defended by the AI security assistant.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The event logs do not record all your operations on ArkClaw. Only events related to these operations are logged: ArkClaw configuration changes (such as changes to model change/cloud disk/messaging channel), version upgrades, backups, and migrations.   </div>
   

&nbsp;
