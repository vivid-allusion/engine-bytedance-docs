---
title: "Dashboard overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Dashboard_overview"
---

FaaS connects to [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor), providing the feature of observing function performance metrics. After the function code is executed by the target trigger, on the function detail page, click **Monitoring**, select the monitoring time range to view the current function's performance monitoring metrics, helping you understand if the function's operational status meets expectations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Click <strong>View more metrics</strong> to jump to the cloud monitoring console and view the current function's monitoring dashboard.</div>


* <div data-tips="true" data-tips-type="tip">Click <strong>Create alert policy</strong> to navigate to the cloud monitoring console where you can configure an alert policy for the current function. When metrics reach the trigger conditions for an alert, the system will push notifications through your specified method to help you promptly discover anomalies in the service. For specific operations, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a>.</div>



<span id="basic-metrics"></span>
## Basic metrics

<span id="function-execution-qps"></span>
### Function Execution QPS

Displays the number of times each version of the function is triggered per second during the current sampling period. For example: The graph above shows the fluctuation curve of the number of times version 1 of the function is triggered per second in the last hour.

<span id="function-execution-latency"></span>
### Function execution latency

Display the processing time of function requests across different versions during the current sampling period.


* **P99**: Represents the execution duration of requests at the 99% position in ascending order during the specified sampling period.

* **P90**: Represents the execution duration of requests at the 90% position in ascending order during the specified sampling period.

* **P50**: Represents the execution duration of requests at the 50% position in ascending order during the specified sampling period.

* **Avg**: Represents the average execution duration of all requests during the specified sampling period.


<span id="function-error-qps"></span>
### Function Error QPS

Display the QPS of various execution errors by different versions of functions during the current sampling period. Errors are classified into two types: internal and user.


* Internal: System internal error. [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

* user: User error. Further investigation is required based on the specific error code.


<span id="outbound-traffic-for-functions"></span>
### Outbound traffic for functions

Displays the usage of outbound traffic by the function during the current sampling period.

<span id="cpu-usage-for-functions"></span>
### CPU Usage for functions

Displays the CPU usage of various versions of functions during the current sampling period. Average the usage rates across all instances under each version.

<span id="memory-usage-for-functions"></span>
### Memory usage for functions

Displays the memory usage of various versions of functions during the current sampling period. Average the usage rates across all instances under each version. Wherein, the memory usage = the actual memory consumed / the maximum allowed memory.

<span id="number-of-function-instances"></span>
### Number of function instances

Displays the number of instances occupied by various versions of functions during the current sampling period.

<span id="gpu-metrics"></span>
## GPU metrics

For GPU functions, in addition to the basic metrics mentioned above, the following GPU monitoring metrics are also provided.

<span id="gpu-memory-usage-for-functions"></span>
### GPU memory usage for functions

Displays the GPU memory usage of various versions of GPU functions during the current sampling period. Average single\-card GPU memory usage across all instances in each version.

<span id="function-gpu-memory-usage"></span>
### Function GPU memory usage

Displays the memory usage of GPU functions across versions during the current sampling period. Average single\-card GPU memory usage rate across all instances in each version. Wherein, memory usage rate = memory usage / total single\-card memory.

<span id="function-gpu-usage-rate"></span>
### Function GPU usage rate

Displays the usage rate of the GPU cores for functions across versions during the current sampling period. Average usage rate of single\-card GPU cores across all instances in each version.
