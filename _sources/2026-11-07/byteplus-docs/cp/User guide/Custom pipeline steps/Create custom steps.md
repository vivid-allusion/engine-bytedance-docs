---
title: "Create custom steps"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_custom_steps"
---

To meet the personalization needs of different enterprises and fully leverage team creativity, Code Pipeline has introduced the capability for custom steps. This enables team members to package internal tools that they are familiar with and find easy to use as custom steps, thereby improving business delivery efficiency. This article explains how to create custom steps.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

A custom step consists of a YAML description file. The YAML file contains basic information about custom steps, step input parameters, step output parameters, the step execution script (script), and the step image (image). When running Custom steps, the pipeline creates a group of Pods based on the current YAML and executes a script task.

The following is an example of a custom steps YAML file used in this document. You can quickly adapt this template—based on the version used for our team—to create custom steps suitable for your own team.

```yaml
#   Custom step name (required field). Supports uppercase/lowercase English letters, numbers, and hyphens ("-"); length ranges from 2 to 50 characters, and duplicate names are not allowed.
step: v2-custom-step
#   Custom step version (required field). It must follow the format x.y.z, where x, y, and z are all integers in the range [0, 100].
version: 1.0.0
   Custom step name(required field). It supports uppercase/lowercase Chinese and English letters, numbers, and hyphens ("-"); the length ranges from 2 to 50 characters. It is used for step name display, and cannot be empty or duplicated.
displayName: custom step v2-demo-doc
# Custom steps description (optional). Up to 200 characters. Supports Chinese and English, including English uppercase and lowercase letters and special characters.
description: custom step v2-demo-doc
# Category, required field. Currently, only the following categories are supported: [构建] Build, [测试] Test, [部署] Deploy, [镜像仓库] Registry, [命令执行] Command, and [其他] Other.
category: Other
# Runtime image, required field. Supports public images and private images. You must configure the access credentials with the imageCredential parameter for private images.
image: xxx.cr.volces.com/ns/busybox:latest
# Credential information for pulling private images; optional. The following uses the BytePlus image repository as an example.
imageCredential:
# Image repository URL. You only need to enter the host address.
  registry: xxx.cr.volces.com
# Image repository username.
  username: xxx@1400******
# Image repository access password; supports permanent and temporary passwords. Caution: Temporary passwords have a validity period. After expiration, you cannot pull private images normally. When the frontend displays the custom steps YAML, passwords are masked.
  password: xxxxxxxxx
# Run the script
Required fields cannot be empty. Functions similarly to ENTRYPOINT in a Dockerfile, and is used to specify the container's startup program and parameters.
# Step input parameters can be set by using export xxx=$(inputs.KEY). Caution: Ensure that the KEY value matches the value of inputs.name; otherwise, you will not be able to successfully reference the Step input parameter.
# You can inject pipeline preset variables by using export xxx=$(preset variable name).
script: |
# Examples of referencing input configuration parameters of custom steps. Obtain the settings command and execute it. Example of referencing configuration parameters in a custom step's input. Retrieve the set command and execute it.
  $(inputs.cmd)
# Example of referencing input parameters for custom steps Obtain the value of the parameter and output it. Example of referencing configuration parameters in a custom step's input. Retrieve the value of the configuration item and output it.
  export ENV=$(inputs.pipeline-env)
  echo "ENV：$ENV"
#   Example of referencing the pipeline's preset variables. Print the pipeline ID.
  echo "PIPELINE_ID：$(PIPELINE_ID)"
  Example of referencing the pipeline's preset variables. Print the pipeline execution time.
  echo "DATETIME：$(DATETIME)"
# Define input information for the step (optional). Supports the configuration of input parameters for multiple steps.
inputs:
    # Field name, required field. Supports uppercase and lowercase English letters, numbers, and hyphens; length must be between 2 and 50 characters; duplicate names are not allowed.
  - name: cmd
    # Field display name, required field. Parameter names can contain uppercase and lowercase Chinese and English letters, numbers, and hyphens ('-'), and must be 2 to 50 characters long. Each name must be unique and cannot be empty.
    displayName: Execute a custom command
    description: Execute a custom command
    # Field type (required field).
    type: string
    # Field default value, optional field.
    defaultValue: echo hello world
    # Whether the field is required, required field. When set to true, a small red asterisk will appear before fields on the step configuration page, and it will validate whether the fields have been filled in when saving.
    required: true
    # Field configuration style.
    uiConfig:
      type: CodeEditor
  - name: pipeline-env
    displayName: Variables
    description: Variables
    type: string
    defaultValue:
    required: true
    uiConfig:
      type: Input
# Define the output information for the step. Optional.
# This example does not use outputs.
# outputs:
#   - name: xxx
#     displayName: xxx
#     type: string#   Custom step name (required field). Supports uppercase/lowercase English letters, numbers, and hyphens ("-"); length ranges from 2 to 50 characters, and duplicate names are not allowed.
step: v2-custom-step
#   Custom step version (required field). It must follow the format x.y.z, where x, y, and z are all integers in the range [0, 100].
version: 1.0.0
   Custom step name(required field). It supports uppercase/lowercase Chinese and English letters, numbers, and hyphens ("-"); the length ranges from 2 to 50 characters. It is used for step name display, and cannot be empty or duplicated.
displayName: custom step v2-demo-doc
# Custom steps description (optional). Up to 200 characters. Supports Chinese and English, including English uppercase and lowercase letters and special characters.
description: custom step v2-demo-doc
# Category, required field. Currently, only the following categories are supported: [构建] Build, [测试] Test, [部署] Deploy, [镜像仓库] Registry, [命令执行] Command, and [其他] Other.
category: Other
# Runtime image, required field. Supports public images and private images. You must configure the access credentials with the imageCredential parameter for private images.
image: xxx.cr.volces.com/ns/busybox:latest
# Credential information for pulling private images; optional. The following uses the BytePlus image repository as an example.
imageCredential:
# Image repository URL. You only need to enter the host address.
  registry: xxx.cr.volces.com
# Image repository username.
  username: xxx@1400******
# Image repository access password; supports permanent and temporary passwords. Caution: Temporary passwords have a validity period. After expiration, you cannot pull private images normally. When the frontend displays the custom steps YAML, passwords are masked.
  password: xxxxxxxxx
# Run the script
Required fields cannot be empty. Functions similarly to ENTRYPOINT in a Dockerfile, and is used to specify the container's startup program and parameters.
# Step input parameters can be set by using export xxx=$(inputs.KEY). Caution: Ensure that the KEY value matches the value of inputs.name; otherwise, you will not be able to successfully reference the Step input parameter.
# You can inject pipeline preset variables by using export xxx=$(preset variable name).
script: |
# Examples of referencing input configuration parameters of custom steps. Obtain the settings command and execute it. Example of referencing configuration parameters in a custom step's input. Retrieve the set command and execute it.
  $(inputs.cmd)
# Example of referencing input parameters for custom steps Obtain the value of the parameter and output it. Example of referencing configuration parameters in a custom step's input. Retrieve the value of the configuration item and output it.
  export ENV=$(inputs.pipeline-env)
  echo "ENV：$ENV"
#   Example of referencing the pipeline's preset variables. Print the pipeline ID.
  echo "PIPELINE_ID：$(PIPELINE_ID)"
  Example of referencing the pipeline's preset variables. Print the pipeline execution time.
  echo "DATETIME：$(DATETIME)"
# Define input information for the step (optional). Supports the configuration of input parameters for multiple steps.
inputs:
    # Field name, required field. Supports uppercase and lowercase English letters, numbers, and hyphens; length must be between 2 and 50 characters; duplicate names are not allowed.
  - name: cmd
    # Field display name, required field. Parameter names can contain uppercase and lowercase Chinese and English letters, numbers, and hyphens ('-'), and must be 2 to 50 characters long. Each name must be unique and cannot be empty.
    displayName: Execute a custom command
    description: Execute a custom command
    # Field type (required field).
    type: string
    # Field default value, optional field.
    defaultValue: echo hello world
    # Whether the field is required, required field. When set to true, a small red asterisk will appear before fields on the step configuration page, and it will validate whether the fields have been filled in when saving.
    required: true
    # Field configuration style.
    uiConfig:
      type: CodeEditor
  - name: pipeline-env
    displayName: Variables
    description: Variables
    type: string
    defaultValue:
    required: true
    uiConfig:
      type: Input
# Define the output information for the step. Optional.
# This example does not use outputs.
# outputs:
#   - name: xxx
#     displayName: xxx
#     type: string
```


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Docker images for use by custom steps are ready. It is recommended to upload to the BytePlus image repository. For operations related to uploading to the BytePlus image repository, refer to [Push and pull images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Accounts with CPAdminAccess permission can create custom steps. IAM users can contact the corresponding BytePlus root user to be granted this permission. For specific operations, see [Configure permissions](https://docs.byteplus.com/en/docs/cp/Configure_IAM_user_permissions).

* By configuring the image access credentials (imageCredential) in the YAML file, custom steps can use private images. If you have higher requirements for image security, we recommend using the following solutions.

   * <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Solution introduction:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Upload the built custom step image to the BytePlus private image repository. You can refer to <a href="https://docs.byteplus.com/en/docs/cr/push-and-pull-images">Push and Pull Images</a> for specific operations.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Install the passwordless image pull component in Vital Kubernetes Engine, and set the private image repository to allow passwordless pulls. For specific operations, refer to <a href="https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2">Install the password\-free component</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Use Vital Kubernetes Engine clusters as a private resource pool to run custom pipeline steps. For specific operations, refer to <a href="https://docs.byteplus.com/en/docs/6461/1251518">Create a private resource pool</a>.   </div>
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp), and in the left navigation pane, select **Template Marketplace \> Step Template**.

2. On the step template page, click **Create custom steps**. The Create custom steps panel appears.

3. In the text box on the left, write the step content according to the YAML requirements for custom steps.

4. After you finish writing, click **confirm**.

   Custom steps that are successfully created will be displayed under the corresponding category.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After custom steps are created successfully, team members can use them in the pipeline. For specific operations, refer to [Use custom steps](https://docs.byteplus.com/en/docs/cp/Use_custom_steps).
