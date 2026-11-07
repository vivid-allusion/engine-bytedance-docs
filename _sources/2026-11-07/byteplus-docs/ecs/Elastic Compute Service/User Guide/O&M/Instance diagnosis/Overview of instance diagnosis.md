---
title: "Overview of instance diagnosis"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance_diagnosis_overview"
---

The instance self\-diagnosis feature is used to check instance performance, network statuses, volumes, and other items. This helps you timely identify and learn common issues with ECS instances to ensure the normal operation of your instance.

<span id=".5o6o6I2Q5Zy65pmv"></span>
## Recommended scenarios


|Applicable scenarios |Description |
|---|---|
|Troubleshoot the known instance issues |When encountering issues during instance usage, such as instance login failure, you may need a specific diagnosis for solutions. For such scenarios, you can use the self\-diagnosis feature. |
|Regularly and comprehensively check the health status of instances​ |During regular O&M tasks, you can use this feature to learn the overall health condition of the instance. This can help you promptly discover and troubleshoot exceptions and prevent impacts on businesses. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage notes


* If you are using the instance diagnosis service for the first time, you need to click the "Create now" button to trigger a role request. This action authorizes your account with a role (CustomRoleForDiagnose) that has read and write permissions for ECS resources. The instance diagnosis then assumes this role when accessing the cloud resources involved in your diagnosis task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you click the "Create now" button, the system automatically completes the authorization.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cross\-service access is implemented via IAM roles. The IAM role gives the current cloud service permissions to access your cloud resources, and the current service then assumes the role to access resources in other cloud services. For more information about Identity and Access Management (IAM), refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-3">IAM overview</a>.   </div>
   


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Currently, only accounts that have completed enterprise real\-name authentication can use this feature.

<span id=".5ZCN6K-N6Kej6YeK"></span>
## Terms


|Term |Description |
|---|---|
|Troubleshooting period |The duration of each collected monitoring metric of the instance, which is captured by the instance self\-diagnosis feature. |
|Diagnosis item |The specific diagnosis item (such as high disk usage and high CPU usage) checked by the instance self\-diagnosis feature within the troubleshooting period. |


<span id=".5byC5bi457G75Z6L"></span>
## Exception type

After the diagnosis is complete, the diagnosis report displays diagnosis items based on the exception type.


|Type |Description |
|---|---|
|Suggestion |Diagnosis items in this category show minor exceptions or non\-urgent information. These types of exceptions do not directly affect the stable operation or performance of ECS instances, but may indicate potential issues in the future. |
|Warning |Diagnosis items in this category may cause issues such as degraded service availability and performance, as well as abnormally quick resource consumption. These types of exceptions do not directly affect the operation stability or performance of ECS instances, but may indicate potential issues in the future. |
|Severe |Diagnosis items in this category may threaten the stable operation and data integrity of ECS instances, or have already caused service interruptions, inaccessibility, and other issues in the instance. |
