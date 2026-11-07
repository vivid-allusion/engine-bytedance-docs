---
title: "Overview of AI application monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_AI_application_monitoring"
---

As AI and LLMs explode in popularity, AI application architectures are evolving toward distributed and heterogeneous systems. Model inference has evolved from single\-node execution to complex pipelines involving data preprocessing and multimodal fusion. In these dynamic topologies, traditional monitoring solutions struggle to track performance fluctuations or locate faults. End\-to\-end observability is therefore critical to trace anomalous data flows across components and pinpoint bottlenecks throughout the inference pipeline. Server\-side Monitoring now supports mainstream agents and inference frameworks. It not only enables root cause analysis in LLM scenarios but also collects golden signals specific to AI workloads. This achieves comprehensive coverage for all AI scenarios and full support for LLMs, ensuring high availability and cost optimization for LLM applications.

<span id="SIhtQl6N"></span>
## Core features

AI application monitoring supports end\-to\-end observability and monitoring for AI applications. By integrating with AI application monitoring instrumentation, you can achieve the following:


* **Metrics**: Collects service RED metrics and Gen_AI\-related metrics (such as token consumption, TTFT, and TPOT) to monitor application performance.

* **Distributed tracing (Tracing)** : Records critical paths and intermediate states during AI application execution.

* **Log collection (Log)** : ** ** Automatically collects logs and associates them with traces for analysis.

* **M\-T\-L integration**: Perform correlated analysis across metrics, traces (Tracing), and logs.

* **Visual analytics**: Use advanced features such as multidimensional search, topology generation, and custom dashboards through the console.

* **Insight analysis**: Analyze sessions in bulk based on insight rules.


<span id="dnylCfN9"></span>
## Integration methods

Server\-side Monitoring has been adapted for various programming languages and deployment methods of AI applications. This ensures users can complete integration quickly and cost\-effectively. The integration descriptions and best practices are as follows:


|Language/service/framework |Integration description |Best practice |
|---|---|---|
|Python |For AI applications developed in Python, such as those built with frameworks like LangChain or OpenAI, you can use the auto\-instrumentation feature of Server\-side Monitoring for integration. For details, see [Python application integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Python_applications). |[VeADK agent trace monitoring](https://docs.byteplus.com/en/docs/Observability_Platform/VeADK_agent_trace_monitoring)<br><br> |
|Nodejs |For AI applications developed in Nodejs, such as those built with frameworks like OpenAI, you can use the auto\-instrumentation feature of Server\-side Monitoring for integration. For details, see [Nodejs application integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_a_Nodejs_application). |/ |
|GoLang |For AI applications developed in GoLang, we recommend following the [GoLang application integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Go_applications) guide. |[Eino integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_Eino)<br><br>[Reporting observability data of Eino-Assistant application](https://docs.byteplus.com/en/docs/Observability_Platform/Reporting_observability_data_of_Eino-Assistant_application) |
|FaaS service |Function Service (FaaS) is deeply integrated with Server\-side Monitoring. For functions deployed on FaaS, simply enabling Server\-side Monitoring allows the function monitoring data to be automatically integrated. This enables automatic trace collection, metric generation, and supports advanced features such as call chain search and log search.  |[MaaS high-code trace monitoring](https://docs.byteplus.com/en/docs/Observability_Platform/MaaS_high-code_link_monitoring) |
|vLLM |vLLM is an open\-source framework dedicated to‌ the inference and deployment of large language models (LLMs). It is designed to optimize and accelerate LLM usage, especially for efficient inference. You can seamlessly monitor the vLLM inference engine via Server\-side Monitoring. Server\-side Monitoring collects observability data from vLLM, enabling you to analyze conversations and gain deeper insights into your LLMs. |[vLLM inference engine trace monitoring](https://docs.byteplus.com/en/docs/Observability_Platform/vLLM_inference_engine_trace_monitoring) |
|AgentKit application |AgentKit is an enterprise\-level foundational development tool platform provided by . It can be used for building, deploying, and running AI agents, offering flexible, open, and modular add\-on capabilities for AI agents. This helps developers and enterprises in quickly building, deploying, and managing agents through a unified runtime environment, integrated resource scheduling, and security assurance mechanisms.<br><br>AI application monitoring seamlessly integrates with AgentKit, providing comprehensive observability into AgentKit runtime, memory, and AI agent\-related data. This facilitates viewing the health status of AgentKit and AI agents and quickly locating faults. |[Getting started with AgentKit](https://docs.byteplus.com/en/docs/agentkit/Quick_start_with_AgentKit) |
