---
title: "Manage parameter template"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Managing_parameter_templates"
---

This topic describes how to manage parameter templates for RDS for MySQL, such as view, edit, copy, and delete.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its parameter template feature to support project authentication. After the project\-based authentication capability is launched, historical customized parameter templates are automatically assigned to the "Global resources" project. For customized parameter templates under the "Global resources" project, you need to select the "All resources" project in the top navigation bar to view them.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A parameter template for RDS for MySQL has been created. For more detailed information please see [Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the parameter template belongs.

3. In the left navigation bar, click **Parameter templates** to enter the **Custom templates** tab.

   * **View parameter template list**

      On the **Customized template** and **System template** tabs, you can view all the parameter templates in the current region.

   * **View parameter template details**

      In the **Parameter templates** list on the **Customized template** and **System template** tabs, click the name of a parameter template. In the displayed **Parameter template details** page, you can view information such as the template's name, description, applicable database engine version, and included parameters.

   * **Edit parameter template**

      In the **Parameter templates** list under the **Custom templates** page, click **Edit** of the **Action** column, the name, description and parameters of the parameter template, can be modified in the pop\-up **Modify parameter template** page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">System parameter templates (parameter templates on the <strong>System template</strong> tab) cannot be edited.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The database engine version of the parameter template does not support modification.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The parameters of a parameter template can be modified in the same way as creating a parameter template. For more detailed information please see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template">Creating a parameter template</a>.      </div>
      

   * **Copy parameter template**

      In the **Parameter templates** list on the **Customized template** and **System template** tabs, click **Copy** in the **operation** column. In the **Copy as customized template** window, complete the following configurations and click **OK**.

      
      |Configuration item |Required? |Description |
      |---|---|---|
      |Region |Yes |The target region for copying the parameter template. |
      |Template name |Yes |Fill in the name of the parameter template. The template name should satisfy the following rules:<br><br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* 2 to 64 characters in length.<br><br>* Cannot start with digits or hyphen (\-).  |
      |Template description |No |Add the description information of the template to facilitate the application and management of subsequent templates. Supports up to 200 characters. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Modifying the database engine version and parameters of a parameter template during replication is not supported.      </div>
      

   * **Reset parameter template**

      In the **Parameter templates** list on the **Customized template** tab, click  **…**  \> **Reset parameter template** in the **operation** column. In the dialog box that appears, click **OK**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">System parameter templates (the parameter templates on the <strong>System template</strong> tab) cannot be reset.      </div>
      

   * **Delete parameter template**

      In the **Parameter templates** list under the **Custom templates** page, click  **…**  \> **Delete** of the **Action** column, click **OK** in the pop\-up Copy as custom template page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">System parameter templates (the parameter templates on the <strong>System template</strong> tab) cannot be deleted.      </div>
