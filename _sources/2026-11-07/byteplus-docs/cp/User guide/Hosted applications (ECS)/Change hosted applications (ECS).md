---
title: "Change hosted applications (ECS)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Change_hosted_applications_ECS"
---

Supports performing upgrade, rollback, and other change actions on managed applications (ECS). Each change generates a change record to facilitate traceability.

<span id=".56uL5Y2z6YOo572y"></span>
## Deploy immediately

Update and upgrade the application, including updating the application package, version number, runtime parameters, health check configuration, and other items.


1. Log in to the current application.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

   5. On the application management page, select the target hosted application, click the application card, and go to the basic information tab for the current application.

2. Switch to the environment tab and click **Deploy now.**  The page displays the most recent deployment configuration information, which you can modify as needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The basic configuration and advanced configuration parameters are the same as those on the create application page. For a detailed description, refer to <a href="https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_applications_ECS">Create and deploy managed applications (ECS)</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to update the application's <strong>version number</strong> to facilitate version management.   </div>
   

3. Click **confirm**, and the system will automatically navigate to the environment tab of the current application and begin deploying the application. After deployment is complete, the deployment status will change to **Completed**.


<span id=".5Zue5rua"></span>
## Rollback

With the rollback feature, you can quickly restore the environment to one of the available versions of the application. Applicable to scenarios where, after a new version is released, the results do not meet expectations and a rollback is desired.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The rollback feature will roll back all configurations of the application.</div>



1. On the environment tab of the current hosted application, click **Rollback**.

2. In the pop\-up dialog box, select the target version you wish to revert to.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The page only displays version information for the application from the most recent 10 successful deployments.   </div>
   

3. (Optional) Click  **＋**  to view detailed configuration information for the target version.

4. Click **Confirm** to start rolling back the application. After the rollback is complete, the deployment status will change to **Completed**.


<span id=".57uI5q2i6YOo572y"></span>
## Terminate deployment

If an exception occurs during deployment or rollback, you can terminate the deployment at any time.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deployment is terminated, the environment does not revert to its pre\-deployment state. You need to log in to the ECS instance yourself, confirm the current status of the application, and carry out subsequent processing tasks.</div>



1. During deployment or rollback, click the **Terminate deployment** button to the right of the deployment status.

2. In the pop\-up confirmation dialog, click **confirm**. The system will terminate the current deployment. After the deployment has been terminated, the deployment status will change to **Terminated**.


<span id=".5p-l55yL5Y-Y5pu06K6w5b2V"></span>
## View change log

Each time deployment or rollback actions are performed on an application, a change record will be generated to facilitate traceability for operations and maintenance personnel.


1. In the environment tab of the currently managed application, click **Change log**. This switches to the Change log tab.

2. Select the target change record, and click **details** in the **Actions** column to view detailed information for this change record.
