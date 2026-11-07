---
title: "Exporting parameters as a template"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/exporting_parameters_as_a_template"
---

You can export the parameter configuration of the primary node of an instance as a custom parameter template for future reuse. This topic describes the procedure for exporting a parameter configuration as a custom parameter template.

<span id=".5pON5L2c5q2l6aqk"></span>
## Precautions

When you export the parameter configuration of an instance as a custom parameter template, the exported custom parameter template is automatically assigned to the project selected in the navigation bar. To adjust the affiliated project of a parameter template, refer to [Changing the project of a parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Changing_the_project_of_a_parameter_template).

<span id="1YbBgKYi"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.</div>



3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Parametes**.

6. On the **MySQL parameters** tab, click **Export as a template**.

7. In the dialog box that appears, set the **Template name** and **Template description**, and click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/RDS_for_MySQL/saveasparametertemplate1) |Call the SaveAsParameterTemplate API to save the parameter configuration of a specified instance as a parameter template. |
