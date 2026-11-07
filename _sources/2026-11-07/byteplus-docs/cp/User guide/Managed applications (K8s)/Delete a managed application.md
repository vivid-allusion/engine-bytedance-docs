---
title: "Delete a managed application"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Delete_a_managed_application"
---

Only application administrators have permission to delete managed applications.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Deleting a managed application will also clean up resources in the application's environment.</div>


* <div data-tips="true" data-tips-type="danger">Deleting the application will permanently delete all data associated with the application. This action cannot be undone. Please exercise caution.</div>


1. Log in to the application management page.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter that workspace.

   4. Select **Application Delivery \> Application Management** in the left navigation bar.

2. On the application management page, select the target hosted application, and click  **`...`**  **\> delete**.

3. In the pop\-up confirmation dialog box, confirm the name of the application to be deleted. After confirming that everything is correct, enter the application name in the delete confirmation box.

4. (Optional) If you need to also delete resources in the application's environment, for example, Deployment and other resources, please select **Synchronously delete application\-related resources in the associated deployment cluster**.

5. Click **OK** to delete the current application.
