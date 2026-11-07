---
title: "AI Security overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/agent-security-overview"
---

With the widespread adoption of generative AI (AIGC) tools, enterprise employees are introducing various AI Agents by installing desktop clients, IDE plugins, or using command\-line tools (CLIs) to improve work efficiency. However, AI tools that have not been approved for access may lead to enterprise sensitive data leakage, and malicious Skill poisoning attacks have also become a new threat to endpoint security.

The SealSuite **AI Security** provides enterprises with a one\-stop security management experience for AI office scenarios. By building a closed\-loop control process from asset inventory to Agent task audit and traceability, it helps security administrators unleash AI productivity while creating a visible, controllable, and traceable endpoint security environment.

<span id="eeff84a5"></span>
## Core Capabilities

With the **Agent Security** module, you can achieve the following management objectives:


* **AI asset identification and inventory**

   The system automatically collects and identifies AI tools installed on endpoints, including **clients** (desktop applications and CLI packages) and **IDE extensions** (such as extensions for VS Code, Cursor, Trae, and other IDEs). It also provides visualized statistics for key metrics such as AI Agent types, installation distribution, and active users, enabling transparent management of AI assets across the organization.

* **One\-click process\-based disabling**

   Supports process\-based disabling policies for specific AI Agents. Administrators can customize the effective scope (users/devices) and exclude specific allowlisted objects for precise blocking. For the specific control scope, see [AI Tool Control Capabilities List](https://docs.byteplus.com/docs/sealsuite/ai-tool-control-capabilities-list).

* **Skill poisoning risk protection**

   Provides dedicated security detection capabilities for extensions (Skills) loaded by AI Agents. By scanning landed files in real time, the system identifies potential malicious code, high\-risk permissions, or abnormal network communication, and issues warnings before the Agent loads the Skill to protect core enterprise data.

* **Agent Behavior Guardrails**

   Provides system\-level constraints and supports fine\-grained control over AI Agent **file access, network requests, command execution, and registry operations**. By intercepting high\-risk behavior at the driver layer, it effectively defends against unauthorized access and data theft risks caused by prompt injection or Skill poisoning.

* **Agent Full Link Audit**

   Supports auditing the entire process of employee Agent usage, from task initiation to execution results. This helps administrators trace the complete lifecycle of Agent tasks and meet the requirements for risk investigation and offline forensics.


<span id="fb31dfaa"></span>
## Configuration Guide

You can perform the following security management tasks based on your business requirements:


|Task module |Description |Related documentation |
|---|---|---|
|**Asset inventory and disablement** |View AI Agent installation statistics, activity data, and Skill details within the enterprise, and perform one\-click disablement. |[Agent asset inventory and control](https://docs.byteplus.com/docs/sealsuite/agent-asset-inventory-and-control) |
|**Skill security check** |Configure detection policies for AI Agent extension components to prevent attackers from launching poisoning attacks on endpoints through malicious Skills. |[Configuring Skill security detection policy](https://docs.byteplus.com/docs/sealsuite/configuring-skill-detection-policy) |
|**Agent Behavior Guardrails** |Build system\-level physical behavior boundaries for Agents and forcibly intercept high\-risk access to sensitive files, networks, and registries, implementing non\-bypassable security constraints. |[Configuring Agent behavior guardrails policy](https://docs.byteplus.com/docs/sealsuite/configuring-agent-behavior-guardrails-policy) |
|**Agent Full Link Audit** |View and trace the complete execution process of an Agent task, including task initiation, multi\-turn conversations, tool calls, and execution results. |[Agent full link audit](https://docs.byteplus.com/en/docs/SealSuite/agent-full-link-audit?lang=en) |
