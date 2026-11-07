---
title: "AI access security overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/ai-security-protection-overview"
---

As generative artificial intelligence (GenAI) becomes widely used at work, enterprises gain efficiency while facing new security challenges. These include core data leakage, employee misuse of risky applications, and prompt injection attacks.

**AI access security** (GenAI Protection) is a core capability of the SealSuite Secure Web Gateway (SWG). It delivers semantic security protection across AI usage scenarios for AI applications. Deep content auditing and multidimensional application identification on the gateway help enterprises visualize AI assets. The "semantic guardrails" technology identifies and blocks sensitive information leakage and policy violations in prompts in real time.

 &nbsp;

 &nbsp;

<span id="核心价值"></span>
## Core values


* **Full asset visibility**: Automatically identify and inventory all AI assets used by employees across the enterprise. Assets include web\-based AI applications, large language model APIs, MCP Servers, command\-line tools (CLI), and Skill plugins. The asset dashboard quantifies AI usage popularity, organizational distribution, and risk exposure.

* **Semantic\-level deep protection (large model guardrails)** : Use AI semantic recognition to deeply analyze request content. This capability accurately identifies complex prompt attacks, such as role\-playing and goal hijacking. It also enforces action\-level blocking against sensitive data leakage, such as core code and customer privacy.

* **Developer tool security (CLI/MCP audit)** : Provide granular audits for command\-line tools (CLI) commonly used by developers and external Servers (MCP) called by Agents. This provides visibility from tools to atomic behaviors and eliminates blind spots in AI automation workflows.

* **Supply chain risk blocking (Skill detection and removal)** : Based on the Threat Intelligence engine, automatically identify and block Skill downloads that contain risks such as malicious dependencies and counterfeit packages. This ensures the security of AI Skill plugin download chains.


 &nbsp;

 &nbsp;

<span id="应用场景"></span>
## Application scenarios


* **Scenario 1: Identify and govern shadow AI assets**

   * **Pain point**: Employees use unauthorized AI tools or MCP Servers without approval, making enterprise data flows uncontrollable.

   * **Solution**: Configure a "full discovery" baseline policy that covers all employees in [AI protection policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ai-protection-policy), with the action set to "observe". The system continuously monitors traffic based on this baseline and automatically aggregates the asset inventory on the [AI asset discovery](https://docs.byteplus.com/en/docs/sealsuite/ai-asset-discovery-management) page. Administrators can use popularity and risk assessment results to upgrade non\-compliant applications to a "block" policy, creating a closed loop from discovery to governance.

* **Scenario 2: Defend against prompt attacks (jailbreak protection)** 

   * **Pain point**: Employees or external risky users use carefully crafted prompts, such as role\-playing and goal hijacking, to bypass AI compliance restrictions and induce the model to generate non\-compliant output.

   * **Solution**: Enable **SSL decryption** and configure a semantic guardrail policy. Select detection categories such as **role\-playing**, **privilege escalation**, and **goal hijacking**. The system deeply evaluates conversation intent. It identifies and blocks prompt requests with deceptive, misleading, or malicious bypass characteristics, preventing compliance risks caused by model manipulation.

* **Scenario 3: Govern AI plugins and Supply Chain Security**

   * **Pain point**: External Servers (MCP) called by Agents or downloaded Skill plugins may introduce supply chain risks and audit blind spots.

   * **Solution**: Enable SKILL protection. The system uses threat intelligence to automatically block Skill downloads from high\-risk sources. Enable MCP traffic collection to perform deep audits on atomic tool calls through [MCP logs](https://docs.byteplus.com/en/docs/sealsuite/ai-protection-log-audit#mcp-logs), preventing AI supply chain poisoning.

* **Scenario 4: Protect sensitive information sent to AI**

   * **Pain point**: When employees use AI, they may submit sensitive information such as customer data and internal project content to AI.

   * **Solution**: In **DLP \> Strategy Center \> Control Strategy \> GenAI Data Protection**, use classification and grading rules to identify sensitive content in prompts, then audit or block it. For instructions, see [Configure a GenAI data protection policy](https://docs.byteplus.com/en/docs/sealsuite/configure-genai-data-protection-policy?lang=en). After a policy is triggered, see [View GenAI data outbound logs](https://docs.byteplus.com/en/docs/sealsuite/genai-data-outgoing-logs-view?lang=en) to trace related events.


 &nbsp;

 &nbsp;

<span id="开始使用"></span>
## Get started

Before configuring an AI access security policy, make sure you have completed basic SWG configurations, such as traffic steering policies and certificate distribution.


1. **Configure an AI protection policy**: Define audit and blocking rules.

   * See: [AI protection policy configuration](https://docs.byteplus.com/en/docs/sealsuite/configure-ai-protection-policy?lang=en)

2. **Manage AI asset discovery**: Understand AI application usage in the enterprise and identify potential risk assets.

   * See: [AI asset discovery management](https://docs.byteplus.com/en/docs/sealsuite/ai-asset-discovery-management?lang=en)

3. **Audit AI access security logs**: View protection effectiveness, analyze violation details, and continuously optimize policies.

   * See: [AI protection log audit](https://docs.byteplus.com/en/docs/sealsuite/ai-protection-log-audit?lang=en)
