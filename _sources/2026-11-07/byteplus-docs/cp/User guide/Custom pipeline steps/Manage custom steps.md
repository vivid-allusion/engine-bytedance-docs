---
title: "Manage custom steps"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_custom_steps"
---

After you upload custom steps, you can manage the custom steps. Currently supports viewing YAML templates for Custom steps, updating Custom steps, upgrading Custom steps, viewing pipelines associated with Custom steps, and more.

<span id=".5p-l55yLLXlhbWwt5qih5p2_"></span>
## View YAML templates

View the YAML content of the latest version of the current custom step.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To view the YAML content of historical versions, use the <strong>Update Custom steps</strong> feature.</div>



1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. Select **Template Marketplace \> Step Template** in the left navigation bar.

3. On the step template page, click **Custom steps** to switch to the Custom steps tab.

4. Select the target custom step, then click  **`...`**   **\> View YAML template**.

5. In the pop\-up template details panel, view the YAML details. After you have finished viewing, click **OK**.


<span id=".5pu05paw6Ieq5a6a5LmJ5q2l6aqk"></span>
## Update custom steps

Updating custom steps does not increment the version number; only the description, script, image, category, and the defaultValue and description fields of inputs in the step YAML can be updated.


1. On the Custom steps tab, select the custom step card you want to update, and click  **`...`**   **\> Update**.

2. In the pop\-up panel, select the version to update, and update the YAML content within the input box.

3. After the update is complete, click **OK**.

   After the update, pipelines that use steps of this version will automatically use the updated content when running.


<span id=".5Y2H57qn6Ieq5a6a5LmJ5q2l6aqk"></span>
## Upgrade custom steps

Support upgrading custom steps to the latest version. When upgrading custom steps, all fields in the step YAML can be modified.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After upgrading custom steps:</div>



* <div data-tips="true" data-tips-type="tip">Pipelines that were already associated with this step are not affected and will continue to use the version of the step from before the upgrade.</div>


* <div data-tips="true" data-tips-type="tip">When adding a new pipeline or adding the current step to an existing pipeline, the latest version of the step is used by default.</div>


1. On the Custom steps tab, select the custom step card to be updated, and click  **`...`**   **\> Upgrade**.

2. Update the YAML content in the pop\-up panel.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When upgrading custom steps, you must update the version number. The new version number must be greater than the existing version number. Existing steps without a specified version default to version 1.0.0.   </div>
   

3. After the update is complete, click **OK**.


<span id=".5p-l55yL6Ieq5a6a5LmJ5q2l6aqk55qE5YWz6IGU5rWB5rC057q_"></span>
## View pipelines associated with custom steps

View the workspace and pipeline information associated with custom steps by version.


1. On the Custom steps tab, select the target Custom step card, and click  **`...`**   **\> View associated pipeline**, the associated pipeline dialog box appears.

2. Select the target version and workspace name, and the system will display a list of all pipelines in the current workspace that reference this custom step.

3. (Optional) Click the pipeline name to navigate to the details page for the current pipeline.
