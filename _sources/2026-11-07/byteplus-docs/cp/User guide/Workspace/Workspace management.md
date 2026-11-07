---
title: "Workspace management"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Workspace_management"
---

After creating a workspace, you can manage it. This article introduces actions related to workspace management.

<span id=".5p-l55yL5bel5L2c5Yy6"></span>
## View workspace

View information associated with the workspace, including code sources, pipelines, and more.


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), and select **workspace** in the left navigation bar.

2. In the **All** tab, you can view all visible workspace names, the number of associated code sources, the number of associated pipelines, and additional details.

3. Switch to the **My** tab to view information about all workspaces you have created.

4. Click the target workspace name to enter the **Basic Information** page of the workspace. You can view the code source, pipeline, and other information associated with this workspace.


<span id=".5L-u5pS55bel5L2c5Yy65L-h5oGv"></span>
## Modify the workspace information

You can modify workspaces in the visible range. Supports editing workspace name, avatar, description, and member visibility scope.


1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp), and select **workspace** in the left navigation bar.

2. Click the target workspace name to enter the **Basic Information** page of the workspace.

3. At the top of the workspace, click the edit icon to modify the parameters.


<span id=".5aSN5Yi25bel5L2c5Yy6"></span>
## Copy workspace

You can use the workspace copy feature to quickly copy all pipelines and code sources within a workspace, making it convenient to reuse your team's existing code sources and established pipelines.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When a workspace is copied, applications in the application delivery module are not copied.</div>


* <div data-tips="true" data-tips-type="tip">When copying a workspace, the system does not verify the availability of the code source and pipeline under the original workspace.</div>


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), and select **workspace** from the navigation bar on the left.

2. Select the target workspace, click **Copy** in the **Actions** column. The Copy Workspace dialog box appears.

3. Specify a custom name for the new workspace.

4. Click **OK** to complete the workspace copy operation.

   Once the workspace is copied, you can find it in the workspace list.


<span id=".5Yig6Zmk5bel5L2c5Yy6"></span>
## Delete a workspace

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Before deleting a workspace, you must first delete all code sources, pipelines, and applications associated with this workspace.</div>


* <div data-tips="true" data-tips-type="danger">After you delete a workspace, all associated code sources, pipelines, and applications will be cleared. This action cannot be undone. Please proceed with caution.</div>


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp). From the left navigation bar, select **Workspace**.

2. Select the target workspace, click **actions** in the column and then **delete**. A confirmation dialog will appear.

3. Verify the name of the workspace to be deleted. After confirming it is correct, enter the workspace name in the delete confirmation dialog.

4. Click **OK** to delete the current workspace.
