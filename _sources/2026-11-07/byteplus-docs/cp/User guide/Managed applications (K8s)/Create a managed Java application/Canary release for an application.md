---
title: "Canary release for an application"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Canary_release_for_an_application"
---

Canary release for hosted applications is a release policy that makes new versions of an application available to users gradually and in batches. While ensuring that the experience of most users remains unaffected, collect early feedback, promptly identify and resolve potential issues, and advance application updates in a more robust way to reduce the risk of a full rollout. Introduce methods for supporting the delivery of managed applications with canary release

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The managed application has been created. For details on Actions, refer to [Create and deploy managed applications (JAR/WAR)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_apps_JAR_WAR).

* The API gateway has been created. For details, refer to [create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* An Upstream of the Vital Kubernetes Engine type has already been created in the API Gateway. For details on this action, refer to [Create an Upstream of the Vital Kubernetes Engine type](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the name of the target workspace to enter the current workspace.

   4. Select **Application Delivery \> Application Management** from the left navigation bar.

2. At the top of the page, click **Hosted** to filter hosted applications.

3. Click the target application's **environment**.

4. On the **environment** page, click **Deploy now**.

5. On the **Release settings** page, select **Canary release**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Gray release does not involve parameters on the <strong>Basic configuration</strong> and <strong>Advanced configuration</strong> pages, so you can skip the configuration pages.   </div>
   

6. Gray release configuration parameters.

   
   |Parameter |Descriptions |
   |---|---|
   |Number of instances |The number of newly added canary version instances. |
   |Policy type |Currently, traffic can be allocated proportionally between canary version instances and original version instances. |
   

7. Click **Confirm** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Subsequent support is provided for changing the gray ratio, releasing the gray version to all users, or rolling back the version on the **Change Log \> Details \> Gray Monitoring** page.


* Change canary release traffic allocation: Supports adjusting the traffic allocation for the canary release. Click **Edit proportion** to update the flow percentage.

* Release a new version: If the canary version runs as expected, click **End canary \> Full release of new version** to release the canary version as the new version to all users and take the original version instances offline.

* Roll back to the previous version: If the grayscale version does not run as expected, click **End grayscale \> Roll back to previous version**. Then, take the grayscale version offline.
