---
title: "ArkClaw Enterprise metric descriptions"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/ArkClaw_Enterprise_metric_descriptions"
---

This topic describes the metrics exposed by ArkClaw. You can use these metrics as a reference for monitoring, alerting, and observability analysis.

<span id="PXb6wFHB"></span>
## Metric analysis

The following metrics cover the end\-to\-end operation flow of Claw Enterprise, including key stages such as request ingress, gateway startup and shutdown, instance resources, Skill/tool execution, agent call, message processing, session state, Webhook processing, and token consumption.

<span id="K4738o36"></span>
### Request metrics


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_request_count |Counter |Count |Claw Enterprise request count |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* from<br><br>* conversation_id |
|arkclaw_enterprise_request_duration_avg |Histogram |s |Average request processing latency of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* from<br><br>* conversation_id |
|arkclaw_enterprise_request_duration_pct50 |Histogram |s |Request processing latency of Claw Enterprise (P50) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* from<br><br>* conversation_id |
|arkclaw_enterprise_request_duration_pct90 |Histogram |s |Request processing latency of Claw Enterprise (P90) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* from<br><br>* conversation_id |
|arkclaw_enterprise_request_duration_pct99 |Histogram |s |Request processing latency of Claw Enterprise (P99) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* from<br><br>* conversation_id |


<span id="kVVePlJD"></span>
### Gateway metrics


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_gateway_start_count |Counter |Count |Gateway startup count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* operation<br><br>* port |
|arkclaw_enterprise_gateway_stop_count |Counter |Count |Gateway shutdown count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* operation<br><br>* port |


<span id="kiDSVt7f"></span>
### Instance metrics


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_disk_read_bandwidth |\- |B/s |Disk read bandwidth of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id |
|arkclaw_enterprise_disk_read_iops |\- |Count/s |Disk read IOPS of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id |
|arkclaw_enterprise_disk_write_bandwidth |\- |B/s |Disk write bandwidth of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id |
|arkclaw_enterprise_disk_write_iops |\- |Count/s |Disk write IOPS of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id |
|arkclaw_enterprise_instance_cpu_usage_ratio |\- |Ratio |Instance CPU utilization of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id |
|arkclaw_enterprise_instance_memory_usage_ratio |\- |Ratio |Instance memory usage rate of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id |
|arkclaw_enterprise_process_uptime |\- |ms |Process startup time of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id |


<span id="zmcrGv8y"></span>
### Skills and tools


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_skill_visit_count |Counter |Count |Skill access count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* skill_name |
|arkclaw_enterprise_tool_duration_avg |Histogram |s |Average tool execution latency of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* tool_name<br><br>* error_type<br><br>* agent_id<br><br>* session_key |
|arkclaw_enterprise_tool_duration_pct90 |Histogram |s |Tool execution latency of Claw Enterprise (P90) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* tool_name<br><br>* error_type<br><br>* agent_id<br><br>* session_key |
|arkclaw_enterprise_tool_error_count |Counter |Count |Tool call failure count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* tool_name<br><br>* error_type<br><br>* agent_id<br><br>* session_key |
|arkclaw_enterprise_tool_error_rate |\- |Ratio |Tool execution error rate of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* tool_name<br><br>* error_type<br><br>* agent_id<br><br>* session_key |
|arkclaw_enterprise_tool_execution_count |Counter |Count |Tool execution count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* tool_name<br><br>* error_type<br><br>* agent_id<br><br>* session_key |


<span id="uL6bvYmF"></span>
### Agent call


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_active_agent_count |\- |Count |The total number of agents that generated data interactions within a specified time range, deduplicated by agent_id. |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* agent_id |
|arkclaw_enterprise_agent_call_count |Counter |Count |Agent call count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* agent_id<br><br>* session_key<br><br>* is_success |
|arkclaw_enterprise_agent_duration_avg |Histogram |s |Average agent call latency of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* agent_id<br><br>* session_key<br><br>* is_success |
|arkclaw_enterprise_agent_duration_pct90 |Histogram |s |Agent call latency of Claw Enterprise (P90) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* channel_id<br><br>* agent_id<br><br>* session_key<br><br>* is_success |
|arkclaw_enterprise_llm_success_rate |\- |Ratio |LLM call success rate of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* error_type<br><br>* api_type<br><br>* model<br><br>* provider<br><br>* stop_reason<br><br>* llm_turn |


<span id="EQoGXc9m"></span>
### Message conversation


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_message_count |Counter |Count |Message count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_outcome |
|arkclaw_enterprise_message_duration_avg |Histogram |ms |Average message processing latency of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_outcome |
|arkclaw_enterprise_message_duration_pct50 |Histogram |ms |Message processing latency of Claw Enterprise (P50) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_outcome |
|arkclaw_enterprise_message_duration_pct90 |Histogram |ms |Message processing latency of Claw Enterprise (P90) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_outcome |
|arkclaw_enterprise_message_duration_pct99 |Histogram |ms |Message processing latency of Claw Enterprise (P99) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_outcome |
|arkclaw_enterprise_message_failure_rate |\- |Ratio |Message processing failure rate of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_outcome |
|arkclaw_enterprise_message_received |Counter |Count |Received message count of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* from<br><br>* channel_id<br><br>* conversation_id |
|arkclaw_enterprise_message_success_rate |\- |Ratio |Message processing success rate of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_outcome |
|arkclaw_enterprise_queue_depth_avg |Histogram |Count |Average queue length of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_source<br><br>* openclaw_lane |


