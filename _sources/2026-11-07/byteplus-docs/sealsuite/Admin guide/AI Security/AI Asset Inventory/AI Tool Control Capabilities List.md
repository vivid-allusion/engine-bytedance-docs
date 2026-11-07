---
title: "AI Tool Control Capabilities List"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/ai-tool-control-capabilities-list"
---

The SealSuite **AI Security** module can identify and report AI tools installed on endpoints, and allows administrators to disable unauthorized AI tools with one click in the Admin Console, reducing the risk of sensitive enterprise data being exposed through unauthorized AI tools.

This document details the scope of AI tools currently supported for identification and control, including AI Agent **desktop applications**, **command\-line tools (CLI)** , and **IDE plugins**. You can use the lists below to quickly look up the support status for a specific AI tool across capabilities such as asset identification, one\-click disablement, and behavior guardrails.

## Client

### Desktop applications

|**Tool name** |**Asset identification** |**One\-click disablement** |**Document outgoing control** |**AI development tools operation control** |**Agent behavior guardrails** |**Agent full link audit** |
|---|---|---|---|---|---|---|
|Aime Desktop |✖️win |✅ | | | | |
|Antigravity Desktop |✅ |✅ | | | | |
|CDClaw |✅ |✖️mac | | | | |
|Chatbox | | |✅ | | | |
|ChatGPT Desktop |✅ |✅ |✅ |✅ |✅ |✅ |
|Cherry Studio |✅ |✅ |✅ | | | |
|Claude Code Desktop |✅ |✅ |✅ |✅ |✅ |✅ |
|CodeBuddy CN Desktop |✅ |✅ | | | |✅ |
|Cursor |✅ |✅ |✅ |✅ | |✅ |
|Deepseek Harness | | | | | |✅ |
|Dola |✅ |✅ | | | | |
|EasyClaw | | |✅ | | | |
|Gemini Desktop |✖️win |✅ |✅ | | | |
|Kimi |✅ |✅ |✅ | | | |
|Mira Desktop |✅ |✅ | | | | |
|OpenCode Desktop |✅ |✅ | | | |✅ |
|Poe | | |✅ | | | |
|QClaw |✅ |✅ |✅ | | | |
|Qoder CN Desktop |✅ |✅ | | | |✅ |
|QoderWork CN |✅ |✅ | | |✅ | |
|QwenPaw |✅ |✅ | | | | |
|QwenWork |✅ |✅ | | | | |
|StepClaw | | |✅ | | | |
|TRAE Desktop |✅ |✅ |✅ |✅ | | |
|TraeCode CN Desktop |✅ |✅ |✅ |✅ | |✅ |
|TRAE Work Desktop |✅ |✅ | | | | |
|TraeWork CN Desktop |✅ |✅ |✅ | |✅ |✅ |
|Windsurf/Devin Desktop |✅ |✅ | | | | |
|WorkBuddy |✅ |✅ |✅ | |✅ |✅ |
|Doubao |✅ |✅ |✅ |✅ | |✅ |
|Doubao Work |✅ |✅ | | | |✅ |
|Coze |✅ |✅ | | | | |
|Tiangong AI | | |✅ | | | |
|Qwen |✅ |✅ |✅ | | | |
|Wenxiaoyan | | |✅ | | | |
|iFlytek Spark |✅ |✅ | | | | |
|Yuanbao |✅ |✅ |✅ | | | |
|Zhipu Qingyan |✅ |✅ |✅ | | | |
|Autoclaw |✅ |✅ | | | | |

### Command\-line tools (CLI)

|**Tool name** |**Asset identification** |**One\-click disablement** |**Document outgoing control** |**AI development tools operation control** |**Agent behavior guardrails** |**Agent full link audit** |
|---|---|---|---|---|---|---|
|Antigravity CLI |✖️win |✅ | | | | |
|Claude Code CLI |✅ |✅ |✅ |✅ |✅ |✅ |
|CodeBuddy CN CLI |✅ |✅ |✅ | | |✅ |
|Codex CLI |✅ |✅ |✅ |✅ |✅ |✅ |
|Cursor CLI | | | | | |✅ |
|Gemini CLI |✅ |✅ | | | | |
|GitHub Copilot CLI |✅ |✅ | | | | |
|Grok CLI |✅ |✅ | | | | |
|Hermes |✅ |✅ | | |✅ | |
|Openclaw |✅ |✅ |✅ | |✅ | |
|OpenCode CLI |✅ |✅ | | | |✅ |
|Qoder CN CLI |✖️win |✅ |✅ | | |✅ |
|TraeCode CN CLI |✖️win |✅ | | | | |
|Windsurf/Devin CLI |✖️win |✅ | | | | |
|WorkBuddy CLI | | | | |✅ |✅ |

## IDE Plugins

> **说明**

> IDE plugin control currently covers four mainstream IDE tools: VS Code, Windsurf, Cursor, and Trae.

|**Tool name** |**Asset identification** |**One\-click disablement** |**Document outgoing control** |**AI development tools operation control** |**Agent full link audit** |
|---|---|---|---|---|---|
|Claude Code for VS Code |✅ |✅ |✅ |✅ |✅ |
|Codex – OpenAI’s coding agent |✅ |✅ |✅ |✅ |✅ |
|Gemini Code Assist |✅ |✅ | | | |
|GitHub Copilot |✅ |✅ | | | |
|GitHub Copilot Chat |✅ |✅ | | | |
|TRAE AI: Coding Assistant |✅ |✅ | | | |

## Policy configuration guide

Policy configuration entry points for the preceding AI tool control capabilities are distributed across different feature modules in the Admin Console. You can use the table below to quickly locate each policy and follow the corresponding documentation to complete the configuration.

|**Control policy** |**Configuration entry point** |**Related documentation** |
|---|---|---|
|**Asset identification / One\-click disablement** |AI Security \> Asset Inventory |[Agent asset inventory and control](https://docs.byteplus.com/docs/sealsuite/agent-asset-inventory-and-control) |
|**Document outgoing control** |DLP \> Strategy Center \> Control strategy \> Document outgoing control |[Configuring document outgoing control policies](https://docs.byteplus.com/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule) |
|**AI development tools operation control** |DLP \> Strategy Center \> Control strategy \> AI development tools operation control |[Configuring AI development tools operation control policies](https://docs.byteplus.com/docs/sealsuite/configuring-ai-development-tools-operation-control-policies) |
|**Agent behavior guardrails** |AI Security \> Security Protection \> Agent Behavior Guardrails |[Configuring Agent behavior guardrails policy](https://docs.byteplus.com/docs/sealsuite/configuring-agent-behavior-guardrails-policy) |
|**Agent full link audit** |AI Security \> Security Protection \> Agent Full Link Audit |[Agent full link audit](https://docs.byteplus.com/en/docs/sealsuite/agent-full-link-audit) |
