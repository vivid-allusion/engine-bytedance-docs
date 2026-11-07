---
title: "Managing and using AI applications"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing_and_using_AI_applications"
---

After creating an AI application by using an AI application template, you can view, edit, and use the application. This topic mainly describes management operations on AI applications created through AI application templates.

<span id="r7vBvMp5"></span>
## Manage an AI application


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **ServingKit \> List of AI applications**.

3. On the **List of AI applications** page, find the target application, hover the pointer over the application module, and then click `...` to manage it.

   
   |Operation |Description |
   |---|---|
   |Update |Update the configuration of the AI application. For parameter descriptions, see **Procedure**. |
   |Copy |Copy all configurations of the current AI application to quickly create an AI application. |
   |Upgrade |When a version of the AI application template is available for upgrade, we recommend that you upgrade the application to ensure the normal use of related features. |
   |Scaling |Specify the number of replicas for the current application based on your business requirements, which is the number of instances. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <strong>Number of replicas</strong> parameter indicates the desired total number of replicas, not the number of replicas to be added. For example, the application has three replicas before scale\-out. If you set the <strong>Number of replicas</strong> parameter to 5, the system will automatically add two replicas instead of five replicas to ensure that the application has five replicas.</div><br> |
   |Delete |Check the prompted information about the application to be deleted and associated resources again, and then delete the AI application.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">After you delete the application, it cannot be restored. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This operation will also delete the autoscaling rules associated with the application.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you delete the application, resources that are related to the application will not be deleted, such as VKE clusters, node pools, APIG instances, VMP workspaces, and EIC instances. To delete the related resources, go to the corresponding service console and manually delete the resources based on the on\-screen prompts.</div><br> |
   


<span id="EApV6nX8"></span>
## Use an AI application


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation pane, click **ServingKit \> List of AI applications**.

