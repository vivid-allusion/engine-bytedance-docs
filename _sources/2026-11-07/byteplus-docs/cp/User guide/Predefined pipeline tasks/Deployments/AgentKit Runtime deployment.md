---
title: "AgentKit Runtime deployment"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/AgentKit_Runtime_deployment"
---

By adding the **AgentKit Runtime update** task in pipeline orchestration, you can complete the update of AgentKit Runtime. This article describes how to use pipeline tasks to accomplish this operation.

<span id="CEjAQCbz"></span>
## Background

AgentKit is a development tool platform provided by BytePlus for building, deploying, and running AI Agents. It helps developers and enterprises lower the threshold for Agent development, providing infrastructure such as security, built\-in tools, memory, knowledge, monitoring, evaluation, and more, beyond models, for Agents, enabling enterprises to efficiently build, deploy, and operate complex, intelligent, enterprise\-level Agents.

AgentKit intelligent runtime (Agent Runtime) provides Agents with a securely isolated, framework\- and model\-independent managed runtime environment.

<span id="5Ew15LmF"></span>
## Prerequisites

AgentKit Runtime has been created. For operation details, see [create runtime (Console)](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console) or [create runtime (CLI tool)](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool).

<span id="SXVbIF2J"></span>
## Description


|Parameter |Description |
|---|---|
|Job name |Default is AgentKit Runtime deployment; custom job names are supported. |
|Upstream task |Display the upstream serial task name of the current task. Display as `-` when there is no upstream task. |
|Region |Select the region where the AgentKit runtime needs to be deployed. |
|Runtime ID |Select the AgentKit Runtime to deploy. |
|Deployment policy |Supports **full release** and **gray release** methods. After selecting gray release, you need to fill in the percentage for the gray version.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Gray release is not supported for the first release; this feature is supported starting from the second release.</div><br> |
|Task output |Display the parameter used to query task output status. After completing this task, the following AgentKit runtime information will be output.<br><br><br>* Runtime ID: runtimeId<br><br>* Deployment record ID: releaseRecordId<br><br>* Deployment status: releaseStatus |
|Advanced settings |**Webhook notification**: Supports pushing task\-level messages via generic Webhook and Larkbot, helping you stay informed of task dynamics in time. For details, see [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification). |
