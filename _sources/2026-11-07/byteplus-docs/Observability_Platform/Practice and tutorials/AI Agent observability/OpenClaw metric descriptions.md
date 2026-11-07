---
title: "OpenClaw metric descriptions"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/OpenClaw_metric_descriptions"
---

This topic describes the OpenTelemetry metrics exposed by OpenClaw through the `diagnostics-otel` plugin. You can use these metrics as a reference for monitoring, alerting, and observability analysis.

<span id="J2hbqQkR"></span>
## Metric analysis

Currently, OpenClaw generates 18 metrics through the `diagnostics-otel` plugin, including 12 counter\-type metrics for cumulative counting and 6 histogram\-type metrics for measuring value distributions. These metrics cover several key aspects of the OpenClaw system, including: model usage, webhook processing, message queuing, and session management.

<span id="vjzdTsHH"></span>
### Model usage\-related metrics

These metrics are directly related to the costs incurred by LLM calls and are critical for controlling expenses. By monitoring token consumption, estimated cost, runtime, and context usage, you can clearly understand the cost of each call and avoid resource waste caused by improper configuration.


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|openclaw.tokens |Counter<br><br> |1 |Token consumption during model processing, differentiated by input and output. |openclaw.channel<br><br>openclaw.provider<br><br>openclaw.model<br><br>openclaw.token |
|openclaw.cost.usd |Counter |1 |Estimated model usage cost (USD) based on token usage. This allows real\-time tracking of expenses.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This metric is used to record the estimated cost of model usage, calculated in US dollars (USD).</div><br><br><br>* <div data-tips="true" data-tips-type="warning">It is generated only when the upstream OpenClaw <code>model.usage</code> event explicitly includes the <code>costUsd</code> field. If the upstream event does not include cost information, no data will be generated under this metric.​</div><br> |openclaw.channel<br><br>openclaw.provider<br><br>openclaw.model |
|openclaw.run.duration_ms |Histogram |ms |Agent runtime duration, indicating the time from the start to the end of a task and reflecting the overall response speed. |openclaw.channel<br><br>openclaw.provider<br><br>openclaw.model |
|openclaw.context.tokens |Histogram |1 |Context window size and usage, indicating the number of context tokens occupied by the current conversation or task. |openclaw.channel<br><br>openclaw.provider<br><br>openclaw.model<br><br>openclaw.context |


<span id="bG6Z4aC1"></span>
### Webhook processing\-related metrics

Webhook is an important channel for OpenClaw to interact with external systems. By monitoring Webhook reception volume, error rate, and processing time, you can promptly detect exceptions in external service calls and ensure the stability of system integration.


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|openclaw.webhook.received |Counter |1 |The total number of Webhook requests received. |openclaw.channel<br><br>openclaw.webhook |
|openclaw.webhook.error |Counter |1 |Number of errors that occurred during Webhook processing. |openclaw.channel<br><br>openclaw.webhook |
|openclaw.webhook.duration_ms |Histogram |ms |The average duration for processing one Webhook request. |openclaw.channel<br><br>openclaw.webhook |


<span id="iJIig6MC"></span>
### Message queue\-related metrics

The message queue acts as an intermediary for task processing in OpenClaw. By tracking the number of enqueued/dequeued messages, queue depth, and wait time, you can determine whether the system is congested or tasks are backlogged. This enables timely resource adjustment and bottleneck analysis.


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|openclaw.message.queued |Counter |1 |Number of messages enqueued, indicating the total volume of messages entering the pending queue and reflects request pressure. |openclaw.channel<br><br>openclaw.source |
|openclaw.message.processed |Counter |1 |Number of messages processed. This indicates the number of completed message\-processing operations and is categorized by outcome (such as success and failure). |openclaw.channel<br><br>openclaw.outcome |
|openclaw.message.duration_ms |Histogram |ms |Message processing duration, indicating the average number of milliseconds required to process a message. |openclaw.channel<br><br>openclaw.outcome |
|openclaw.queue.depth |Histogram |1 |Queue depth at enqueue/dequeue, indicating the number of messages accumulated in the queue when a message is enqueued or dequeued. |openclaw.channel<br><br>openclaw.source<br><br>openclaw.lane |
|openclaw.queue.wait_ms |Histogram |ms |Queue waiting time before message execution. |openclaw.lane |
|openclaw.queue.lane.enqueue |Counter |1 |Number of enqueues into a command queue lane. |openclaw.lane |
|openclaw.queue.lane.dequeue |Counter |1 |Number of dequeues from a command queue lane. |openclaw.lane |


