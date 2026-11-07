---
title: "Use custom steps"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Use_custom_steps"
---

After custom steps are uploaded successfully, they can be used in the target pipeline. This article explains how to use custom steps in a pipeline.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

This article uses the [YAML example](https://docs.byteplus.com/en/docs/cp/Create_custom_steps) from the process of developing Custom steps to demonstrate how to use Custom steps in a pipeline and how to use pipeline variables within a step, showcasing more advanced usage scenarios.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Custom steps have been created. For detailed instructions, see [Custom steps](https://docs.byteplus.com/en/docs/cp/Create_custom_steps).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5re75Yqg6Ieq5a6a5LmJ5q2l6aqk"></span>
### Step 1: Add custom steps

Create or edit a pipeline, add the current custom step, and fill in the step parameters.


1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace**. On the workspace page, click the name of the target workspace to enter the current workspace.

3. Create or edit a pipeline, then go to the pipeline process orchestration page.

4. Click ➕ to add a stage.

5. Click **add task** to enter the task editing panel.

6. Click **Add step**, select **Custom steps**, and then select the custom step created in the prerequisites.

7. Fill in the parameters for the current step as required. After completing the form, click **OK**.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Step name |This example keeps the default settings unchanged. |
   |Execute custom commands |This example adds the following command to the default commands.`b`Pipeline dynamic variables set for this example.<br><br>```shell```<br>```echo from front $(parameters.b)```<br> |
   |Variables |As indicated by the YAML file of the current custom step, the script for the current step will reference and output this parameter. In this example, the parameter is set to the variable a, so the expected output of the step is the value of a.<br><br>This example is set to `$(parameters.a)`. |
   |Skip on failure |This configuration is a system configuration. If you want subsequent pipeline tasks to continue running even if the current step fails, you can enable this switch. This example is not enabled. |
   

8. Click **Save** to save the pipeline configuration.


<span id=".5q2l6aqk5LqM77ya6L-Q6KGM5rWB5rC057q_"></span>
### Step 2: Run the pipeline


1. In the pipeline list, select the pipeline created in Step 1, and click **Run** in the **Actions** column. The **Run Pipeline** dialog box will appear.

   * Set the runtime value of dynamic variable b to 1000 in this example.

   * Operation instructions: Optional. This example is left blank.

2. Click **OK** to start the pipeline. The system redirects to the details page for the current pipeline.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

Based on the current custom step YAML example and step parameter configuration, the following information will be output:

```text
hello world
from front 1000
ENV：10
PIPELINE_ID：xxxx
DATETIME：xxxx
```


View the pipeline run results. The log information shows that the results meet expectations.
