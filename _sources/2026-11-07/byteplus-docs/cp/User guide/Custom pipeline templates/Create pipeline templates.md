---
title: "Create pipeline templates"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_pipeline_templates"
---

Code Pipeline provides the capability for custom pipeline templates, allowing users to orchestrate and adapt pipeline templates according to their actual needs to meet their team's specific requirements. Facilitates the development of unified CICD process standards for the team and improves team members' efficiency in configuring pipelines. This article explains how to create Pipeline templates.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Accounts with CPAdminAccess permission can create pipeline templates. Sub\-users can contact the corresponding BytePlus account to be granted this permission. For detailed instructions, refer to [Configure permissions](https://docs.byteplus.com/en/docs/cp/Configure_IAM_user_permissions).


<span id="STQhFxEq"></span>
## Procedure


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp) and, in the left navigation bar, select **Template Marketplace \> Pipeline templates**.

2. On the pipeline templates page, click **Create pipeline template**.

3. On the page for creating custom pipeline templates, configure the pipeline templates according to requirements.

   ### Basic Information    <span id=".5Z-65pys5L-h5oGv"></span>

   * Basic Information

   
   |Configuration Item |Descriptions |
   |---|---|
   |Template constraint type |You can create the following two types of pipeline templates:<br><br><br>* **Constraint template**: Pipelines created using the constraint template do not support subsequent adjustments to any arrangement information within the pipeline, including stage, task, and step arrangement information, build resource pool information, cache directory, and variable information. This is typically used when an enterprise wants to enforce a fixed CICD process, requiring team members to strictly configure pipelines according to pipeline templates.<br><br>* **Flexible template**: Pipelines created using a flexible template can later have their pipeline arrangement freely adjusted, without being restricted by the template. |
   |Name |The name of the custom pipeline template. |
   |Description |Enter remarks for the current pipeline template. This field can be left empty. |
   

   ### Process orchestration    <span id=".5rWB56iL57yW5o6S"></span>

   * Arrange the execution order and specific content of each stage, task, and step in the pipeline. For detailed instructions, refer to [Process orchestration](https://docs.byteplus.com/en/docs/cp/Process_orchestration).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">All required fields for each task and step in the constraint template must be completed.   </div>
   

   * (Optional) Variables used for pipeline orchestration. For detailed instructions, see [Variable management](https://docs.byteplus.com/en/docs/cp/Variable_management).

   ### Cache directory    <span id=".57yT5a2Y55uu5b2V"></span>

   (Optional) Configure the cache directory for the build task. For detailed instructions, see [Cache directory](https://docs.byteplus.com/en/docs/cp/Cache_directory).

4. Click **Save** to complete the creation of the pipeline template.

   After pipeline templates are created successfully, the default status is **enabled**.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

**Use pipeline templates**: Create pipelines using custom pipeline templates. For detailed steps, see [Create pipelines](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Pipelines created using free templates can freely modify their configuration information and are not restricted by the template.</div>


* <div data-tips="true" data-tips-type="tip">Pipelines created using a constraint template support adding code sources, triggers, notification, and configuring advanced settings for tasks. Orchestration information for stages, tasks, and steps, build resource pool information, Cache directory, and variable information are not supported.</div>
