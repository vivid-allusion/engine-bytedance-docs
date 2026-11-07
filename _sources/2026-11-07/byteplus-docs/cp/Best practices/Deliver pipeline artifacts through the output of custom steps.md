---
title: "Deliver pipeline artifacts through the output of custom steps"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Deliver_pipeline_artifacts_through_the_output_of_custom_steps"
---

This article introduces how to define output artifacts through the output of custom steps, and how to reference this artifact in downstream tasks or steps.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The workspace has been created. For detailed instructions, refer to [Create a workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

* The YAML content for custom steps is ready. For details, refer to [Custom steps YAML rules](https://docs.byteplus.com/en/docs/cp/Step_YAML_rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu66Ieq5a6a5LmJ5q2l6aqk"></span>
### Step 1: Create custom steps

Define the YAML content of custom steps, and upload it to the Code Pipeline console.


1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp), and in the left navigation bar, select **Template Marketplace \> Step Template**.

2. On the step template page, click **create custom steps**. The create custom steps panel will pop up.

3. In the text box on the left, write the step content according to the YAML requirements for custom steps.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Artifacts must be defined via outputs, passed in the script, and written to the <code>/tekton/results/<artifact_name>_${CP_STEP_NAME}</code> file.    </div>
   

   The YAML example used in this document is as follows:

   ```yaml
   # Custom step name, required field. Supports uppercase and lowercase English letters, numbers, and the hyphen '-', with a length of 2 to 50 characters. Duplicate names are not allowed.
   step: test-output
   # Custom steps version, required field. The format must be x.y.z, and x, y, and z must each be integers in the range [0, 100].
   version: 1.0.0
   # Display name of the custom step, required field. Supports Chinese and English letters (both uppercase and lowercase), numbers, and hyphen (-); length: 2 to 50 characters. Displayed as the step name; cannot be empty and must be unique.
   displayName:  Custom Step Output Artifact
   # Custom steps description, optional. Up to 200 characters. Supports Chinese characters, English letters (both uppercase and lowercase), and special characters.
   description:  Specify multiple artifacts to be output through the `outputs` field, and allow downstream tasks/steps to reference them.
   # Category, required field. Currently, only the following categories are supported: [构建] Build, [测试] Test, [部署] Deploy, [镜像仓库] Registry, [命令执行] Command, and [其他] Other.
   category: Other
   # Runtime image, required field. Supports public and private images.
   image: xxx.cr.volces.com/ns/busybox:latest
   # Define the input information for the step. Optional. Supports configuring multiple input parameters for steps.
   inputs:
     - name: arg1
       displayName: arg1
       type: string
       required: true
       uiConfig:
         type: CodeEditor
     - name: arg2
       displayName: arg2
       type: string
       required: true
       uiConfig:
         type: CodeEditor
   
   # Define the output information for the step. Optional.
   outputs: 
     - name: result1
       displayName: result1
       type: string
     - name: result2
       displayName: result2
       type: string
   
   # When running the script, required fields cannot be empty. Functions similarly to ENTRYPOINT in a Dockerfile and is used to specify the program and parameters that the container runs on startup.
   script: |
     #  Obtain the input of two arguments
     result1='$(inputs.arg1)'
     result2='$(inputs.arg2)'
     #  Artifacts need to be transferred via files; therefore, in the running script, the artifact information must be written into a file under a fixed directory.
     # The fixed directory to write to is：/tekton/results/
     #  Each artifact must have its content written to a separate file in the directory, with the filename formatted as: <name>_${CP_STEP_NAME}
     # As shown below, write the content of the first artifact Result1 into the file /tekton/results/result1_${CP_STEP_NAME}
     echo -n "$result1" > /tekton/results/result1_${CP_STEP_NAME}
     # As shown below, write the content of the second artifact Result2 into the file /tekton/results/result2_${CP_STEP_NAME}
     echo -n "$result2" > /tekton/results/result2_${CP_STEP_NAME}
   ```
   

4. After you finish writing, click **confirm**. Successfully created custom steps will be displayed under the corresponding category.


<span id=".5q2l6aqk5LqM77ya57yW5o6S5rWB5rC057q_"></span>
### Step 2: Orchestrate pipeline

By arranging a sequence of custom steps and command execution tasks in a pipeline, you can reference the output of upstream custom steps in downstream command execution tasks.


1. [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

2. Configure custom steps.

   1. [Add Custom steps](https://docs.byteplus.com/en/docs/cp/Use_custom_steps#.5q2l6aqk5LiA77ya5re75Yqg6Ieq5a6a5LmJ5q2l6aqk).

   2. Enter the parameter information for the custom steps. In this example, parameter 1 input: `hello arg1`; parameter 2 input: `hello arg2`.

   3. Copy the output expression of custom steps from the task output location for later use.

3. Configure a command execution task

   1. Add a stage, and add a command execution task.

   2. Enter the command to execute: Use the expression copied above to output information about the two upstream artifacts.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The format for referencing upstream products using an expression is: <code>$(your product expression)</code>.      </div>
      

4. Click **Save** to save the pipeline orchestration.


<span id=".5q2l6aqk5LiJ77ya6L-Q6KGM5rWB5rC057q_"></span>
### Step 3: Run the pipeline


1. On the current pipeline details page, click **Run now**.

2. In the pop\-up confirmation dialog box, click **Confirm.**  The pipeline starts running, and the system navigates to the details page of the current pipeline.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

Based on the current pipeline configuration, the following information is expected to be output:

```plain
The first artifact from the upstream is:
hello arg1
The second artifact from the upstream is:
hello arg2
```


View the pipeline run results. By checking the log information from the command execution task, you can see that the results meet expectations.

&nbsp;
