---
title: "Custom variables"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Custom_variables"
---

In addition to preset variables, Code Pipeline supports variables in custom pipelines to accommodate more customization scenarios. Before using a custom variable, you must first create a custom variable, and then reference it using the `$(parameters.variable)` format. This section explains how to create custom variables.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

You can define both variables and environment variables as custom variables, and either can be used to pass pipeline parameters. Please select variables or environment variables according to your specific situation.


* **Variables**: A set of predefined key\-value pairs that replace variable placeholders in all step inputs before the pipeline is executed. The referencing method is `$(parameters.key)`.

* **Environment variables**: A set of predefined key\-value pairs that are replaced in the container environment where the pipeline is executed, using Linux's environment variable mechanism. The referencing method is `${key}` or `$key`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Environment variables are not confidential, and their values may be displayed in logs. They are not suitable for storing sensitive information.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A pipeline has been created. For specific operations, refer to [create pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Go to the process orchestration tab of the pipeline.

   1. Log in to [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the target workspace name, and enter the current workspace.

   4. Select **pipeline** in the left navigation bar to enter the pipeline page.

   5. In the pipeline list, select the target pipeline, and click  **`...`**   **\> edit**, go to the process orchestration tab of the current pipeline.

2. Click **Variable**. The variable settings panel will appear.

3. Switch to the custom variables tab, click **add**, and add a new custom variable. Add multiple variables.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Parameter |Enter the name of the custom variable. The name must be unique within the same pipeline. It is recommended to avoid using names that duplicate preset variables. |
   |Type |Select variable type.<br><br><br>* **String**: The variable is a string, and the default value is entered by the user. If not specified, defaults to an empty string.<br><br>* **Single choice**: The variable is a single choice value. The options are entered by the user, and one of the options can be set as the default value. |
   |Description |Enter remarks for the current variable; this field can be left blank. |
   |Privacy |After turning on privacy settings, the default value of the variable will be displayed as `***`. When a variable is sensitive information that you do not want other users to see, for example, an account password, you can turn on privacy settings. Privacy variables do not support modifying the name or default value. |
   |Updates |Should the dynamic settings switch be enabled?<br><br><br>* Turn on dynamic settings to support modifying the running value of the current variable during pipeline execution.<br><br>   * Afterwards, you can set the runtime value of the current variable in the **Run Pipeline** panel.<br><br>   * For automatically triggered pipelines, you can later set the current variable value via the **Dynamic Parameter** parameter in the corresponding **trigger** panel.<br><br>* When dynamic settings are turned off, the pipeline uses the current variable's default value whether triggered manually or automatically. |
   |Environment variable |Set as environment variable?<br><br><br>* Turn on: It is used as an environment variable. To reference it, use `${key}` or `$key`.<br><br>* turn off: is a variable; the reference method is `$(parameters.key)`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Environment variables are not suitable for storing sensitive information.</div><br> |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Privacy settings and dynamic settings are mutually exclusive and cannot be turned on at the same time.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Single choice</strong> variables have dynamic settings turned on by default, allowing you to select the variable's runtime value when running the pipeline.   </div>
   

4. Click **Confirm** to complete the creation of the custom variable.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After a custom variable is created, you can reference it in any step of the pipeline where the variable is needed.   </div>
   

5. Click **Save** to save the pipeline configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After completing the corresponding variable configuration, you can flexibly use the pipeline. When running the pipeline, provide the appropriate value for each variable to accomplish different tasks with a single pipeline.

Take deploying Function Service as an example. After setting the **function ID**`$(parameters.id)` variable, when you run the pipeline, you enter different Function Service IDs to deploy different Function Service using a single pipeline.


1. Obtain the Function Service ID from the Function Service console.

2. Enter the corresponding Function Service ID when running a pipeline in Code Pipeline.
