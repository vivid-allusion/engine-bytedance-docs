---
title: "Application templates"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Application-templates"
---

Application templates provided by VKE are built on the standard Kubernetes Helm template. The templates provide centralized resource management and scheduling features, which help you quickly deploy and manage Helm applications and simplify the installation and management of Kubernetes resources.

<span id=".5YWN6LSj5aOw5piO"></span>
## Disclaimer

All application templates provided by the application center in VKE are sourced from open\-source communities. Therefore, you need to take note of the following items:


* VKE provides technical support only for the process of installing and deploying these application templates in VKE clusters, and does not provide compensation or other commercial services for business losses caused by defects in open source software during use.

* You need to upgrade the software related to the installed application templates in your cluster and promptly fix defects or issues caused by open source software.

* Before you upgrade the cluster version, you need to check for the version compatibility of the software or add\-ons.


If you install related software by using application templates from the VKE application center, it indicates that you fully understand and agree to all the content described in this disclaimer.

<span id=".5bqU55So5qih5p2_5LuL57uN"></span>
## Introduction to application templates

Application templates that are provided by VKE are built on the official [Helm](https://helm.sh/) templates.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Application templates provided by the application center use the default configurations provided by the open\-source community, which may pose security risks. For example, public access is enabled by default, or password\-free login or weak passwords are used. Therefore, when you use application templates in your production environment, we recommend checking for security risks.</div>


You can perform the following steps to view detailed information for each application template:


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, select **Application center \> Application template**.

3. On the **Application template** page, find the target application template, and click the template name to view detailed information about the application template.



|Tab |Description |
|---|---|
|Overview |Displays the introduction, installation procedure, parameters, considerations, and other information about the application template. |
|Parameter configuration |Displays the detailed code of the `values.yaml` file for the application template. |


<span id=".6YOo572y5bqU55So5qih5p2_"></span>
## Deploying application templates


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Application template**. Scroll to the bottom of the page, and click **More application templates**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For instructions on using the AI cloud\-native inference service template, see <a href="https://docs.byteplus.com/en/docs/vke/AI_cloud-native_inference_suite">AI cloud\-native inference suite</a>.   </div>
   

3. On the **Application template** page, find the target application template, move the pointer over the application template section, and then click **Deploy**.

4. On the **Deploy application** page, specify the parameters based on the parameter descriptions in the following table.

   
   |Parameters |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |The selected target application template is displayed by default. You can also replace the application template. |
   |Parameter configuration |Specify a method of accessing values passed to the chart. The configuration method varies based on the `values.yaml` file of each application template. For detailed descriptions, see the annotations in the `values.yaml` file.<br><br>Click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_cf394bc8c873478efaa287daa2da8a0c.png) </span> icon to edit the `values.yaml` file. After you edit the file, click **Confirm**. |
   |Name |Specify the name of the application. The name must be unique within the same namespace. |
   |**Deployment environment** ||
   |Cluster |Select the project where the application needs to be deployed and the target cluster in the project.<br><br>The **default project** is selected by default. For more details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Namespace |Select a namespace for the target cluster. |
   |Protocol |Carefully read and understand the terms of the agreement. After you agree to the terms, select the agreement. |
   

5. Click **Confirm** to deploy the application in the target cluster.

   After the application is deployed, it will be displayed on the **Helm** page.


<span id=".566h55CG5bqU55So5qih5p2_"></span>
## Managing application templates

You can perform operations on applications that are created through application templates, such as updating, rolling back, and deleting. For detailed operations, see [Managing applications](https://docs.byteplus.com/en/docs/vke/Managing-applications).
