---
title: "Creating Helm applications"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-Helm-application"
---

Helm is a packaging tool for managing Kubernetes applications. VKE provides centralized resource management and scheduling features by using templates that comply with the Kubernetes Helm standard. This topic mainly describes how to create a Helm application.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

VKE provides three methods of creating a Helm application. You can select an appropriate method based on your business requirements:


* Create a Helm application by using an application template provided by VKE.

* Create a Helm application by using a Helm chart from CR.

* Create a Helm application by using a Helm chart from a third party.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A namespace has been created in the cluster. For detailed operations, see [Creating namespaces](https://docs.byteplus.com/en/docs/vke/Creating-a-namespace).

* To create a Helm application by using a Helm chart from CR, make sure that the Helm chart has been managed in a Standard Edition CR instance. For detailed operations, see [Pushing and pulling charts](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Helm**.

3. On the **Helm** page, click **Create Helm**.

4. On the **Create Helm** page, specify the parameters based on the parameter descriptions in the following table.

   
   |Parameter ||Description |
   |---|---|---|
   |**Orchestration template** |||
   |Chart source |Application template |Use an [application template](https://docs.byteplus.com/en/docs/vke/Application-templates) provided by VKE as the source of the chart file.<br><br>You need to specify the following parameters:<br><br><br>* **Application template**: Select the Helm chart and version that correspond to the target development environment from the templates provided by VKE based on your business requirements.<br><br>* **Parameter configuration**: Specify the method of accessing the values passed to the chart. You need to implement this method and ensure that the method works. Click the edit icon to edit the `values.yaml` file. After you edit the file, click **Confirm**.<br><br>* **Name**: Specify the name of the Helm application. The name must be unique within the same namespace.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When you create a Helm application, a fixed prefix will be automatically added to the resources associated with the Helm application. The resource name is in the format of <code>application name-resource name</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For NGINX applications, a switch is added to control whether a prefix is automatically added to the IngressClass name. You can specify this option by using the <code>ResourceNamePreEnable</code> parameter of <code>values.yaml</code> based on your business requirements.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>true</strong>: Automatically adds a prefix. This value is used by default. Add the application name <code>.Release.Name</code> as a prefix to the resource name to ensure that it is unique within the cluster.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>false</strong>: Does not automatically add a prefix. When you deploy multiple Nginx Ingress controllers in a cluster, you need to make sure that the resource name is unique. Otherwise, the normal operation of Nginx Ingress controllers will be affected.</div><br> |
   ||Container Registry |Use the Helm chart file from the specified CR instance as the source.<br><br>You need to specify the following parameters:<br><br><br>* **Container Registry instance**: Select the target standard CR instance that hosts the Helm chart.<br><br>* **Repository namespace**: Select the namespace of the standard CR instance.<br><br>* **Chart**: Select the Helm chart and version that correspond to the target development environment from the CR namespace.<br><br>* **Parameter configuration**: If you set the Chart source parameter to **Container Registry**, the `values.yaml` file is empty. After you create the Helm application, the system automatically generates the **parameter configuration** based on the selected chart source of the CR type. No configuration is required.<br><br>* **Name**: Specify the name of the Helm application. The name must be unique within the same namespace. |
   ||Third party |Use the Helm chart file from a third\-party repository as the source.<br><br>You need to specify the following parameters:<br><br><br>* **Chart**: Select the Helm chart and version that correspond to the target development environment from the templates provided by VKE based on your business requirements.<br><br>* **Authentication method**: Specify whether authentication is required when you access the chart from a third\-party repository. The following two authentication methods are supported:<br><br>   * **None**: No authentication is required.<br><br>   * **Basic**: Enable HTTP basic authentication. You need to specify the username and password for basic authentication as the access credentials for the third\-party repository.<br><br>* **Parameter configuration**: If you set the Chart source parameter to **Third party**, the `values.yaml` file is empty. After you create the Helm application, the system automatically generates the **parameter configuration** based on the configured third\-party chart source. No configuration is required.<br><br>* **Name**: Specify the name of the Helm application. The name must be unique within the same namespace. |
   |**Deployment environment** |||
   |Cluster type ||You can use a managed VKE cluster or a registered cluster as the target cluster for deploying the Helm application. |
   |cluster ||Select the project where the application needs to be deployed and the target cluster in the project.<br><br>The **default project** is used by default. For more details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Namespace ||Select a namespace for the target cluster. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Protocol ||This parameter is displayed when the **Chart source** parameter is set to **Application template**. Carefully read and understand the terms of the agreement. After you agree to the terms, select the agreement. |
   

5. Click **Confirm**.

   After you create the application, you can view all Helm applications that you have created on the **Helm** page.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

[Managing applications](https://docs.byteplus.com/en/docs/vke/Managing-applications)
