---
title: "Redefining panoramic full-stack observability in the AI era"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Redefining_panoramic_full-stack_observability_in_the_AI_era"
---

The AI\-native era is confronted with common challenges such as the shift of application logic from deterministic to probabilistic, and the evolution of system architecture from monolithic to distributed collaboration featuring "agent + inference engine". Traditional application monitoring methodologies are no longer sufficient to address these changes. How can we make the operational status of AI applications transparent? How can we quickly identify performance bottlenecks in intelligent applications? The AI scenario monitoring service launched by Observability Platform provides end\-to\-end monitoring spanning from code to models, offering a solution to the observability challenges of the AI era. This topic details how the AI scenario monitoring service of Observability Platform redefines panoramic full\-stack observability in the AI era.

<span id="L7yKc9di"></span>
## Observability challenges

Today, artificial intelligence is transforming industries, and large language models (LLMs) are reshaping application architectures with unprecedented depth. However, this technological transformation has also brought new O&M challenges. Modern AI applications, especially those built on LLMs, have increasingly complex internal structures. These structures are often interwoven with multiple business services, AI frameworks, and model call chains, forming an elusive "black box". Developers and O&M teams are faced with unprecedented observability challenges:

<span id="cFqVDgUv"></span>
### **Unpredictability of intelligent applications**


* The randomness of large model inference results renders traditional deterministic monitoring ineffective.

* Issues, such as fluctuating token usage, jittery inference latency, and session context loss, occur frequently.

* The complex decision\-making chains of agents make troubleshooting analogous to navigating a maze.


<span id="kFsoZkUZ"></span>
### **Visibility blind spots in multi\-layer architectures**


* The workflow spans multiple system boundaries, from user input and agent decision\-making to model inference.

* Calls to frameworks and protocols, such as LangChain, OpenAI SDK, and MCP, are deeply nested, resulting in intricate call relationships.

* The internal state of inference engines, such as SGLang, vLLM, and Dynamo, is opaque, making it difficult to locate performance bottlenecks.


<span id="manWghWQ"></span>
### **Exponential growth of O&M costs**


* Traditional APM tools cannot interpret the semantics of AI applications and only provide basic HTTP/RPC monitoring.

* Manual instrumentation is costly and difficult to cover rapidly iterating AI frameworks.

* Troubleshooting requires cross\-layer analysis of business logic, framework calls, and model inference, leading to low efficiency.


<span id="Zu2lFaYK"></span>
## Solutions

The AI scenario monitoring service launched by Observability Platform deeply integrates the three core monitoring metric types: metrics, traces, and logs. It focuses on resolving the "black box" problem of AI applications and provides end\-to\-end monitoring spanning from code to models. It not only monitors traditional metrics, such as QPS, latency, and error rate, but also prioritizes AI\-specific metrics, including token consumption, time per output token (TPOT), and time to first token (TTFT). This enables integrated monitoring and reshapes the observability experience for AI applications.

<span id="93l4TAei"></span>
### AI monitoring dashboard

Preset AI monitoring dashboards are provided to visually track performance metrics such as model calls, token usage, and TTFT from both model and service perspectives. For more details, refer to [LLM monitoring dashboard](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_monitoring_dashboard).


* **Model perspective**: Navigate to the monitoring dashboard page in AI scenario monitoring, and select a query time range and model to view the model monitoring data. For example, you can view the model call count, latency, and token usage ranking, facilitating performance monitoring of the model.

* **Service perspective**: Navigate to the details page of the specified AI service to access the LLM performance dashboard and token usage dashboard. The LLM performance dashboard displays the overall performance data of all models used by the service, including model call latency, TTFT, TPOT, and model call count ranking. The token usage dashboard shows the token usage of the current service, including total token usage and token usage per model call.


<span id="uiTohV11"></span>
### AI trace analysis

AI trace analysis provides robust query and tracing capabilities, allowing you to view AI trace lists and analyze specific call chains in depth. For more details, refer to [LLM trace analysis](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_trace_analysis).


* **Query AI trace list**: Navigate to the trace analysis page to directly view trace and Span data, including the model used, input and output content, and token usage. Filtering and sorting of the above information are also supported.

