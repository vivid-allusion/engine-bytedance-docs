---
title: "Sandbox template overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Tool_overview"
---

Sandbox is one of the most widely used runtime environment tools in the AgentKit tool ecosystem. AgentKit sandbox templates provide various runtime environments required by agents when executing tasks. The sandbox templates can be quickly integrated and conveniently called. This topic provides a detailed introduction to what a sandbox is, its typical use cases, applicable boundaries, and underlying principles, helping you quickly understand sandbox templates and know where to get started.

## What is a sandbox template

**You can think of a sandbox template as a temporary "isolated mini\-machine" that an agent borrows.**  It is better suited for tasks that require running code, executing commands, or performing browser\-based operations in an isolated environment, rather than for scenarios where an agent needs to persist state long\-term or run continuously.

**How it works**

Sandbox templates use microVMs as the foundation to provide a secure, isolated runtime environment. AgentKit manages the lifecycle of tools and instances. Instances support retaining context during a session (such as in\-memory context, file system state, etc.) and are automatically reclaimed after their lifecycle expires or manually reclaimed on demand. Sandbox tools integrate with identity and permission services, using API Keys and other methods to perform inbound authentication.

## Core concepts

|Concept |Description |
|---|---|
|**Tool** |In AgentKit, a tool refers to an "external capability" that an agent can invoke during task execution. It typically provides an interface that can be invoked by the model and runs a runtime environment or external service in the background. |
|**Sandbox Templates** |A sandbox template is a type of "runtime environment tool" that provides an isolated execution environment for running code, executing commands, or completing browser\-based tasks. Its goal is to allow an agent to "borrow an environment to complete a task" when needed, rather than keeping the environment running as a long\-term service. |
|**Tool instance** |A tool instance is the runtime carrier of a sandbox tool and can be understood as "a sandbox environment that remains available throughout a session". Instances have a lifecycle: you can set a lifecycle duration for automatic reclamation or reclaim them manually. Instances can run for up to 24 hours. |
|**Session identifier (session_id)**  |In code examples, multiple tool invocations are typically chained into a single coherent session using a session_id. A tool instance is created the first time a session_id is used. The default lifecycle is 30 minutes (refer to the official examples). The lifecycle duration can be adjusted as needed. |
|**Inbound authentication (API Key)**  |When a sandbox tool is integrated with identity and permission services, you can choose to use an API Key for inbound authentication to protect the data security of the tool invocation chain. |

## Applicable scenarios

* **When to use a sandbox template:**  The task needs to run in an isolated environment (for example, running code, executing commands, or accessing a browser), and you want the agent to invoke it on demand at runtime.

* **When not to use a sandbox template:**

   * The task does not require an isolated runtime environment.

   * You need to persist process or memory state over the long term (sandbox instances have a lifecycle of up to 24 hours).

   > **tip**

   > The "status" of a sandbox template is managed through an **instance**, which can be automatically reclaimed. Context during a session is held in memory and is not retained after the session ends.

* When deciding whether to use a sandbox template, you can refer to the following boundaries.

   |**When sandbox templates are recommended** |**When sandbox templates are not recommended** |
   |---|---|
   |* An isolated runtime environment is required.<br><br>* The agent needs to invoke runtime capabilities on demand during execution.<br><br>* A controllable reclamation mechanism for the instance lifecycle is desired.<br><br>* The runtime environment complexity needs to be decoupled from the business host environment. |* The task is essentially a simple API call or information retrieval and does not require a runtime environment.<br><br>* Long\-term persistence of process state or long\-running resident services is required (sandbox instances have a lifecycle limit).<br><br>* You want to store data on local disks for a long time without using persistent storage (the data is not retained after the session ends). |

* The following scenarios are better suited for sandbox templates:

   * **Code execution and command execution:**  The task needs to run in an isolated environment (for example, running code, executing commands, or accessing a browser), and you want the agent to invoke it on demand at runtime.

   * **Browser\-based tasks:**  Tasks that require page access, rendering, or web interaction in a controlled environment.

   * **Multi\-step tasks:**  The same task requires multiple tool invocations, and you want to reuse context and file system state across invocations during a session (achieved through the sandbox template instance lifecycle).

## Advantages

* **Lifecycle management capabilities for tools**

   * Supports running for up to 24 hours, effectively supporting long\-running task execution.

   * Instances can be automatically reclaimed when the specified lifecycle expires. They can also be reclaimed manually.

   * Session context is retained in memory, with data destroyed after the session ends.

* **Secure, isolated environment and end\-to\-end identity authentication**

   * Based on the microVM environment, operations can be performed in a secure and isolated sandbox environment.

   * Deeply integrated with[ identity and permission ](https://docs.byteplus.com/en/docs/agentkit/Identity_and_permission_01)services. Inbound identity authentication supports using an API Key, enabling end\-to\-end data security protection across the tool invocation chain.

## Metrics

|**Metric** |Metric value |Metrics |
|---|---|---|
|**Cold start latency** |100 ms |Latency for instance cold start. |
|**Large\-scale creation throughput** |Up to 120,000 sandboxes/min |Large\-scale elastic creation capability for high\-concurrency scenarios such as AgentRL. |
|**Sleep\-to\-wake latency** |Typical: 1s–10s |Fast resume with filesystem state preserved. |

## Fees and security notes

* **Fee:**  No charges are incurred when a sandbox template is created. Fees apply after you create a sandbox instance from the template, and billing stops once the sandbox instance is deleted. If you configure a TOS mount point for the sandbox template, activate and integrate Observability Platform to view logs, or trigger capabilities such as model calls in the sandbox, fees for the corresponding services may be incurred after the sandbox instance is created. We recommend starting with a minimal configuration to get the workflow running during the getting\-started phase and enabling these capabilities as needed afterward.

* **Data security:**  We recommend using the authentication capabilities provided by the platform (for example, inbound API Key) to avoid hardcoding sensitive keys in code repositories. If AK/SK must be configured via environment variables, ensure they are only configured in trusted environments and follow the principle of least privilege.

* **Interruption and reclamation:**  Sandbox instances have a lifecycle and a reclamation mechanism. For tasks that require long\-running execution or multiple consecutive invocations, we recommend designing with recoverability in mind: the task should be retryable after an interruption and able to recreate an instance and resume execution.

## Usage procedure description

1. [Create a sandbox template](https://docs.byteplus.com/en/docs/agentkit/Creating_tools): Create various built\-in sandbox templates (for example, AIO Sandbox) in the console as needed, so that agents can quickly integrate and easily call various runtime environments during running.

2. [Integrate a sandbox template into an agent (using VeADK as an example)](https://docs.byteplus.com/en/docs/agentkit/Code_sandbox_tool_example): You can integrate the sandbox template into your agent code. This allows the agent to call an isolated environment to execute code, perform browser\-related tasks, and handle other complex operations.

3. [Create a sandbox template instance](https://docs.byteplus.com/en/docs/agentkit/Creating_tool_instances): enable status tracking and context management to support subsequent rounds of operations.
