---
title: "Pipeline variable groups"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_variable_groups"
---

Pipeline variable groups are a group of user\-defined pipeline global variables. Pipeline variable groups can be used across workspaces or pipelines, allowing users to avoid repeatedly defining and maintaining the same variables in multiple pipelines, improve the reusability of variables, and reduce configuration costs. This document introduces the related operations for pipeline variable groups.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Accounts with the CPAdminAccess permission can create, edit, and delete pipeline variable groups.</div>


<span id=".5Yib5bu65rWB5rC057q_5Y-Y6YeP57uE"></span>
## Create pipeline variable groups


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global configurations \> Pipeline variable groups**.

3. On the pipeline variable groups page, click **Create pipeline variable groups**.

4. On the Create Variable Group page, fill in the following parameters as required.

   * Variable group configurations

   
   |Configuration Item |Descriptions |
   |---|---|
   |Variable group name |Duplicate names are allowed for custom variable groups. The variable group name is used to filter variable groups when referenced by a pipeline. |
   |Variable group ID |Enter the variable group ID. Duplicate IDs are not allowed under the same account. The system has provided a default ID, which can be modified.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The variable group ID is the unique identifier for the variable group. It cannot be changed after creation.</div><br> |
   |Description |Enter remarks information for the variable group; this field can be left blank. |
   |Sharing scope |Select the shared workspace scope for the current variable group. Only pipelines in the selected workspace can be associated with this variable group. |
   |Variable configuration |Configure the variables of the current variable group. Supports adding up to 100 variables.<br><br>Click `+ Add variable`, and in the 'Add variable' dialog that appears, configure the variables as required in the table below. |
   

   * Variable configuration

   
   |Configuration Item |Descriptions |
   |---|---|
   |Parameter |Enter the name of the custom variable. The name must be unique within the same pipeline. It is recommended to avoid using names that conflict with predefined variables. |
   |Type |Select variable types.<br><br><br>* **String**: The variable is a string, and the user enters the default value.<br><br>* **Single choice**: The variable is a single\-choice value, with options entered by the user. One of the options can be set as the default value. |
   |Description |Enter remarks for the current variable. This field may be left blank. |
   |Privacy |After you turn on privacy settings, the default value of the variable will be displayed as `***`. When a variable contains sensitive information that you do not want other users to see (for example, account passwords), you can turn on privacy settings. Privacy variables do not support modifying the name or default value. |
   |Updates |Do you want to enable the dynamic settings switch?<br><br><br>* Turn on dynamic settings to allow modification of the current variable's runtime value during pipeline execution.<br><br>   * For manually triggered pipelines, you can set the Value of the current variable in the **Run Pipeline** panel afterwards.<br><br>   * For automatically triggered pipelines, you can later set the runtime Value of the current variable in the corresponding **trigger** panel via the **Dynamic Parameter** parameter.<br><br>* When dynamic settings are turned off, the pipeline uses the current variable's default value, regardless of whether it is triggered manually or automatically. |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Privacy settings and activity settings are mutually exclusive and cannot be turned on at the same time.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Single choice</strong> Variables have dynamic settings turned on by default, allowing you to select the variable's runtime value when running the pipeline.   </div>
   

5. After all variables have been configured, click **confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the variable group is created, you can associate the variable group on the variable page of the target pipeline. After associating the variable group, you can reference its variables in each step of the pipeline.   </div>
   

<span id=".5p-l55yL5Y-Y6YeP57uE"></span>
## View variable groups

Supports viewing the details of variables in variable groups and quickly adding, modifying, or deleting variables.


1. On the Pipeline variable groups page, you can view information about all variable groups.

2. Click the target variable group name to view its details.

3. On the variable group details page, you can quickly add, modify, or delete variables.


<span id=".57yW6L6R5Y-Y6YeP57uE"></span>
## Edit variable groups

You can modify the variable group name, description, and the scope of workspaces with which it is shared. You can also add, edit, or delete variables in the variable group.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please exercise caution when modifying the scope of the shared workspace. Deleting a workspace will cause pipelines associated with variable groups in the workspace to run abnormally.</div>



1. On the Pipeline variable groups page, select the target variable group, and click **edit** in the Actions column.

2. On the edit variable group page, modify the corresponding parameters as needed.

3. Click **confirm** to complete the modification.


<span id=".5Yig6Zmk5Y-Y6YeP57uE"></span>
## Delete variable groups

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Before deleting the variable group, please first disassociate any pipelines associated with it.</div>


* <div data-tips="true" data-tips-type="danger">Deleting a variable group will cause pipelines that are already associated with it to run abnormally. Please proceed with caution!</div>


1. On the pipeline variable groups page, select the target variable group, and click **delete** in the Actions column.

2. In the pop\-up secondary confirmation dialog, enter the variable group name.

3. Click **confirm** to delete the variable group.
