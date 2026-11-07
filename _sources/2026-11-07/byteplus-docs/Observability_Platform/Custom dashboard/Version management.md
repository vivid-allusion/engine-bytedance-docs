---
title: "Version management"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Version_management"
---

Version management allows you to view and roll back to previous versions of a custom dashboard. This topic describes how to use version management.

<span id="VQaStrkw"></span>
## View versions


1. Log in to the [Observability Platform ](https://console.byteplus.com/observe/dashboard/dashboard)console, and in the left navigation bar, select **Custom Dashboard**.

2. On the dashboard management page, click the name of the target dashboard to go to the dashboard details page.

3. Click the ** Edit** button, then click ** Settings**, and select the **Version management** tab.

4. On the **Version management** tab, you can view versions, version details, update time, and the operator.


<span id="ldZIULyc"></span>
## Create versions


1. Log in to the [Observability Platform ](https://console.byteplus.com/observe/dashboard/dashboard)console, and in the left navigation bar, select **Custom Dashboard**.

2. On the dashboard management page, click the name of the target dashboard to go to the dashboard details page.

3. Click **Edit ** and modify the dashboard information. Then, click **Save ** to go to the Save dashboard page. For modification instructions, see ****[Managing dashboards](https://docs.byteplus.com/en/docs/Observability_Platform/Managing_dashboards?TagIDs=2,405&lang=en).

4. Enter the version information and select the "Save current time range as dashboard default" checkbox. The current time range is then saved as the default time range of the dashboard.

5. Click the **Save** button. The system generates a new version record based on your changes.


<span id="vTlHvkKj"></span>
## Roll back a version


1. Log in to the [Observability Platform ](https://console.byteplus.com/observe/dashboard/dashboard)console, and in the left navigation bar, select **Custom Dashboard**.

2. On the dashboard management page, click the name of the target dashboard to go to the dashboard details page.

3. Click the ** Edit** button, then click ** Settings**, and select the **Version management** tab.

4. In the Actions column of the target version, click **Revert**. After you read the prompt, click **Revert** again to restore the dashboard to the configuration of the selected version.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The rollback operation causes the current unsaved changes to be lost. To cancel this operation, click <strong>Cancel</strong>.   </div>
   

5. After the rollback is complete, the system generates a new version record to record the rollback.


<span id="5m00FKmx"></span>
## Compare versions


1. Log in to the [Observability Platform ](https://console.byteplus.com/observe/dashboard/dashboard)console, and in the left navigation bar, select **Custom Dashboard**.

2. On the dashboard management page, click the name of the target dashboard to go to the dashboard details page.

3. Click the ** Edit** button, then click ** Settings**, and select the **Version management** tab.

4. In the version list, select the two versions that you want to compare. Currently, you can compare only two versions at a time.

5. Click **Version comparison**. The system displays the JSON configurations of the two versions in a side\-by\-side view and highlights the fields that differ.


&nbsp;
