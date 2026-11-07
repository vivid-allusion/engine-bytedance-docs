---
title: "Runtime overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Agent_runtime_overview"
---

An agent runtime (hereinafter referred to as the "runtime") is a hosted runtime environment provided by AgentKit for agents. It provides security isolation and is framework\- and model\-agnostic, supports automatic scaling of associated instances based on business traffic, and supports built\-in IAM roles to control the permissions for the agent runtime to access cloud resources.

<span id="GDcisAA4"></span>
## What is a runtime

A runtime is where an agent actually runs. After you create a runtime, AgentKit generates an agent runtime environment that can be hosted, published, and observed based on the code or image you provide, runtime configurations, model configurations, secure access rules, and associated component information. For users, a runtime serves as the deployment carrier for an agent, as well as its invocation entry, version management unit, and O&M management unit.

In terms of its role, the runtime sits between "development completed" and "live service". Upstream, it connects to agent code, models, and tool capabilities. Downstream, it connects to instances, networking, logs, permissions, and the release system. Developers do not need to build the underlying compute, networking, and security infrastructure themselves. They only need to focus on agent logic and business configurations, while the platform handles instance startup, elastic scheduling, access control, and version release.

<span id="tx77Xnn8"></span>
## Core capabilities


* **Serverless fully hosted execution**: No manual maintenance of compute, networking, storage, or security policies is required. The platform handles underlying resource orchestration and automatically generates a unified access domain name.

* **Automated elastic scaling**: The platform automatically scales instances in and out based on request concurrency and compute load. You can configure a minimum number of resident instances to eliminate cold starts. Idle instances are automatically destroyed when there are no requests, reducing costs.

* **Framework\- and model\-agnostic**: Natively and deeply integrated with VeADK. With simple decorator modifications, mainstream Python agent frameworks such as LangGraph and ADK can be hosted. It is not tied to any specific large model and is compatible with various model services.

* **Comprehensive access control**: Provides a complete identity management system that supports configuring flexible inbound and outbound access rules for agent runtimes as needed.

* **End\-to\-end observability**: Supports collecting monitoring metrics, logs, and call traces across three dimensions: **runtime, session, and trace**. Enables observability into agent performance, tool calls, model outputs, and errors to quickly identify failure points.

* **Integration with the AgentKit Gateway ecosystem**: Agent code inside a runtime connects to the AgentKit Gateway via an MCP Client, directly consuming all MCP tool capabilities managed by the gateway to form a complete agent solution.


<span id="JcePuymi"></span>
### Comparison with agent deployment on self\-managed Kubernetes/VMs


|**Dimension** |**Agent Runtime** |Agent deployment on self\-managed Kubernetes/VMs |
|---|---|---|
|Underlying O&M |Hosted by the platform. No cluster, machine or restart policy maintenance is required. |Self\-managed cluster, monitoring, and self\-healing |
|Elastic capability |Out\-of\-the\-box automatic scaling. Idle instances are automatically released. |Manual configuration of HPA and scaling rules is required. |
|Security and permissions |Built\-in IAM roles and inbound/outbound network access policies |Self\-implemented RBAC, network policies, and secret management |
|Observability |Runtime/session/trace three\-level observability out of the box |Custom instrumentation and self\-built logging and tracing systems are required. |
|Agent framework adaptation |Mainstream agent frameworks can be hosted with minimal code modifications. |No encapsulation. All adaptation logic requires custom development. |
|Ecosystem integration |Natively integrated with the AgentKit Gateway MCP tool ecosystem |Self\-managed integration with an MCP Client and authentication logic is required. |


<span id="XCUkTZRF"></span>
### Relationship with each component


|**Component** |**Relationship with a runtime** |
|---|---|
|**AgentKit Gateway** |The **only egress point** for a runtime to call external MCP tools: The MCP Client inside the runtime connects to the gateway, which handles inbound authentication, protocol conversion, routing, and outbound credential injection. The gateway carries MCP tools only. It does not carry sandbox templates. |
|**A2A space** |A runtime must be registered in an A2A space to enable cross\-agent invocation. The A2A underlying gateway handles the protocol and is responsible for agent addressing, authentication, and request routing. A runtime can be registered in only one A2A space. |
|**Knowledge Base** |After the knowledge base is bound in the form, connection configurations are automatically injected into the runtime. The agent uses the knowledge base SDK to connect directly to the knowledge base for RAG retrieval. Knowledge data is managed independently. The knowledge base network mode must be consistent with that of the runtime. |
|**Memory** |After the memory is bound in the form, connection configurations are injected into the runtime. The agent uses the SDK to read and write long\-term memory across sessions. Memory data is stored independently and does not reside in the runtime instance. The memory network mode must be consistent with that of the runtime. |
|**Observability service** |The runtime instrumentation module automatically reports logs, metrics, and traces to APMPlus and TLS, with no instrumentation required in business code. When the observability service is disabled, business execution continues normally. Only troubleshooting and online evaluation capabilities become unavailable. |
|**ModelArk (model service)**  |A model can be selected in the runtime form, and the platform automatically injects the corresponding endpoint and authentication credentials. The agent SDK calls the model API directly. The runtime is decoupled from the model and can also integrate with external models outside of ModelArk. |
|**IAM role** |Once an IAM role is bound to a runtime, temporary credentials issued by IAM are accepted by the runtime permission module and injected into the sandbox. The BytePlus SDK and processes inside the sandbox use them automatically. If no IAM role is bound to the runtime, BytePlus cloud resources cannot be accessed. |
|**External business backend** |A runtime **does not** call the business backend directly. All calls must go through the Gateway proxy, which handles credential hosting and auditing. Direct connections from the runtime sandbox to the business backend are not allowed. |
|**Sandbox template** |A subtype of tool; a microVM\-isolated execution environment. The agent creates instances via the Sandbox SDK and a sessionId. An instance is created on the first call and reused for the duration of the session (30\-minute idle timeout by default; 24\-hour maximum lifetime). Inbound authentication is handled by Identity using an API Key, ** running in parallel with the Gateway MCP call chain**, with no shared call path. |


