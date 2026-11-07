---
title: "GPU function resource management"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GPU_function_resource_management"
---

After the function is first released successfully, on the function details page, click **Resource Management** to view the current function's resource allocation information, instance\-level information, and perform maintenance on the function's instance resources.

<span id="resource-limits"></span>
## Resource Limits

Displays the resource limits for the current GPU function, including GPU computing power, GPU memory, memory specifications, memory resource limits, video memory resource limits, and instance number range. Among these:


* Memory resource limit = Function memory specification × Maximum number of instances

* Video memory resource limit = Function video memory specification × Maximum number of instances

* Instance number range: Consists of the minimum and maximum number of instances.

   * Minimum number of instances: or [Reserved instance](https://docs.byteplus.com/en/docs/faas/Reserved_instance). The system will maintain at least this number of instances, continuously running until you set it to 0. Reserved instances will continue to be billed during their operation; for billing details, refer to [Billing](https://docs.byteplus.com/en/docs/faas/Billing).

   * Instance Count Limit: The maximum number of instances to which a function can scale. You can adjust the resource limit of a function in real\-time by modifying its instance count limit. It is recommended that you set the instance count limit based on the business needs of the function and to also avoid excessive costs due to overcalling the function.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The instance count limit applies to the instance count of each revision. For example: If the instance count limit of a function is set to 2, then the online revision of the function can support up to 2 instances, and the canary revision can also support up to 2 instances.</div>


* <div data-tips="true" data-tips-type="tip">When there is a canary revision, adjusting the instance count limit is not supported.</div>



<span id="resource-occupancy"></span>
## Resource Occupancy

This displays the current memory usage and video memory usage of the GPU function, as well as the remaining available memory and video memory capacity of the account, helping you understand the resource usage of the current function. \nIf more resources are needed, please click to **apply for resources**.

<span id="instance-list"></span>
## Instance List

The instance list displays all the instance information of the current function, supports managing the function instances, including viewing instance logs, logging into the instance for command\-line operations, migrating instances, etc.

<span id="view-instance-logs"></span>
### **View instance logs**

Instance logs refer to the logs of standard output within the instance, including the startup logs, error logs, and business logs printed within the code of the function instance. Compared to persistent storage function logs, instance logs are more time\-sensitive and suitable for scenarios such as debugging functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After an instance is scaled down, you will not be able to view its logs. Select the target function instance, click the <strong>Log</strong> button in the <strong>Operation</strong> column to view real\-time logs of the current function instance.</div>


<span id="webshell"></span>
### **Webshell**

Webshell \*\*\*\* allows you to log in to the function instance and execute command line operations. For example: viewing the environmental information of the instance and debugging functions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please be cautious when operating after logging into an instance. Your operations may affect online requests and any impacts will not be included in the service SLA guarantees.</div>


* <div data-tips="true" data-tips-type="warning">A single connection can last for 15 minutes, after which it will automatically disconnect. If you need to use it again, please log in again.</div>


* <div data-tips="true" data-tips-type="warning">The runtime provided by veFaaS service comes pre\-installed with commonly used Webshell tools. When deploying functions through container images, be sure to package the necessary Webshell tools into the image.</div>


* <div data-tips="true" data-tips-type="warning">Only function instances that are in a running state are supported for login. If an instance is scaled down, the connection will automatically be disconnected. Select the target instance, click on the <strong>Operation</strong> column's <strong>Webshell</strong>, the page will redirect to the logged\-in instance command line page where you can execute commands as needed.</div>



<span id="migrate-instance"></span>
### **Migrate instance**

If your function instance is experiencing issues, you can launch a new instance through the instance migration feature.


1. Select the target instance, click on the **Operation** column's **Migrate**.

2. In the pop\-up confirmation box, click **Confirm**, the platform will terminate the current instance and launch a new one for you.
