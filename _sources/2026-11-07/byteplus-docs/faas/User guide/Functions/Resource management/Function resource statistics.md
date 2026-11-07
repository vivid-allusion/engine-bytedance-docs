---
title: "Function resource statistics"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Function_resource_statistics"
---

FaaS allows you to set resource usage limits for each function, preventing resource contention between different functions under the same account. This is also beneficial for managing the maximum number of concurrent instances, controlling costs, and avoiding unexpected expenses. This article introduces resource statistics at the function level. After the function is first released successfully, on the function details page, click **Resource management** tab to view the resource statistics of the current function.

<span id="maximum-resource"></span>
## Maximum resource


* Memory specification: The memory specification of the function is for the online revision. You can modify the function's memory specification in the **Function Configuration** tab, but changes will only take effect after being released.

* Maximum resource limit = Maximum number of instances x Function memory specification

* Instance number range: Consists of the minimum and maximum number of instances. By clicking the edit icon, you can change the minimum and maximum instance numbers. For detailed operation refer to [Configure static reserved instances](https://docs.byteplus.com/en/docs/faas/Reserved_instance#configure-static-reserved-instances).

   * The lower limit of the number of instances, that is, the reserved instance numbers, ensures that the system will keep this minimum number of instances running continuously until you set it to 0. Reserved instances will continue to incur charges during operation. For details on billing, refer to [Billing overview](https://docs.byteplus.com/en/docs/faas/Billing_overview).

   * Instance count limit: The maximum number of instances to which a function can scale. You can adjust the resource limit of a function in real\-time by modifying its instance count limit. It is recommended that you set the instance count limit based on the business needs of the function and to also avoid excessive costs due to overcalling the function.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The instance count limit applies to the instance count of each revision. For example: If the instance count limit of a function is set to 2, then the online revision of the function can support up to 2 instances, and the canary revision can also support up to 2 instances.</div>


* <div data-tips="true" data-tips-type="tip">When there is a canary revision, adjusting the instance count limit is not supported.</div>



<span id="usage-ratio"></span>
## Usage ratio

**Usage ratio** display the maximum resource size for the current function, the remaining usable resources of the account, and the proportion of the resources used by the current function to the account’s total resources. For example: The above figure shows that the current function's resource usage is 0.05% of the account's resources.

<span id="scheduled-policy"></span>
## Scheduled policy

When your functions exhibit noticeable periodic patterns or predictable traffic peaks, you can configure a scheduled policy based on business characteristics, allowing dynamic scaling of instance numbers to improve utilization and reduce resource waste. Once the scheduled policy is configured, the number of instances will dynamically scale according to the policy, and the names of the generated reserved instances will contain a `reserved` identifier. For instructions on creating a scheduled scaling policy, refer to [reserved policy](https://docs.byteplus.com/en/docs/faas/Reserved_instance).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For microservices applications, it supports configuration of elastic scaling policies. You can select suitable policies and metrics, set elastic target values, and combine them with your business scenario to achieve a balance between resource costs and stability. For how to configure elastic policies for microservices applications, refer to <a href="https://docs.byteplus.com/en/docs/faas/Elastic_scaling">Auto\-scaling</a>.</div>


<span id="instance-list"></span>
## Instance List

The instance list displays information about the instances occupied by each online version of the current function, including instance name, status, startup time, instance logs, and Webshell, helping you understand function instance\-level information.


* **Instance logs**

   Instance logs include standard output log content such as the startup logs, error logs, and business logs printed within the function instance. Compared to persistent storage TLS logs, function instance logs are more time\-sensitive and suitable for debugging functions and similar scenarios. After an instance is scaled down, you will not be able to view its logs.

   Select the target function instance, click the **Log** button in the **Actions** column to view the logs at the function instance level.

   * Supports enabling the auto\-refresh button for real\-time log loading.

   * Supports switching of log themes.

   * Supports searching by entering keywords.

* **Webshell**

   Through Webshell, you can log in to the function instance and perform corresponding command line operations. For example: viewing the environmental information of the instance and debugging functions.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Exercise caution when operating after logging into an instance. Your operations may affect online requests and any impacts will not be included in the service SLA guarantees.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A single connection can last for 15 minutes, after which it will automatically disconnect. If you need to use it again, please log in again.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The runtime provided by FaaS service comes pre\-installed with commonly used Webshell tools. If you are using a custom image to submit your business, be sure to pack the required Webshell tools into the image as well.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only function instances that are in a running state are supported for login. If an instance is scaled down, the connection will automatically be disconnected.   </div>
   

   Select the target instance, click the **Webshell** button in the **Actions** column, to log in to the instance. You can perform the necessary command\-line operations as needed.

* **Migrate instance**When the instance is abnormal, you can choose to migrate the instance. After the migration, the old instance will be terminated and a new instance will be restarted. Select the target instance, click **Migrate** in the **Actions** column, and confirm the operation to start the migration. When the instance status changes from `Starting` to `Ready`, it indicates that the migration is complete.
