---
title: "Features"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Product_features"
---

This topic details the features provided by AgentKit.

<span id="LhNXtyR3"></span>
## Core features

<span id="aWhA0rJW"></span>
### **Rich product components**


|Product component |Description |Related documents |
|---|---|---|
|Agent runtime |Runtimes are the cloud\-hosted execution environments and lifecycle containers for agents. One agent runtime corresponds to one agent and is responsible for agent startup, operation, and resource boundary management.<br><br>Their core value is to standardize agent execution into a scalable, rollback\-capable, and maintainable production model, enabling stable delivery and continuous iteration. |[Runtime overview](https://docs.byteplus.com/en/docs/agentkit/Agent_runtime_overview) |
|A2A Center |The A2A Center is the inter\-agent connectivity and collaboration management unit built on the Agent\-to\-Agent (A2A) protocol. One A2A connection represents a standardized communication channel between agents, responsible for cross\-agent task dispatching, result callback, and state synchronization.<br><br>Its core value is to standardize multi\-agent collaboration into an orchestratable and governable model, supporting parallel and sequential multi\-agent execution in complex workflows. |[Overview of the A2A Center](https://docs.byteplus.com/en/docs/agentkit/A2A_Center_overview) |
|Skill |A Skill is a reusable capability packaging unit that consolidates the knowledge instructions, execution flow, code scripts, and associated resources required for a task, enabling an agent to execute specific tasks on demand and reliably, similar to calling a function library.<br><br>Its core value is to consolidate reusable capability boundaries, support versioned management and collaborative reuse, reduce redundant development, and improve delivery consistency. |* [AgentKit Studio Skill overview](https://docs.byteplus.com/en/docs/86681/2228348)<br><br>* [Skills Center overview](https://docs.byteplus.com/en/docs/agentkit/Skill_Overview) |
|Tool |Tools provide the runtime environment tools and modular capability packages required by agents during task execution, supporting rapid integration and convenient calling.<br><br>Their core value is to lower the barrier to agent capability extension, allowing developers to introduce tool capabilities as needed and improving task execution flexibility and efficiency. |* [Tool overview](https://docs.byteplus.com/en/docs/agentkit/Tool_overview)<br><br>* [Tool types](https://docs.byteplus.com/en/docs/agentkit/Tool_type)<br><br>* [Procedure](https://docs.byteplus.com/en/docs/agentkit/Procedure) |
|Sessions |Sessions provide short\-term memory management for organizing multi\-turn interaction context and persisting short\-term memory, ensuring conversational continuity and a stable state.<br><br>Their core value is to support one\-click configuration and integration with mainstream relational databases (MySQL, RDS PostgreSQL, etc.), enabling reliable persistence of short\-term conversation context into existing databases for continuous operation and analysis in production environments. |[Sessions overview](https://docs.byteplus.com/en/docs/agentkit/Sessions_overview) |
|Memory |Memories provide enterprise\-grade long\-term memory management for storing and retrieving accumulated cross\-session information and recalling it when needed.<br><br>Their core value is to connect to mainstream memory store frameworks through a unified interface, helping agents achieve cross\-session context awareness, personalized interaction, and continuous evolution while meeting enterprise\-grade permission and governance requirements. |[Memory overview](https://docs.byteplus.com/en/docs/agentkit/Memory_overview) |
|Knowledge base |Knowledge bases manage enterprise knowledge assets and provide retrieval\-augmented capabilities for agents, supporting one\-click configuration, import, and association with mainstream knowledge bases.<br><br>Their core value is to provide a unified knowledge base interface and framework integration approach, reducing the cost of connecting and switching across multiple knowledge sources, and enabling enterprise knowledge to be used by agents in a controllable, updatable, and evaluable way. |[Knowledge base overview](https://docs.byteplus.com/en/docs/agentkit/Knowledge_base_overview) |
|Gateway |Gateways provide a unified access point for connecting agents with external systems and services and handling data exchange, while providing a secure and reliable access channel for MCP services.<br><br>Their core value is to support rapid API\-to\-MCP conversion for faster integration of existing systems, provide semantic\-search\-based automatic tool matching to improve tool discovery and calling efficiency, and facilitate governance policies such as authentication, throttling, and fault isolation. |[Gateway overview](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview) |
|Identity and permissions |Identity and permissions capabilities handle user authentication, credential management, and permission boundary management, and validate an agent's controlled access to internal and external resources.<br><br>Their core value is to provide an auditable access chain and consistent authorization governance mechanism, ensuring that agent inbound and outbound operations meet enterprise requirements for security isolation and compliance. |[Identity and permissions](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01) |
|Observability |Observability provides an end\-to\-end application observability system covering real\-time monitoring, metric collection, logging, anomaly detection, and alerting, along with visual dashboards for key component status.<br><br>Its core value is to improve observability and diagnosability in production environments, support foundational monitoring and issue identification for memories and MCP services, and provide a basis for tuning and stability maintenance. |[Observability overview](https://docs.byteplus.com/en/docs/agentkit/Observability_overview) |
|Log |Logging provides persistent log storage, log delivery, and viewing capabilities. Enabling observability for resources deployed in AgentKit automatically enables log collection and retrieval.<br><br>Its core value is to cover full runtime logs for runtime, tools, and MCP services, supporting log retrieval and information analysis to help quickly identify resource anomalies and support audit tracing. It provides persistent log storage capability. Observability is enabled by default for resources deployed in AgentKit, requiring no additional configuration. Log delivery and viewing are available immediately. |[Enable logs](https://docs.byteplus.com/en/docs/agentkit/Enabling_logs) |


<span id="M74QPwM5"></span>
### **Support for multiple frameworks and deployment methods**


* Supports native agent building with [VeADK](https://deepwiki.com/volcengine/veadk-python). Agents built with VeADK can connect directly to AgentKit and reuse the platform capabilities and runtime governance system.

* Provides an **AgentKit SDK decorator\-based** adaptation solution, allowing agents built with mainstream **Python frameworks** to access AgentKit through lightweight adaptation.

* Supports migration of existing agents built with **LangChain, LangGraph, ADK, Strands**, and **Bedrock AgentCore**, converting them into applications deployable on the AgentKit cloud.

* Supports multiple deployment options, including **local code packages** and **container images**.

* Supports multiple access protocols, including **HTTP Server, A2A, and MCP**, to suit different system integration and calling scenarios.


<span id="gPJ99oBI"></span>
### Serverless service model


* Provides a **Serverless hosting** mode with no O&M required, reducing environment dependencies and configuration costs, and lowering delivery and O&M complexity.

* Supports **Pay\-as\-you\-go billing** and elastic scaling. Compute resources are dynamically adjusted based on online traffic, reducing resource waste from overprovisioning during peak periods and idleness during off\-peak hours, and improving cost efficiency.
