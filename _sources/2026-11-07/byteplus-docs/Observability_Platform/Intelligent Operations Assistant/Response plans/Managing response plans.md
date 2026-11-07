---
title: "Managing response plans"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/manage-response-plan"
---

This topic describes the operations available for managing response plans.

## Procedure

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select **Response plan**.

3. Click an action button in the "Actions" column to the right of a response plan to perform the corresponding action.

   |Actions |Description |
   |---|---|
   |Enable/Disable |In the "Toggle" column, switch the response plan on or off.<br><br><br>* **Enable**: The response plan enters a listening state. When the trigger condition is met, the remediation Runbook is executed and a repair recommendation is provided.<br><br>* **Disable**: The response plan is disabled and cannot trigger execution. |
   |Details |Click **Details** in the "Actions" column on the right side of the plan list to view detailed information about the target response plan. The details include its configuration and execution history.<br><br>In the execution history, click "**Go to Session**" in the "Actions" column of a target record. The session shows the execution conclusion, repair recommendations, and other details. |
   |Edit |Click "**Edit**" in the "Actions" column on the right side of the plan list to modify the configuration information of the target response plan. |
   |Delete |Click "**Delete**" in the "Actions" column on the right side of the target response plan to delete the response plan if it is no longer required.<br><br>> **warning**<br><br><br>> Deleted response plans cannot be recovered. Proceed with caution.<br> |
