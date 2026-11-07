---
title: "Change the hosted application"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Change_the_hosted_application"
---

Supports upgrade, scaling, rollback, and other change operations for managed applications. A change record is generated for each change to facilitate traceability.

<span id=".56uL5Y2z6YOo572y"></span>
## Deploy immediately

Update or upgrade the application using a rolling release approach, including updating the application package, application configuration, version number, service specifications, or changing the application's deployment method (whether to use VCI Instance), and more.


1. Log in to the current application.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

   5. On the application management page, select the target hosted application, click the application card, and enter the basic information tab for the current application.

2. Switch to the environment tab, and click **Deploy now.**  The page displays the most recent deployment configuration information, which can be modified as needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to fill in the <strong>Description</strong> on the basic configuration page to facilitate tracing and auditing the content of this change. Other Basic configuration and Advanced configuration parameters are the same as those on the create application page. For detailed explanations, refer to the following documentation:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_apps_JAR_WAR">Create and deploy applications (JAR /WAR)</a>   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_app_container_image">Create and deploy hosted applications (container images)</a>   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_binary_packages">Create and deploy managed applications (binary packages)</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to update the application's <strong>version number</strong> to facilitate version management.   </div>
   

3. Click **confirm**, and the system will automatically redirect to the environment tab for the current application to begin deploying the application.

   After deployment is complete, the deployment status will change to **Completed**.


<span id=".5Zue5rua"></span>
## Rollback

With the rollback feature, you can quickly revert the environment to a usable version of the application. Applicable to scenarios where the new version does not meet expectations after release and a rollback is desired.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The rollback functionality will roll back all configuration of the application, including service specifications, instance count, application package, and other items.</div>


* <div data-tips="true" data-tips-type="warning">The rollback feature does not affect whether the VCI Instance is used: if the current version uses the VCI Instance, the rolled\-back version will continue to use the VCI Instance deployment method; if it is not used, the rolled\-back version will continue to use the standard Kubernetes deployment method.</div>


1. In the environment tab of the current hosted application, click **Rollback**.

2. In the dialog box that appears, select the target version to roll back to.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The page only displays the version information of the last 10 successful application deployments and does not include versions from failed deployments, terminated deployments, rollbacks, or scaling operations.   </div>
   

3. (Optional) Click  **＋**  to view detailed configuration information for the target version.

4. Click **OK** to start rolling back the application.

   After the rollback is completed, the deployment status will change to **Completed**.


<span id=".57uI5q2i6YOo572y"></span>
## Terminate deployment

If an error occurs during deployment, scaling, or rollback, you can terminate the process at any time. After terminating the deployment, the environment does not revert to its pre\-deployment state.


1. During deployment, scaling, or rollback, click **Terminate Deployment** to the right of the deployment status.

2. In the confirmation dialog box that appears, click **Confirm**. The system will terminate the current deployment.

   After the deployment has been terminated, the deployment status will change to **Terminated**.


<span id=".5p-l55yL5Y-Y5pu06K6w5b2V"></span>
## View change history

Performing deployment, scaling, or rollback actions on an application, or creating, updating, or deleting services for an application, will generate a change record to facilitate traceability for operations and maintenance personnel.


1. In the environment tab of the current hosted application, click **Change history** to switch to the change history tab.

2. Select the target change record, then click **details** in the **actions** column to view detailed information about this change record.


&nbsp;
