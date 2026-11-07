---
title: "Account resource statistics"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/FaaS_account_resource_statistics"
---

FaaS supports viewing the quota allocation of each BytePlus account in the target region, allowing you to understand the resource usage proportions of different functions and allocate resources under the account rationally. This article introduces the resource allocation statistics at the account level. Log in to the [Function Service console](https://console.byteplus.com/vefaas), select the region where your business is located, and from the left navigation menu select **Quota** to view the current account's resource allocation in the target region.

<span id="resource-statistics"></span>
## Resource statistics

**Resource statistics** area displays critical data indicators, resource usage statistical pie charts, and a bar chart of the top 5 function resource usage.


* Total account resources: Each account has a default total resource of 1024000 MB in a single region. If more resources are needed, [submit a ticket](https://console.byteplus.com/workorder/create) to apply.

* Available resources: Available resources = Total account resources \- Allocated resources.

* Allocated resources: Allocated resources = Total of the upper limit resources assigned to all online functions.

* Released functions: Counts the number of online functions.

* Resource Usage Pie Chart: Displays the proportion of allocated resources versus available resources.

* Top 5 Function Resource Usage Bar Chart: Displays the top 5 functions that use the most resources.


<span id="function-resource-allocation"></span>
## Function resource allocation

The function resource allocation list shows the current resource allocation rules for all online functions, including the function's status, memory specifications, instance range, resource cap, and resource usage percentage.


* Click the function name to navigate to the **Resource management** page, where you can view or adjust the function's resources. For more information, refer to [Function resource statistics](https://docs.byteplus.com/en/docs/faas/Function_resource_statistics).