<span id="V79WwTr9"></span>
## Runtime build methods

AgentKit supports multiple methods for hosting an agent on a runtime. Refer to the following scenarios to select a method that fits your needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Selection recommendations (by priority)</strong>: If your goal is to continuously iterate on your agent after it goes live, prefer integrating your agent into an engineering\-based workflow (AgentKit CLI or VeADK). If your goal is rapid validation, the console is usually the faster option. If you have existing online assets, prioritize migrating them to avoid redundant development.</div>



<Tabs>
<Tab zoneid="WMPhAXmOIV" title="Use the console">
<TabTitle>Use the console</TabTitle>

* Purpose: Create, configure, deploy, and validate agents online with zero or minimal code. This method is suitable for quick trials and solution demonstrations.

* **Applicable scenario**

   * You are new to AgentKit runtimes and want to complete deployment via the shortest path.

   * You prefer console\-based operations and do not want to set up a local development environment first.

   * You need to quickly validate how models, tools, and knowledge bases work together.

   * Your use case is a PoC, demonstration, training, or product solution validation.

* **Not suitable for**: Long\-term projects requiring complex engineering structures, custom build processes, strict version governance, or automated release pipelines (consider switching to the AgentKit CLI).

* **Document link:**  [Getting started: Deploy an agent in 1 minute](https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_AgentKit)


</Tab>
<Tab zoneid="JczHem0MWI" title="Use the AgentKit CLI tool">
<TabTitle>Use the AgentKit CLI tool</TabTitle>

* **Purpose**: A code\- and engineering\-centered development approach that emphasizes maintainability, reproducible builds, and continuous delivery.

* **Applicable scenario**

   * You need to include your agent in a code repository with version control and CI/CD pipelines.

   * You need to customize the engineering structure, dependencies, build process, or deployment parameters.

   * You need to support frequent iteration, testing, and regression validation.

   * Your development team needs to maintain a complex agent application over the long term.

* **Not suitable for**: Short\-term validation, demonstrations, or one\-off deliverables with no engineering requirements (the console is a lighter\-weight option).

* **Document link:**  [Developing and deploying agents with the AgentKit CLI](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool)


</Tab>
<Tab zoneid="GJmI5wq2Ej" title="Use VeADK">
<TabTitle>Use VeADK</TabTitle>

* **Purpose**: Organize agent logic using the VeADK SDK while keeping the code maintainable and integrating with AgentKit runtime hosting and observability capabilities.

* **Applicable scenario**

   * You already use VeADK to write agent logic and want to keep your current code\-based development approach.

   * You need to organize multi\-turn conversations, tool calls, or workflow logic through the SDK.

   * You want to keep the code maintainable while integrating with the AgentKit runtime.

   * Your team has development capabilities and prefers code\-based development.

* **Not suitable for**: Teams that lack the ability to maintain an SDK or code, or use cases that only require a lightweight, configuration\-driven agent (the console may be a better fit).

* **Document link​:**  [Developing and deploying agents with VeADK](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial)


</Tab>
<Tab zoneid="H4Sv8yYwAn" title="Migrate existing agents">
<TabTitle>Migrate existing agents</TabTitle>

* **Purpose**: Smoothly migrate existing online or legacy agents to an AgentKit runtime. The goal is to unify deployment, observability, and O&M without rewriting business logic.

* **Applicable scenario**

   * You have an online or legacy agent and want to migrate it to an AgentKit runtime.

   * You need to preserve your existing business logic, framework structure, or development assets.

   * You plan to consolidate your original agents under the AgentKit observability, deployment, and O&M ecosystem.

   * Your use case calls for incremental adoption or a smooth migration.

* **Migration recommendation**: Prioritize interface compatibility and behavioral consistency. Complete a minimal working version first, and then gradually switch to the standardized engineering and image specifications and release pipeline.

