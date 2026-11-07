---
title: "Agent development and deployment overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/advanced_quick_start_overview"
---

AgentKit supports three methods for creating, developing, and publishing an agent: AgentKit Studio, AgentKit CLI, and VeADK + AgentKit. AgentKit Studio is suitable for visual validation and a quick start. AgentKit CLI is suitable for standardized delivery. VeADK + AgentKit is suitable for in\-depth customization and business integration. This topic describes the differences, advantages, and applicable scenarios of each method to help you quickly choose the path that best fits your business needs.

<span id="hMqQKgje"></span>
## Quick selection


<columns>
<columnsItem zoneid="egRJ2MyC3Q">


<card mode="container" href="https://docs.byteplus.com/en/docs/86681/2630032" iconSet="1" iconSize="" icon="" img="" >

**AgentKit Studio**: Visual building, unified entry point


* Recommended when you want **visual orchestration**.

* **Low** learning curve. Build, test, and deploy agents through a visual workbench.

</card>



</columnsItem>
<columnsItem zoneid="EXMzzQsaeH">


<card mode="container" href="https://docs.byteplus.com/en/docs/86681/1844871" iconSet="1" iconSize="" icon="" img="" >

**AgentKit CLI**: Lightweight, easy to get started, and quick to deliver


* Recommended when you want **standardized initialization and fast delivery**.

* **Low** learning curve. Use official templates to quickly initialize a project and complete the full development, deployment, and testing cycle, reducing upfront setup costs.

</card>



</columnsItem>
<columnsItem zoneid="EsY8bfNqTk">


<card mode="container" href="https://docs.byteplus.com/en/docs/86681/2155817" iconSet="1" iconSize="" icon="" img="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d63fb48083ceceb5ae7d8afeea1ef71d.jpeg" >

**VeADK + AgentKit**: In\\-depth customization and flexible extensibility


* Recommended when you want **code\\-level in\\-depth customization of agent capabilities and system integration**.

* Has a **steeper** learning curve. Requires developers to be familiar with the VeADK framework and how agent code is organized.

</card>



</columnsItem>
</columns>


<span id="X1Yjs5Jx"></span>
## Method comparison


|Comparison dimension |[AgentKit Studio](https://docs.byteplus.com/en/docs/86681/2630032) |[AgentKit CLI](https://docs.byteplus.com/en/docs/agentkit/Creating_runtime_via_CLI_tool) |[VeADK + AgentKit](https://docs.byteplus.com/en/docs/agentkit/agent_development_and_deployment_tutorial) |
|---|---|---|---|
|**Applicable scenario** |Suitable for low\-code agent creation, rapid business scenario validation, and building up reusable configurations.<br><br><br>* Team members can use a unified entry point to build, test, deploy, and validate agents within the same workbench.<br><br>* Supports quick integration with an AgentKit agent runtime through custom configurations, code package deployment, and more.<br><br>* Supports visual use of runtimes already deployed to AgentKit. |Suitable for scenarios where you want to quickly start a project and reduce upfront build costs.<br><br><br>* Provides quick commands covering the entire agent lifecycle.<br><br>* Comes with built\-in agent templates to reduce upfront build costs, while also supporting integration of self\-developed code.<br><br>* Supports flexible switching between agent deployment modes, adapting to different stages from developing an agent to publishing it in production. |Suitable for complex scenarios that require high engineering controllability and deep customization.<br><br><br>* Offers greater engineering freedom, allowing deep customization of agent application logic and project structure.<br><br>* More suitable for handling complex workflows, business logic, or fine\-grained code control requirements.<br><br>* Code\-based development facilitates long\-term extension and maintenance, making it suitable for continuously iterating on complex agent capabilities and for deep integration with existing development workflows, code repositories, and CI/CD systems. |
|**Development method** |* Visually create custom agents through the Studio workbench, or deploy to the AgentKit runtime by uploading a code package.<br><br>* Operations are organized around configuration, testing, deployment, updates, integration, and management. |* Uses the CLI to initialize, configure, build, deploy, and manage agents locally.<br><br>* Supports quick startup with built\-in templates, as well as self\-developed code.<br><br>* Supports Local, Cloud, and Hybrid deployment modes, allowing developers to deploy flexibly based on the stage of agent development. |* Develops agents locally based on the VeADK code framework, and then uses AgentKit to complete deployment and operation.<br><br>* Fully code\-based, with application logic, project structure, and extension methods all managed by the developer.<br><br>* Includes built\-in local testing tools, allowing developers to perform more thorough engineering\-level verification before publishing. |
|**Capability extension** |Suitable for configuring models, system prompts, tools, skills, memory, knowledge bases, code execution, and other capabilities through the workbench. |Suitable for development based on AgentKit project templates, the configuration system, and platform capabilities. |More suitable for deeply customizing tools, workflows, runtime logic, and engineering integration methods. |
|**Version management** |The workbench retains only local drafts and does not provide source\-code\-level version history. |All configuration is centrally managed through the `agentkit.yaml` file. |Can be directly incorporated into Git and existing engineering systems for full code version management. |


<span id="0It2m7T3"></span>
## <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In practice, we recommend combining these tools for agent development and real\-world implementation. For example, use AgentKit Studio to complete business workflow validation, online testing, evaluation, and integration method confirmation, and then use the AgentKit CLI or VeADK + AgentKit for engineering development, code version management, CI/CD, and complex extensions.</div>


<span id="1SiL61ba"></span>
## Key components


|Component |Description |AgentKit feature |
|---|---|---|
|Tool |A tool is an executable capability that an agent can invoke to transform model decisions into concrete actions. This enables the agent to not only understand problems but also perform real operations such as data queries, API calls, and resource reads and writes. |[Tool types](https://docs.byteplus.com/en/docs/agentkit/Tool_type)<br><br> |
|Skills |A skill is a standardized capability unit encapsulated for a specific task. It typically integrates the knowledge descriptions, execution workflows, code scripts, and related resources required to complete the task. This allows the agent to invoke ready\-made capabilities on demand, reducing repetitive configuration and improving execution quality and efficiency. |[Skills overview](https://docs.byteplus.com/en/docs/86681/2605772?) |
|Memory |A memory persistently stores user information, task context, and completed steps accumulated by the agent during conversations. This enables the agent to maintain context across multi\-turn conversations or cross\-session interactions without rebuilding the context from scratch, and prevents memory loss. |[Memory overview](https://docs.byteplus.com/en/docs/agentkit/Memory_overview) |
|Knowledge Base |A knowledge base provides the agent with an external, retrievable, and updatable knowledge source (such as enterprise documents, product rules, or business processes). Before generating a response, the agent retrieves relevant content and generates a response based on the retrieval results, improving response accuracy and business relevance. |[Knowledge base overview](https://docs.byteplus.com/en/docs/agentkit/Knowledge_base_overview) |
|Gateway |A gateway manages connectivity and data exchange between the agent and external systems. It provides fast API\-to\-MCP conversion and supports automatic matching of the most relevant tools through semantic search. |[MCP overview](https://docs.byteplus.com/en/docs/agentkit/MCP_Overview) |
