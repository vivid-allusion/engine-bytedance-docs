---
title: "SDK overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/SDK_overview"
---

This topic provides a brief overview of the AgentKit SDK, covering its core architecture design, module dependencies, and key features.

<span id="bVCNuPHf"></span>
## SDK introduction

AgentKit SDK is a Python development toolkit for quickly building Agent applications that comply with the AgentKit standard. The SDK provides a set of concise decorators and client interfaces ([AgentKit API overview](https://docs.byteplus.com/en/docs/agentkit/API_overview)). This helps developers focus on implementing agent business logic and creating and managing resources.

<span id="GT8zamLl"></span>
## SDK address


|Programming language |GitHub address |Guide |
|---|---|---|
|Python |[agentkit-sdk-python](https://github.com/volcengine/agentkit-sdk-python) |[Installation guide](https://volcengine.github.io/agentkit-sdk-python/content/1.introduction/2.installation.html) |


<span id="MOFEpqqa"></span>
## Core architecture

AgentKit SDK adopts a modular design built around these main parts:

<span id="DqZU9ZDR"></span>
### Runtime application framework

Provides multiple application modes and encapsulates user code into HTTP services that comply with the AgentKit standard:

<span id="xuMvt8RS"></span>
#### AgentKitSimpleApp

The most commonly used application framework, applicable for standard Agent applications.

**Core decorators**:


* `@app.entrypoint`: Defines the main entry function of an Agent.

* `@app.ping`: Defines the health check function.


**Standard routes**:


* `/invoke`: Agent call endpoint.

* `/ping`: Health check.

* `/health`, `/readiness`, `/liveness`: Kubernetes readiness probes.


<span id="9D4xoDXg"></span>
#### AgentKitMCPApp

An application framework based on the MCP (Model Context Protocol) protocol, used to encapsulate tools as MCP services.

**Core decorators**:


* `@app.tool`: Registers a function as an MCP tool.

* `@app.agent_as_a_tool`: Encapsulates an Agent as an MCP tool.


<span id="6UZMqxdq"></span>
#### AgentKitA2aApp

An application framework based on the A2A (Agent\-to\-Agent) protocol, used to build Agents that can communicate with each other.

**Core decorators**:


* `@app.agent_executor`: Registers an Agent executor.

* `@app.task_store`: Registers task storage (optional).


<span id="TMiiAHG0"></span>
### AgentKit service client

Provides convenient client interfaces for accessing various services on the AgentKit Platform.

<span id="0xiGhBNy"></span>
#### AgentKitMemory

A client for the memory service, managing the agent's long\-term and short\-term memory.

**Main features**:


* `create_memory_collection()`: Creates memory.

* `list_memory_collections()`: Lists memories.

* `get_memory_collection()`: Retrieves memory details.

* `update_memory_collection()`: Updates memory configuration.

* `delete_memory_collection()`: Deletes memory.

* `get_memory_connection_info()`: Retrieves connection information.


**Design concept**: Control plane and data plane decoupling


* **Control plane** (provided by SDK): Manages memory creation, configuration, and connection information.

* **Data plane** (ADK implementation): Memory read and write operations are handled via the MemoryBase or Mem0 protocol.


<span id="jYVa4ZLo"></span>
#### AgentKitKnowledge

A knowledge base service client that provides management capabilities for a vectorized knowledge base of an Agent.

**Main features**:


* `list_knowledge_bases()`: Lists knowledge bases.

* `add_knowledge_base()`: Adds a knowledge base.

* `get_knowledge_connection_info()`: Retrieves knowledge base connection information.

* `delete_knowledge_base()`: Deletes knowledge base.


**Applicable scenarios**:


* Retrieval\-Augmented Generation (RAG) applications

* Document Q&A systems

* Knowledge graph integration


<span id="bdTjjUuP"></span>
#### AgentKitMCP

An MCP Gateway client for managing and routing a large number of MCP tools.

**Main features**:


* Used to register and manage MCP services.

* Aggregates tools and provides intelligent routing capabilities.

* Reduces tool integration complexity.


<span id="MBFo8L2b"></span>
#### AgentKitRuntime

A Runtime management client for managing the runtime environment of Agents.

**Main features**:


* Enables the creation and management of runtime instances.

* Allows querying of Runtime status.

* Used to configure environment variables and resources.


<span id="ckvIVYUT"></span>
### Infrastructure modules

<span id="wX3L9YI6"></span>
#### BaseAgentKitClient

The base class for all clients, providing unified configuration and HTTP request capabilities.

**Configuration items**:


* API endpoint configuration

* Authentication credential management

* Request retry and timeout settings

* Logging and monitoring


<span id="Oyfwzu45"></span>
#### Context management

Uses `contextvars` to manage the context information of each request, including:


* User identity

* Session ID

* Request metadata

* Tracing information


<span id="OMrLMAQn"></span>
## Module dependencies

```Plain Text
AgentKit SDK
│
├── Runtime Apps (Application framework)
│   ├── AgentkitSimpleApp
│   ├── AgentkitMCPApp
│   ├── AgentkitA2aApp
│   └── AgentkitAgentServerApp
│
├── Platform Clients (Service client)
│   ├── AgentkitMemory
│   ├── AgentkitKnowledge
│   ├── AgentkitMCP
│   └── AgentkitRuntime
│
└── Infrastructure (Infrastructure Layer)
    ├── BaseAgentkitClient
    ├── Context
    └── Telemetry (Observability)
```


<span id="kYGwpERK"></span>
## Main features

<span id="pzRUsuYX"></span>
### Decorator\-driven

Simplified application development with Python decorators. This allows developers to focus only on business logic.

```Python
from agentkit.apps import AgentkitSimpleApp

app = AgentkitSimpleApp()

@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    # Business logic
    return response
```


<span id="VlFJGHhA"></span>
### Framework agnostic

The SDK does not restrict the use of specific Agent frameworks. It supports:


* Volcengine ADK (VeADK)

* Google ADK (gadk)

* LangChain

* Custom frameworks


<span id="TcXlhxl0"></span>
### Automated observability

Built\-in OpenTelemetry support enables automatic collection of:


* Tracing data (Tracing)

* Performance metrics (Metrics)

* Logs (Logging)


<span id="sZQovTaj"></span>
### Production ready

Provides comprehensive production environment support, including:


* Health check endpoints

* Graceful shutdown

* Error handling

* Request retry


<span id="uDcGiC8W"></span>
### Type security


* Complete Python type annotations, which enable:

* IDE autocompletion

* Type checking

* Improved code maintainability
