---
title: "Synchronization Settings"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/synchronization_setting"
---

Due to differences such as project members and file directories between the target and source projects, to avoid frequent modifications after synchronization to the target project, this feature allows setting default synchronization rules, which developers will use by default during synchronization.

<span id="_1-约束限制"></span>
## Use Scenarios

Synchronization function is mainly suitable for the following scenarios:


* Inter\-regional/inter\-project task code copying, specifically including:

   * In the test environment, after code development is validated, it is necessary to manually copy the completed code to the production environment for deployment and posting.

   * Create two projects in the same environment, one for code development and one for production deployment. Manually copy the code from the development project to the production project and deploy it.

   * Inter\-regional business requires code deployment in multiple locations, such as deploying task codes from North China in East China in bulk.

* When initializing the project, batch create tasks, specifically including:

   * After deploying the new region, you need to migrate or copy the task code, batch create under the new project, and complete project initialization.


<span id="5ff5bf05"></span>
## Limitations

Only project administrators can configure synchronization.

<span id="_2-前提条件"></span>
## Prerequisites

A project has been created.

<span id="_3-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap Console.

2. Click on **Projects** in the left navigation bar to enter the **Project Management** page.

3. Select the **My managed projects** option to display a list of projects you manage.

4. Click any button in the **Action** column of the project list you want to manage to enter the **Project Console**.

5. Click on the **Synchronization** in the left navigation bar to enter the Synchronization settings page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f1af965d857424ab8c2a2671fa62c6b~tplv-goo7wpa0wc-image.image) </span>

6. Create a target project that allows synchronization of entities in this project.

   1. Click the **Create project** button to enter the project configuration page and set the target project information.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cae2234fc04342f4a3ef7068f7b9c311~tplv-goo7wpa0wc-image.image) </span>

      The parameter description is shown in the following table. Parameters marked with an \* are required, while those without an \* are optional.

      
      |Parameters |Description |
      |---|---|
      |\*Target Area/Project |To synchronize the target project entity of this project, you can select the activated areas and created projects from the dropdown menu in order.<br><br><br>1. Target region: Supports options Southeast Asia Pacific (Johor).<br><br>2. Target project: Projects already created in the selected area.<br><br><br>Multiple target areas/projects can be configured. By clicking the **new Project** button on the row where the target project is located, you can add new target projects. |
      |\*Sync Content |Currently, only tasks are supported.<br><br>The settings for synchronization rules are as follows:<br><br><br>* Task Mapping: Priority task ID mapping; if no specific task ID is provided, use the same name mapping.<br><br>   Click the **Task ID Mapping Details** button to edit the mapping relationship. When synchronizing tasks and task dependencies, the mappings defined here will be used to locate the corresponding tasks.<br><br>* Sync Mode: Supports three options: default, update only, and create only.<br><br>   * Default: Update if mapping exists; otherwise, create.<br><br>   * Update Only: Only updates tasks that can be mapped; tasks without mappings are not synchronized.<br><br>   * Create Only: Only creates new tasks; tasks that can be mapped are not synchronized.<br><br>* After Synchronization: Supports three options: keep in draft, auto commit, and auto publish.<br><br>   * Keep Draft: Generates a draft version for the task.<br><br>   * Auto Commit: Automatically commits the task and generates a submitted version.<br><br>   * Auto Publish: Auto publish tasks. |
      |New Settings |For new tasks, you can set the directory, owner, resource group, and engine instance in the target project.<br><br><br>* Directory for new tasks: Supports "Original Directory" or "Specify Directory".<br><br>   * When  **"Original Directory"**  is selected, if no directory exists, a new one will be automatically created in the target project.<br><br>   * When  **"Specify Directory"**  is selected, you need to select a directory, with dropdown options available from directories in the target project.<br><br>* Owner for new tasks: Supported options are "Default" or "Designee".<br><br>   * When  **"Default"**  is chosen, the system automatically retains the original owner after syncing to the target project. If the original owner is not a member of the target project, the project owner is set as the new owner.<br><br>   * When choosing **designee**, you must choose an owner yourself; after entering the account keyword, you can select from the dropdown.<br><br>* Scheduling resource group for new tasks<br><br>   * Tasks are scheduled in this project's resource group: It automatically shows the scheduling resource groups supported by this project.<br><br>   * Sync to the target project's scheduling resource group: You can choose from the scheduling resource groups already added to the target project in the dropdown.<br><br>* Compute resource group for new task<br><br>   * Tasks in this project's computing resource group: It automatically displays the computing resource groups supported by this project.<br><br>   * Sync to the target project's compute resource group: You can choose from the computing resource groups already added to the target project in the dropdown.<br><br>* Data Transmission Service resource group for newly created tasks<br><br>   * The task is in the Data Transmission Service resource group of this project: It automatically shows the data integration resource groups supported by this project.<br><br>   * Sync to the Data Transmission Service resource group of the target project: You can select from the data integration resource groups already added to the target project in the dropdown.<br><br>* Engine instance for new task<br><br>   * Engine type: Automatically displays the engine type bound to this project.<br><br>   * Task in the engine instance of this project: Automatically displays the engine instance bound to this project.<br><br>   * Engine instance synced to target project: Dropdown to select the engine instance with the same name bound to the target project.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">About resource groups and engine instances, for synchronous tasks that use a resource group or are linked to a related engine instance, it is necessary to select the corresponding resource information in the target project, and other unrelated items can be left empty.</div><br> |
      |Update Settings |For the update task, you can set the range of the update, with the following options available for multiple selection:<br><br><br>* Code (without set statement): Default selected, not editable.<br><br>* Code (Set statement)<br><br>* Basic Info (Priority, Queue, etc.)<br><br>* Scheduling attribute (Scheduling interval, earliest Backfill time, auto\-rerun, etc.)<br><br>* Dependencies (Upstream tasks, Self\-dependent)<br><br>* Input and output parameters |
      

   2. Click the **OK** button to complete the synchronization settings.

7. Click the **Synchronization** switch button to turn on synchronization and enable this function in this project.


<span id="_4-后续操作"></span>
## Subsequent Operations

After the synchronization settings are complete, you can go to the **Publish Center** to perform task synchronization operations.
