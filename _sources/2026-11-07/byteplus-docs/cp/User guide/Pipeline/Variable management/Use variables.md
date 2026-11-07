---
title: "Use variables"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Use_variables"
---

Referencing variables in the pipeline can improve the flexibility and versatility of the pipeline. This article explains how to use variables in a pipeline.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* The text boxes for each step in the pipeline, including the command execution text box, YAML text box, and Dockerfile text box, all support the use of variables.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The three parameters—step name, output, and image reference—do not support the use of pipeline variables.   </div>
   

* When using variables, combining fixed values, custom variables, and predefined variables is supported. For example: `v1.0-$(DATETIME)`.

* When variables have the same name, the order of precedence is as follows:

   * **Variables within a step**, **custom variables**, and **preset variables** each take effect independently and do not affect one another.

   * Assignment of Dynamic Parameter Value (the value set by code source trigger, scheduled trigger, Webhook trigger, or during manual execution) \> default value of custom variable \> default value of variables with the same name in Pipeline variable groups.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Example 1: Step variables and custom variables have the same name   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>kubectl release</strong> step, the image reference variable is set to <code>image = upstream artifact</code>, while the custom variable in the pipeline is <code>image = userxy2015/ngnix</code>, so the image used in the final <strong>kubectl release</strong> step will reference the upstream artifact. In other steps that involve image references, the image will use <code>userxy2015/ngnix</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Example 2: Name conflict between custom variable and preset variable   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, <code>DATETIME = 20220801</code>, and the preset variable <code>DATETIME = UTC + 0:00</code>; when referenced as <code>$(parameters.DATETIME)</code>, the custom variable 20220801 takes effect, and when referenced as <code>$(DATETIME)</code>, the preset variable takes effect.   </div>
   


<span id=".5byV55So6aKE572u5Y-Y6YeP"></span>
## Reference preset variables


* For SCM\-related preset variables, reference them in the target step of the pipeline using `${preset variable name}`.

* For other predefined variables, in the target step of the pipeline, reference them using the format `$(predefined variable name)`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Quickly copy variables</strong>: Supports copying the full expression of a variable by clicking the copy icon in the <strong>Actions</strong> column on the <strong>Preset Variables</strong> page.</div>


<span id=".5byV55So6Ieq5a6a5LmJ5Y-Y6YeP"></span>
## Reference custom variables


1. Create custom variables in the target pipeline.

2. Reference this variable in the target step of the current pipeline.   

   * The method for referencing environment variables is `${variable}` or `$variable`.

   * The method for referencing a variable is `$(parameters.variable)`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Quickly copy variables</strong>: This feature is supported on the <strong>Custom Variables</strong> page. Click the copy icon in the <strong>Actions</strong> column to copy the full expression of the variable to be used.</div>


<span id=".5byV55So5rWB5rC057q_5Y-Y6YeP57uE"></span>
## Reference pipeline variable groups


1. Create pipeline variable groups.

2. Associate the current pipeline variable group in the target pipeline.

   1. In the pipeline **Process orchestration \> Variables \> Pipeline variable groups** panel, click`+`.

   2. In the pop\-up dialog box, check the target pipeline variable groups.

   3. Click **confirm**.

3. In the current pipeline target step, reference variables using the format `$(parameters.variable)`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Quickly copy variables</strong>: On the <strong>Pipeline variable groups</strong> page, click the variable group you want to use. This will take you to the variable details page. Supports clicking the copy icon in the <strong>Actions</strong> column to copy the complete expression of the variable to be used.</div>


<span id=".56S65L6L"></span>
## Example:

The following uses a Kubernetes image upgrade task, where the target image references a custom dynamic variable, as an example to illustrate how to use variables in a pipeline.


1. Create custom variables in the target pipeline.

   The variable name is image, with the default value set to the image version to be upgraded: `nginx:lastest`. Turn on dynamic settings.

2. Switch to the Process orchestration tab, edit the Kubernetes image upgrade task, and use the newly created variable "image" as the image.

3. After configuring other parameters, click **confirm** to complete the task edit operation.

4. Click **Save** to save the pipeline.

5. Click **Run now**, and in the popup run pipeline panel, set the runtime value of the image variable.

6. Click **Confirm** to run the pipeline. Upgrading the application using different versions of images can be accomplished through a single pipeline.
