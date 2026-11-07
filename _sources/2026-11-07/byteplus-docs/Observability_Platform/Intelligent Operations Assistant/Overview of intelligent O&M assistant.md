---
title: "Overview of intelligent O&M assistant"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_Intelligent_Operations_Assistant"
---

The intelligent O&M assistant is a full\-stack intelligent O&M hub built on monitoring data and dedicated to AI O&M. Primarily tailored for observability scenarios, it possesses in\-depth domain expertise and provides data query, basic analysis, and cross\-service comprehensive troubleshooting capabilities. Its vision is to codify top experts' expertise into platform capabilities, build an ever\-evolving "AI SRE teammate", and ultimately achieve 24/7 autonomous event response and root cause analysis.

The intelligent O&M assistant serves as the AI\-native intelligent orchestration and decision\-making layer. By forming a complete closed loop of "Connect \-\> Diagnose \-\> Act \-\> Extend \-\> Govern", it systematically addresses the fundamental pain points in the O&M of large\-scale distributed systems. It will seamlessly cooperate with the existing observability platforms, event centers, release systems, and ChatOps tools of enterprises, and act as the core engine driving continuous reliability improvements across the entire technical stack.

> **tip**

> [Public beta]: This feature is currently in public beta.

## Feature overview

|Feature |Description |
|---|---|
|[Initiate tasks](https://docs.byteplus.com/en/docs/Observability_Platform/Using_Intelligent_Operations_Assistant) |Use a natural language conversation to describe issues, alert symptoms, and troubleshooting targets, and call an agent to initiate an intelligent O&M task. |
|[Automation](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_automated_tasks) |A scheduled intelligent O&M task that runs periodically based on custom prompts, an agent, and a configured execution time. Suitable for periodic scenarios such as routine inspections and resource health checks. |
|[Response plans](https://docs.byteplus.com/en/docs/Observability_Platform/create-response-plan) |A condition\-triggered automated analysis workflow based on alerts. When an alert is triggered, the system follows the Runbook\-defined workflow to automatically check for faults. Finally, it provides remediation recommendations for manual confirmation and reference during remediation. |
|[Expert agent](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_expert_agents) |Configure agents derived from observability experience in the intelligent O&M assistant to extend its capabilities and meet the need for on\-demand agent customization. |
|[Skill](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_skills) |A skill is a standardized capability package encapsulated for specific business scenarios. Configuring skills for an agent provides it with a complete set of operational specifications, enabling it to autonomously identify intent, complete professional tasks based on defined workflows, and deliver practical execution capabilities. |

## Scope of application

Currently, four observability products including[ AI application monitoring](https://docs.byteplus.com/en/docs/apmplus/What_is_server_monitoring), [Server-side Monitoring](https://docs.byteplus.com/en/docs/apmplus/Application_Performance_Management_Plus), [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus), and [Cloud Monitor ](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor)have been successfully integrated with the Intelligent Operations Assistant. [RUM ](https://docs.byteplus.com/en/docs/apmplus/What_is_client_monitoring) do not yet support access to the Intelligent Operations Assistant.

## Core capabilities

Positioned as an AI\-native intelligent orchestration and decision\-making hub, the intelligent O&M assistant does not replace existing monitoring and log systems. Instead, it acts as an upper\-layer O&M brain. Relying on three core capabilities: Connect Everything, Understand Context, and Act Autonomously,  covering the full processes of observability and O&M.

The list of available tools and corresponding capability descriptions is provided as follows:

|Product |Tool |Description |
|---|---|---|
|Cloud Monitor |cloudmonitor__get_metric_data |Query time series data for specific metrics. |
||cloudmonitor__list_o11y_agent_vpc_endpoints |Query the endpoints of collection plugins. |
||cloudmonitor__list_o11y_agent_ecs_process_configs |Query ECS process monitoring configurations. |
||cloudmonitor__get_o11y_agent_ecs_auto_install |Obtain the auto\-installation configuration of the ECS collection plugin. |
||cloudmonitor__list_o11y_agent_ecs_instances |Query the status of the ECS collection plugin. |
||cloudmonitor__list_o11y_agent_ecs_instance_metadata |Query the metadata information of the ECS collection plugin. |
||cloudmonitor__cloudmonitor_list_rules |List alert rules. |
||cloudmonitor__cloudmonitor_list_rules_by_ids |Query alert rules by ID. |
||cloudmonitor__cloudmonitor_list_alert_group |Query alert history. |
||cloudmonitor__cloudmonitor_list_resource |Query instance metadata information. |
||cloudmonitor__cloudmonitor_list_metric_docs |Obtain metric documentation. |
||cloudmonitor__cloudmonitor_list_namespaces |Obtain the namespace list of the product. |
|Server\-side Monitoring |apmplus__apmplus_server_list_alert_rule |List alert rules. |
||apmplus__apmplus_server_list_notify_group |List notification groups. |
||apmplus__apmplus_server_list_logs |Query service logs. |
||apmplus__apmplus_server_query_metrics |Query metrics via PromQL. |
||apmplus__apmplus_server_get_trace_detail |Obtain trace details. |
||apmplus__apmplus_server_list_span |List Spans. |
||apmplus__apmplus_server_get_service_topo |Query the service topology. |
||apmplus__apm_server_list_alert_history |List alert history. |
||apmplus__apm_server_list_aggregated_alert_history |Aggregate alert history into an overview. |
||apmplus__apmplus_server_list_metrics |List available metrics. |
||apmplus__apmplus_server_list_genai_sessions |List GenAI sessions. |
|Vital Managed Service for Prometheus |vmp__list_workspaces |List workspaces. |
||vmp__list_workspace_instance_types |List instance types. |
||vmp__query_metrics |Execute instant queries via PromQL. |
||vmp__query_range_metrics |Execute range queries via PromQL. |
||vmp__query_metric_names |List metric names. |
||vmp__query_metric_labels |List metric labels. |
||vmp__query_series |Query time series. |
|Vital Kubernetes Engine (VKE) |vke__guide |View the VKE user guide. |
||vke__get_note |Obtain parameter descriptions. |
||vke__list_clusters |List clusters. |
||vke__list_supported_resource_types |List supported resource types. |
||vke__list_supported_addons |List supported plugins. |
||vke__list_addons |List installed plugins. |
||vke__list_node_pools |List node pools. |
||vke__list_nodes |List nodes. |
||vke__list_virtual_nodes |List virtual nodes. |

## Common examples

The intelligent O&M assistant delivers DevOps services including observability data query, basic product analysis, and cross\-service comprehensive troubleshooting. Common examples and execution actions are listed below:

|Scenario |Sample prompt |
|---|---|
|Observability data query<br><br> |* Top 5 instances with the highest CPU usage over the past hour.<br><br>* Display the P99 latency trend of order\-service.<br><br>* Query error logs around 23:00 yesterday. |
|Alert troubleshooting analysis |* Analyze the current alert: Sudden latency spike of order\-service.<br><br>* Troubleshoot the surging error rate of payment\-api.<br><br>* What could be the causes of the current alert? |
|Topology analysis and diagnosis |* Which downstream services does order\-service depend on? Which service has the slowest response?<br><br>* Analyze trace bottlenecks of order\-service.<br><br>* Which layer does the current timeout issue occur at? |

## Usage Process

**Preset agent use cases**

No additional configuration is required. You can directly use the system preset VeOps Agent for task processing.

* For details on using the conversation interface, see [Using intelligent O&M assistant](https://docs.byteplus.com/en/docs/Observability_Platform/Using_Intelligent_Operations_Assistant).

* For details on configuring custom tasks, see [Configuring automated tasks](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_automated_tasks).

**Custom agent use cases**

1. [Configure skills](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_skills): Upload skills derived from historical observability experience to the intelligent O&M assistant.

2. [Configure expert agents](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_expert_agents): Customize agent prompts and add skills.

3. Use custom agents: Select a custom expert agent for task processing.

   * For details on using the conversation interface, see [Using intelligent O&M assistant](https://docs.byteplus.com/en/docs/Observability_Platform/Using_Intelligent_Operations_Assistant).

   * For details on configuring custom tasks, see [Configuring automated tasks](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_automated_tasks).
