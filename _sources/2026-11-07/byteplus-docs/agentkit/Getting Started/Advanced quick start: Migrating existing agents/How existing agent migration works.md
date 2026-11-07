---
title: "How existing agent migration works"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/How_existing_agent_migration_works"
---

<span id="ppkAUPmN"></span>
## Two migration methods: high\-code and low\-code

The same `agentkit migrate` entrypoint has two built\-in migration paths, determined by `--framework`. There is only one selection criterion: **whether the deliverable is loadable framework source code or a DSL/exported project from a low\-code platform.** 


<columns>
<columnsItem zoneid="uX0WT0IC">

**High\-code method (structured framework migration)** 

For LangChain, LangGraph, ADK, Strands, and Bedrock AgentCore. Executes **locally** and generates an AgentKit hosting layer alongside the original project: a wrapper for simple call scenarios, or a bridge when runtime behavior is required.


* Source code is preserved with minimal intrusion. Business source code is not statically modified.

* Generated files are written to the project root directory, defaulting to `AgentkitAgentServerApp`.

* Completed with a single command: `agentkit migrate --framework <fw> --entry <entrypoint>`.

</columnsItem>
<columnsItem zoneid="GcNFcyqG">

**Low\-code method (platform migration)** 

For Dify (`--framework dify`) and any framework (`--framework any`). Runs a **remote sandbox** task, driven by Codex for conversion.


* `create` uploads the source code and starts Codex. `status` queries and downloads the output.

* Generates a migration profile first, then performs DSL native conversion, hybrid migration, or spec\-based reconstruction.

* Outputs a native AgentKit + VeADK project and **automatically generates an evaluation dataset**.

* The output must be written outside the source directory (e.g., `../agentkit-output`).

</columnsItem>
</columns>


&nbsp;

The fundamental difference: wrapping vs. rebuilding


* High\-code: The original runnable code is loaded as the source object, with a protocol conversion layer wrapped around it. Business code is preserved as\-is.

* Low\-code: There is no directly loadable runtime object. Codex analyzes the platform configuration in a sandbox and regenerates the project following AgentKit best practices. The business identity, input semantics, and tool boundaries, instead of the original files, are preserved.


<span id="3pxoOQNG"></span>
## Takeover boundaries and preservation boundaries

Migration boundaries operate at two levels: the **general layering** between AgentKit and the original framework, and the specific items taken over or preserved for **each framework** under each migration method.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the high\-code method, the preservation boundary is the original runnable code, and AgentKit only wraps a protocol layer around it. For the low\-code method, the preservation boundary is the business semantics, and AgentKit is responsible for rebuilding the entire project based on those semantics. Capabilities with strong platform dependencies or low confidence are added to the migration plan and require manual confirmation, rather than being hosted or forwarded to an external application.</div>


<span id="NzSaJkmh"></span>
### General layering: What AgentKit takes over and what the framework preserves


<columns>
<columnsItem zoneid="cx2iWO54eT">

**AgentKit unified takeover layer**


* Service entrypoint and protocols: `/run`, `/run_sse`, session, A2A

* Runtime and deployment configuration: runtime name, env mapping, Dockerfile

* User and session context

* Streaming event normalization

* Observability: OTel/APMPlus collection

</columnsItem>
<columnsItem zoneid="W7Vutvmaxn">

**Original framework preservation layer**


* Business orchestration logic and prompts

* Agent/Graph status and execution model

* Tools and ecosystem dependencies

* Model call method (optionally replaced with an ARK model via `--model-id`)

* Business semantics of the original framework

</columnsItem>
</columns>


<span id="NcSgfYZa"></span>
### High\-code method: Takeover and preservation boundaries per framework

In the high\-code method, AgentKit hosts the entrypoint alongside, while business execution is still handled by the original framework code. The preservation boundary is therefore the original runnable logic.


