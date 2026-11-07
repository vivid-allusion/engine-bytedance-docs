---
title: "Application scenarios"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Application_scenarios"
---

veFaaS is an event\-driven serverless computing platform that hosts functions. It enables you to quickly and cost\-effectively create complex applications without managing servers. This topic describes the typical application scenarios of veFaaS.

<span id=".5b6u5pyN5Yqh5byA5Y-R"></span>
## AI agent development

Based on large language models (LLMs) and plugin tools, veFaaS supports highly customized and flexible AI agent application development. It is applicable to use cases such as intelligent Q&A, retrieval\-augmented generation (RAG), autonomous decision\-making, and complex workflow processing. Leveraging the application form of veFaaS, agent applications are delivered out\-of\-the\-box, deployed with a few clicks, and are O&M\-free. When faced with unpredictable traffic, veFaaS performs autoscaling and helps you run agent services stably and reliably when used together with AI\-native observability. During development, you can use LLM capabilities and APIG to handle ingress traffic to achieve trace observability.

For example, an AI agent of veFaaS receives a user request that passes through an APIG instance. The agent uses MCP‑compatible tools to invoke LLMs and AI Search (knowledge base and memory) to perform intelligent Q&A and autonomous decision\-making.

<span id="7ME62GWC"></span>
## MCP Server

In the MCP Server scenario, veFaaS collaborates with APIG to address session affinity scheduling issues across multiple instances. Combined with the elasticity of stateless computing, MCP services can quickly perform scale\-out to handle unpredictable traffic. Agents access the Function Tools deployed in veFaaS via the MCP SDK by using the MCP protocol. APIG completes authentication, session management, and connection persistence, and veFaaS automatically scales in/out based on request volume. This eliminates the need to reserve fixed resources for the MCP service.

For example, an AI Agent invokes multiple Function Tools deployed in veFaaS via the MCP SDK. APIG routes requests to the corresponding instances based on session affinity and scales automatically with traffic.

<span id="cnWfF83j"></span>
## AI inference

After training the model, you can quickly deploy the model as an online inference service by using veFaaS. veFaaS delivers O&M\-free and autoscaling features. This enables algorithm engineers to focus on the algorithm without managing underlying servers, achieving quick deployment of elastic and highly available inference services. When inference requests fluctuate, veFaaS can provision massive computing resources quickly, removing GPU computing power constraints. During inference, models can be loaded from FileNAS or TOS, and function execution logs can be recorded through TLS for troubleshooting and monitoring.

For example, when a user initiates an inference request, veFaaS loads the model from TOS or FileNAS, completes the inference, and returns the response result, while simultaneously writing function logs to TLS.

<span id="k4S9vW1O"></span>
## Microservices development

With the advancement of cloud‑native and digital transformation, monolithic services are gradually being replaced by microservice architectures. You can easily develop and deploy a microservice in a serverless manner by using the template framework provided by veFaaS and filling in your business logic. Combined with the APIG trigger provided by the platform, you can quickly expose service capabilities and enable inter‑microservice calls. In addition, the platform provides native monitoring, logging, and alerting to help developers deliver end‑to‑end services.

For example, quickly implement a standalone HTTP API by using veFaaS. The API is accessible via internal or external networks.

<span id=".5a6e5pe25pWw5o2u5aSE55CG"></span>
## Real\-time data processing

In real‑time data processing scenarios, message queue products are typically used as middleware to cache messages. veFaaS abstracts various message queue products into triggers and provides a managed consumption solution. This handles complex logic of message queue consumption, such as multi‑site disaster recovery and consumer scheduling and allocation. This allows users to focus on writing business code for data processing and gain the benefits of quick integration and flexible development. In addition, veFaaS can automatically scale in or out based on actual request volume. This helps you easily handle unpredictable traffic fluctuations.

Typical use cases include crediting of red packet rewards, automatic comment moderation, license plate recognition systems, and AI‑powered customer service chatbots.

<span id=".5a6e5pe25paH5Lu25aSE55CG"></span>
## Real\-time file processing

Real‑time file processing is a common use case in daily life. For example, a website crops images immediately after they are uploaded. veFaaS provides a TOS trigger, which can monitor TOS events in real time and pass events that meet the rules to functions. This triggers the corresponding logic and enables users to promptly process changed files.

For example, in video transcoding tasks, when a video is uploaded to TOS, veFaaS automatically detects the file creation event and triggers the corresponding function to execute the processing logic. Video transcoding is a typical resource‑intensive, short‑running task. veFaaS allows a single instance to handle multiple concurrent requests and automatically scales out as needed, dynamically provisioning resources based on the volume of incoming video files. Compared with traditional methods, this method is more efficient and significantly reduces development and operations costs.

<span id=".5a6a5pe25Lu75Yqh5aSE55CG"></span>
## Scheduled task processing

veFaaS provides a timer trigger. It helps you handle scheduled tasks. Many scheduled tasks require quick function startup, and extended latency can seriously affect data accuracy. veFaaS features fast startup, which ensures the timeliness of tasks. In addition, veFaaS can pre\-warm instances before scheduled tasks are triggered. This ensures the accuracy of the trigger time.

Typical use cases include report computation, system health checks, and liveness detection.
