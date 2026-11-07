---
title: "Manage code sources"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_code_sources"
---

After creating a code source, you can manage it. This article introduces actions related to code source management.

<span id=".5qCh6aqM5Luj56CB5rqQ"></span>
## Verify code source

Manually verify that the code source is accessible and functioning correctly, specifically including:


* Is the token valid

* Does the code source address comply with the rules?

* Can the code source address be accessed via the public internet?

1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), and select **workspace** in the left navigation bar.

2. Click the name of the target workspace to enter that workspace.

3. Select **code source** from the left navigation bar to enter the **code source** page.

4. Select the target code source, and click **Verify** in the **actions** column to display the verification dialog box.

5. Check the information for the code source to be verified. After confirming, click **Confirm** to start verifying the code source.

   * If the code source cannot be accessed via the public network, the system will display a warning: **Code repository failed public network access verification**.

   * If validation fails for other reasons, the system will display a validation failure message.


<span id=".57yW6L6R5Luj56CB5rqQ"></span>
## Edit code source

You can modify all information except the code source type.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the code source is associated with a pipeline, the code source name cannot be modified.</div>



1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), and select **workspace** from the left navigation bar.

2. Click the target workspace name to enter the workspace.

3. In the left navigation bar, select **code source**, and go to the **code source** page.

4. Select the target code source, click **edit** in the **actions** column, and the edit dialog box will appear.

5. Modify code source information as needed.

6. Click **Validate and update**. After validation, the code source information is successfully updated.


<span id=".5Yig6Zmk5Luj56CB5rqQ"></span>
## Delete code source

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before deleting the code source, disassociate it from related pipelines.</div>


* <div data-tips="true" data-tips-type="warning">After you delete a code source, pipelines associated with that code source will no longer function properly. Please proceed with caution.</div>


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp), and select **workspace** from the left navigation bar.

2. Click the name of the target workspace to enter that workspace.

3. From the left navigation bar, select **code source** to go to the **code source** page.

4. Select the target code source, and in the **actions** column, click  **`...`**  After clicking **Delete**, a confirmation dialog appears.

5. Verify the code source information. After confirming, click **delete**.
