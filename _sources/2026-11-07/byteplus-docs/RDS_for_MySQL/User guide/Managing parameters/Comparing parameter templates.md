---
title: "Comparing parameter templates"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Comparing_parameter_templates"
---

RDS for MySQL supports comparing parameter templates to facilitate their management and application. This topic describes the procedure for comparing parameter templates.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* System parameter templates cannot be directly compared with customized parameter templates.

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its parameter template feature to support project authentication. After the project\-based authentication capability is launched, historical customized parameter templates are automatically assigned to the "Global resources" project. For customized parameter templates under the "Global resources" project, you need to select the "All resources" project in the top navigation bar to view them.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and Region for the parameter template.

3. In the left\-side navigation pane, click **Parameter templates**, and go to the **Customized template** tab or the **System template** tab.

4. On the **Customized template** tab or the **System template** tab, select the parameter templates to compare, and then click **Parameter comparison** to go to the **Parameter comparison** page.

5. The **Parameter comparison** page displays the comparison results of two parameter templates. You can view only the different items or all comparison items. Click **OK** to close the **Parameter comparison** page.
