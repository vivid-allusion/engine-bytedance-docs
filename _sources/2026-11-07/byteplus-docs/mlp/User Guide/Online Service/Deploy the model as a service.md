---
title: "Deploy the model as a service"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Deploy_the_model_as_a_service"
---

When users need to deploy the model in [Model Management] as an online service, they can create a service in the [Inference Services] module, and get the corresponding API and sample code to call the model for inference.

<span id="操作步骤"></span>
## Procedure


1. Log in to the Machine Learning Platform and click [Model Services] \- [Inference Services] in the left navigation bar to enter the list page.

2. Click [+ Create Service] at the top left of the list page to enter the creation page.

3. Fill in the relevant parameters on the creation page, the specific parameters are as follows:



|**Parameter** |**Parameter Description** |
|---|---|
|service name |* Fill in the name of the service. **Required** .<br><br>* Supports 1 to 200 visible characters, and only includes uppercase and lowercase letters, Chinese, numbers, dashes, and underscores.<br><br>* Service names can be repeated. |
|service description |* Fill in an appropriate description of the service. **Optional** .<br><br>* Supports 1 to 500 visible characters. |
|visible range |* Configure which account ranges the service can be visible in. **Optional** .<br><br>* Visible in the main account: All users under the main account can view the service and details.<br><br>* Members of the queue are visible: Users with privileges on the queue to which the service belongs can view the service and its details.<br><br>* The specified sub account is visible: Users in the specified account list have permission to view the service and details.<br><br>* Only the creator is visible: Only the service creator has permission to view the service and its details. |
|mirror |Select the mirror for the inference engine. **Required** . |
|Model |The model and version used by the service. **Optional** . |
|Entry command |Start command of mirror. **Optional.**  |
|environment variables |* Environment variables that will be injected into the container instance. **Optional** .<br><br>* Environment variables key values only support uppercase and lowercase letters, numbers, underscores, and cannot start with numbers.<br><br>* Multiple environment variables can be configured. |
|Health Check |Select whether to perform a health check on the port. The health check script can regularly detect the status of the server level port and ensure that the services provided by the port are in a normal state. **Checked by default.**  |
|Elegant closing time |Wait for a period of time before the instance goes offline to process the request that the instance has received to reduce the request error caused by the instance change, **optional** . |
|queue |Select the queue for inference services. Required. |
|calculation specification |* The computing resources that run the service. **Required** .<br><br>* Each computing specification includes a specific number of CPUs, memory, and GPUs. |
|number of instances |* Number of instances of the service. **Required** .<br><br>* Number of instances \> = 1. |
|priority |Consistent with the priority configuration of custom tasks, see [Initiate stand-alone/distributed training tasks](https://docs.byteplus.com/docs/mlp/Initiate_stand-alone_distributed_training_tasks)[ ](https://www.volcengine.com/docs/6459/72350). |
|Automatic capacity expansion and reduction |Support capacity expansion and reduction strategies based on timing or metrics, **optional** . See [Configure automatic capacity expansion and reduction for services](https://docs.byteplus.com/docs/mlp/Configure_automatic_capacity_expansion_and_reduction_for_services). |
|rolling update |* Support for configuring rolling update policies, **required** .<br><br>* Maximum unavailable: The number of instances that are unavailable during the rolling update process as a percentage of the expected number of instances. Assuming the expected number of instances is 10 and the maximum unavailability is 20%, the minimum number of instances available during the update is 8<br><br>* Maximum overrun: The percentage of the expected number of instances that exceeded expectations during rolling updates. Assuming the expected number of instances is 10 and the maximum overrun is 10%, the number of instances during the update process can reach up to 11 |
|private network |Support for configuring users' private networks, subnets, and SecurityGroups, so that users can invoke services created on the platform in a private network environment. **Optional.**  |
|Port |* Support custom listening port and calling port, **optional** .<br><br>* Listening port limit range: 1\-29999, 32768\-65535.<br><br>* Call port limit range: 1\-65535.<br><br>* Port Use: Supports only HTTP, RPC, Metrics, and Others.<br><br>   * When the port is used for Metrics, it supports additional filling in the collection path of custom indicators, and the platform will push the indicator data under this path to the VMP workspace designated by the user (you need to turn on the function of monitoring and archiving in the [global configuration] module in advance). |
|Load balancer (CLB) |* Select a load balancer, **optional** .<br><br>* Improve service availability and reliability through load balancing to meet business scenarios with high service visits.<br><br>* If you need public network access to the service, you need to select the load balancing with public IP configured. See [CLB documentation ](https://docs.byteplus.com/en/docs/clb/Product-Overview-01). |



4. After completing the configuration of the above form, click [Submit] to start deploying the service, and the model inference can be performed when the service status reaches `the running`.
