---
title: "Configure ECS image build pipeline templates"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Configure_ECS_image_build_pipeline_templates"
---

CP has added ECS image build pipeline templates, enabling end\-to\-end completion of the full image creation process: covering ECS instance creation, dependency installation, validation, and image testing. Once the process is complete, it also supports releasing instances, greatly simplifying operations and improving image build efficiency and security.

<span id="Uq08lDaf"></span>
## Scenario introduction

The following ECS image build pipeline templates are currently supported:


* **ECS image build:**  No code source integration, suitable for scenarios without self\-developed code, or for simple image creation based on an existing Dockerfile or customization from a base image.

* **ECS image build (code source integration):**  Includes code source integration, suitable for self\-developed application DevOps continuous integration and delivery scenarios with frequent code iterations, version tracking, and compliance auditing requirements.


<span id="lOIkECbt"></span>
## Prerequisites


* A VPC has been created. For details, refer to [Create VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* A subnet has been created. For details, refer to [Create subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

* A security group has been created. For details, refer to [Create security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* (Optional) When using the **ECS image build (code source integration)**  template, you need to create a code source first. For details, refer to [Create code source](https://docs.byteplus.com/en/docs/cp/Create_a_code_source).


<span id="PuLDtVMj"></span>
## Procedure

Compared to the method without code source integration, the code source integration method adds a **code source synchronization** step. You also need to configure the **install dependencies** and **dependency test** nodes to download artifacts from the upstream **code source synchronization** download links.


* **ECS image build**: Create pipeline \> Create ECS instance \> Install dependencies \> Dependency test \> ECS image build \> Delete ECS instance

* **ECS image build (code source integration)** : Create pipeline \> Create ECS instance \> Code source synchronization \> Install dependencies \> Dependency test \> ECS image build \> Delete ECS instance


<span id="apYETIjI"></span>
## Procedure

<span id="GGOGivcS"></span>
### Step 1: Create a pipeline


1. Log in to the [CP Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace**. On the workspace page, click the target workspace name to enter the current workspace.

3. Click **Create pipeline**. On the **Select pipeline template** page, select **Others** \> **ECS image build** or **ECS image build (code source integration)** .

4. Click **Create**.


<span id="frJmUU57"></span>
### Step 2: Create ECS instance

For detailed actions, refer to [ECS instance creation](https://docs.byteplus.com/en/docs/cp/Create_ECS_instance).

<span id="kXg4ucno"></span>
### Step 3: Code source synchronization

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This step is required only when using the <strong>ECS image build (code source integration) template</strong>.</div>


Synchronize the code source, which integrates installation dependencies and test code, to TOS. For details, refer to [TOS upload](https://docs.byteplus.com/en/docs/cp/TOS_upload).

<span id="gH8W2iI9"></span>
### Step 4: Install dependencies

The following introduces the parameters of this built\-in task.


* **Job name**

   Custom job name.

* **Upstream task**

   Show the name of the upstream sequential task for the current task.

* **Artifact download**

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This parameter is required only when using the <strong>ECS image build (code source integration) template</strong>.   </div>
   

   Click **Add** on the right to configure download links for the upstream artifact **Code source synchronization**.

* **Task configuration**

   
   |Parameter |Description |
   |---|---|
   |Region |Select the ECS instance region, which must be consistent with the region selected in **ECS instance creation**. |
   |ECS instance |Select **Upstream artifact**, and select the ECS instance created by the upstream built\-in task **ECS instance creation**. |
   |Execution path |Custom path for executing dependency installation commands. |
   |Execution user |Specify a user in the instance to execute the command.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Please specify a user with permission to execute commands. It is recommended to avoid using <code>root</code> user to reduce security risks.</div><br> |
   |Timeout duration |Set the timeout period for command execution on the instance. If execution times out, the task will be considered to have failed on the instance. |
   |Command type |Select the command type to execute. Currently, **Shell** and **Python** are supported. |
   |Command content |Enter the script to install dependencies in the ECS instance. |
   

* **Task output**

   No

* **Advanced settings**

   * [Webhook notification](https://docs.byteplus.com/en/docs/cp/Webhook_notification): Supports pushing task\-level messages via Webhook and Larkbot, helping you stay updated on task status.


<span id="g8EfbKHP"></span>
### Step 5: Test dependencies

The parameter configuration for the **Test dependencies** task is the same as the parameter configuration for the **Install dependencies** task by default. Manual modification is supported if adjustment is needed.

<span id="0ZRk0LKo"></span>
### Step 6: Create ECS image

For action details, refer to [ECS image creation](https://docs.byteplus.com/en/docs/cp/ECS_image_creation).

<span id="TSobgqXb"></span>
### Step 7: Release ECS instance

For action details, refer to [ECS instance deletion](https://docs.byteplus.com/en/docs/cp/Delete_ECS_instance).

<span id="HfFHD93s"></span>
## What to do next


* [Run pipeline](https://docs.byteplus.com/en/docs/cp/Run_a_pipeline)

* [Manage pipeline](https://docs.byteplus.com/en/docs/cp/Pipeline_management)
