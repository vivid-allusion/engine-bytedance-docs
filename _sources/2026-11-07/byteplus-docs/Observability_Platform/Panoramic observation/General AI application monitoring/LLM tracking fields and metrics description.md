---
title: "LLM tracking fields and metrics description"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/LLM_tracking_fields_and_metrics_description"
---

AI application monitoring provides an instrumentation monitoring solution for the training, inference, and agent scenarios of large language models (LLMs). The overall solution covers two core modules: **distributed tracing (Tracing)**  and **metric monitoring (Metrics)** . The instrumentation data will be continuously updated and optimized as the OpenTelemetry community develops. This topic describes instrumentation\-related details.

<span id="tLxQUMUb"></span>
## Span Attributes

For LLM trace spans, additional Gen AI attributes are added to record details such as model call duration and token consumption count. The main fields include:

<span id="ENmHl9wU"></span>
### Model and request metadata


|**Attribute** |**Type** |**Description** |**Example** |
|---|---|---|---|
|gen_ai.system |string |Generative AI system identifier, such as platform name or framework name. |"openai", "arkitect", "Langchain" |
|gen_ai.request.model |string |Name of the requested model. |"gpt\-4" |
|gen_ai.request.type |string |Classification of the request type. |"chat"， "completion"<br><br> |
|gen_ai.response.model |string |Model name that actually responds. |"gpt\-4\-1106\-preview" |
|gen_ai.request.max_tokens |int |Maximum number of tokens generated for the request. |1000 |
|gen_ai.request.temperature |float |Generation temperature parameter for the request, used to control randomness. |0.7 |
|gen_ai.request.top_p |float |Top\-P sampling parameter for the request. |0.9 |


<span id="l85XeeRl"></span>
### **Input and output content**


|**Attribute** |**Type** |**Description** |**Example** |
|---|---|---|---|
|gen_ai.prompt.{index}.role |string |Role in the input message, such as user or system. |"user","system" |
|gen_ai.prompt.{index}.content |string |Content of the input message. |"Introduce yourself" |
|gen_ai.completion.{index}.role |string |Role in the output message, such as assistant. |"assistant" |
|gen_ai.completion.{index}.content |string |Content of the output message. |"I am Doubao..." |
|gen_ai.response.finish_reason |string |Reason for generation completion, such as stop and length. |"stop" |
|gen_ai.response.stop_reason |string |Specific stopping condition, such as triggered stop sequence. |"\n" |


<span id="2XXNRU82"></span>
### Token usage statistics


|**Attribute** |**Type** |**Description** |**Example** |
|---|---|---|---|
|gen_ai.usage.input_tokens |int |Input token count. |1024 |
|gen_ai.usage.output_tokens |int |Output token count. |512 |
|gen_ai.usage.total_tokens |int |Total token count. Total token count = Input token count ** ** + Output token count. |1536 |
|gen_ai.usage.cache_creation_input_tokens |int |Number of input tokens during cache creation. |2048 |
|gen_ai.usage.cache_read_input_tokens |int |Number of input tokens read from cache. |1024<br><br> |


<span id="1PLKYYO7"></span>
### Streaming processing and performance metrics


|**Attribute** |**Type** |**Description** |**Example** |
|---|---|---|---|
|gen_ai.is_streaming |bool |Whether it is a streaming request. |true |
|gen_ai.chat_completions.streaming_time_to_first_token |float |Time to First Token (TTFT) for streaming requests. |0.3 |
|gen_ai.chat_completions.streaming_time_per_output_token |float |Average generation duration per output token (seconds), applicable for streaming requests. |0.02 |


<span id="lw2h1hHn"></span>
### User and session information


|<div style="text-align: center"><br><strong>Attribute</strong></div><br> |<div style="text-align: center"><br><strong>Type</strong></div><br> |<div style="text-align: center"><br><strong>Description</strong></div><br> |<div style="text-align: center"><br><strong>Example</strong></div><br> |
|---|---|---|---|
|gen_ai.user.id |string |User ID. |"user_#a3f9b2" |
|gen_ai.session.id |string |Session ID. |a2b1ee10\-22df\-42d9\-8daa\-986a609b1686 |


<span id="nWCUhJ72"></span>
## Metrics

To better collect performance metrics and token consumption data for LLMs, relevant metrics are recorded. These metrics can be viewed in the AI application monitoring console or used to build custom dashboards. Labels of LLM metrics are as follows:


* The following labels are recorded for all LLM metrics:



|**Dimension key** |**Example** |**Descriptions** |
|---|---|---|
|service |llm\-demo |Service name. |
|gen_ai_system |openai |LLM system. |
|stream |true |Whether it is a streaming request. |
|server_address |127.0.0.1 |Request address. |
|gen_ai_response_model |"gpt\-4\-1106\-preview" |Name of the model that responds. |
|gen_ai_operation_name |"chat" |Operation type. |



* The following labels are recorded for some LLM metrics:



|**Dimension key** |**Example** |**Descriptions** |
|---|---|---|
|gen_ai_token_type |input, output |Token type. |
|gen_ai_response_finish_reason |stop |Generation completion reason. |


<span id="qxl7OUEW"></span>
### Statistical metrics of the generated results


|**Metric** |**Type** |**Descriptions** |**Special dimension** |
|---|---|---|---|
|gen_ai.chat.count |Counter<br><br> |Total number of chat sessions.<br><br> |None |
|gen_ai.client.generation.choices |Counter |Number of generation choices for scenarios with multiple candidate results. |gen_ai_response_finish_reason |


<span id="ZWUWsk5v"></span>
### Token consumption metric


|**Metric** |**Type** |**Descriptions** |**Special dimension** |
|---|---|---|---|
|gen_ai.client.token.usage |Histogram |Token consumption distribution. |gen_ai_token_type |


<span id="FEko8iDq"></span>
### Streaming processing duration metrics


|**Metric** |**Type** |**Descriptions** |**Special dimension** |
|---|---|---|---|
|gen_ai.client.operation.duration |Histogram |The total request time (end\-to\-end).<br><br> |None |
|gen_ai.chat_completions.streaming_time_to_first_token |Histogram |Time to First Token (TTFT) for streaming requests.<br><br> |None |
|gen_ai.chat_completions.streaming_time_to_generate |Histogram |Time to First Token (TTFT) for streaming requests. |None |
|gen_ai.chat_completions.streaming_time_per_output_token |Histogram |Average generation duration per output token (seconds), applicable for streaming requests. |None |


<span id="DveMYLE9"></span>
### Request exception statistics


|**Metric** |**Type** |**Descriptions** |**Special dimension** |
|---|---|---|---|
|gen_ai.chat_completions.exceptions |Counter |Exception count of LLM calls. |None |
