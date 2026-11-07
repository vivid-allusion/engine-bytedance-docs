---
title: "Updating lifecycle duration"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Modify_the_lifecycle_duration_of_a_tool_instance"
---

The lifecycle duration determines how long a sandbox instance remains active from creation until it is automatically destroyed. You can modify the lifecycle duration to extend the instance's running time (for example, when a task is not yet complete) or to shorten it (for example, to release resources early). This topic describes how to modify the lifecycle duration of a sandbox instance.

## Instructions

After an instance's lifecycle duration is modified, the instance's **automatic termination** time is reset to the **current time** plus the **newly specified lifecycle duration**. After each modification, the total lifecycle duration of the instance cannot exceed 86,400 seconds (24 hours).

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, click "Sandbox Templates". Click the target template name. On the "Instance management" tab, find the target instance and click "Modify lifecycle" in the Actions column.

3. In the dialog box, modify the lifecycle duration and click "Confirm".

4. After the modification is complete, verify that the "Auto release time" of the target instance is updated to the new duration on the **Instance management** tab.
