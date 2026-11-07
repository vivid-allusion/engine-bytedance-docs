---
title: "Create environments"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_environments"
---

An environment provides the runtime context for running an application. Each environment instance is associated with a deployment resource, such as a Kubernetes cluster. An application supports creating multiple environment instances for different scenarios, such as development, testing, staging, and production. This article explains how to create an environment instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The application has been created. For details, see [Create an application](https://docs.byteplus.com/en/docs/cp/Create_an_application).

* Deploy resource has been integrated. For detailed actions, see [Deploy resource](https://docs.byteplus.com/en/docs/cp/Deploy_resource_management).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the current application

   1. Log in to [the Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

   5. Click the target application card to open the application.

2. Click **environment** to open the Environment tab.

3. On the environment page for the current application, click **create environment**.

4. On the create environment page, configure the environment information as required.

   * Environment level

   
   |Configuration Item |Descriptions |
   |---|---|
   |Environment level |Select the environment level for the current environment instance. Supports four environment levels: **development**, **testing**, **pre\-release**, and **production**. Role permissions vary by environment level. |
   

   * Environment configuration

   
   |Configuration Item |Descriptions |
   |---|---|
   |Environment name |Display name of the custom environment. It is recommended that names be unique within the same application. |
   |Environment ID |Enter the Environment ID as prompted by the interface. The Environment ID is the unique identifier for the environment and cannot be changed after it is created. The value of the preset placeholder envName in the application orchestration YAML file will use the Environment ID you provide. |
   |deploy resource |Select the actual deployment location for the application, for example, Kubernetes clusters, cloud servers, virtual machines, physical machines, and more. Currently, only deploy resources of the Kubernetes cluster type are supported. |
   |Override Namespace |After checking the box, you must enter the Namespace name. When deploying the current environment, the Namespace name specified here will override the Namespace defined in the application orchestration YAML file. If the Namespace does not exist in the target cluster, it will be created during deployment. |
   

5. Click **OK** to complete environment creation.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* If you need to use variables in application orchestration to enable differentiated deployment of a single application orchestration across multiple environments, you must prepare custom configuration items in advance. For specific actions, see [Configuration item](https://docs.byteplus.com/en/docs/cp/Configuration_Item).

* Orchestrate applications as needed. For specific actions, see [application orchestration](https://docs.byteplus.com/en/docs/cp/Application_orchestration).
