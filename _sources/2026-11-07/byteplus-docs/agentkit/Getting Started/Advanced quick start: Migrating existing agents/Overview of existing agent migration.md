---
title: "Overview of existing agent migration"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Overview_of_existing_agent_migration"
---

<span id="aDgfwQ4v"></span>
## Capability overview

`agentkit migrate` is a command\-line migration workflow that converts a customer's existing agent projects into standard applications that can be deployed and called on the AgentKit platform.

**Problems it solves:** 


* Existing agents are built with a variety of frameworks and platforms, each with different entrypoints, protocols, session models, and observability, making it impossible to run them directly on AgentKit cloud.


**Migration boundaries:** 


* **AgentKit takes over the service entrypoint, protocol, deployment configuration, session context, and observability. The original business orchestration and execution model remains unchanged.** 

* After migration, applications expose the AgentKit protocols `/run`, `/run_sse`, session, and A2A by default, so the same business logic gains cloud deployment, unified authentication, and distributed tracing without any rewrite.


**What migration gives you:** 


* **Unified entrypoint:**  All frameworks are converged to `AgentkitAgentServerApp` (the AgentKit framework), with a consistent external\-facing protocol.

* **Zero business logic rewrite:**  The original agent, graph, tool, and model call logic is preserved. Migration only generates a hosting layer alongside the existing code or rebuilds one semantically.

* **Cloud deployment:**  Generates `deploy` configurations, Dockerfile, and a migration plan. Once deployed with `agentkit deploy`, the applications are ready to be called via `invoke`.

* **Default observability:**  Migrated applications are integrated with AgentKit runtime's OTel/APMPlus collection by default. Request spans and bridge spans are linked in a single trace.


<span id="SXkifWYB"></span>
## Supported migration frameworks

The migration tool classifies existing projects into two categories based on **whether loadable framework source code is available**. For high\-code frameworks, an integration layer is generated locally. For low\-code platforms, the project is rebuilt in a remote sandbox.


|**Framework** |**Migration method** |**Entry format (**  **`--entry`** **)**  |**Migration description** |
|---|---|---|---|
|LangChain |High\-code |`file.py:object` |Supports the full capabilities of Runnable, LCEL orchestration, and Agent executors. Existing LangServe interfaces require no modifications. Add `--compat langserve` at startup to maintain compatibility with existing callers. |
|LangGraph compiled graph |High\-code |`graph.py:graph` |Suitable for projects that already have a Graph workflow defined. By default, it is directly compatible with the standard chat message structure (messages state). Use `--input-key` for custom state fields, and use `--stream-node` to specify streaming nodes. |
|LangGraph Server |High\-code |`langgraph.json[:graph_id]` |For official LangGraph online service projects, add `--server-mode langgraph` at startup. After migration, the service simultaneously supports native LangGraph interfaces (`/threads`, `/runs/stream`) and the AgentKit standard protocol. Original business calls are not affected. |
|ADK |High\-code |`agent.py:root_agent` |Native ADK agents can be migrated seamlessly without an intermediate conversion layer. The original tools (ADK tools), callbacks, and sub\-agent scheduling logic are fully preserved. The agents are finally deployed as standard AgentKit online services. |
|Strands |High\-code |`agent.py:build_agent` |A zero\-argument factory function is recommended as the program entry point. After migration, a Strands agent instance is created for each conversation session independently, preventing state confusion and data interference across multi\-user conversations. |
|Bedrock AgentCore |High\-code |`app.py:app` |For projects already using the official Bedrock framework (`BedrockAgentCoreApp`). After migration, AgentKit standard interfaces are provided, while the original `/ping` health check and `/invocations` interfaces are preserved. The full Bedrock AgentCore Runtime platform capabilities are not replaced. |
|Dify |Low\-code |Remote `create`/`status` |No significant code changes are required. Upload your Dify workflow or chatflow configuration file, and the tool automatically parses the prompts, model configurations, and tool configurations to generate a complete VeADK project, test cases, and migration documentation in one step. |
|any (any agent framework) |Low\-code |Remote `create`/`status` |A generic fallback migration solution suitable for any agent project with source code. Codex automatically analyzes the existing project code, rebuilds the entire project according to VeADK best practices, and automatically generates batch evaluation cases to reduce manual rebuilding workload. |
