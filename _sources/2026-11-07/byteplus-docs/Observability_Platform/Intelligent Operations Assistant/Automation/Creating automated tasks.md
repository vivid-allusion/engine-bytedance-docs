---
title: "Creating automated tasks"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_automated_tasks"
---

An automated task is a scheduled observability task. It is suitable for periodic scenarios such as routine inspections and resource health checks. This topic describes how to create an automated task.

## Prerequisites

* A prompt of no more than 4,000 characters has been prepared with a clearly defined task objective. Markdown syntax is recommended.

* (Optional) If a custom expert agent is used to execute tasks, it must be created in advance. For more details, see [Creating agents](https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_expert_agents).

## Procedure

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Automation**.

3. Click **Create automation**, configure the relevant information in the pop\-up window, and click **Confirm**.

   |Parameter |Description |
   |---|---|
   |Name |Specify a name for the automation. Duplicate names are not allowed. |
   |Execution Agent |Select the agent to execute the task based on the actual scenario.<br><br>> **tip**<br><br><br>> The agent used to execute the automated task must have query permissions for the resources involved. It must also have skills that match the task scenario. Insufficient permissions or missing skills prevent the agent from obtaining the necessary information, making it unable to produce accurate task conclusions.<br> |
   |Prompt |Paste or enter the prompt for task execution. |
   |Execution Time |Configure the execution cycle of the automated task, accurate to the minute. |
