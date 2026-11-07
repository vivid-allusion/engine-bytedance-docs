---
title: "Delete Project"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/delete_project"
---

With this feature, you can delete projects that are no longer needed.

<span id="_1-约束限制"></span>
## Constraints


* Only Project Administrators can delete projects.

* To prevent accidental deletion, the system automatically checks when deleting a project. If there are enabled tasks under the project, deletion is not allowed.


<span id="990e8594"></span>
## Prerequisites

Projects must be created.

<span id="_2-操作步骤"></span>
## Operation Steps

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When deleting a project, all related content under the project, including bindings with the engine and existing tasks, templates, monitoring, etc., will be deleted and cannot be restored.</div>


* <div data-tips="true" data-tips-type="warning">This action does not delete settings on the engine side (Queue/Storage/Resource/Function); for related operations, proceed to the respective engine side.</div>


1. Log in to the DataLeap Console.

2. Click **Projects** in the left navigation bar to enter the **Project Management** page.

3. Select the **My managed projects** option to display a list of projects managed by you.

4. Click the  **... \> Delete** button in the **Action** column of a project, and one of the following two results will appear.

   * A project deletion window pops up, input the name of the current project to delete, click the **Delete** button to complete the deletion.

      * When there are no Unenabled data development assets under the project, the deletion window is as shown below.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2384191617c54506a42af5654cbb9705~tplv-goo7wpa0wc-image.image) </span>

      * When there are Unenabled data development assets under the project, the deletion window will display a corresponding note, as shown below.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2965cc41d1724d33a2913bb4b2c6fbb2~tplv-goo7wpa0wc-image.image) </span>

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Only when a task has been created and not deployed, or when enabled tasks are closed/stopped, will this deletion prompt appear.         </div>
         

   * A Cannot delete project description window pops up, indicating that there are Enabled data development assets under the project. Click the **Quantity** column of each Enabled data development asset to go to the respective Data Development page, close/stop the assets, and then proceed to delete.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/994c1f38949f426984c9ca83a8735326~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-操作结果"></span>
## Operation Result


* Deleted projects are removed directly from the Project Management list and cannot be restored. Also, if there are tasks, templates, monitoring, etc., under the project, they will also be deleted and cannot be restored.

* Other product pages such as Data Development and Data Service no longer display information about deleted projects.
