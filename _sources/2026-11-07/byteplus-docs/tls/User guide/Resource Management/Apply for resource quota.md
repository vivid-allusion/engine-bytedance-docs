---
title: "Apply for resource quota"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Apply_for_resource_quota"
---

Torch log service (TLS) grants each BytePlus account a certain amount of service resources by default. If you need to create more resources, apply to increase quota in the quota center. This topic describes how to apply for a resource quota.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Each BytePlus account has a default quota for TLS resources. For example, you can create up to 50 dashboards. If the default quota does not meet your business needs, you can apply to increase quota in quota center. You can specify parameters like region and quota. The backend service will automatically initiate a quota application process. Once your quota request is submitted, the operation and maintenance team will handle it as soon as possible.

Resource quota parameters that can be configured are as follows:


|Quota parameters |Description |Default value |Maximum value |
|---|---|---|---|
|total_split_shards_per_topic |The maximum number of shards that is achieved by splitting shards after creating a log topic |50 |256 |
|total_shards_per_topic |Maximum initial number of shards when creating a log topic |10 |100 |
|total_machine_groups_per_region |The number of host groups that can be created in the current region |200 |200 |
|total_consumer_group_count_per_project |The number of consumer groups that can be created in each project. |150 |150 |
|total_dashboard_count_per_project |The number of dashboards that can be created in each project |50 |100 |
|total_dashboard_subscription_count_per_project |The number of dashboard subscription tasks that can be created in each project |100 |200 |
|total_alarm_policy_per_topic |The number of alarm policies that can be created per log topic |10 |20 |
|total_alarm_policy_per_project |The number of alarm policies that can be created in each project |100 |200 |
|total_etl_tasks_per_project |The number of transformation tasks that can be created in each project |100 |150 |
|total_etl_tasks_per_topic |The number of transformation tasks that can be created per log topic |30 |45 |
|total_output_topics_per_task |The number of log topics that can be output by each transformation task |20 |30 |
|total_topics_per_project |The number of topics that can be created for each project. |200 |500 |
|total_projects_per_account |The number of projects that can be created in the current region |100 |300 |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [BytePlus Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=TLS) and select TLS.

2. Locate the required quota parameter and select the correct region

3. Click **Apply** in the **Actions** column.

4. Confirm the applicant, set the expected parameter thresholds. Set the expected parameter thresholds based on actual business needs and provide with an application reason. A detailed and comprehensive application reason will help shorten the approval process.

5. Click **Submit**.