3. On the **List of AI applications** page, find the target AI application, hover the pointer over the application module, and then click  **→**  to go to the application details page. On this page, you can view, edit, and use the application.

   
   <Tabs>
   <Tab zoneid="Cmh3czEoss" title="Service overview">
   <TabTitle>Service overview</TabTitle>
   
   
   |Module |Description |
   |---|---|
   |Service configuration |If an APIG instance has been associated, the configuration information of the associated service is displayed. Pay special attention to the following items:<br><br><br>* **Edit**: You can update the associated APIG instance or disable APIG.<br><br>* **Service domain names**: the domain name that is used to access the backend service of the model application. You can access the AI application by using the domain. |
   |Service specifications |The instance information of the AI application. Click buttons in the **Actions** column for the instance to view or manage the corresponding pod. For pod operation details, see [Viewing pod information](https://docs.byteplus.com/en/docs/vke/Viewing-pod-details).<br><br>The instances displayed for applications with PD disaggregation architecture and PD co\-location architecture are different. For details, see [PD disaggregation architecture](https://docs.byteplus.com/en/docs/vke/Servingkit_overview#FRfrxPHf). |
   |Overview |Displays basic information about the AI application, such as its model series, framework, orchestration, and deployment environment. |
   
   
   
   </Tab>
   <Tab zoneid="HKQynnLJRG" title="Application configuration">
   <TabTitle>Application configuration</TabTitle>
   
   Displays configuration information of the AI application, such as the framework, orchestration, deployment environment, and service. To update the application configuration, click **Update**. For details, see **Managing the AI application**.
   
   
   </Tab>
   <Tab zoneid="LbBCvhLrHh" title="Autoscaler">
   <TabTitle>Autoscaler</TabTitle>
   
   <span id="2sFwWroQ"></span>
   ### CronHPA rules
   
   You can configure a CronHPA policy together with the [elastic scheduled scale-out](https://docs.byteplus.com/en/docs/vke/Elastic_scheduled_scale-out) feature for an AI application. In this way, you can execute specified scaling rules at specified time points to automatically scale out or scale in computing resources. This meets your business requirements and controls costs.
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   
   * <div data-tips="true" data-tips-type="warning">CronHPA rules depend on the cronhpa add\-on in the cluster of the application. Make sure that the add\-on is installed and its version is v1.0.16 or later. For information about the add\-on, see <a href="https://docs.byteplus.com/en/docs/vke/cronhpa">cronhpa</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="warning">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features">Beta \- apply for trial</a>]: The v1.0.16 version of the cronhpa add\-on is in beta. To use it, you need to apply for a trial.</div>
   
   
   * Add CronHPA rules
   
      Click **Add CronHPA rule**. In the **Create CronHPA rule** dialog box, specify related parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Name |Specify a custom name for the CronHPA rule based on the on\-screen prompt. |
      |Scaling object |Configure the target that needs scaling. Select the scaling target from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can configure only one CronHPA rule for each scaling object.</div><br> |
      |Policy configuration |* **Repeat regularly**: You can start scaling as scheduled by hours, days, weeks, or months, or by using Cron expressions. For information about how to configure it by using a Cron expression, see [Cron](https://docs.byteplus.com/en/docs/vke/Cron-expressions).<br><br>* **Split ratio**: Scaling objects are automatically adjusted to the specified value at the scheduled time.<br><br>* **Actions**: You can delete a scheduled policy that has been filled in.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you create a CronHPA, at least one policy is required. When there is only one policy, the <strong>Delete</strong> button is disabled.   </div><br>   <br><br>* **Add**: You can add a policy. Ensure that multiple policies do not conflict with each other. |
      
   
   * Manage CronHPA rules
   
      After the rule is created, click an operation name in the **Actions** column to perform the corresponding operation on the rule.
   
      
      |Action |Description |
      |---|---|
      |Update |Update an existing CronHPA rule to make it better meet your business requirements. After modification, the CronHPA rule takes effect based on the new configuration. |
      |Delete |Delete an existing CronHPA rule. |
      
   
   
   <span id="wwB35UVP"></span>
   ### HPA rules
   
   Configure the metrics used for scaling to elastically scale out or scale in computing resources based on these monitoring metrics.
   
   
   * Add autoscaler rules
   
      Click **Add autoscaler rule**. In the **Create autoscaler rule** dialog box, specify related parameters.
   
      
      |Parameter |Description |
      |---|---|
      |Name |Specify a custom name for the HPA rule based on the on\-screen prompt. |
      |Scaling object |Configure the target that needs scaling. Select the scaling target from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can configure only one HPA rule for each scaling object.</div><br> |
      |Instance count range |Specify the minimum and maximum number of instances for the autoscaler of the AI application. When the policy is triggered, the scaling target will scale within this range. |
      |Monitoring metrics |The monitoring metrics for AI application autoscaling. The system determines whether scaling is required based on these metrics. The following metrics are supported in ServingKit:<br><br><br>* **GPU usage**: The average GPU usage across all instances of the AI application. When GPU usage reaches this value, scaling is triggered.<br><br>* **GPU memory usage**: The percentage of the total usage of GPU video memory shared by all instances of the AI application to the total GPU video memory requests shared by all instances. When the GPU memory usage reaches this specified value, scaling is triggered.<br><br>* **Time to first token (TTFT)** : The average time taken from receiving an inference request to returning the first token across all instances of the AI application. Scaling is triggered when the first TTFT reaches this value.<br><br>* **Time per output token (TPOT)** : The average time taken to generate each token after the first token is generated across all instances of the AI application. Scaling is triggered when the TPOT reaches this value.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In addition to the preceding preset metrics, ServingKit allows you to use custom metrics for autoscaling monitoring of AI applications. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling">Achieving autoscaling by using custom metrics</a>.</div><br> |
      |Scale\-out observation period |You can configure a stabilization window for scale\-out or scale\-in. After a scaling action is performed, no further scaling actions will be triggered during this stabilization window, preventing frequent instance count fluctuations that could cause system oscillations. |
      |Scale\-in observation period ||
      
   
   * Manage autoscaler rules
   
      After the rule is created, click an operation name in the **Actions** column to perform the corresponding operation on the rule.
   
      
      |Action |Description |
      |---|---|
      |Scaling record |Display the latest five scaling records for the current rule. You can analyze the resource usage of the AI application based on the scaling records and adjust the HPA rules as needed. |
      |Update |Update an existing HorizontalPodAutoscaler (HPA) rule to make it better meet your business requirements. After modification, the HPA rule takes effect based on the new configuration. |
      |Delete |Delete an existing HPA rule. |
      
   
   
   </Tab>
   <Tab zoneid="ZaPyewqhv0" title="Observability">
   <TabTitle>Observability</TabTitle>
   
   ServingKit provides basic observability and in\-depth observability capabilities for AI applications. Basic observability provides the metrics for AI resources and inference services. Deep observability provides end\-to\-end performance monitoring services for inference applications.
   
   
   * **Basic observability**
   
      ServingKit provides basic observability for AI applications by using VMP. If **Observability configuration** is enabled for the heterogeneous computing managed cluster associated with the AI application, the current tab will display the preset monitoring dashboard for the AI application, including metrics such as token\-related data, cache hit rate, and running queue data. If basic observability is not enabled when the cluster is created, follow the prompts on the current tab to enable VMP observability. For more information, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability).
   
   * **Deep observability**
   
      ServingKit provides in\-depth observability for AI applications by using APMPlus. In the upper\-right corner of the tab, click **Enable APM deep monitoring**. In the message that appears, confirm the billing description and workspace information, and then click **Confirm** to enable in\-depth observability. After it is enabled, the **Enter APM deep monitoring** button will be displayed. Click it to go to the [Observability Platform](https://console.byteplus.com/observe/apmplus-server) to view monitoring information of the AI application, such as the global service topology, service overview, and instance analysis. For more descriptions, see [Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring).
   
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   
   * <div data-tips="true" data-tips-type="warning">You can enable in\-depth observability only for AI applications that are deployed through preset images (starting with <code>ai-container-**</code>).</div>
   
   
   * <div data-tips="true" data-tips-type="warning">To enable in\-depth observability, the apmplus\-opentelemetry\-collector add\-on v3.0.2 or later must be installed in the cluster. If the add\-on is not installed or its version does not meet requirements, follow the on\-screen prompts to install or upgrade it. For details, see <a href="https://docs.byteplus.com/en/docs/vke/apmplus-opentelemetry-collector-add-on">apmplus\-opentelemetry\-collector</a>.</div>
   
   
   * <div data-tips="true" data-tips-type="warning">For information about how to specify custom dashboard statistics, see <a href="https://docs.byteplus.com/en/docs/vke/AI_application_observability">AI application observability</a>.</div>
   
   
   
   </Tab>
   </Tabs>
