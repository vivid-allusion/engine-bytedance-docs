---
title: "Account resource statistics (including GPU)"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Account_resource_statistics"
---

VeFaaS supports viewing the quota allocation of each BytePlus account in the target region, allowing you to understand the resource usage proportions of different functions and allocate resources under the account rationally. This article introduces the quota allocation and statistical information at the account level when GPU instances are involved.

Log in to the [Function Service console](https://console.byteplus.com/vefaas), select the region where your business is located, and from the left navigation menu select **Quota** to view the current account's resource allocation in the target region.

<span id="quota"></span>
## Quota

**Resource Allocation** area displays critical data indicators, resource usage statistical pie charts, and a bar chart of the top 5 memory resource usage by functions.


* Total Memory Resources: Displays the overall memory resources for the current account in a single region, including memory resources within GPU instances.

* Total Display Memory Resources: Displays the overall display memory resources for the current account in a single region.

* Released functions: Counts the number of online functions.

* Resource Usage Pie Chart: Displays the proportion of allocated resources versus available resources.

   * Total memory = Allocated resources + Available resources

   * Allocated resources = Total upper memory resources of all released functions under the current account.

   * The upper memory resource of each released function = Instance memory specification \* Maximum number of instances

* Top 5 Function Memory Usage Bar Chart: Displays the top 5 functions with the most memory resources among released functions.


<span id="usage-ratio"></span>
## Usage ratio

**Usage Ratio** area displays the current account's memory usage, GPU usage, and function release rate. Memory usage = Allocated memory resources / Total memory. GPU usage = Allocated GPU resources / Total GPU resources. Function release rate = Released functions / Total functions. If more resources are needed, **click** to apply.

<span id="allocation-details"></span>
## Allocation details

Allocation details displays resource allocation information and latest usage status of all released functions in table format, including function status, memory specification, GPU specification, instance range, upper memory resources, upper GPU resources, memory usage ratio, and GPU usage ratio. Click the function name to jump to the **resource management** page, where you can view or adjust the function's resources. For detailed information, refer to [GPU function resource management](https://docs.byteplus.com/en/docs/faas/GPU_function_resource_management).
