---
title: "View hosted application details"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/View_hosted_application_details"
---

Supports viewing basic information, member composition, environment information, orchestration information, and more for managed applications.


1. Log in to the application management page

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the name of the target workspace to enter it.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

2. On the application management page, select the target hosted application, click the application card to enter the basic information tab for the current application.


<span id=".5Z-65pys5L-h5oGv"></span>
## Basic Information

Displays the application's basic information and member details, supports adding and deleting members, and allows modification of member permissions.


|Feature |Descriptions |
|---|---|
|Add members |Click **Add member** to add a new member to the current application. Only users who have permissions in the current workspace can be selected. |
|Configuration permissions |The system provides two preset roles: administrator and read\-only. Permissions for one or more roles can be configured for each member.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is not permitted to cancel administrator privileges for the main account or to delete the main account.</div><br> |
|Delete members |Click **delete** to delete unnecessary members. |


<span id=".546v5aKD"></span>
## environment

Display application environment information, corresponding instance list, and change records


|Feature |Descriptions |
|---|---|
|Environment information |Displays information about the Kubernetes cluster and namespace associated with the current environment, the binary package used for deployment, deployment status, deployment time, and other relevant details.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, managed applications support only a single environment instance. Each environment is linked to a deploy resource (which is currently a Kubernetes cluster).</div><br> |
|Instances |Displays information for all instances in the current environment. A status of **Running** indicates that the application is running normally.<br><br><br>* View real\-time logs: Click **Real\-time logs** to view real\-time log information for the instance, making operations and troubleshooting more convenient.<br><br>* View events: Click **Events** to view information about events that occurred in the instance within the last hour.<br><br>* Log in to an instance: Click  **`···`** , then  ** \> Console** to log in to the instance. You can perform the corresponding command\-line actions to perform fine\-grained debugging on the instance. |
|Change history |Performing deployment, scaling, or rollback actions on an application, or creating, updating, or deleting services for an application, will generate a change record, making it easier for operations personnel to trace changes.<br><br>Click **details** to view detailed information about this change record. |
|Autoscaling |Configure an autoscaling strategy for the application to optimize deployment performance and cost. For a detailed introduction, see [Auto Scaling](https://docs.byteplus.com/en/docs/cp/Auto_scaling). |


<span id=".5bqU55So57yW5o6S"></span>
## Application orchestration

Display the latest orchestration information for the application, including basic configuration, advanced configuration, and application access methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Any configuration information modified during each deployment is automatically updated in the application orchestration.</div>



|Feature |Descriptions |
|---|---|
|Basic configuration |Display the application's current basic configuration, including deployment method, technology stack language, application package type, service specifications, whether VCI Instance is used, and other information. |
|Advanced configuration |Display the application's current advanced configuration, including the start command, start parameters, environment variables, health checks, and other information. |
|Access method settings |Display all access methods for the application's current configuration, including internal load balancer, external load balancer, and Service. For more information, see [Access methods](https://docs.byteplus.com/en/docs/cp/Access_methods).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only managed applications deployed to the <strong>Container Service VKE cluster</strong> support access settings.</div><br> |
