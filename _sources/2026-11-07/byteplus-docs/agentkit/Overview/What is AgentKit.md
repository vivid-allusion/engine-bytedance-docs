---
title: "What is AgentKit"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/What_is_AgentKit"
---

<span id="cf7YOrxa"></span>
## Product overview

BytePlus **AgentKit** is a platform for enterprises and developers to build and run agents. It provides full lifecycle capabilities spanning from code\-side development to cloud\-hosted execution, covering key stages including creation, configuration, deployment, calling and testing, observability, and evaluation.

As enterprises integrate agents into their business workflows, they often encounter the problem of "works in demos but is hard to productionize, callable but difficult to govern," such as unclear permission boundaries, fragmented tool integrations, lack of observability and audit traces, and high costs for troubleshooting and quality assessment after deployment. AgentKit standardizes these capabilities into platform components, helping teams deliver and maintain agents consistently and reducing the engineering complexity of moving from demo to production.

<span id="bt4mTvWy"></span>
## Applicable scenarios

AgentKit is suitable for enterprises and development teams that need to engineer and deploy agent capabilities in production. Typical scenarios include:


* **Internal employee assistant**: Supports document Q&A, ticket handling, knowledge base retrieval, and collaborative workflow automation.

* **Intelligent transformation of business systems**: Targets systems such as ticketing, order management, approvals, and CRM. Existing APIs can be integrated as tools or via MCP to quickly enable agent interaction capabilities for these systems.

* **Multi\-agent orchestration and complex workflows**: Supports cross\-system calls and long\-chain task execution to meet orchestration and governance requirements for complex business workflows.

* **Platform\-based delivery of production\-grade AI applications**: Provides unified authentication, call auditing, full\-chain observability, evaluation, and O&M capabilities to support production deployments that require security compliance and stability guarantees.


<span id="S0bKruNq"></span>
## Features

&nbsp;


<columns>
<columnsItem zoneid="N524ngmpLg">

<div style="text-align: center">
<strong>Agent Runtime</strong></div>


<div style="text-align: center">
<strong>(Runtime)</strong></div>


<div style="text-align: center">
Provides a managed execution environment and runtime management capabilities to support stable agent operation and production deployment.</div>


</columnsItem>
<columnsItem zoneid="Qf9CJDNygO">

<div style="text-align: center">
<strong>Unified authentication</strong></div>


<div style="text-align: center">
<strong>(Identity)</strong></div>


<div style="text-align: center">
Provides controlled access and credential/permission boundary management to meet enterprise requirements for security isolation and compliance governance.</div>


</columnsItem>
<columnsItem zoneid="TXMJVxhkdA">

<div style="text-align: center">
<strong>Tool integration</strong></div>


<div style="text-align: center">
<strong>(Gateway)</strong></div>


<div style="text-align: center">
A unified entry point for Agents to access external systems and services, responsible for connectivity, routing, and call governance. Supports connecting to MCP Servers via the Gateway, or quickly converting existing REST/OpenAPI services for integration, reducing the cost of modifying existing systems.</div>


</columnsItem>
<columnsItem zoneid="VNyTjDqERM">

<div style="text-align: center">
<strong>A2A protocol support</strong></div>


<div style="text-align: center">
<strong>(Agent to Agent)</strong></div>


<div style="text-align: center">
Based on the A2A protocol, supports multi\-agent orchestration with cross\-agent task distribution, result callback, and state synchronization, meeting the requirements for multi\-agent collaborative execution in complex workflows.</div>


</columnsItem>
</columns>



<columns>
<columnsItem zoneid="Z8yzH3FXxV">

<div style="text-align: center">
<strong>Session and memory management</strong></div>


<div style="text-align: center">
<strong>(Session/Memory)</strong></div>


<div style="text-align: center">
Provides layered management of short\-term and long\-term memory. Sessions handle context persistence across multi\-turn conversations, while memories support information retention and recall across sessions, together ensuring conversational continuity and personalized interaction.</div>


</columnsItem>
<columnsItem zoneid="zbvvb0uGvS">

<div style="text-align: center">
<strong>Knowledge retrieval and tuning</strong></div>


<div style="text-align: center">
<strong>(Knowledge)</strong></div>


<div style="text-align: center">
Provides knowledge retrieval and tuning capabilities, serving as standard components for building enterprise knowledge Q&A and retrieval\-augmented applications.</div>


</columnsItem>
<columnsItem zoneid="UzwirZA4Sx">

<div style="text-align: center">
<strong>End\-to\-end observability and troubleshooting</strong></div>


<div style="text-align: center">
<strong>(Observability)</strong></div>


<div style="text-align: center">
Provides call chain observability and issue identification capabilities, enabling differentiation of anomaly sources across components such as models, runtimes, gateways, tools, and memory/knowledge modules.</div>


</columnsItem>
<columnsItem zoneid="uvVPCxPOaq">

<div style="text-align: center">
<strong>Evaluation and quality loop</strong></div>


<div style="text-align: center">
<strong>(Evaluation)</strong></div>


<div style="text-align: center">
Provides evaluation and quality loop capabilities to support pre\-launch validation, post\-launch continuous optimization, and release gate management.</div>


</columnsItem>
</columns>
