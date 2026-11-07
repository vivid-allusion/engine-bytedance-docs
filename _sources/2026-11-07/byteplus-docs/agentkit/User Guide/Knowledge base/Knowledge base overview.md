---
title: "Knowledge base overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Knowledge_base_overview"
---

AgentKit Knowledge provides one\-click configuration and import capabilities for mainstream knowledge bases, including . This enables you to easily deploy agents associated with knowledge bases on the AgentKit platform.


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

<span id="ZHgWEitg"></span>
## Background information

When deploying agents in enterprise environments, organizations typically use platform\\-level knowledge bases and retrieval engines to aggregate private data and build agents with knowledge Q&A capabilities. However, the APIs of various vector databases, knowledge bases, and multimodal retrieval services on the market are incompatible with one another. Integrating them directly leads to significant duplicated development effort, and switching the underlying retrieval solution requires changes to business code. In addition, there is no unified entry point for debugging and observability.

To address this, AgentKit provides the Knowledge gateway component for unified retrieval, which exposes standard retrieval interfaces to upstream layers while remaining compatible with multiple heterogeneous retrieval backends downstream. This reduces the development, migration, and operation costs for knowledge\\-based agents.

</card>



<span id="cmNjgDJC"></span>
## What is AgentKit Knowledge

**AgentKit Knowledge** is a unified retrieval gateway component launched by AgentKit for retrieval scenarios. It provides standardized retrieval capabilities for agent development.

AgentKit Knowledge exposes a unified call interface to the upstream agent orchestration engine and integrates with multiple heterogeneous retrieval backends downstream. It provides native support for Viking Knowledge Base.

AgentKit Knowledge abstracts away the differences in protocols, input parameters, and response formats across various knowledge bases and retrieval engines. This allows agents to conveniently call capabilities such as text RAG, image search, and video retrieval and provides unified support for agent development with private knowledge retrieval capabilities.

<span id="Yblm2ZzZ"></span>
## How it works


1. **Request access layer**: Agent applications initiate knowledge retrieval requests by calling the standard search interface of the Knowledge component in a unified manner. Multiple request types are supported, including text Q&A retrieval, image retrieval, and video retrieval.

2. **Gateway adaptation layer**: Requests are routed to the specified backend service based on configuration:

   * Routed to **Viking Knowledge Base**: Standard requests are converted to the Viking RAG call protocol to perform semantic document recall and reranking.

3. **Result standardization layer**: Heterogeneous results returned by different backends are uniformly encapsulated into a standard result structure containing text snippets, source metadata, image/video resources, similarity scores, and more.

4. **Prompt assembly and business feedback**: Standardized knowledge context is sent to a large language model to generate a response. Meanwhile, retrieval latency, recalled items, and hit status are collected across the entire call chain and reported to the unified observability module to support debugging and metrics analysis.

5. **Seamless switching between multiple backends**: Agent service code does not need to be modified. You can switch the underlying knowledge base or retrieval engine only by changing the configuration, enabling flexible migration across development, testing, and production environments.


<span id="qzkLEr5J"></span>
## Core capabilities

As a unified retrieval gateway, AgentKit Knowledge abstracts away backend differences upstream and encapsulates engine capabilities downstream. Its core value is concentrated in the following capabilities:


* **Unified search API**: A set of standardized call interfaces allows agent application code to access or switch between multiple backends (Viking and ContextSearch) with zero code changes.

* **Result standardization**: Parameters, return structures, field names, and similarity scores from heterogeneous backends are uniformly encapsulated into a standard result object that contains text snippets, source metadata, image/video resources, and more.

* **Unified configuration, debugging, and observability**: A built\-in debugging panel and full\-chain instrumentation enable unified collection of retrieval latency, recalled items, and hit status, supporting metric analysis and online troubleshooting.

* **Seamless migration across multiple environments**: You can switch the underlying knowledge base or retrieval engine across development, testing, and production environments by changing the configuration alone, without modifying agent application code.


<span id="Dud6lxxU"></span>
## Applicable scenario

<span id="ROojnGdo"></span>
### Text RAG agent scenarios based on Viking Knowledge Base


* **Q&A agents based on internal corporate documents**: Intelligent Q&A for corporate policies, technical wikis, product manuals, and contract documents. These agents enable self\-service information lookup for employees, reducing consultation costs.

* **Intelligent customer service in vertical industries**: After\-sales or consulting agents for finance, automotive, legal, and education scenarios to answer high\-frequency business questions based on private business documents.

* **Professional assistants**: Game design knowledge bases, health education, project document Q&A, and more, filling the gap in private knowledge in large language models and mitigating AI hallucinations.


<span id="VuZbVWzH"></span>
### General R&D and maintenance scenarios


* **Multi\-environment iterative development**: Use a test knowledge base in the development environment and switch to the production knowledge base in the production environment by modifying the configuration only, without changing agent application code.

* **Unified O&M**: Use the same set of observability and debugging tools for multiple different retrieval backends, reducing the complexity of multi\-engine maintenance.


<span id="1yIBXmXo"></span>
## Procedure


1. **Prepare retrieval backend resources**: Create the target retrieval service instance  in the BytePlus console, and complete data source upload and chunk configuration.

2. [Import a knowledge base](https://docs.byteplus.com/en/docs/agentkit/Managing_knowledge_bases#AXRPmjaf): Import the knowledge base in the console to easily deploy agents associated with knowledge bases on the AgentKit platform. .

3. [Test retrieval performance online](https://docs.byteplus.com/en/docs/agentkit/Knowledge_retrieval): Enter queries in the built\-in debugging panel, verify recalled snippets and source metadata, and tune chunk settings, thresholds, Top\-K, and reranking parameters.

4. [Integrate the knowledge base into an agent](https://docs.byteplus.com/en/docs/agentkit/Integrating_knowledge_base_in_agent): Inject the environment variables from the integration code into the agent, and call the Knowledge component via the unified search API, decoupling code from the backend.

5. [Publish the agent application](https://docs.byteplus.com/en/docs/agentkit/Releasing_runtimes): Save all configurations and publish the agent version, then perform end\-to\-end conversation verification after the agent is published.

6. [Perform maintenance and iteration](https://docs.byteplus.com/en/docs/agentkit/Observability-): Use the unified observability dashboard to monitor memory chain metrics, perform memory correction and cleanup as needed, and switch the underlying memory backend without code changes.