* **View** **single trace details**: Click the target trace ID to view in\-depth details of the corresponding trace, including the call list, service topology map, flame graph, and Span details, enabling precise identification of performance bottlenecks.

   * The call list presents trace call details in tabular form and supports filtering and highlighting Spans by component labels for step\-by\-step analysis. In addition, it can mark the call types of AI traces and Spans and display token usage of large model calls. Call types include tool, task, and llm.

   * The service topology map clearly visualizes the upstream and downstream call relationships and execution flow of the trace, helping understand the execution of AI planning.

   * The flame graph intuitively displays performance hotspots of the trace, facilitating quick location of time\-consuming processes and identification of application performance bottlenecks.

   * Span details enable viewing of granular information for individual Spans, including AI process input and output, the model called, and the number of tokens consumed.


<span id="55IG2O8i"></span>
### MTL integrated correlation

MTL integrated correlation breaks down data silos and enables correlated query of metrics, traces, and log data. Examples include log\-to\-trace ID correlation, reverse log query via trace, and real\-time metric correlation via Span.


* Navigate to the log query page: The trace ID associated with the current log is displayed alongside log data. Clicking the ID jumps directly to the trace details page.

* Navigate to the trace analysis page: You can directly query the logs generated during the execution of the current trace.

* Navigate to the Span details page in AI trace analysis: You can locate the large model metrics associated with the current request, with corresponding timestamps marked by dotted lines.


<span id="E1vq2e67"></span>
### AI end\-to\-end full\-trace observability

AI end\-to\-end full\-trace observability enables end\-to\-end trace connectivity from user terminals to AI and middleware. The complete trace includes: user terminals (such as Android/iOS/Web/mini\-programs) → access gateways (such as API Gateway/Ingress/Nginx) → backend services (such as Java/Go/Python) → agents (such as LangChain, OpenAI, and Eino) → large model inference engines (such as SGLang and vLLM), achieving true end\-to\-end observability.

This core capability integrates multiple dimensions including end\-side instrumentation, AI framework support, and inference engine monitoring, forming a comprehensive monitoring ecosystem. It accurately monitors every key node throughout the entire process from user request initiation to final response.


* **Full trace coverage**: Enables end\-to\-end tracing spanning Android/iOS/Web/mini\-programs → API Gateway/Ingress/Nginx → Java/Go/Python applications → AI services/databases/caches/message queues → large model inference engines.

* **Automatic instrumentation**: Adopts a multi\-level automatic instrumentation mechanism based on bytecode enhancement, compile\-time processing, and runtime proxy.

* **Standardized processing**: Based on the OpenTelemetry standard, it establishes unified data instrumentation specifications and trace context propagation protocols. The end\-to\-end full trace tracing fully enables end\-to\-end connectivity spanning user terminals (such as Android/iOS/Web/mini\-programs) → access gateways (such as API Gateway/Ingress/Nginx) → backend applications (such as Java/Go/Python) → AI and middleware (such as databases, caches, and message queues) → large model inference engines (such as SGLang and vLLM).


After the app\-side and server\-side applications are connected properly, requests initiated from the app side are sent to the server\-side application. You can navigate to the trace details page in server\-side monitoring to view the Spans of app requests. The trace list also displays the Spans of app requests. Clicking the "Shift to mobile monitoring" button in the target app request redirects you to the app page in client\-side monitoring for more details.

