---
title: "Cluster diagnosis overview"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Cluster_Diagnosis_Overview"
---

Cluster diagnosis is a diagnostic tool for high\-performance computing (HPC) clusters. It offers comprehensive diagnostic items for HPC\-optimized instances, including system status, hardware health, applications, performance, and network. This helps you timely identify and understand common issues with instances to ensure the normal operation of your instance.

<span id=".5o6o6I2Q5Zy65pmv"></span>
## Recommended scenarios

You can use the cluster diagnosis feature in the following scenarios to learn the health status of instances.


|Applicable scenarios |Description |
|---|---|
|Troubleshoot the known instance issues |When issues occur during instance usage, such as network access failure, you may need a specific diagnosis for solutions. For such scenarios, you can use this feature. |
|Regularly and comprehensively check the health status of instances​ |During regular O&M tasks, you can use this feature to learn the overall health condition of the instance. This can help you promptly discover and troubleshoot exceptions and prevent impacts on businesses. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* RIs for HPC\-optimized instances are currently only available to accounts that have completed enterprise real\-name authentication. 

* Currently, this feature is only available for Linux instances in the **Running** state.

* Instances to be diagnosed need to have the [cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) installed.


<span id=".5byC5bi457G75Z6L"></span>
## Exception type

After the diagnosis is complete, the diagnosis report displays diagnosis items based on the exception type.


|Type |Description |
|---|---|
|Suggestion |Diagnosis items in this category show minor exceptions or non\-urgent information. These types of exceptions do not directly affect the stable operation or performance of ECS instances, but may indicate potential issues in the future. |
|Warning |Diagnosis items in this category may cause issues such as degraded service availability and performance, as well as abnormally quick resource consumption. These exceptions do not directly affect the operation stability or performance of ECS instances, but may indicate potential issues in the future. |
|Severe |Diagnosis items in this category may threaten the stable operation and data integrity of ECS instances, or have already caused service interruptions, inaccessibility, and other issues in the instance. |
