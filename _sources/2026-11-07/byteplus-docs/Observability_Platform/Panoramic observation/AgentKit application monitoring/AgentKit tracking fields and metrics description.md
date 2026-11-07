---
title: "AgentKit tracking fields and metrics description"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/AgentKit_tracking_fields_and_metrics_description"
---

AI application monitoring provides an instrumentation tracking solution tailored for AgentKit. OpenTelemetry instrumentation is built into the AgentKit SDK to enable comprehensive observability of the call processes of AgentKit runtimes. The overall solution covers two core modules: **distributed tracing (Tracing)**  and **metric monitoring (Metrics)** . This topic describes instrumentation related details.

<span id="cn4zwDyp"></span>
## Span

Each call of the AgentKit runtime generates a span tracking record. Span attributes include:


|**Attribute** |**Type** |**Description** |**Example** |
|---|---|---|---|
|gen_ai.system |string |Generative AI System identifier, fixed as `agentkit`, which indicates AgentKit instrumentation. |"agentkit"<br><br> |
|gen_ai.func_name |string |Specific called function. |"run" |
|gen_ai.user.id |string |Caller user ID. |"user_#a3f9b2" |
|gen_ai.session.id |string |Call session ID. |a2b1ee10\-22df\-42d9\-8daa\-986a609b1686 |
|gen_ai.span.kind |string |Span type of Gen AI instrumentation, such as "workflow" and "llm". |"workflow" |
|gen_ai.operation.name |string |The operation executed on AgentKit Runtime, such as invoke_agent and tool. |"invoke_agent" |
|gen_ai.operation.type |string |The type of operation executed on AgentKit Runtime, such as agent and a2a_agent. |"agent" |
|gen_ai.input |string |The input of the call. |{"prompt": "hello"} |
|gen_ai.output |string |The output of the call.​ |"Hello! Glad to help you. Is there anything I can do for you?" |


<span id="7zGztkNO"></span>
## Metrics

Duration\-focused metrics cover metrics such as call duration and QPS. The statistical metrics of the generated results are as follows:


|**Metric** |**Type** |Descriptions |**Metric dimensions** |
|---|---|---|---|
|agentkit_runtime_operation_latency |Histogram<br><br> |Call duration<br><br> |* `error_type`: Enumeration values of call errors. An empty value indicates a successful request.<br><br>* `gen_ai_operation_name`: The operation executed on AgentKit Runtime, such as invoke_agent and tool.<br><br>* `gen_ai_operation_type`: The type of operation executed on AgentKit Runtime, such as agent and a2a_agent. |
|agentkit_runtime_operation_latency_count |Counter |Call count |* `error_type`: Enumeration values of call errors. An empty value indicates a successful request.<br><br>* `gen_ai_operation_name`: The operation executed on AgentKit Runtime, such as invoke_agent and tool.<br><br>* `gen_ai_operation_type`: The type of operation executed on AgentKit Runtime, such as agent and a2a_agent. |
