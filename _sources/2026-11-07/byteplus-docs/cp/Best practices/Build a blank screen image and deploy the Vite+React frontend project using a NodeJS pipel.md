---
title: "Build a blank screen image and deploy the Vite+React frontend project using a NodeJS pipeline"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Build_a_blank_screen_image_and_deploy_the_Vite_React_frontend_project"
---

This document uses the deployment of a Vite\-based React frontend application as an example to demonstrate how to use a Node.js pipeline to build frontend application images that prevent white screen issues, and how to enable application updates and public access through application hosting.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

This article will demonstrate how to address white screen issues during container image builds and Kubernetes deployment for a Vite + React project by combining the pipeline and application delivery features of Code Pipeline. Suitable for developers who are not familiar with Dockerfile and Kubernetes (K8s) related knowledge but want to complete containerized deployment of frontend applications.


* **NodeJS compilation and hosted application image build**: This pipeline task compiles and builds the source code of the Vite + React project, and packages the resulting static assets into a container image using a static asset containerization approach, where the container image serves only static resources and displays a blank screen until the frontend loads. Nginx is used in the image to act as a reverse proxy for static resources.

* **NodeJS application hosting**: NodeJS hosted applications are deployed using container images. This article deploys a NodeJS application using images produced by the pipeline. Enable public access to the Vite + React project by adding a load balancing (public network) method.

