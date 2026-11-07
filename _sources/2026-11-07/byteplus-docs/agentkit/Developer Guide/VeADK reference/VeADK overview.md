---
title: "VeADK overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/VeADK_overview"
---

This topic describes what VeADK is and how to use it to help you understand the design philosophy and core components of agent development. It also explains the core capabilities that VeADK, built on the BytePlus ecosystem, provides for the entire agent lifecycle. For more information, see [VeADK documentation](https://docs.veadk.xyz/productions/veadk/preview/zh).

> **tip**

> To avoid ambiguity, certain terms in this topic are defined below:

* > Tools refer to external capabilities that can be called.

* > Short\-term memory refers to the context within a single session, and long\-term memory refers to context across sessions.

## About VeADK

VeADK (Volcengine Engine Agent Development Kit) is an agent development suite launched by BytePlus. It is designed to offer developers a comprehensive solution for building, deploying, and managing agent applications. Based on a modular design philosophy, it enables the decomposition of the complex agent development process into composable components, allowing developers to focus on business logic rather than underlying technical details. In VeADK, an agent is defined as a software entity with the following core capabilities:

* **Autonomous decision\-making**: determines next actions based on the current context and goals

* **Tool usage**: involves calling external tools and systems to complete complex tasks

* **Learning and adaptation**: learns from interactions and optimizes behavioral strategies

* **Memory**: stores and recalls past interaction information to guide current decision\-making

* **Multimodal interaction**: supports various interaction modes such as text, image, and voice

## VeADK and agent lifecycle

VeADK offers supporting capabilities at key stages of an enterprise\-grade agent application's lifecycle. This helps developers address various challenges. A typical enterprise\-grade agent application cycle is as follows:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1da351a08e03834e8bc364423400cc3.png)

1. **Develop**: Define the core logic of the agent, including its goals, tools, and memory.

2. **Deploy**: Deploy the agent to the cloud so it can stably handle real\-world requests.

3. **Observe**: Gain deep insight into agent behavior at runtime. Monitor its performance and decision paths.

4. **Evaluate**: Measure agent performance using systematic methods to identify issues and areas for improvement.

5. **Iterate**: Optimize the agent design based on observability data and evaluation results, then enter the next development cycle.

Throughout the agent lifecycle, VeADK provides a rich set of tools and services to help developers create efficient and reliable agent applications at each stage:

* **Simplified agent development**: provides a standardized development framework and best practices to reduce complexity.

* **Ready\-to\-use BytePlus built\-in tools**: seamlessly integrates with various services in the BytePlus ecosystem.

* **Comprehensive observability and evaluation solutions**: ensure agent reliability and maintainability in production environments

* **Modular architecture design**: supports flexible replacement and extension of components

* **Enterprise\-grade security and compliance**: meets the security and compliance requirements of enterprise applications.

## VeADK architecture

VeADK is based on a modular design. Its main components include agent runtime, tools, memory system, knowledge base, observability system, and evaluation system. Each component is decoupled through well\-defined interfaces, enabling replacement or extension in different business scenarios.

### Core components

|**Core component** |**Main responsibility** |**Key modules/capabilities** |
|---|---|---|
|**Agent** |Defines models, instructions, tools, skills, knowledge bases, memories, and execution runtimes. |Model configuration, runtime configuration, system prompt, prompt management, structured output, skills, remote sandbox agent |
|**Execution engine (Runner)**  |Core engine coordinating all components |Event processing, memory management, session management |
|**Tools** |Enables interaction with external capability sources |Built\-in BytePlus ecosystem tools, custom tools, tool orchestration |
|**Memory** |Storage and retrieval of context and historical information |Short\-term memory (within a single session), long\-term memory (cross\-session) |
|**Knowledge base** |Provides storage and retrieval of external knowledge |BytePlus knowledge base, Llama\-index ecosystem |
|**Observability system** |Ensures runtime behavior is monitorable |Log recording, trace observability, metric observability |
|**Evaluation system** |Systematically measures agent quality |Data\-driven feedback optimization |

### Runtime

Main workflow of agent runtime:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a0b9080d5ff0f017718e6c3579dcb2b.png)

