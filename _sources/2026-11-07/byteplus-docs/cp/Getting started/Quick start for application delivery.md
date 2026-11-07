---
title: "Quick start for application delivery"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Quick_start_for_application_delivery"
---

This document uses the example of deploying a Kubernetes YAML application in a development environment to introduce the basic capabilities and workflow of application delivery, helping you quickly get started with application delivery.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

The application delivery feature is centered on applications and provides one\-stop capabilities for application orchestration, environment management, configuration management, and application release. This helps simplify the complexity of deploying microservices in cloud\-native scenarios, improves application delivery efficiency, and reduces release risks.


1. **Application initialization**: Including application creation, environment configuration, and application orchestration. After initialization is complete, the application is essentially ready for deployment.

   1. Create application: Select the type of application to create, and complete the application's basic information.

   2. Environment configuration: An environment provides the platform for running an application. Pre\-configure at least one environment instance for the application and associate it with a deploy resource, so that subsequent application orchestration records can take effect in that environment.

   3. Application orchestration: Orchestrate YAML description files for applications to ensure that the deployed applications behave as expected.

2. **Deploy an application**: Use the immediate deployment feature to deploy the application to the target environment.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Apart from [preparatory work](https://docs.byteplus.com/en/docs/cp/Preparations), you also need to complete the following actions:


* Workspace has been created. For specific actions, see [Create workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

* The images to be deployed are ready.


<span id=".5q2l6aqk5LiA77ya5bqU55So5Yid5aeL5YyW"></span>
## Step 1: Application initialization

Application initialization includes application creation, environment configuration, and application orchestration. After initialization is complete, the application is essentially ready for deployment.

<span id=".XzEt5Yib5bu65bqU55So"></span>
### 1. Create an application

Create an independently deliverable unit that provides services externally


1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the workspace area of the Overview page, select the target workspace name to enter that workspace.

3. On the current workspace page, select **Application Delivery \> Application Management** in the left navigation bar, and click **Create Application**.

4. On the create application page, enter the required application configuration information.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Application type |Select **K8s YAML application**. |
   |Application ID |Enter the Application ID as prompted by the interface. The Application ID is the unique identifier for an application and cannot be changed after creation. The value of the predefined appName placeholder in the application orchestration YAML file will be set to the Application ID you provide. This example is `k8s-1218-w`. |
   |Application name |Display name for custom application This example is `k8s-1218-w`. |
   |Description |Enter remarks for the current application. This field can be left blank. |
   |Member management |Easily configure the members of the current application and assign different permissions to each member to meet the needs of collaborative application delivery by multiple roles.<br><br>The BytePlus account and the creator are administrators of the application by default. No members are added in this example. |
   |Deployment methods |Currently, only **predefined K8s YAML deployment** is supported, that is, applications are deployed using a K8s YAML file. |
   

5. Keep the checkbox selected to continue initializing the application process, click **OK**, and proceed to the next **Environment configuration** page.


<span id=".XzIt546v5aKD6YWN572u"></span>
### 2. Environment configuration

The environment is the platform for running the application. Create an environment instance for the current application and associate it with deployment resources.


1. On the Environment configuration page, configure environment information as required. Supports adding multiple environments as needed.

   
   |Configuration Item |Descriptions |
   |---|---|
   |environment |* Environment level: Click the dropdown and select the environment type to configure. The currently supported environment types are development, testing, staging, and production. This example is for **development**.<br><br>* Environment name: Custom environment name. This example uses **development environment 1**. |
   |Environment ID |Enter the Environment ID as indicated on the interface. The Environment ID is the unique identifier for the environment and cannot be changed once created. The value of the predefined placeholder envName in the application orchestration YAML file will use the Environment ID you provide. This example is `dev1`. |
   |deploy resource |Associate a deployment resource with the current environment. Select the BytePlus container service cluster that was prepared in the prerequisites `deploycluster` here. |
   |Namespace |Optional. After you enter a value, the Namespace name entered here will override the Namespace defined in the YAML. If the Namespace does not exist in the target cluster, it will be created during deployment. Leave this example blank. |
   

2. Keep the checkbox selected to continue initializing the application process, then click **confirm** to go to the **application orchestration** page.


<span id=".XzMt5bqU55So57yW5o6S"></span>
### Application orchestration

Orchestrate the YAML description files for each resource of the application. The system provides template files for Deployment, Service, and Configmap. In each template, every parameter's value is represented by a placeholder, and each placeholder is pre\-filled with a commonly used default value to help you quickly orchestrate your application.


1. On the application orchestration page, arrange the YAML content for each resource as needed.

   This example uses the default Deployment and Service template files, with only the replica count adjusted to 3.

2. Click **confirm** to open a dialog box where you can specify the effective environment for the current orchestration record.

   In this example, the selection is effective up to the previously configured **Development environment 1**.

3. Click **create** to display a guide box titled **Congratulations on completing application initialization configuration**.

4. Click **I understand** to go back to the application orchestration page of the current application.

   At this point, the application has been orchestrated to a deployable state.


<span id=".5q2l6aqk5LqM77ya56uL5Y2z6YOo572y5bqU55So"></span>
## Step 2: Immediately deploy an application

Deploy the application quickly to the target environment.


1. Switch to the **environment** tab, find **Development Environment 1**, and click **Deploy Now**.

2. On the immediate deployment page, fill in the deployment configuration information as required.

   * Deployment details

   
   |Configuration Item |Descriptions |
   |---|---|
   |Application orchestration |Display the application orchestration version Click to view whether the application orchestration for the current version meets expectations. |
   |Image list |Specify the container images used by the resources of the K8s YAML application. The format of the image address is `host/namespace/repo:tag`.<br><br>In this example, only the Deployment resource has an image, which uses the public Docker Hub image `nginx:latest`. During deployment, replace the image placeholder `image.backend` in the artifact with the `nginx:latest` image. |
   |Environment configuration |Click **view details**, and check whether the configuration meets the environment requirements: whether the enabled configuration items and their values are correct. Environment configuration is not enabled in this example. |
   

   * Deployment plan

   
   |Configuration Item |Descriptions |
   |---|---|
   |Components list |Displays the resources contained in the current application and their deployment order. Allows you to configure the deployment strategy for each resource. This example keeps the default. |
   |Deploy YAML |* Display the actual deployed YAML content after placeholder replacement Click **view details** and confirm whether it meets expectations.<br><br>* Click **Yaml comparison** to view the details of changes in this deployment compared to the previous one, and confirm whether they meet expectations. |
   

3. Click **OK** to go to the application's deployment page. The application is being deployed.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


* **Vital Kubernetes Engine**

   Log in to the container service console, locate the default namespace, and check whether the deployed Deployment application meets expectations.

   As shown in the figure, the Deployment name is `k8s-1218-w-dev1`, the label is `k8s-1218-w-dev1`, and the number of instances is`3`The associated service is `k8s-1218-w-dev1`, and everything is as expected.


At this point, you have completed the application delivery quick start guide.
