---
title: "Quick start"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/user_quick_start"
---

This topic describes the complete process for developing, deploying, and managing agents via VeADK, the AgentKit CLI, and the AgentKit platform.

<span id="2eaEUjtU"></span>
## Relationship between AgentKit and VeADK

AgentKit is an enterprise\-grade AI agent platform that integrates VeADK and BytePlus ecosystem capabilities. Through a visual console, CLI tool, and other infrastructure, AgentKit lowers the barriers to agent development, deployment, and operations. It also supports integrating agents built with third\-party frameworks. VeADK serves as an agent development toolkit, providing a comprehensive capability abstraction and development framework.​ The two components complement each other: VeADK, as an agent development toolkit, enables modular capability integration for convenient agent development for users. AgentKit is designed to deliver a user\-friendly operational experience and deployment and operations capabilities. Together, they cover the full lifecycle requirements of agents from development and debugging to deployment and operations.

<span id="zSk2iilM"></span>
## Agent building and deployment workflows

Processes for developing, deploying, and managing agents are shown in the following figure. We recommend that you use the [VeADK](https://deepwiki.com/volcengine/veadk-python) development framework to build agents.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c3becf5e7a85b378f824bc07fdc6d5a6.png) </span>


1. Determine the foundation model and components (such as tools, memory, and knowledge base) of the agent, and use VeADK or other mainstream agent development frameworks to build the agent.

2. Use the AgentKit CLI to deploy the agent to AgentKit.

3. Test the agent via the online test feature in the AgentKit console or the AgentKit CLI tool.

4. Manage the agent in AgentKit.


<span id="FNXt2O3L"></span>
## Quick start


* [Rapidly deploy an agent via the console](https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_AgentKit)

   Ideal for beginners, quick demos, or non\-developer operators.

* [Deploy an agent via the CLI tool](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool)

   Ideal for developers during daily development and debugging, and applicable to automated deployment processes and custom builds.

* [End-to-end agent development and deployment](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial)

   Applicable to complex enterprise\-grade agent development, deep integration with the BytePlus ecosystem, long\-term iteration and optimization, and cross\-platform or multi\-protocol integration scenarios.


<span id="JI2yE9KT"></span>
## Key components


|Component |Description |Related documents |
|---|---|---|
|Tool |Integrates built\-in sandbox tools (AIO Sandbox, Skills Sandbox, and Code Sandbox), custom tools, and VeADK built\-in tools to support quick calls. |[Tool types](https://docs.byteplus.com/en/docs/agentkit/Tool_type)<br><br> |
|Memory |Enables cross\-session context storage and personalized interactions. |[Memory overview](https://docs.byteplus.com/en/docs/agentkit/Memory_overview) |
|Knowledge Base |Allows one\-click import of mainstream knowledge bases and supports knowledge retrieval. |[Knowledge base overview](https://docs.byteplus.com/en/docs/agentkit/Knowledge_base_overview) |
|Gateway |Manages connections and data exchange between agents and external systems, delivers fast API\-to\-MCP conversion capabilities, and supports automatic matching of the most relevant tools via semantic search. |[MCP overview](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview) |


<span id="ke90hnPu"></span>
## Deployment modes

The AgentKit CLI supports flexible deployment modes tailored to different stages from development to production.


|Deployment modes |Core advantages |Applicable scenario |
|---|---|---|
|Local mode (Local) |Fast iteration, offline support, and convenient direct testing. |Suitable for rapid development and testing. |
|Cloud mode (Cloud) |Eliminates the need for a local Docker environment. Leverages cloud\-based continuous delivery products for fully cloud\-based deployment, with built\-in observability, high environment consistency, enhanced security, and reliability. |Suitable for production environments. |
|Hybrid mode (Hybrid) |Balances the flexibility of local builds with the stability of cloud runtime environments. |Suitable for the development and debugging phase; build an image locally and then push it to the cloud to run. |