Meanwhile, the app page in client\-side monitoring also offers a direct link to the corresponding trace details page in server\-side monitoring. In the details section of the log retrieval page, clicking the link under "End\-to\-end trace" redirects you to the single trace query page on the server side for more information. For more details, refer to [APMPlus end-to-end full tracing](https://docs.byteplus.com/en/docs/apmplus/APMPlus_end-to-end_distributed_tracing).

<span id="sOZQYy0I"></span>
### In\-depth support for AI frameworks and inference engines


* **In\-depth** ** AI framework support**: The AI ecosystem includes many frameworks but is highly fragmented. APMPlus achieves in\-depth support for mainstream AI frameworks through intelligent probe technology. All monitoring capabilities adopt a zero\-code intrusion design. Developers can obtain complete observability capabilities with simple configurations, without modifying any business logic. The framework support capabilities include:

   * Instrumentation probes for multiple programming languages, including Python, Node.js, and Java, enabling full coverage of multi\-language probe support.

   * Compatibility with mainstream AI frameworks, such as LangChain and OpenAI, which automatically identifies chain, agent and tool calls and delivers fine\-grained execution path analysis.

   * In\-depth integration with the MCP protocol, providing comprehensive monitoring of service discovery, tool calls, and context management for the Model Context Protocol.

   * Eino framework integration, enhancing monitoring instrumentation for ByteDance's in\-house AI framework.

* **In\-depth inference engine monitoring**: Observability capabilities are extended down to the AI inference engine layer, supporting the monitoring of high\-performance inference frameworks, such as SGLang, Dynamo, and vLLM. Key performance metrics from within the inference engine can be collected, including model call QPS, model call latency, TPOT, and TTFT. This helps users identify and optimize performance bottlenecks at the inference layer.

   * After the inference engine is deployed with its dedicated image, the traces, metrics, and logs are automatically collected from the underlying execution of the inference engine into AI scenario monitoring. Navigate to the trace details page to view the traces and Spans instrumented at the inference engine layer.

   * Navigate to the service overview, LLM performance, token usage, and other related pages to view the core metrics and golden signals for large models. Examples of such metrics and golden signals include large model call count, token usage, response latency, TTFT, TPOT, QPS, and request error rate.

   * Navigate to the runtime monitoring tab to view runtime\-related monitoring information for the inference engine, such as CPU latency, CPU usage, memory usage, GC object count, thread count, and context switch count.

   * Navigate to the trace analysis tab of the inference engine service and click the trace details for a specific request to view the internal trace and Span information of the inference engine. This information can also be contextually correlated with other trace information across the entire call chain.


<span id="NXuuBDOZ"></span>
### LLM session observability

LLM session observability traces the full lifecycle of each session, supports retrieval by session ID, user, and other dimensions, and correlates token usage and traces for each conversation turn. These capabilities enable drill\-down analysis. For more details, refer to [LLM session analysis](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_session_analysis).


* **Multi\-dimensional session search**: Quickly locate target sessions using filters such as session time, session ID, user, latency, and token count. Enter filter criteria on the LLM session analysis page. A list of matching sessions will be displayed with metrics, including session latency, total token usage, and trace count.

* **Full lifecycle session tracing**: From session creation to termination, it records the input/output and token usage for every conversation turn. Click the target session name or the "Details" button in the "Actions" column on the right of the target session to view detailed information, such as total tokens, trace count, and the start time, input, output, trace ID, user ID, token count, and model name for each turn.

* **Single\-turn conversation drill\-down analysis**: Click the trace ID of a specific conversation turn to redirect to the trace analysis page and view detailed large model trace analysis. For a detailed introduction to trace analysis, refer to [Trace analysis](https://docs.byteplus.com/en/docs/apmplus/Trace_analysis).


<span id="XanI48Qw"></span>
## Application scenarios

AI scenario monitoring delivers full\-link, multi\-dimensional, and low\-intrusion monitoring capabilities that seamlessly unify metrics, traces, and logs. It transforms complex, cross\-domain AI application issues into clear, intuitive, and traceable data insights, guiding developers through the entire process from issue detection to root cause localization and resolution. This empowers users to accurately gain insights into AI application performance, optimize resource consumption and user experience, and significantly lower the barriers and time costs associated with troubleshooting and performance monitoring. Typical application scenarios are as follows:

<span id="9r7OXEcW"></span>
### Scenario 1: Performance diagnosis and optimization for agent applications

A customer deployed an agent application on veFaaS, enabled AI scenario monitoring in the application monitoring and Observability Platform, and adopted the inference engine image with built\-in instrumentation provided by the platform. The customer achieved zero\-development\-cost access without any modifications to the business system.

<span id="JmteY6pQ"></span>
#### **Issue detection \- Alert insights for instant response**

During evening peak hours, the customer received an immediate alert from AI scenario monitoring via Lark, which indicated that the P99 latency of the agent application exceeded 5 seconds. The alert not only clearly identified the problematic service and abnormal metrics but also included a direct link to the monitoring dashboard. The customer accessed the troubleshooting interface immediately without any manual lookup.

<span id="UkjvT4aL"></span>
#### **Root cause localization \- Layered drill\-down for precise root cause identification**


1. Locate the service with increased latency using the alert card, and navigate to the service details page in AI scenario monitoring to view detailed response latency information.

2. Access the trace analysis page to check the single\-trace details of the corresponding trace, which supports three visualization views: flame graph, list, and topology graph. At this stage, an exclamation mark appears on the llm_request Span, indicating an error in the Span.

3. Click the llm_request Span to view its detailed information on the right panel, which shows that the Span belongs to the Dynamo inference engine service. Switch to the Events tab to check the complete error stack trace of the Span.


Based on the error stack trace, the root cause is identified as a memory allocation failure in the vLLM engine. It is thus confirmed that the increased agent response latency was caused by an inference engine malfunction. This completes the root cause localization process.

<span id="cVkKdbYN"></span>
#### **Issue resolution \- Targeted troubleshooting with closed\-loop verification**

With the root cause clarified, the resolution path became clear. The customer immediately notified the R&D team to optimize the memory allocation of the inference engine. After the updated version was deployed, the customer verified the optimization effect on the service monitoring dashboard in AI scenario monitoring. The dashboard data showed that the P99 latency of service responses dropped rapidly to under 2 seconds, and the issue was fully resolved.

<span id="MhaQzROk"></span>
#### **Key achievements**


* Timely anomaly detection: Abnormalities were detected promptly via the alert system.

* Significantly improved troubleshooting efficiency: Abnormal inference Spans were quickly filtered out, and the root cause was identified within 5 minutes.

* Substantial cost reduction: The customer resolved the issue independently, saving the troubleshooting effort of three engineers and drastically shortening the troubleshooting time.


<span id="IXkqrZLu"></span>
### Scenario 2: Token usage monitoring and cost optimization

<span id="6UBA9mTH"></span>
#### **Business background**

An enterprise deployed an AI writing assistant application that handles a large number of text generation tasks and incurs substantial token usage. As the business scales up, precision cost control has become the core challenge for the customer.

<span id="PIKdimMq"></span>
#### **Solutions**

A comprehensive cost management system was established by leveraging the token monitoring capabilities of AI scenario monitoring.


* **Real\-time monitoring**: Refined alert rules are configured based on the token usage metrics recorded by AI scenario monitoring to enable real\-time monitoring of token usage.

* **Comparative analysis**: The token usage dashboard is utilized to conduct multi\-dimensional comparative analysis across dimensions such as model type and application scenario.

* **Data\-driven decision\-making**: The token usage ranking feature clearly identifies significant differences in token usage among different models.


<span id="VpSQc80c"></span>
#### **Implementation results**

Through data comparison and cost analysis, significant differences were identified in token usage and cost\-effectiveness across different models. Leveraging accurate data support from AI application monitoring, we ultimately selected a model solution with optimal cost efficiency. This case demonstrates that AI scenario monitoring not only provides basic monitoring capabilities, but also enables enterprises to achieve refined cost management through in\-depth data insights. AI scenario monitoring, in turn, lays a solid foundation for the large\-scale commercial deployment of AI applications.


* **Significant cost reduction**: Overall token usage costs decreased by 30%.

* **Comprehensive monitoring system**: A real\-time monitoring and forecasting mechanism was established to ensure cost controllability.

* **Improved decision\-making efficiency**: Data\-driven decision\-making replaced experience\-based judgment, leading to a substantial boost in optimization efficiency.


<span id="5BQxH6Jp"></span>
## Future outlook

Artificial intelligence is profoundly transforming the world, and this transformation cannot be realized without an observable, predictable, and controllable technical environment. Against this backdrop, the AI observability solution provided by AI scenario monitoring has emerged at the right moment. It is more than a monitoring tool. It is an indispensable technical infrastructure for the AI era. It ensures that every token consumed, every inference latency, and every intelligent decision can be traced.

Looking ahead, we will continue to deepen our expertise in the AI observability field, striving to become the observability standard for the AI\-native era. Our goal is to make the operation of intelligent systems more transparent and reliable, and truly drive artificial intelligence to create tangible business value. Our continuous evolution will focus on the following three strategic directions:

**Build advanced AI comprehension capabilities**


* Continuously expand compatibility with mainstream and emerging AI frameworks, such as Dify and ADK.

* Enhance monitoring capabilities for multimodal AI applications, enabling unified observability across visual, speech, and text modalities.

* Enhance monitoring for AI agent collaboration modes to support the analysis and traceability of complex interactive behaviors in multi\-agent systems.


**Develop intelligent troubleshooting workflows**


* Provide pre\-configured dashboards and alert rules covering typical AI scenarios, significantly lowering the barrier to user adoption.

* Based on real\-time observability data, automatically perform root cause analysis when faults occur and proactively deliver diagnostic conclusions to assist users in quickly locating issues.


**Promote open ecosystem development**


* Offer standardized AI observability APIs to enable seamless integration with various third\-party tools and platforms.

* Establish industry\-wide standard formats for AI observability data to facilitate interoperability and data sharing across different systems.