The agent runtime process mainly involves the following steps:

1. **Message reception**: When a user message enters the agent runtime, the session manager creates or updates the session context.

2. **Intent resolution**: The runtime sends the user message to a cloud\-based large model to parse the user intent and generate execution plans.

3. **Tool calling decision**: Based on the intent analysis results, a decision is made on whether to call tools or retrieve information from memory/knowledge base.

4. **Tool execution**: If a tool needs to be called, the tool dispatcher constructs a normalized request and logs the calling context.

5. **Result integration**: After the tool returns the result, the runtime integrates it into the reasoning context.

6. **Response generation**: A final response is generated based on all available information and returned to the user.

7. **Observability recording**: All key events and metrics (such as token consumption, tool invocation latency, and error rate) are pushed in real time to the Observability Platform for further analysis.

## BytePlus ecosystem integration

The core strength of VeADK lies in its seamless integration with the BytePlus ecosystem, providing powerful support at every stage of the agent lifecycle.

|**Stage** |**VeADK capabilities** |**BytePlus ecosystem support** |
|---|---|---|
|**Development** |Modular construction, tool definition |* **Doubao large model**: provides inference capabilities.<br><br>* **ModelArk platform**: offers various advanced parameter combinations. |
|**Deployment** |Containerized packaging, configuration management |* **APIG**: provides APIG instances for seamless interaction between agents and external systems.<br><br>* **VeFaaS**: provides serverless computing capability, enabling highly scalable and cost\-effective deployment of agents as functions. |
|**Observability** |Trace tracking, metric monitoring |* **APMPlus**: provides end\-to\-end tracing and performance monitoring, helping developers locate and optimize agent performance issues.<br><br>* **CozeLoop**: enables rapid root cause identification through trace tracking, performance statistics, real\-time exception alerting, intelligent tagging, and real\-time data evaluation. |
|**Evaluation** |Automated evaluation |**CozeLoop**: covers agent end\-to\-end testing for precise effectiveness measurement. |

## Multi\-language support

VeADK provides agent development capabilities covering **Python, Java, and Go**. Teams with different tech stacks can use their preferred language to build agent applications quickly.

|Development languages |Description |Release notes |
|---|---|---|
|[VeADK Python](https://docs.veadk.xyz/productions/veadk/preview/zh) |An agent development framework for Python developers.<br><br>It is compatible with Google ADK's agent and runtime mechanisms. It also integrates with ModelArk models, AgentKit, memory, knowledge bases, observability, security, and the enterprise frontend. This allows the same agent code to work across both local development and cloud deployment. |[Change log (Python)](https://docs.veadk.xyz/productions/veadk/preview/zh/changelog) |
|[VeADK Java](https://docs.veadk.xyz/productions/veadk-java/preview/zh) |An agent development toolkit for Java developers.<br><br>It reuses ADK Java's LlmAgent, Runner, session, and tool execution pipeline. It also provides a VeADK\-style Agent.builder(), model defaults, metadata, tools, skills, memory, knowledge bases, observability, and AgentKit Runtime integration. |[Change log (Java)](https://docs.veadk.xyz/productions/veadk-java/preview/zh/changelog) |
|[VeADK Go](https://docs.veadk.xyz/productions/veadk-go/preview/zh) |An agent development framework for Go developers.<br><br>It is built on top of ADK Go's agent, Runner, session, and event streaming. It adds ModelArk model configuration, tools, memory, knowledge bases, observability, and application packaging. This allows Go applications to directly embed agent capabilities or expose agent capabilities externally. |[Change log (Go)](https://docs.veadk.xyz/productions/veadk-go/preview/zh/changelog) |
