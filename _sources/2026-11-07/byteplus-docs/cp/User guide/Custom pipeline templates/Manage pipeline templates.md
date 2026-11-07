---
title: "Manage pipeline templates"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manage_pipeline_templates"
---

This article introduces actions for managing custom pipeline templates, including how to edit pipeline templates, delete pipeline templates, enable or disable pipeline templates, synchronize pipeline templates, and other related actions.

<span id=".5ZCv55SoLeemgeeUqOa1geawtOe6v-aooeadvw=="></span>
## Enable/disable pipeline templates

When creating a pipeline, only enabled pipeline templates can be used.


1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Template Market \> Pipeline templates**.

3. On the Pipeline templates page, click **Custom pipelines**, and switch to the **Custom pipelines** tab.

4. Select the pipeline template card that you want to enable or disable, then click the switch in the upper right corner to enable or disable the current template.


<span id=".57yW6L6R5rWB5rC057q_5qih5p2_"></span>
## Edit pipeline template

Modify the content of pipeline templates as needed. Modification of the constraint template type is not supported.


1. On the **Custom pipelines** tab, select the pipeline template to be modified, and click  **`...`** . \> edit.

2. On the Edit Pipeline Templates page, modify each parameter as needed.

3. After making changes, click **Save**.


<span id=".5ZCM5q2l6Iez5rWB5rC057q_77yI5LuF57qm5p2f5qih5p2_77yJ"></span>
## Sync to pipeline (templates only)

For constraint templates, after the update is completed, the status is **Pending synchronization**. You can synchronize the updated pipeline configuration to all pipelines that use this template, ensuring that pipeline orchestration remains consistent with the constraint template.


1. On the **Custom pipelines** tab, select an unsynchronized constraint template, and click  **`...`**  **Sync to pipeline.** 

2. In the pop\-up confirmation dialog, after confirming the pipeline information to be used for this template, click **Confirm**.

   Modification of pipeline templates is not allowed during synchronization. After synchronization is complete, the status of pipeline templates will become **Synchronized**.


<span id=".5Yig6Zmk5rWB5rC057q_5qih5p2_"></span>
## Delete pipeline templates

Support deleting pipeline templates that are no longer in use. After you delete a pipeline template, pipelines that are already using the current template are not affected.


1. On the **Custom pipelines** tab, select the pipeline templates to delete, and click  **`...`**   **\> delete**。

2. In the pop\-up confirmation dialog, confirm the pipeline template information. After confirming that there are no errors, click **delete**.