<span id="ta8NmmrX"></span>
### Session management\-related metrics

Session status changes and the number of stuck sessions reflect the health of interactions. By monitoring metrics such as stuck sessions and retry counts, you can quickly identify conversations that are stuck in loops or abnormal states and improve user experience.


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|openclaw.session.state |Counter |1 |Session status transition. |openclaw.state<br><br>openclaw.reason |
|openclaw.session.stuck |Counter |1 |Number of sessions stuck in processing with no progress. |openclaw.state |
|openclaw.session.stuck_age_ms |Histogram |ms |Age of stuck sessions, indicating how long these sessions have been stuck. |openclaw.state |
|openclaw.run.attempt |Counter |1 |Number of task execution retries, used to help identify unstable components. |openclaw.attempt |


<span id="5LqPZvFB"></span>
## Tag descriptions

The following section provides detailed meanings and optional values of tags used in the above metrics. By utilizing these metrics to build monitoring dashboards, you can gain a comprehensive understanding of the runtime status of the OpenClaw system, promptly identify and resolve issues, optimize system performance, and enhance user experience.


|**Label** |Description |Optional values |
|---|---|---|
|openclaw.token |Specifies the type of token to further distinguish the openclaw.tokens metric.<br><br> |* **input**: Number of input tokens received by the model.<br><br>* **output**: Number of output tokens generated by the model.<br><br>* **cache_read**: Number of tokens read from the cache.<br><br>* **cache_write**: Number of tokens written to the cache.<br><br>* **prompt**: Total number of prompt tokens (usually refers to the original text sent to the model), including cache information.<br><br>* **total**: The sum of all the above types of tokens. |
|openclaw.context |Indicates the usage of the context window, used for the openclaw.context.tokens metric. |* **limit**: The maximum context window length supported by the model.<br><br>* **used**: The actual number of context tokens used in this call. |
|openclaw.outcome |Indicates the final result of message processing, used for the openclaw.message.processed and openclaw.message.duration_ms metrics. |The output status of the event, typically indicating "unknown" when the value is unknown. Typical examples: completed, error, and skipped. |
|openclaw.channel |Identifies the source channel or communication platform of the event.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For diagnostic.heartbeat events, this dimension is set to heartbeat and used to record the openclaw.queue.depth metric.</div><br> |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: slack, telegram, discord, api, and cli. |
|openclaw.provider |Identifies the provider of the model service. |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: openai, anthropic, google, azure, and groq. |
|openclaw.model |Identifies the specific model name. |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: gpt\-4\-turbo, claude\-3\-opus\-20240229, and gemini\-1.5\-pro. |
|openclaw.webhook |Identifies the specific Webhook update type or event name.<br><br> |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: message, callback_query, inline_query. |
|openclaw.source |Identifies the source that pushes the message into the queue.<br><br> |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: webhook, rpc, internal |
|openclaw.lane |Identifies the "lane" or partition of the internal command processing queue.<br><br> |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: default, high_priority. |
|openclaw.state |Identifies the specific status of the session.<br><br> |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: idle, processing, waiting_for_input, blocked, finished |
|openclaw.reason |Provides the reason for session status transition.<br><br> |Typically "unknown" when the value is unknown. Sample values are for reference only. Typical examples: user_message, tool_call, model_response, error, timeout. |
|openclaw.attempt |Marks the number of task execution attempts, usually starting from 1.<br><br> |Typical sample values: 1, 2, 3... |
