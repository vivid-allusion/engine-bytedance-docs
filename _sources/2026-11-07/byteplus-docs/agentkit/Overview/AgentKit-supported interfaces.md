---
title: "AgentKit-supported interfaces"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/AgentKit-supported_interfaces"
---

BytePlus AgentKit provides multiple operation interfaces for the development and deployment of AI agents. The simplest method is to use the AgentKit Python SDK to write agent code and deploy agents with the AgentKit starter toolkit.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The AgentKit Python SDK and CLI do not support all agent operations provided by VeADK. If a specific agent operation is unsupported by either, implement it via the VeADK multilingual development toolkit.</div>


<span id="Y2af2YG6"></span>
## AgentKit starter toolkit

The AgentKit starter toolkit provides a command\-line interface tool ([AgentKit CLI](https://docs.byteplus.com/en/docs/agentkit/CLI_overview)) and a development toolkit ([AgentKit Python SDK](https://docs.byteplus.com/en/docs/agentkit/SDK_overview)). This enables core operations throughout the agent development and deployment process.


* **AgentKit CLI**: A command\-line tool complements the capabilities of the AgentKit console. It supports developers in rapid engineering operations and can be combined with automatic scripts to automate the agent DevOps process.

* **AgentKit Python SDK**: A development toolkit for agents tailored by BytePlus for Python developers. It deeply encapsulates VeADK core capabilities and provides a minimalist decorator\-style API. This allows developers to focus on business logic development without concern for underlying framework details, thus lowering the development barrier. Built\-in core capabilities include:

   * Runtime encapsulation: Lightweight encapsulation of VeADK agent runtime capabilities. You can quickly define the agent entry function via `@app.entrypoint`, simplifying code writing.

   * Memory integration: Seamless integration with short\-term and long\-term memory services. This provides persistent storage for conversation history and agent context.

   * Tool calling: Built\-in BytePlus ecosystem tool clients. This feature supports one\-click calling of tools such as web search, image generation, and code sandbox.

   * Authentication: Secure identity authentication and access management based on AgentKit Identity, ensuring the security of agent development and operation.

   * Platform service integration: Out‑of‑the‑box access to AgentKit platform services such as memory, knowledge base, and MCP Gateway, without additional integration and development.

   * Multi\-framework adaptation: Compatibility with mainstream agent development frameworks, which enables flexible development and migration of business logic.

   The AgentKit Python SDK supports multiple development frameworks, including Google ADK and LangGraph. If you need to use other BytePlus services, integrate them by building on your existing code with the VeADK multilingual development toolkit.


<span id="HCOdbUe8"></span>
## AgentKit MCP

AgentKit MCP is the tool integration hub of the BytePlus agent ecosystem. Built on the model context protocol, it enables standardized connections between agents and various tools and services. Its core capabilities include:


* Unified tool access: Connects to a vast array of tools in the MCP marketplace and supports standardized access and management of third‑party custom tools.

* Gateway lifecycle management: Uses APIs and CLI to create, configure, update, and destroy gateways, to meet tool calling requirements in different business scenarios.

* Local and cloud collaboration: Supports debugging and calling of tools in local development environments, and seamlessly connects to the cloud production environment to simplify development and testing.

* Calling policy control: Provides fine‑grained control over agent tool calling behaviors, including calling permissions, rate limits, and result filtering to ensure calling security.

* Multi\-client compatibility: Adapts to mainstream MCP clients and supports session‑based command invocation, enabling automation of complex tool calling workflows.


<span id="qMVqn8H0"></span>
## VeADK (BytePlus agent development kit)

You can use [VeADK](https://volcengine.github.io/veadk-python/) to implement all AgentKit Python SDK features and perform additional operations that the AgentKit Python SDK does not support. To integrate with other BytePlus services or when Python is not used as the development language, you need to use this toolkit.

When you configure and deploy agents, use the AgentKit control plane API to perform actions like creating an agent runtime, updating agent runtime configurations, and managing gateways.

During agent runtime, you can perform various actions through the AgentKit data plane API, such as adding memory events to the agent's memory. You can call an agent deployed in an agent runtime by performing the corresponding data plane operations via client code.

<span id="8MTUA3Yk"></span>
## AgentKit console

You can create and manage various AgentKit services required for agent operation in the AgentKit console. You can also obtain integration code snippets for services deployed in the agent runtime.
