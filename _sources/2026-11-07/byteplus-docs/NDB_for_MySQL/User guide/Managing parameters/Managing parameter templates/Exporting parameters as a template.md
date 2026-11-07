---
title: "Exporting parameters as a template"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Exporting_parameters_as_a_template"
---

Supports exporting parameter configurations of existing instances as parameter templates for easy reuse. This article describes how to export an existing parameter as a template.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Parameters**.

5. On the **Parameter list** subtab, click **Export as custom template**.

6. In the dialog box that pops up, set the **Template name** and **Template description**, and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the export is successful, the template can be viewed in the parameter template list. For details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_parameter_template">Viewing parameter template information</a>.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
### Related APIs


|API |Description |
|---|---|
|[SaveAsParameterTemplate](https://docs.byteplus.com/en/docs/NDB_for_MySQL/SaveAsParameterTemplate) |Calling the SaveAsParameterTemplate saves the parameter configuration of the instance as a parameter template. |