* **NodeJS compilation build & hosted application image build + hosted application deployment**: Subsequently, this pipeline template can be used to automate updates for Vite + React projects.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The frontend project has been prepared and uploaded to your code repository. This article uses the following commands to create the simplest Vite + React project and upload it to the Gitee code repository. For more information about developing Vite frontend projects, refer to [Vite official documentation](https://cn.vitejs.dev/).

   ```shell
   npm create vite@latest react-demo -- --template react-ts
   ```
   

* Code Pipeline preparations

   * Workspace has been created. For detailed operations, refer to [Create workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

   * The code repository containing the frontend project has been integrated into Code Pipeline. For detailed actions, refer to [Integrate code source](https://docs.byteplus.com/en/docs/cp/Integrate_code_source).

   * The Kubernetes cluster to be deployed has already been connected. For specific operations, refer to [deploy resource](https://docs.byteplus.com/en/docs/cp/Deploy_resource).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77yabm9kZWpzLee8luivkeaehOW7ui3miZjnrqHlupTnlKjplZzlg4_mnoTlu7o="></span>
### Step 1: **NodeJS compile and build & hosted application image build**


1. **Create pipelines**

   1. Log in [Code Pipeline Console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**. On the workspace page, click the target workspace name to enter the current workspace.

   3. Click **Create pipeline** to open the **Select pipeline template** dialog box.

   4. Select **NodeJS \- Compile Build & Host Application Image Build \- Application Deployment**, click **confirm**, and enter the process orchestration page for the current pipeline.

2. **Process orchestration**

   1. Configure code sources In the code source & trigger area, click **add \> code source**. This document selects the Gitee code source created in the prerequisites. Event triggering is not enabled.

   2. Configure the **NodeJS compilation/build and hosted application image build** task.

      1. Click the **NodeJS compilation build & hosted application image build** task card to open the edit task panel.

      2. Configuration **NodeJS build and compilation** step.

         
         |Configuration Item |Descriptions |
         |---|---|
         |Step name |By default, NodeJS is used for compilation and build; this example uses the default setting. |
         |Version |Select the NodeJS version used for compilation and build. This example uses **20.11.0**. |
         |Compile command |Write compilation commands based on the actual business. The example is as follows:<br><br>```shell```<br>```npm install```<br>```npm run build```<br> |
         |Skip on failure |Once enabled, if the current step fails, it will be skipped immediately. This example is not turned on. |
         

      3. Configuration steps for **managed application image build**.

         
         |Configuration Item |Descriptions |
         |---|---|
         |Step name |By default, managed application image build is used. This example keeps the default setting. |
         |Mirror address |Enter the Repository URL to which the image will be pushed after a successful build. HTTP and HTTPS protocols are supported. The format is `host/namespace/repo:tag`.<br><br>In this context, the image address supports the use of dynamic parameters. For example: `xxx.com/doc-demo/react-demo:$(PIPELINERUN_ID)_$(DATETIME)`. |
         |Username/password |Enter the login account and password for the target image repository. |
         |Skip certificate verification |Optional configurations. After checking the checkbox, all content in the current step will no longer validate the HTTPS certificate's validity. For example, the Repository URL for pushing or pulling images no longer validates the validity of the HTTPS certificate. This example is kept turn off. |
         |Whether to use image cache |Cache is turned on by default to accelerate image building and solve the problem of long pull times for base images. |
         |Nginx configurations |Static resources are served via a reverse proxy for web access.<br><br>The Nginx configuration for this example is as follows:<br><br>```shell```<br>```server {```<br>```  listen       80;```<br>```  server_name  localhost;```<br>```  location /assets {```<br>```        root /usr/www/html;```<br>```  }```<br>```  location / {```<br>```      root   /usr/www/html;```<br>```      index  index.html index.htm;```<br>```  }```<br>```}```<br> |
         |Whether to copy static files |Should static files be copied into the image?<br><br>In this example, static assets generated by compiling and building with NodeJS need to be copied into the image, so this switch should be enabled. |
         |Source file directory |Specify the directory where the static file resources are located.<br><br>This example project is built using vite, and the generated output is located in the dist directory. Therefore, the source file directory for this example is `dist`. |
         |The target file directory |Specify the target directory in the image where static files will be copied. This directory must be consistent with the root defined in the nginx configuration.<br><br>The target file directory for this example is `/usr/www/html`. |
         |Skip on failure |Once enabled, if the current step fails to run, it will be skipped immediately. This example is not enabled. |
         

      4. All other parameters remain at their default values. Click **Confirm** to complete the configuration of the current task card.

   3. Delete the **application hosting deployment** stage.

      Since a Nodejs hosted application has not yet been created, it is not possible to deploy the application using the pipeline **application deployment** task. Therefore, delete the **application hosting stage** first.

   4. Click **Save** to save the current pipeline configuration.

3. **Run pipeline**

   1. On the pipeline list page, select the target pipeline that was just created, and click the run icon in the Actions column.

   2. In the pop\-up run pipeline dialog box, confirm the code source branch information and optionally enter a run description.

   3. Click **confirm**. The pipeline starts running, and the system navigates to the details page for the current pipeline.

      After the pipeline runs successfully, you can obtain the address of the built image. Copy the image address for later use.


<span id=".5q2l6aqk5LqM77yabm9kZWpzLeW6lOeUqOaJmOeuoQ=="></span>
### Step 2: **NodeJS application hosting**


1. **Create and deploy a NodeJS hosted application**

   1. In the current workspace, select **Application Delivery \> Application Management** from the left navigation bar.

   2. On the application management page, click **create application**.

   3. On the create application page, select **Application Hosting**, and fill in the required application configuration information as instructed.

      1. Enter **application information**. After completing the entry, click **Next: Basic configuration**.

         
         |Configuration Item |Descriptions |
         |---|---|
         |Application ID |Enter the Application ID as prompted by the interface. The Application ID is the unique identifier for the application and cannot be changed after it is created. |
         |Application name |Display name of a custom application |
         |Application technology stack |In this scenario, select **Other**. |
         |Description |Enter remarks information for the current application. This field can be left empty. |
         |Member management |Quickly configure the members of the current application and configure different permissions for each member to meet the requirements of multi\-role collaboration in application delivery.<br><br>The system will, by default, add the BytePlus account (root user) and the application creator as administrators. No further members will be added in this example. |
         

      2. Fill in **basic configuration**. Once completed, click **Next: environment configuration**.

         
         |Configuration Item |Descriptions |
         |---|---|
         |Deployment method |In this scenario, select **Image deployment**. |
         |Application image |Enter the image address used by the application. The image address format is `host/namespace/repo:tag`.<br><br>In this example, enter the image address obtained in Step 1. |
         |Image pull authentication |If you are using a private image, you must enable the image pull authentication switch and enter the correct image repository username and password.<br><br>The image repository used in this example is public and does not need to be turned on. |
         |Version |Version number of the custom application. You can click the **Use timestamp as version number** on the right to automatically generate a version number. |
         |Vital Container Instance (VCI) |Whether to deploy the application using the Vital Container Instance method. This example is not enabled. |
         |Service specifications |Define the service specifications for the application according to business requirements, including the number of instances, and the CPU and memory specifications for each instance. This example keeps the default. |
         

      3. Fill in **environment configuration**. After completion, click **Next: Advanced configuration**.

         
         |Configuration Item |Descriptions |
         |---|---|
         |deploy resource |Select Kubernetes clusters that have already been connected in the prerequisites. |
         |Namespace |Select the namespace to deploy to. |
         |Environment ID |Automatically generated based on the Application ID; can be modified. This example maintains the default settings. |
         

      4. Leave **Advanced configuration** at its default setting.

      5. Click **Confirm**. The application will begin deployment. You can view application deployment progress on the Environment tab.

         Deployment status changes to **Completed,**  and instance running status is **running** indicate deployment is successful.

2. **Add load balancing (public network)** 

   1. Switch to the application orchestration tab. In the access method settings section, select **Load Balancer (Public Network) \> Add Load Balancer (Public Network)** .

   2. In the Add Load Balancer (Public Network) dialog box, set load balancer parameters.

      The container port must match the port that nginx listens on in the configuration. This example is 80.

   3. Click **confirm**, and creation of the public load balancer will begin.

      After creation is complete, you can view the port mapping for the public load balancer in the table: `<Load balancer IP>:<Port number>`.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

Using a machine with public network access permission, enter `<load balancer IP>:<port number>` in the browser address bar—for example, `101.xx.xx.xx:80`. You will be able to successfully access the homepage of the Vite + React project.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7559b9692933c78535c4ed9b5a944c3a.png) </span>

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

In this document, the NodeJS hosted application is deployed using the manual deployment method. However, during the agile iteration process, the team prefers to automatically trigger image building and application deployment in response to pipeline code change events. To achieve the above objective, only two modifications to the current pipeline are required:


1. On the current pipeline **Process orchestration** page, click in the code source area to open the configuration input source dialog box. Turn on **event trigger** and check **Trigger event**. For more information, refer to [Code Source Trigger](https://docs.byteplus.com/en/docs/cp/Trigger_from_code_source).

2. On the current pipeline **process orchestration** page, add an **application deployment** task after **NodeJS compilation and managed application image build**, and use upstream artifacts to upgrade the image of the NodeJS managed application. For more information, refer to [application deployment](https://docs.byteplus.com/en/docs/cp/Application_deployment#.5omY566h5bqU55So).