|**Framework** |**AgentKit takeover boundary** |**Original framework preservation boundary** |
|---|---|---|
|LangChain |Unified standard `/run` and streaming `/run_sse` interfaces, session management, and streaming event output |Runnable, callable functions, LCEL orchestration chain, and agent executor are fully preserved. When compatibility mode (`--compat`) is not enabled, existing HTTP call interfaces require minor modifications. |
|LangGraph compiled graph |Hosts the unified entrypoint communication protocol and exposes streaming node and interrupt capabilities. |The message state, input key, and the original graph execution logic are preserved. Full HITL resume protocol is not automatically generated. Complex persistence requires user configuration. |
|LangGraph Server |Mounts a set of standard AgentKit protocol routes on top of the original service, with both protocols coexisting. |The official LangGraph configuration file and native interfaces (`/threads` for session management, `/runs/stream` for streaming tasks) are fully preserved, and both the original and new interfaces can serve traffic simultaneously. |
|ADK |`AgentkitAgentServerApp` hosts `/run`, `/run_sse`, session management, and A2A cross\-agent communication. |Original ADK tools, callbacks, and sub\-agent scheduling logic are fully preserved. A2A capability relies on ADK experimental features and may change in later versions. |
|Strands |Creates a new agent instance per session and wraps it with a unified standard communication protocol. |All Strands business logic and custom tools remain unchanged. A zero\-argument factory function is recommended as the project entry point to prevent cross\-session data interference. |
|Bedrock AgentCore |Adds standard AgentKit protocol support while preserving the existing `/ping` health check and `/invocations` interface. |The core agent business logic remains unchanged. Platform\-side capabilities, including IAM authentication, workload identity, Memory, Gateway, MCP tools, and credentials, remain the responsibility of the original project and deployment environment. |


<span id="tqMwmwQj"></span>
### Low\-code method: Takeover and preservation boundaries

In the low\-code method, there is no loadable runtime object. AgentKit takes over the **full reconstruction and hosting of the project**: Codex rebuilds the platform configuration into a native AgentKit + VeADK project in a sandbox, and AgentKit then provides unified protocol support, deployment, and observability.


|**Scenarios** |**AgentKit takeover boundary** |**Preservation boundary** |
|---|---|---|
|Dify |Automatically parses workflows, chatflows, prompts, tools, and model configurations. Reconstructs the full runtime project based on VeADK + AgentKit and outputs migration documentation, interface contracts, and automated test cases. |The business positioning, input semantic logic, and tool call rules are preserved. A semantic reconstruction solution is used. The original project is not directly wrapped. |
|any (any agent framework, fallback solution) |Codex performs static and dynamic code analysis on the source code, rebuilds the project based on VeADK standards, and automatically generates an evaluation dataset. |The original core business logic, input/output semantics, tool capabilities, and deployment characteristics are preserved. The acceptance criterion is full alignment with core business capabilities, not just basic conversation support. |


<span id="u32GGACr"></span>
## Migration principles

Migration does not rewrite business logic. Instead, it generates an AgentKit hosting layer alongside the project. The original project's Agent, Graph, ADK `root_agent`, Strands agent, or `BedrockAgentCoreApp` entrypoint is still loaded as the **source object**. The AgentKit SDK bridge handles the conversion of inputs, outputs, streaming events, sessions, and compatibility routing to the AgentKit protocol.

```Plain Text
Source project
  └─ agentkit migrate
      └─ generated agentkit_app.py
          ├─ default: AgentkitAgentServerApp
          │   └─ /run  /run_sse  /session  /A2A
          └─ --server-mode langgraph: AgentkitLangGraphServerApp
              ├─ AgentKit routes
              └─ native LangGraph Server routes
```



* High\-code migration method

   * `agentkit_app.py` is automatically generated. This file loads the user's original entry point and creates the hosting service application.

   * Simple call scenarios: A lightweight wrapper is generated to handle request forwarding.

   * When runtime capabilities such as session, `run_async`, `/run_sse`, streaming events, or A2A are required, a framework bridge adapter layer is automatically generated. The original framework's native execution chain is preserved throughout.

* Low\-code migration method

   * The source project is parsed in a remote sandbox. Codex rebuilds a new project based on VeADK + AgentKit standards. The output is a complete, standalone project, not a simple wrapper around the original source code.

* Unified observability

   * The migration output is integrated with AgentKit runtime's OTel/APMPlus collection pipeline by default. Request spans, framework bridge spans, and core metrics are all attached to the same trace.

   * The migrate tool does not statically modify any LangSmith, Strands telemetry, ADK telemetry, or custom OpenTelemetry initialization code in the original project.

   * If any such instrumentation logic is detected, it is recorded in `migration-plan.json` along with boundary adaptation messages.
