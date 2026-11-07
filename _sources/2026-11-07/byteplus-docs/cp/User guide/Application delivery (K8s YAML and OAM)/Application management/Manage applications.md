---
title: "Manage applications"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_applications"
---

After an application is created, you can modify the application's basic information, delete the application, and perform other actions. This article introduces actions for managing applications.

<span id=".5L-u5pS55bqU55So5Z-65pys5L-h5oGv"></span>
## Edit the application's basic information

You can currently modify the application name and description.


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp), and select **workspace** from the left navigation bar.

2. Click the target workspace name, then in the left navigation bar of the current workspace, select **Application Delivery \> Application Management**.

3. Click the target application card to open the selected application. Click **Settings**, and then switch to the Settings tab.

4. In the basic information area, locate the configuration item you want to modify and click the edit icon to edit it.


<span id=".5Yig6Zmk5bqU55So"></span>
## Delete applications

Only application administrators can delete applications.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">After you delete the application, all data associated with the application will be lost and cannot be recovered. Please proceed with caution.</div>



1. On the application management page, locate the target application card and click  **`...`**   **\> Delete**.

2. In the pop\-up secondary confirmation dialog, check the name of the application to be deleted. After confirming that there are no errors, enter the application name in the delete confirmation box.

3. (Optional) If you need to also clean up resources in the environment where the application resides (for example, Deployment resources and others), please select **Synchronously delete resources related to the application within the associated deployment cluster**.

4. Click **OK** to delete the current application.