* **Document link:**  [Advanced quick start​: Migrating existing agents](https://docs.byteplus.com/en/docs/agentkit/Migrating_existing_agents)


</Tab>
<Tab zoneid="jJ15czKDkh" title="Use TRAE for integration">
<TabTitle>Use TRAE for integration</TabTitle>

* **Purpose**: Complete the full cycle of requirement expression, solution generation, rapid testing, and runtime deployment using a natural language\-driven approach. This method is particularly suitable for office collaboration and business automation agents.

* **Applicable scenario**

   * You already use TRAE and want to leverage its development experience to speed up integration.

   * You need to quickly deliver a deployable agent for office collaboration scenarios.

   * You want to complete prototyping and iteration using natural language with low\-code or minimal\-code supplements, reducing engineering boilerplate and scaffolding effort.

   * Your team has diverse roles beyond engineering (such as product, operations, and business members), but the final output still needs to be deployable, observable, and maintainable.

   * You want to quickly connect enterprise system capabilities (such as knowledge bases, approvals, ticketing, spreadsheets, and documents) and centrally manage permissions, monitoring, and troubleshooting on the runtime side.

* **Not quite suitable for**: Deep development projects with strong customization requirements for engineering structure, dependency isolation, or build processes, or projects that require frequent and complex testing (AgentKit CLI or VeADK is generally more suitable).

* **Document link:**  [Natural language-driven: Developing and deploying agents with TRAE](https://docs.byteplus.com/en/docs/agentkit/developing_and_deploying_agents_with_trae)


</Tab>
</Tabs>


<span id="pWxrcNH7"></span>
## Procedure


1. [Build an agent and deploy it to a runtime](https://docs.byteplus.com/en/docs/347/86686#V79WwTr9) **:**  Based on your chosen build method, define the agent capabilities (prompts, tools, knowledge bases, and business code) in the corresponding entry point. Generate a deployable artifact, publish it to the AgentKit runtime, and configure runtime parameters (environment variables, resource specifications, routing domain name, authentication, and more). For the first deployment, use a test or canary environment to facilitate validation and rollback.

2. [Call and test the agent](https://docs.byteplus.com/en/docs/agentkit/Testing_agents): Test the agent using the online testing feature in the console, or call it locally by sending a POST request with `curl` to the specified domain name.

3. [Observe and troubleshoot](http://volcengine.com/docs/86681/1873528) **:**  Use runtime global metrics, session records, trace call chains, and instance logs to identify performance bottlenecks, tool call errors, business code exceptions, and resource issues.

4. [Evaluate](https://docs.byteplus.com/en/docs/agentkit/Evaluation): The runtime executes the agent and generates session outputs. Based on the session sample outputs from the runtime, connect to AgentKit evaluation capabilities, input test sets in batches, and evaluate agent answer accuracy and tool call correctness to iteratively refine the agent image code.


<span id="iVQ12E0N"></span>
## Common misconceptions


|**Common misconception** |**Correct understanding** |**Description** |
|---|---|---|
|A runtime contains the agent's business logic. |A runtime is a hosting environment. Business logic is implemented by the agent code deployed to the runtime. |A runtime handles execution and hosting. It does not generate business logic on behalf of developers. |
|A runtime persistently stores session, memory, and knowledge base data. |Session, memory, and knowledge base data are managed by the respective independent components. |A runtime can be associated with these components, but does not replace their data management capabilities. |
|Only VeADK agents can be deployed to a runtime. |A runtime is deeply integrated with VeADK, but can also host agents built with other mainstream Python agent frameworks. |Refer to the product documentation and console for the supported framework list. |
|Instances at the minimum instance count are not billed when there is no traffic. |Instances at the minimum instance count are always\-on resident instances that are billed even when there are no incoming requests. |If your workload is not sensitive to cold starts, adjust the minimum instance count based on your cost targets. |
|Binding the Guardrails service automatically protects all call paths. |After enabling the Guardrails service, you must also integrate the Guardrails service in the agent. Otherwise, protection policies do not take effect. |The protection scope depends on where the Guardrails service is integrated in the business code and how the product capabilities are configured. |
|A runtime has large model inference capabilities. |A runtime does not handle model inference. Inference is provided by ModelArk or other model services. |Agent code must call the model via the model SDK, API, or environment variable configuration. |
|Registering an A2A space automatically enables multi\-agent orchestration. |An A2A space provides the foundation for agent addressing and communication. Orchestration logic must still be implemented in business code or by the primary agent. |Task decomposition, invocation strategies, and result aggregation are not automatically generated by the A2A space. |
|Sandbox tools are built\-in capabilities of a runtime. |Sandbox tools are tool capabilities that can be called by the agent. A runtime can be associated with them as needed. |Agent code must still integrate the sandbox tools as described in the documentation. Associating a sandbox tool does not mean it is called automatically. |
|An IAM role can replace third\-party API authentication. |IAM roles are used to access BytePlus cloud resources and are not suitable for third\-party service authentication. |Accessing third\-party services still requires the API Key, OAuth Client, or other credentials required by those services. |
|Changes to IAM role permissions take effect immediately in the runtime. |Configuration changes to a runtime typically take effect only after the runtime is published. |After making changes to permissions, go to the runtime details page and publish the runtime. |
