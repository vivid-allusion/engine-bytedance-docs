---
title: "Exporting parameter configuration as parameter template"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Exporting_parameter_configuration_as_a_parameter_template"
---

RDS for PostgreSQL supports the creation of parameter templates to achieve templated configuration of instance parameters, so as to quickly apply instance parameter settings to other instances. This article describes the process of exporting an instance's parameter settings as a parameter template.

<span id="XMCA4oZX"></span>
## Prerequisites

The instance that needs to export the parameter configuration as a parameter template is  in the **Running** state.

<span id="kuGXOtoZ"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Parametes**.

6. On the **PostgreSQL parameter** tab, click **Export as a template**.

7. In the pop\-up **Export as custom template** window, after completing the following settings, click **OK**.



|**Configuration item** |**Is it required?**  |**Note** |
|---|---|---|
|Template name<br><br> |Yes |Fill in the name of the parameter template. The template name should satisfy the following rules:<br><br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* 2 to 64 characters in length.<br><br>* Cannot start with a digit or a hyphen (\-). |
|Template description |No |Add the description information of the template to facilitate the application and management of subsequent templates. Supports up to 200 characters. |


<span id="phnGlkBX"></span>
## **Subsequent Steps**

[Managing parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Managing_a_parameter_template)

<span id=""></span>
## Related APIs


|API |Note |
|---|---|
|[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_PG/SaveAsParameterTemplate) |Call SaveAsParameterTemplate API to export the current parameter configuration of the instance as a parameter template. |
