---
title: "Template Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/template_management"
---

Project templates are primarily used for unified settings and batch modifications of task execution queues, priorities, and parameters. Project templates created through this feature can be applied to the EMR Serverless Spark SQL tasks under the project, enabling batch settings of EMR Serverless Spark SQL task queues, priorities, or parameters.

<span id="84183b24"></span>
## Limitations

Only Project Administrators can configure template information.

<span id="a0cebcbf"></span>
## Operation Steps


1. Log in to the DataLeap Console.

2. Click on **Projects** in the left navigation panel to enter the project list display page.

3. Click any button in the **Action** column of the project you want to configure to enter the relevant page.

4. Click on the **Template** in the left navigation bar to enter the template management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2030e10cd9ba42f99b7f76ac5bff9451~tplv-goo7wpa0wc-image.image) </span>

5. The following actions can be performed:

   * Create a new template

      Click on the **New Template** button, set the template parameters in the pop\-up window, and click the **OK** button to complete the creation.

      
      |Parameters |Description |
      |---|---|
      |\*Template Name |The name of the project template can be set by yourself. |
      |\*Template Type |Only supports **EMR Serverless Spark SQL**. |
      |Set as Default Template |Option to set this template as the default template for the project. |
      |\*Service Instance |The service instance adopted only supports serverless_spark_default; dropdown options available. |
      |Resource Queue |The task computation queue provided by the engine used in the project template. Configure as needed, dropdown to select from created queues.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">At least one of three items must be set: <strong>Resource Queue</strong>, <strong>Priority</strong>, and <strong>Parameter Setting</strong>.</div><br> |
      |Priority |The priority of the project template. Configure based on actual needs, supporting three options: Normal (D5), High Priority (D4), and Super High Priority (D3), all selectable from a dropdown menu.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">At least one of three items must be set: <strong>Resource Queue</strong>, <strong>Priority</strong>, and <strong>Parameter Setting</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Modifying the template priority will overwrite the priority settings of tasks that reference this template and take immediate effect in the production environment; proceed with caution.</div><br> |
      |Parameter Setting |Set parameters as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Resource queue</strong>, <strong>Priority</strong>, and <strong>Parameter setting</strong> must have at least one set.</div><br> |
      

   * Edit Template

      Click the **Edit** button in the **Action** column of a list item to modify the template information in the pop\-up window.

   * Delete Template

      Click the **Delete** button in the **Action** column of a list item, confirm again, and then remove the template.

   * View Used Tasks

      Click the **View Used Tasks** button in the **Action** column of a list item to view task information that has used this template.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When no tasks reference the template, the <strong>View Used Task</strong> button is grayed out.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When tasks reference the template, the template cannot be deleted. It can only be deleted after the references are removed.   </div>
   


<span id="cab0adf7"></span>
## Subsequent Actions

After configuring the project template, you can use the corresponding template as needed during the development and operation process of the EMR Serverless Spark SQL task. For instructions related to task development, please refer to [EMR Serverless Spark SQL](https://docs.byteplus.com/docs/dataleap/emr_serverless_spark_sql).
