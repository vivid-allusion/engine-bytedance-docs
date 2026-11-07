---
title: "Release notes"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/New-feature-release-notes"
---

This topic describes the latest updates to the features of Vital Managed Service for Prometheus (VMP). New features will be rolled out across regions. We are looking forward to your hands\-on experience.

> **tip**

* > The **Regions** column lists the regions where the feature change applies at the time of the release. The actual supported regions are subject to those displayed in the console. In this column, **All** refers to all regions where the service is available. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vmp/Regions-and-availability-zones).

## October 2026

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Alert rules |Dynamic threshold detection is added. The system automatically retrieves historical metric data to learn trends, dynamically calculates thresholds, identifies abnormal fluctuations, and uses an AI model to determine whether to trigger an alert. You do not need to manually maintain threshold rules. |All |[Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules) |

## August 2026

##
|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Alert template |Alert templates are added to the integration center, enabling you to create alert rule groups based on alert templates. |All |[Cloud Monitor integration](https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services?lang=en) |
|Billing by written metric volume |A new billing method based on the written metric volume has been added. This new billing method offers a monthly free quota of 50 GB for custom metrics and other cloud service metrics. Only usage beyond this free quota will be charged according to standard billing rates. |All |* [Pay-as-you-go](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go)<br><br>* [Creating common workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces)<br><br>* [[Billing updates] Billing by written metric volume is supported for VMP](https://docs.byteplus.com/en/docs/vmp/Billing_updates_Billing_by_written_metric_volume_is_supported) |

## May 2026

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Dedicated workspaces for cloud services |VMP workspaces created by cloud services are dedicated to these cloud services. VMP allows you only to view these dedicated workspaces and prohibits workspace management operations (such as editing or deletion). |All |[Managing workspaces](https://docs.byteplus.com/en/docs/vmp/Managing-workspaces) |
|Task export experience optimizations |The following optimizations have been made to data export tasks to enhance user experience:<br><br><br>* Added a monitoring dashboard for exported data.<br><br>* Added explanatory prompts for workspaces that do not support exporting basic metrics.<br><br>* Added the "No authentication" option for the authentication method for exporting metrics to self\-managed Prometheus instances.<br><br>* Introduced instant validation for data filters. After configuring filter rules, you can immediately run a test and view the check results. |All |* [Exporting metrics to Kafka message queue](https://docs.byteplus.com/en/docs/vmp/Creating_an_export_task)<br><br>* [Exporting metrics to self-managed Prometheus](https://docs.byteplus.com/en/docs/vmp/Exporting_metrics_to_self-managed_Prometheus)<br><br>* [Exporting metrics to TOS](https://docs.byteplus.com/en/docs/vmp/Exporting_metrics_to_TOS) |
|Pod\-level storage usage metric monitoring |The Access Center adds support for components related to container storage metrics. This enables real\-time monitoring of Pod\-level storage usage metrics for applications deployed in VKE clusters, ensuring the stability of configuration management and service discovery in distributed systems. |All |[Container storage metric integration](https://docs.byteplus.com/en/docs/vmp/Container_storage_metric_integration) |
|Integration with the new Alert Center for efficient alert management |VMP is integrated with the new version of Alert Center. On\-call scheduling support is added. The new Alert Center provides a unified workflow for features such as notification policies, notification templates, aggregation policies, and suppression policies, delivering a comprehensively upgraded user experience. Feel free to explore the notification policy configuration in the new Alert Center. |All |* [Notification policy](https://console.byteplus.com/observe/alert/notify/rules)<br><br>* [Notification templates](https://console.byteplus.com/observe/alert/notify/template)<br><br>* [Aggregation policies](https://console.byteplus.com/observe/alert/aggregate)<br><br>* [Silence policy](https://console.byteplus.com/observe/alert/silence) |

## March 2026

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|The conditional duration for alert rules has been expanded. |The selection range for the duration of custom alert triggering policies has been expanded to include 3 hours, 6 hours, and 12 hours. |All |[Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules) |
|Exporting metrics to TOS |VMP workspaces support exporting data to TOS buckets, meeting the requirement for consuming data using TOS. |All |[Exporting metrics to TOS](https://docs.byteplus.com/en/docs/vmp/Exporting_metrics_to_TOS) |
|The node Pod Container list now supports sorting by specified fields. |Added sorting functionality for cpu.usage, memory.usage, requests.cpu, requests.memory, limits.cpu, and limits.memory, enabling sorting by these fields in the node Pod Container list on VKE.<br><br>The path to the list: VKE \> Cloud Native Observability \> Monitoring Center \> Monitoring Dashboard \> Node Details Monitoring \> Node Pod Container List. |All |None |
|Prometheus 3.0 read/write protocol |Compatible with the Prometheus 3.0 read/write protocol, providing native support for any valid UTF\-8 characters throughout the complete data lifecycle (read/write path). |All |None |

## December 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Slow queries |Slow queries can be identified and managed. You can perform precise management of resource\-intensive queries by identifying high\-risk queries with durations exceeding 5 seconds. |All |[Slow queries](https://docs.byteplus.com/en/docs/vmp/Slow_queries) |
|workspace |Common workspaces and aggregation query workspaces support custom authentication methods, including Bearer Token and Basic Auth. ||* [Creating common workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces)<br><br>* [Creating aggregation query workspaces](https://docs.byteplus.com/en/docs/vmp/Creating_an_aggregate_query_workspace) |
|Alert policy |The recovery level of alerts is added, which is used to indicate that the alert has returned to normal (The metric value has fallen back below the threshold). This prevents operation and maintenance personnel from repeatedly troubleshooting issues that are already addressed. ||[Creating an alert policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules) |
|Integration between VMP and MCP |VMP can be integrated with MCP. You can use VMP features by using MCP in a secure manner to achieve metric queries and analysis based on natural language. ||[ChatOps: Managing VMP by using the MCP service](https://docs.byteplus.com/en/docs/vmp/Managing_VMP_by_using_the_MCP_service) |

## November 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|GPU/RDMA millisecond\-level monitoring |VMP can be integrated with High Performance Computing Optimized ECS instances to provide millisecond\-level GPU/RDMA monitoring. |All |[GPU/RDMA millisecond-level monitoring integration](https://docs.byteplus.com/en/docs/vmp/GPU_RDMA-millisecond-level-monitoring-integration) |
|Filtering ECS objects by subnet |Custom metric collection from Elastic Compute Service (ECS) supports subnet\-based filtering, which allows you to collect metrics from ECS instances only within a specific subnet of the virtual private cloud (VPC). |All |[ECS integration](https://docs.byteplus.com/en/docs/vmp/ECS-monitoring) |
|http_sd_configs |Custom metric collection from ECS supports the Prometheus\-native service discovery configuration http_sd_configs. |All |[ECS integration](https://docs.byteplus.com/en/docs/vmp/ECS-monitoring) |
|consul_sd_configs |Custom metric collection from ECS supports the Prometheus\-native service discovery configuration consul_sd_configs. |All |[ECS integration](https://docs.byteplus.com/en/docs/vmp/ECS-monitoring) |
|Query pre\-aggregation |Queries can be automatically rewritten to use pre\-aggregated metrics based on the configured rules. |All |[Creating recording rules](https://docs.byteplus.com/en/docs/vmp/Creating-a-recording-rule) |

## October 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Stacked package purchases |Lift package purchase restrictions and support stacked package purchases. A root user can have 10 packages at the same time, with each package spanning the same number of days.<br><br>In addition, package management has been optimized, allowing you to manage automatic package renewals or cancel packages in the VMP console. |All |* [Purchasing packages](https://docs.byteplus.com/en/docs/vmp/Purchasing-a-resource-package)<br><br>* [Viewing Packages](https://docs.byteplus.com/en/docs/vmp/Viewing-resource-packages) |
|vLLM and Dynamo integration |Support integration of two AI add\-ons: vLLM and Dynamo. You can use VMP to monitor vLLM instances and Dynamo instances deployed in VKE clusters, enabling alerting and optimization for key metrics. |All |* [vLLM integration](https://docs.byteplus.com/en/docs/vmp/vLLM_integration)<br><br>* [Dynamo integration](https://docs.byteplus.com/en/docs/vmp/Dynamo_integration) |
|Custom workspaces for Recording Rules |When creating Recording Rules, you can choose the write destination to write data that has been queried from the source workspace to a specific workspace. |All |[Creating recording rules](https://docs.byteplus.com/en/docs/vmp/Creating-a-recording-rule) |
|Preset alert rule templates available in Integration Center |Preset alert rule templates are available on the Integration task page of Integration Center. When you create an integration task, you can navigate to the alert group creation page to create and enable alert configurations based on a preset alert rule template. This streamlines integration of services such as Kafka, Nacos, and SGLang. |All |* [Nacos integration](https://docs.byteplus.com/en/docs/vmp/Nacos_Integration)<br><br>* [SGLang integration](https://docs.byteplus.com/en/docs/vmp/SgLang_Integration)<br><br>* [Ray integration](https://docs.byteplus.com/en/docs/vmp/Ray_Integration)<br><br>* [etcd integration](https://docs.byteplus.com/en/docs/vmp/ETCD_integration)<br><br><br>... |
|Projects and labels can be configured for local workspaces and aggregation query workspaces. | **[Beta \- apply for trial]**  Local workspaces and aggregation query workspaces support associating projects and adding labels. This facilitates billing splitting and instance categorization among different resources. |All |* [Creating local workspaces](https://docs.byteplus.com/en/docs/vmp/Creating_a_local_workspace)<br><br>* [Creating aggregation query workspaces](https://docs.byteplus.com/en/docs/vmp/Creating_an_aggregate_query_workspace) |
|Optimized user experience with the Explore page |Optimized the metric search experience on the Explore page. The optimizations include a minimum step filter, metric preview in times series diagrams and tables, and unit configuration for chart statistics. |All |[Metric queries](https://docs.byteplus.com/en/docs/vmp/explore-metrics) |
|Status optimization of resources on workspace deletion |After a workspace is deleted, alert rules associated with the workspace are set to the Deactivated status, and integration tasks associated with the workspace are set to the Paused state. |All |[Managing workspaces](https://docs.byteplus.com/en/docs/vmp/Managing-workspaces) |

## September 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|workspace |The workspace provides public endpoints, including the query URL and the remote write URL, which allow you to write or read data in the workspace. |All |[Creating common workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces) |
|Export tasks |The workspace allows you to export data to self\-managed Prometheus instances. |All |[Exporting metrics to self-managed Prometheus](https://docs.byteplus.com/en/docs/vmp/Exporting_metrics_to_self-managed_Prometheus) |
|Integration center |When you integrate VMP with other cloud services by using Cloud Monitor, you can filter metrics by project, sub\-namespace, metric ID, or instance ID. |All |[Cloud Monitor integration](https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services) |
|Federate endpoint |When you scrape workspace time series by using the federate endpoint, you can specify a maximum time range for historical data scraping within a custom cycle. |All |[Scraping workspace time series by using the federate endpoint](https://docs.byteplus.com/en/docs/vmp/Scraping_selected_time_series_using_the_federate_endpoint) |
|SDK |OpenAPI SDKs are added, which can be used to call OpenAPIs. |All |[SDK overview](https://docs.byteplus.com/en/docs/vmp/SDK_overview) |

## June 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|workspace |The throttling feature is added for the workspace, which allows you to configure workspace\-level throttling based on Identity and Access Management (IAM) users. |All |[Throttling](https://docs.byteplus.com/en/docs/vmp/Throttling) |
|Export tasks |The workspace allows you to export data to Kafka instances to use message queues for consumption. |All |[Export tasks](https://docs.byteplus.com/en/docs/vmp/Creating_an_export_task) |
|Alert notification |The text message alert template is added to the message notification templates. Extension functions can be used to obtain the names of Vital Kubernetes Engine (VKE) clusters or the endpoint names in ModelArk. |All |* [Creating notification templates](https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template)<br><br>* [Extension functions and variables](https://docs.byteplus.com/en/docs/vmp/variable-structure-and-parameters) |
|Integration center |* Nacos integration is added, which allows you to integrate Nacos instances that are deployed in VKE clusters with VMP in the console.<br><br>* SGLang integration is added, which allows you to integrate SGLang instances that are deployed in VKE clusters with VMP in the console.<br><br>* Ray integration is added, which allows you to integrate Ray instances that are deployed in VKE clusters with VMP in the console.<br><br>* etcd integration is added, which allows you to integrate etcd instances that are deployed in VKE clusters with VMP in the console.<br><br>* Custom collection is added, which allows you to configure custom collection rules in VKE clusters in the console.<br><br>* Prometheus federation integration is added, which allows you to scrape specified time series by using the federate endpoint of a workspace to achieve data aggregation for multiple Prometheus services.<br><br>* Health inspection (blackbox) integration is added, which allows you to deploy blackbox probes in VKE clusters to perform inspection on collection targets. |All |* [Nacos integration](https://docs.byteplus.com/en/docs/vmp/Nacos_Integration)<br><br>* [SGLang integration](https://docs.byteplus.com/en/docs/vmp/SgLang_Integration)<br><br>* [Ray integration](https://docs.byteplus.com/en/docs/vmp/Ray_Integration)<br><br>* [etcd integration](https://docs.byteplus.com/en/docs/vmp/ETCD_integration)<br><br>* [Custom collection](https://docs.byteplus.com/en/docs/vmp/service-discovery)<br><br>* [Prometheus federation integration](https://docs.byteplus.com/en/docs/vmp/Federate_API_Integration)<br><br>* [Health inspection (blackbox) integration](https://docs.byteplus.com/en/docs/vmp/Blackbox_Integration) |

## May 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Integration center |Support Kafka integration in the console. VMP can monitor Kafka instances that are deployed in Vital Kubernetes Engine (VKE) clusters, Elastic Compute Service (ECS) instances, or Message Queue for Kafka instances. |All |[Kafka integration](https://docs.byteplus.com/en/docs/vmp/Kafka_Integration) |

## April 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Workspace specification |The specifications of Standard Edition workspaces are updated to provide more capabilities:<br><br><br>* New workspace specifications and packages are supported, with no additional fees being incurred.<br><br>* Workspace specifications are updated, which allows you to specify configurations such as custom active time series and QPS. |All |* [Creating common workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces)<br><br>* [Pay-as-you-go](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go)<br><br>* [Package overview](https://docs.byteplus.com/en/docs/vmp/Resource-package-overview) |
|Local workspace | **[Beta \- apply for trial]** : Local workspaces are supported. You can associate custom Prometheus instances in the VMP console. |All |* [Creating local workspaces](https://docs.byteplus.com/en/docs/vmp/Creating_a_local_workspace)<br><br>* [Associating a local workspace with a local Prometheus instance](https://docs.byteplus.com/en/docs/vmp/Associating_a_local_workspace_with_a_local_Prometheus_instance) |

## January 2025

|**Feature** |**Description** |**Regions** |**Related document** |
|---|---|---|---|
|Cloud Monitor integration |* The templates of Grafana Cloud Monitor dashboards can be obtained.<br><br>* Cloud service metrics can be queried.<br><br>* Metric relabeling can be configured. You can add or replace metric labels during metric collection. |All |* [Cloud Monitor integration](https://docs.byteplus.com/en/docs/vmp/Monitoring-cloud-services)<br><br>* [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel) |
|The maximum length of a query statement is increased. |The maximum length of a query statement is increased to 128 KB. |All |[Limits](https://docs.byteplus.com/en/docs/vmp/Limits) |
