---
title: "Manage environments"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_environments"
---

After creating an environment instance, you can perform actions such as editing, deleting, and more on it. This article introduces actions related to managing environments.

<span id=".5p-l55yL546v5aKD5YiX6KGo"></span>
## View environments

Using the environment card, you can quickly access the following information:


* Displays basic information including the environment name, the type of the most recent operation (deployment, rollback, or none), current status (deployment succeeded, deployment failed, or cancelled), and operation details.

* Quickly jump to the details of the most recent action.

* Quickly initiate a deployment

* When configuration updates are available for an environment, including application orchestration and environment configuration, the environment is highlighted. The user is then prompted to update the environment.

1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), and select **workspace** from the left navigation bar.

2. Click the target workspace name, and in the left navigation bar of the current workspace, select **Application Delivery \> Application Management**.

3. Click the target application card to open the application. Click **environment** to switch to the environment tab.

   You can view all environment instances under the current application.


<span id=".57yW6L6R546v5aKD"></span>
## Edit environments

By editing the environment, you can modify the environment display name, deployment resources, and Override Namespace information of an existing environment instance.


1. On the environment page of the current application, locate the environment card to be modified and click  **`...`**   **\>Edit** button.

2. On the edit environment page, modify configuration information as needed.

3. After you have finished making changes, click **OK**.


<span id=".5Yig6Zmk546v5aKD"></span>
## Delete an environment

If you no longer need the current environment instance, you can delete it to release environment resources.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">After the environment instance is deleted, the application will no longer be able to provide services externally. Caution: Data cannot be recovered. Proceed with caution.</div>



1. On the current application's environment page, locate the environment card to delete, and click  **`...`**   **\> delete** button.

2. In the pop\-up confirmation dialog, click **Confirm** to delete the current environment instance.
