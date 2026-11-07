---
title: "Change logs"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Change_logs"
---

Displays all change records for the application in each environment instance and provides rollback functionality, making environment operation and maintenance, as well as rapid rollback, more convenient.

<span id=".5p-l55yL5Y-Y5pu06K6w5b2V"></span>
## View change records

The change records tab displays all change records for the current environment instance, including deployment records and rollback records.


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp), and in the left navigation bar, select **workspace**.

2. Click the target workspace name, in the left navigation bar of the current workspace, select **Application delivery \> Application management**.

3. Click the target application card to enter the current application. Click **environment**, and switch to the environment tab.

4. Click the target environment card to enter the details page of the most recent deployment for the current application.

5. Click **Change Log** to switch to the Change Log tab.

   The change record tab displays the ID, status, type, trigger source, associated configuration, operator, start time, end time, and other information for each change record in the current environment.

   * Click **Change log ID** to view the details of the change log for the corresponding version.

   * Click **Associated configuration ID** to view the configuration details for the corresponding version.


<span id=".5Zue5rua"></span>
## Rollback

By using the rollback feature, you can quickly revert an environment to an available version. Applicable to scenarios where a rollback is desired after a new version is released and does not meet expectations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Rollback is equivalent to redeploying using a historical version; please exercise caution.</div>


In the change record tab for the target environment of the current application, perform a rollback operation. Provides two methods: **rollback to target version** and **rollback to current version**.

<span id=".5Zue5rua5Yiw55uu5qCH54mI5pys"></span>
### **Roll back to the target version**


1. On the change log page, click the **Rollback** button in the upper right corner to display the rollback information dialog box.

2. Select or enter the version ID to roll back to, then click **confirm**.

   The system will redirect to the application's deployment page and begin the rollback operation. After the rollback is complete, the page displays "Rollback successful".


<span id=".5Zue5rua5Yiw5b2T5YmN54mI5pys77yIazhzLXlhbWzvvIk="></span>
### Restore to the version defined in the K8s YAML


1. On the change log tab, select the target version you want to roll back to from the list, then click **Roll back to current version** in the **Actions** column.

2. In the pop\-up confirmation dialog box, click **Confirm**.

   The system will redirect to the application's deployment page and begin the rollback operation. After the rollback is complete, the page displays "Rollback successful."
