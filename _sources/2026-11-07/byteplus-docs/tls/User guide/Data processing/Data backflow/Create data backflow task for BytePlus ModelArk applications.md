---
title: "Create data backflow task for BytePlus ModelArk applications"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Manage_data_backflow_tasks"
---

The data backflow task will automatically create a scheduled SQL task and a log delivery task (with the target type set to deliver to TOS), helping you export logs that meet the requirements.

This section describes how to create a data backflow task for ModelArk applications.

<span id="8db52104"></span>
## Prerequisites


* The target project and log topic have been created, and the index has been configured.

* If the target is set to deliver to TOS, the following conditions must also be met:

   * Object Storage has been enabled, and a bucket has been created in the same region as the specified log topic. For detailed instructions, see [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

   * TLS needs to assume the ServiceRoleForTLS role to access other cloud service resources across services. That is, you need to grant TLS permission to access and write to TOS resources.

      If you have not yet created the ServiceRoleForTLS role, TLS will guide you through the process when you create the delivery configuration. It is recommended to use your BytePlus account for authorization. For related instructions, see [cross-service access authorization](https://docs.byteplus.com/en/docs/tls/Authorizing_cross-service_access).


<span id="2737de19"></span>
## Steps

<span id="184b066a"></span>
### 1. Create a ModelArk application

Create a ModelArk application that meets the following requirements and deploy a function. 


* Region: The ModelArk application and TLS must be in the same region.

* Enable Trace feature: When deploying a function in the ModelArk application, ensure that the **TLS\-Trace** feature is enabled.


Example:


* Deploy a function named `ark-bot-procode-176**-function` in the ModelArk application.

* The following resources will be automatically created in TLS:

   
   |TLS resources |Example value |Description |
   |---|---|---|
   |Trace instance |`ark-bot-procode-176**-function` |Trace instance name, used to manage collected Trace data. |
   |Project to which the Trace instance belongs |`ark-bot-procode-496**` |Project name, used to store data related to the Trace instance. |
   |Trace instance data storage topic |`vefaas_ark_ark-bot-procode-176**-function-trace` |Log topic name, used to store collected raw Trace data. |
   |Trace instance dependency topic |`vefaas_ark_ark-bot-procode-176**-function-dependency` |Dependency log topic name, used to store topological relationship data extracted and aggregated from the raw Trace data. |
   


<span id="411a01d4"></span>
### 2. Create a data backflow task


1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Log application \>**   **Trace storage**.

4. Click the Trace instance of ModelArk  application **Trace instance** to enter the instance list page.

5. Click the corresponding Trace instance name to enter the **Request list** page.

6. Click **Create data backflow task**. The data source will be automatically configured as the data storage topic for this Trace instance. For other parameters, refer to [Create data backflow task](https://docs.byteplus.com/en/docs/tls/Create_data_backflow_task).

7. After completing the parameter configuration, click **Create data backflow task**.
