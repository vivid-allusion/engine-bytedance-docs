---
title: "Achieve a set of orchestrated differentiated deployments through application delivery"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Achieve_a_set_of_orchestrated_differentiated_deployments_through_application_delivery"
---

The application delivery feature is centered on the application and provides one\-stop capabilities for application orchestration, environment management, configuration management, application release, and more. These capabilities help simplify the complexity of deploying microservices in cloud\-native scenarios, improve application delivery efficiency, and reduce release risks.

This document uses the example of deploying a Kubernetes YAML application in a development environment to introduce the basic capabilities and usage process of application delivery. The deployment cluster associated with the development environment uses the Vital Kubernetes Engine cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

In addition to [preparatory work](https://docs.byteplus.com/en/docs/cp/Preparations), you also need to complete the following actions:


* The workspace has been created. For specific operations, refer to [Create workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

* The image to be deployed is ready.


<span id=".5q2l6aqk5LiA77ya5bqU55So5Yid5aeL5YyW"></span>
## Step 1: Application initialization

Application initialization includes application creation, environment configuration, and application orchestration. After initialization is complete, the application is basically able to deploy plugins.

<span id=".XzEt5Yib5bu65bqU55So"></span>
### Create an application

Create an independently deliverable unit that provides external services.


1. Log in [Code Pipeline console](https://console.byteplus.com/cp).

2. In the workspace area of the Overview page, select the target workspace name to enter that workspace.

3. On the current workspace page, select **Application Delivery** in the left navigation bar. On the application delivery page, click **Create Application**.

4. On the create application page, fill in the relevant configuration information as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Application name |Display name of the custom application This example is set to `App-demo`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This name is not the resource name in the YAML file.</div><br> |
   |Application ID |Enter the Application ID as prompted by the interface. The Application ID is the unique identifier for the application and cannot be changed after creation. In the application orchestration YAML file, the value of the preset placeholder appName will be set to the Application ID you enter. This example is set to `appdemo1201`. |
   |Description |Enter remarks for the current application; this field can be left blank. |
   |Application type |Currently, only **K8S** is supported. **YAML** **application**. |
   |Member management |Quickly configure the members of the current application and configure different permissions for each member to meet the needs of multi\-role collaboration in application delivery.<br><br><br>* **Add members**: Add members to the current application. Multiple members can be added.<br><br>* **Permission**: The system provides five predefined roles: administrator, developer, tester, operations, and read\-only. Each member can be assigned permissions for one or more roles.<br><br><br>The BytePlus account is the default administrator for the application and cannot be removed. This example adds a member to the BytePlus root user account and grants development permission. |
   |Deployment method |Currently, only **preset** is supported. **K8S** **YAML** **Deployment** refers to deploying an application using a K8S YAML description file. |
   

5. After completing the form, click **confirm**. The guidance dialog for the next step of **application initialization configuration** will appear.


<span id=".XzIt546v5aKD6YWN572u"></span>
### Environment configuration

The system comes with a total of four environment levels: **development**, **testing**, **pre\-release**, and **production**. A preset environment can be selected for each environment level. It is recommended to preconfigure at least one environment to facilitate subsequent application orchestration and configuration management.


1. Follow the interface guidance and click **Initialize 2: Environment management.** 

2. On the environment management page, check the environment levels that require preset environments. In this example, a development environment and a test environment are pre\-set.

3. Click **confirm**. The **application initialization configuration** next step guidance dialog will appear.


<span id=".XzMt5bqU55So57yW5o6S"></span>
### 3. Application orchestration

Manage the YAML description file for the application. Currently, you can orchestrate YAML files for the Deployment, Service, and Configmap resource types. The system provides template files for Deployment, Service, and Configmap. In each template, every parameter value is represented by a placeholder, and each placeholder is pre\-filled with commonly used default values to help you quickly orchestrate applications.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example uses the default Deployment and Service template files, and makes the following modifications to the Deployment template file to demonstrate how to use variables in application orchestration to achieve differentiated deployment across different environments. The values of the variables will be enabled and populated in subsequent environment configurations.</div>



* Add a label named label to Deployment, and set the label's value using the variable Label.

* Use the variable Replicas to populate the value of the replica count replicas.

1. Following the interface instructions, click **Initialize 3: Application orchestration**.

2. On the application orchestration page, the left side displays the YAML templates for Deployment and Service, while the right side displays information about each placeholder. You can click ➕ to create more YAML files as needed. This example does not add any other YAML files.

   * Currently, only one Deployment\-type resource can be added to an application.

   * An application can add up to 10 YAML files.

3. Configure the Deployment files and set labels.

   1. On the left, below the metadata.labels.run parameter, enter`run: "{{ .Values.label }} "`.

   2. Click **Extract placeholder**, and the custom placeholder area on the right simultaneously displays the label for the newly added custom placeholder.

   3. Set the information for the custom placeholder label. **Type**: select **String**; **Value source**: select **Variable**.

   4. In the **Value** text box, click **Create parameter** to quickly create a custom parameter Label, and use the Label to populate the **Value**.

4. Configure the Deployment file and use the Replicas variable to populate the value of the replicas field.

   1. In the custom placeholder area on the right, locate the replicas parameter. For **type**, select **integer**; for **Value source**, select **variable**.

   2. In the **Value** text box, click **create parameter** to quickly create a custom parameter named Replicas, and use Replicas to fill the **Value**.

&nbsp;

5. Click **Confirm**. A dialog box will pop up, where you can set the effective environment for the current orchestration record. In this example, the selection applies to the **Development environment 1** and **Test environment 1** that were preset in the previous step.

6. Click **create**. A guide box with the message **Congratulations on completing application initialization configuration** appears. Click **Got it** to go back to the release page of the current application.


<span id=".5q2l6aqk5LqM77ya546v5aKD5Yid5aeL5YyW"></span>
## Step 2: Initialize the environment

Perform initialization actions on the pre\-configured environment, mainly to associate the pre\-configured environment with the cluster to be deployed. This example initializes the preset **development environment 1**.


1. Switch to the **environment** tab, find **Development Environment 1**, and click **Environment Initialization**.

2. On the edit environment page, configure parameters as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Environment level |Displays the environment level of the selected environment. In this example, it is **Development**. |
   |Environment name |Defaults to **Development environment 1** and can be modified. This example is not modified. |
   |Environment ID |The Environment ID is the unique identifier for the environment and cannot be modified. This example is `dev1`. The Environment ID corresponds to the value of the predefined placeholder envName in the application orchestration YAML file. |
   |deploy resource |Select the actual deployment location for the application, for example, Kubernetes clusters, cloud servers, virtual machines, physical machines, and so on. Currently, only deploy resource of the Kubernetes cluster type is supported. Here, select the Vital Kubernetes Engine cluster `Demo-Deploy-Resource` that was prepared in the prerequisites. |
   |Override Namespace |After checking, you must enter the Namespace name. When deploying the current environment, the Namespace name specified here will override the Namespace defined in the YAML file. If the Namespace does not exist in the cluster to be deployed, the system will create it during deployment. Do not check the box in this example. |
   |Associate configuration |Check whether the configuration meets the environmental requirements. Environment initialization is performed here and can be skipped. |
   |Associate a workflow |View associated release workflows. The main operation here is environment initialization, which can be skipped. |
   

3. Click **confirm** to complete the environment initialization operation.


<span id=".5q2l6aqk5LiJ77ya5ZCv55SoLeabtOaWsOeOr-Wig-mFjee9rg=="></span>
## Step 3: Enable/update environment configuration

Enable parameters in the environment and assign values to the parameters. In this example, the custom parameters Label and Replicas, which were set in the application orchestration settings in Step 1, are enabled in **development environment 1**. Values for Label and Replicas are then assigned in the current environment.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended that developers first check the relevant environment parameters and complete the configuration update. After that, operations personnel should initiate the deployment.</div>



1. Switch to the **configuration** tab. In the **environment configuration** tab, select **Development Environment 1**, click **edit configuration value**.

2. On the Edit Configuration Values page, enable Label and Replicas. Then assign a value to each. In this example, Label is set to `demo1201-1940`, and Replicas is set to`3`.

3. Click **Confirm** to enable parameters and assign values.


<span id=".5q2l6aqk5Zub77ya6ZuG5oiQ5aSW6YOo5pyN5Yqh"></span>
## Step 4: Integrate external services

Integrate external image repositories. It is recommended to integrate your own image repository into application delivery, so that images are pulled from your repository during application deployment, which improves the efficiency and security of image deployment.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using the workflow publishing method, you must first integrate your own image repository. Workflow publishing currently only supports pulling images from integrated image repositories.</div>



1. Switch to the **External Integration** tab, and click **Add External Service**.

2. On the add service page, enter the parameter information as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Name |Specify a custom name for the external service; in this example, the name is `myharbor`. |
   |Type |Select the type of external service. Currently, the system supports the Harbor image repositories and the general Docker Registry\-type image repositories. This example demonstrates integration with the Harbor image repository. |
   |Address |Enter the HTTP(S) protocol address of the image repository you want to connect. |
   |Item |Enter the project name in the repository. |
   |Username |Enter the username to log in to the repository. |
   |Password |Enter the password to log in to the repository. |
   |Skip certificate verification |Whether to skip certificate verification when using HTTPS addresses. Do not check the box in this example. |
   

3. Click **Validate and create** to integrate your image repository into application delivery.


<span id=".5q2l6aqk5LqU77ya6YOo572y5bqU55So"></span>
## Step 5: Deploy the application

Application delivery provides two deployment methods: immediate deployment and workflow publishing. This example will introduce each of the two deployment methods.


* Deploy immediately: Directly initiate deployment. The operation is simple and agile, making it suitable for initiating deployments at any time in development and test environments for rapid validation.

* Workflow publishing: Create a complete release process, including workflow configuration, manual review, image deployment, and script execution. Supports notification and viewing of real\-time workflow logs, making the release process more comprehensive and reliable. You must create a release workflow for production environment deployment.


<span id=".5pa55byP5LiA77ya56uL5Y2z6YOo572y"></span>
### Step 1: Deploy immediately


1. Switch to the **environment** tab, find **Development Environment 1**, and click **Deploy now**.

2. On the immediate deployment page, fill in the deployment configuration information as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Application version |Show the application orchestration version. Supports clicking to view whether the application orchestration of the current version meets expectations. |
   |Image |Enter the full address of the image to be deployed. Here, the image corresponds to `Deployment.` The value of the image placeholder `image.backend` in the `yaml` file.<br><br>This example uses the Nginx image from the myharbor repository. The full address is `harbor.volces.com/cp-test/nginx:1.9.1`. |
   |Deployment policy |Supports two deployment policies: **native deployment** and **staged release**. It is recommended to use a batch release policy, which supports fine\-grained deployment capabilities for batch, pause, and resume, providing greater control.<br><br>This example uses batch release: two batches, with the first batch accounting for 30% and the second batch accounting for 70%. With Replicas set to 3, the first batch releases 1 instance and the second batch releases 2 instances (for the first batch, if the result is less than or equal to 1, round up to 1; for all other batches, if the result is not an integer, round down). |
   |Environment configuration |Click **view details** to check whether the configuration meets the environment requirements: whether the enabled parameters are correct and whether the parameter values are correct. If quick modification is not properly supported.<br><br>In this example, enable Label and Replicas. The value of Label is set to `demo1201-1940`, and the value of Replicas is`3`, meets the requirements. |
   |Deployment YAMLs |Visually display the final YAML file to be deployed. Click **view details**, check whether the YAML file to be deployed meets expectations.<br><br>This example deploys one Deployment and one Service, and the parameter values meet expectations. |
   

3. Click **confirm**, navigate to the **Run workflow** tab, and start deployment.

4. On the Run Process tab, after the first batch is deployed successfully, the system displays the **Deploy Next Batch** button. After you click it, the next batch starts deploying. Until all batches have been deployed.


<span id=".5pa55byP5LqM77ya5bel5L2c5rWB5Y-R5biD"></span>
### Method two: Workflow publishing

This example creates a **Manual Review \> Image Deployment \> Script Execution** workflow, runs the workflow, and demonstrates the complete procedure for publishing a workflow.


1. Switch to the **Publish** tab, and click **Create workflow**.

2. On the Create Workflow page, fill in the basic information for the **workflow configuration**.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Name |Customize a workflow name. The name of this example is `workflow demo`. |
   |Description |Enter remarks for the current workflow. It can be left blank. |
   |Environment level |This example demonstrates selecting **development.**  |
   |Notification |Configure notification methods for workflow messages. Application delivery supports pushing workflow messages via in\-app messages, SMS, email, and Webhook, helping you quickly understand application deployment results. This example is not enabled. |
   

3. Click **Manual Review** on the left to configure the task information for manual review.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Task name |Custom task name. This example uses the default name. |
   |Approval method |Supports two approval methods: **Joint approval** and **Alternative approval**. In this example, select or sign.<br><br><br>* **Countersign**: When all approvers have approved, the task is considered successful and the pipeline continues to run.<br><br>* **Any sign\-off**: If any approver approves, the task is considered successful and the pipeline continues to run. |
   |Approval role |Select the role of the approver; in this example, select administrator. |
   |Notification |Supports sending notifications in both the **Pending approval** and **Approval failed** situations. After checking notification conditions, you need to further select the notification method. Supports three notification methods: site message, SMS, and email. This example is not enabled. |
   

4. On the left, click **Image Deployment** and configure the task information for image deployment.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Task name |Custom task name. This example uses the default name. |
   |Container Registry |Select which image repository to pull the image from when deploying the application. This example selects the **myharbor** repository that was integrated in Step 4. |
   

5. On the left, click **Script Execution**. Configure the script execution task information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Script execution supports using a custom runtime environment to perform custom tasks, such as database changes, running some scheduled tasks, source code compilation, and more. This example primarily introduces the feature that allows you to pass variables as parameters during script execution.   </div>
   

   
   |Configuration Item |Descriptions |
   |---|---|
   |Task name |Custom task name. This example uses the default name. |
   |Custom images |If you need to customize the runtime environment, you need to upload the image of the custom runtime environment. This example is not used. |
   |Run script |Enter your run script. The execution box supports setting placeholders as variables to pass parameters. When running the workflow, you need to enter the value corresponding to each placeholder, and only constants are supported.<br><br>In this example, enter the following script:<br><br>```bash```<br>```echo {{ .Script.VALUES1}} # Import variable VALUES1```<br>```echo hello world```<br> |
   

6. Click **Save** to complete workflow creation.

7. Find the newly created workflow, and click **Run.** 

8. On the run page, configure the following information as required.

   * Runtime configuration

   
   |Configuration Item |Descriptions |
   |---|---|
   |Environment level |Display the environment level associated with the current workflow. This example is for development. |
   |environment |This example selects **development environment 1**. |
   |Application orchestration |Display application orchestration version Click to view whether the application orchestration for the current version meets expectations. |
   

   * Image deployment configuration

   
   |Configuration Item |Descriptions |
   |---|---|
   |Container Registry |Displays the image repository you selected when creating the workflow. |
   |Image |Enter the address of the image to be deployed: `repo:tag`. The image here corresponds to `Deployment.` The value of the image placeholder `image.backend` in the `yaml` file.<br><br>This example uses the Nginx image from the myharbor repository, with the address `nginx:1.9.1`. |
   |Deployment policy |Supports two deployment policies: **native deployment** and **staged release**. It is recommended to use a batch release policy, which supports fine\-grained deployment capabilities such as batch, pause, and resume, providing greater control.<br><br>This example uses batch release, divided into two batches: the first batch is 30%, and the second batch is 70%. With the number of replicas set to 3, the first batch releases 1 instance and the second batch releases 2 instances (for the first batch, if the calculated number is less than or equal to 1, round up to 1 instance; for all other batches, if the calculated number is not an integer, round it down to the nearest integer). |
   |Environment configuration |Click **view details** and check whether the configuration meets the requirements of the environment: whether the enabled parameters and their values are correct. If quick modification is not correctly supported, please make the necessary corrections.<br><br>This example enables Label and Replicas. Label is assigned the value `demo1201-1940`, and Replicas is assigned the value`3`Meets the requirements. |
   |Deployment YAML |Visually display the final YAML file to be deployed. Click **view details** and check whether the YAML file to be deployed meets expectations. This example deploys one Deployment and one Service, and all parameter values meet expectations. |
   

   * Script execution configuration

   
   |Configuration Item |Descriptions |
   |---|---|
   |Configuration value |Enter the corresponding value for the VALUES1 placeholder. The value entered in this example is `hello app demo`. |
   

9. Click **Run**. You will be redirected to the **Run workflow** tab, where you can start running the workflow.

10. When the workflow reaches the manual review task, the page displays pending approval. After the reviewer clicks **Approve**, the workflow continues. Administrators can select to skip the manual review process.

11. When the process reaches the image deployment task, after the first batch is successfully deployed, the system displays the **Deploy next batch** button. Click **Deploy next batch** to start deploying the next batch. Until all batches have been deployed.

12. After deployment is complete, proceed to the script execution task. The system will automatically execute scripts.

&nbsp;

   The script is expected to successfully print "hello app demo". At this point, the entire workflow has run successfully.


<span id=".5qOA5p-l57uT5p6c"></span>
## Inspection results

You can also log in to the Vital Kubernetes Engine console, locate the namespace and Deployment name of the specific deployment, and check whether the deployed Deployment meets your expectations.

&nbsp;

As shown in the figure, the deployment name is `appdemo1201-dev1`, the label is `demo1201-1940`, and the number of instances is`3`; The deployment image is `harbor.volces.com/cp-test/nginx:1.9.1`; the service associated is `appdemo1201-dev1`, and both meet expectations.

&nbsp;

At this point, you have completed the experience of the application delivery getting started guide.
