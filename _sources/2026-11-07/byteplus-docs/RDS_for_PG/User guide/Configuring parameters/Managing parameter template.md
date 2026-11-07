---
title: "Managing parameter template"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Managing_a_parameter_template"
---

This article describes how to manage parameter templates for RDS for PostgreSQL, such as view, edit, copy, and delete.

<span id="7Rhgx4en"></span>
## Precautions

Parameter templates have no project attributes and are not attributed to a project.

<span id="yncbn5Wl"></span>
## Prerequisites

A parameter template for RDS for PostgreSQL has been created. For more detailed information please see [Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Creating_a_parameter_template).

<span id="0JN3VR5v"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the project and region to which the parameter template belongs.

3. In the left navigation bar, click **Parameter templates** to enter the **Custom template** tab.

   * **View parameter template list** 

      On the **Custom template** tab, you can see all parameter templates of the region. In the parameter templates list, you can filter the parameter templates according to the **Applicable version**.

   * **View parameter template details** 

      In the **Parameter templates** list under the **Custom template** page, click the name of the parameter template to view the name of the parameter template, the template description, the applicable database engine version, and the included parameters in the pop\-up **Parameter template details** page.

   * **Modify parameter template** 

      In the **Parameter templates** list under the ** Custom template** page, click **Edit** of the **Action** column, the name, description and parameters of the parameter template, can be modified in the pop\-up **Modify parameter template** page.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip   </div>
   

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The database engine version of the parameter template does not support modification.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The parameters of a parameter template can be modified in the same way as creating a parameter template. For more detailed information please see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/Creating_a_parameter_template">Creating a parameter template</a>.      </div>
      

   * **Copy a parameter template** 

      In the **Parameter templates list** under the **Custom template** page, click **Copy** of the **Action** column, the parameter template can be cloned after finishing the following configurations and clicking **OK** in the pop\-up **Copy as custom template** page.

      
      |**Configuration item** |**Is it required?**  |**Note** |
      |---|---|---|
      |Template name<br><br> |Yes |Fill in the name of the parameter template. The template name should satisfy the following rules:<br><br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* 2 to 64 characters in length.<br><br>* Cannot start with a digit or a hyphen (\-). |
      |Template description |No |Add the description information of the template to facilitate the application and management of subsequent templates. Supports up to 200 characters. |
      

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Modifying the database engine version and parameters of a parameter template during replication is not supported.   </div>
   

   * **Delete a parameter template** 

      In the **Parameter templates list** under the **Custom template** page, click  **…**  \> **Delete** of the **Action** column, click **OK** in the pop\-up dialog box.


<span id="0uMODkSz"></span>
## Related APIs


|API |Note |
|---|---|
|[CloneParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/CloneParameterTemplate) |Call CloneParameterTemplate API to clone the parameter template. |
|[ModifyParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyParameterTemplate) |Call ModifyParameterTemplate API to modify the parameter template. |
|[DeleteParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DeleteParameterTemplate) |Call ModifyParameterTemplate API to delete the parameter template. |
|[ListParameterTemplates](https://docs.byteplus.com/en/docs/RDS_for_PG/ListParameterTemplates) |Call ListParameterTemplates interface query parameter template list. |
|[DescribeParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeParameterTemplate) |Call DescribeParameterTemplate API to query the details of the parameter template. |
