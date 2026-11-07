---
title: "K8s YAML application deployment"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/K8s_YAML_application_deployment"
---

After completing or updating application orchestration and environment configuration, quickly deploy the application to development, testing, or pre\-release environments so that it can be validated in an agile manner. This article introduces how to deploy a K8s YAML application to the target environment.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Application orchestration completed For details on actions, see [K8s YAML application orchestration](https://docs.byteplus.com/en/docs/cp/K8s_YAML).

* The environment configuration update has been completed. For specific actions, see [Environment configuration](https://docs.byteplus.com/en/docs/cp/Environment_configuration).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the current application

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the name of the target workspace to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

   5. Click the target application card to open the selected application.

2. Click **environment** to switch to the environment tab.

3. On the environment page of the current application, select the target environment card and click **Deploy now**.

4. On the Deploy Now page, enter the required deployment configuration for the application.

   * Deployment details

   
   |Configuration Item |Descriptions |
   |---|---|
   |Application orchestration |Display the application orchestration version. Click to view whether the application orchestration of the current version meets expectations. |
   |Image lists |Specify the container images used by each resource in the K8s YAML application.<br><br><br>* **Artifact**: Displays the image placeholder name in the resource YAML.<br><br>* **Remarks**: Displays the description for this image placeholder.<br><br>* **Image**: Refers to the actual image corresponding to the image placeholder. Please enter the image address to use. The image address must be in the format `host/namespace/repo:tag`. During deployment, the image placeholder is replaced with the specified image.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this is not the first deployment, the platform will by default fill in the image address used in the previous deployment record. You can modify it as needed.</div><br> |
   |Environment configuration |* Click **view details** to check whether the configuration meets the environment requirements: whether the enabled configuration items are correct, and whether the values of the configuration items are correct. If quick modification is not properly supported.<br><br>* If there are configuration changes between this deployment version and the previous deployment, the interface will display a **View change details** link. Click to view all changes. |
   

   * Deployment solutions

   
   |Configuration Item |Descriptions |
   |---|---|
   |Component list |* **Deployment order**: Displays the deployment order of each resource. The resource deployment order follows the rules defined by the backend and does not support user customization.<br><br>* **Name/type**: Displays the name and type of resources pending deployment.<br><br>* **Deployment strategy**: Configure the application's deployment strategy. Deployment supports both **native deployment** and **phased release** strategies, while other resources support only the **native deployment** strategy.<br><br>   * **Native deployment**: Based on Kubernetes' native rolling upgrade capability. This strategy can be used when there is no requirement for batch release or in scenarios such as HPA (Horizontal Pod Autoscaler).<br><br>   * **Staged release (recommended)** : Supports fine\-grained deployment capabilities, including staged deployment, pause, and resume, for greater control.<br><br>      * **Rolling batch**: The batch used to configure the phased release strategy. After each batch release is completed, the workflow enters a waiting state and manual confirmation is required to determine whether to Continue. The default is 2 times; the selectable range is from 2 to 10 times.<br><br>      * **Batch proportion**: Set the proportion for each batch release. The ratio for the last batch is automatically calculated after adjustments to previous batches and cannot be modified. The sum of the proportions must be 100%.<br><br>         Number of instances × proportion per batch = number of upgrades per batch (for the first batch, if the result is less than or equal to 1, round up to 1; for all other batches, if the result is not an integer, round down). For example, if 10 instances are deployed in 3 batches with batch proportions of 30%, 30%, and 40%, then the number of instances deployed in each batch will be 3, 3, and 4, respectively. |
   |Deploy YAML |Deployment Yaml displays the actual YAML content after placeholder replacement. Click **view details**, then confirm whether it meets expectations.<br><br>If this deployment differs from the previous one, click the deployment record ID to view the current deployment details of the application. Click **Yaml comparison** to view the details of the changes and confirm whether they are as expected. |
   

5. Click **OK** to navigate to the **Change Log** tab for the current environment, where the details of this deployment are displayed. For more details, see [Observing the deployment process](https://docs.byteplus.com/en/docs/cp/The_observation_deployment_process).


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results

After the environment is successfully deployed, you can view the real\-time status of Deployment and Service resources in the **Component List** on the **Basic Information** tab of the current environment.


* Deployment

   Display the name, status, list of instances, and other information for Deployment resources.

   * View YAML: Click **YAML** to view the deployment YAML for the Deployment resource.

   * View logs: Click **Log** to view the real\-time logs of the instance.

   * To view events: Click **Event** to view event information for the instance from the past hour.

   * Log in to an instance: Click  **`···`**  ** \> Console** to log in to the instance. You can execute the corresponding command\-line actions for fine\-grained debugging of the instance.

* Service

   Displays the name, type, cluster IP, internal endpoint, and external endpoint of the Service resource.

   * View YAML: Click **Yaml** to view the Service resource deployment YAML.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

If you want to expose the application to external access, you need to create a Service (of the NodePort or LoadBalancer type) and Ingress resources for the application after it has been successfully deployed. If the application is deployed on a Container Service VKE cluster, see [Service](https://docs.byteplus.com/en/docs/vke/Services) and [Ingress](https://docs.byteplus.com/en/docs/vke/Ingresses) for related actions.