<span id="Vp0DeMQS"></span>
### Session analysis


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_session_state |Counter |Count |Session status distribution of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_state<br><br>* openclaw_reason |
|arkclaw_enterprise_session_stuck_count |Counter |Count |Claw Enterprise stuck session count |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_state |
|arkclaw_enterprise_session_stuck_duration_avg |Histogram |ms |Claw Enterprise average duration of stuttering sessions |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_state |


<span id="qt1NBHgQ"></span>
### Webhook


|Metric Name |Type |Unit |Description |Label |
|---|---|---|---|---|
|arkclaw_enterprise_webhook_duration_avg |Histogram |ms |Average Webhook processing latency of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_webhook |
|arkclaw_enterprise_webhook_duration_pct50 |Histogram |ms |Webhook processing latency of Claw Enterprise (P50) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_webhook |
|arkclaw_enterprise_webhook_duration_pct90 |Histogram |ms |Webhook processing latency of Claw Enterprise (P90) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_webhook |
|arkclaw_enterprise_webhook_duration_pct99 |Histogram |ms |Webhook processing latency of Claw Enterprise (P99) |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_webhook |
|arkclaw_enterprise_webhook_error_rate |\- |Ratio |Webhook processing error rate of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_channel<br><br>* openclaw_webhook |


<span id="UxSGnK5R"></span>
### Token usage (ArkClaw gateway)


|**Metric Name** |**Type** |**Unit** |**Description** |**Label** |
|---|---|---|---|---|
|arkclaw_enterprise_apig_cache_hit_rate |\- |Ratio |Token cache hit rate of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* uid<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_model |
|arkclaw_enterprise_apig_cache_read_token_usage_sum |Counter |Count |Cache token usage of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* uid<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_model |
|arkclaw_enterprise_apig_input_token_usage_sum |Counter |Count |Input token usage of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* uid<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_model |
|arkclaw_enterprise_apig_output_token_usage_sum |Counter |Count |Output token usage of Claw Enterprise |* service<br><br>* user_email<br><br>* user_name<br><br>* uid<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_model |
|arkclaw_enterprise_apig_total_token_usage_sum |Counter |Count |Claw Enterprise total tokens for input and output |* service<br><br>* user_email<br><br>* user_name<br><br>* uid<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_model |
|arkclaw_enterprise_apig_total_token_with_cache_usage_sum |Counter<br><br> |Count<br><br> |Claw Enterprise total tokens for input, output, and cache |* service<br><br>* user_email<br><br>* user_name<br><br>* uid<br><br>* user_department<br><br>* claw_space_id<br><br>* openclaw_model |


<span id="HSz5ySXk"></span>
### Token usage (self\-managed gateway)


|**Metric Name** |**Type** |**Unit** |**Description** |**Label** |
|---|---|---|---|---|
|custom_gateway_token_used |Counter |1 (number) |Token consumption<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details about reporting Token usage data for self\-managed gateways and for descriptions of the metrics and labels, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Reporting_self-managed_gateway_usage_data">Reporting usage data from self\-managed gateways</a>.</div><br><br><br> |* service<br><br>* user_email<br><br>* user_name<br><br>* user_department<br><br>* claw_space_id<br><br>* model<br><br>* from<br><br>* provider<br><br>* token_type<br><br>* apmplus_business_carrier |


<span id="3gmRc16n"></span>
## Tag descriptions

Labels used in the above metrics are listed below. By utilizing these metrics to build monitoring dashboards, you can gain a comprehensive understanding of the ArkClaw system running status, promptly identify and resolve issues, optimize system performance, and enhance user experience.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In addition to the following labels, observability metrics are also associated with custom tags of ArkClaw instances for data filtering or grouping. For details of ArkClaw instance custom tags, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Tag_management">Managing tags</a>.</div>



|**Label** |Label name in English |
|---|---|
|service |Service name |
|user_email |User email |
|user_name |User Name |
|user_department |User Department |
|claw_space_id |Claw space ID |
|channel_id |Channel ID |
|from |Sender |
|conversation_id |Conversation ID |
|operation |Operation |
|port |Gateway port |
|skill_name |Skill name |
|tool_name |Tool name |
|error_type |Error flag |
|agent_id |Agent ID |
|session_key |Session key |
|is_success |Is success |
|api_type |API type |
|model |Model name |
|provider |Provider name |
|stop_reason |Stop reason |
|llm_turn |LLM turn |
|openclaw_channel |Channel |
|openclaw_source |Source |
|openclaw_outcome |Outcome |
|openclaw_lane |Queue lane |
|openclaw_state |Session state |
|openclaw_reason |Session state reason |
|openclaw_webhook |Webhook type |
|openclaw_provider |Provider |
|openclaw_model |Model |
|openclaw_token |Token type |
