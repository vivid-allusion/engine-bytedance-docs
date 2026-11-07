---
title: "Changing the project of a parameter template"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Changing_the_project_of_a_parameter_template"
---

This topic describes how to change the affiliated project of a historical customized parameter template.

<span id="CiBaOutu"></span>
## Background

To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its parameter template feature to support project authentication.

After the project\-based authentication capability is launched, historical customized parameter templates are automatically assigned to the "Global resources" project. For customized parameter templates under the "Global resources" project, you need to select the "All resources" project in the top navigation bar to view them. You can change the affiliated project for historical customized parameter templates in the "Global resources" project.

<span id="rErp3yyE"></span>
## Precautions


* This topic provides information only on changing the affiliated project of historical customized parameter templates that were automatically assigned to the "Global resources" project after the project authentication feature was released. To move a customized parameter template from one project to another, refer to [Project Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).

* After a customized parameter template is assigned to a specific project, IAM user that do not have the required project privilege cannot manage the resource. Add the necessary privilege to these IAM user promptly. For details on how to add project privilege for a sub\-account, refer to [Project Permission Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management).

* There is a slight latency when you modify the affiliated project of a customized parameter template. After the modification is complete, wait for a moment, and then refresh the page to confirm the result.


<span id="x2gAOmts"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the region for the parameter template, and select the **All resources** project.

3. In the left navigation bar, click **Parameter templates** to enter the **Custom templates** tab.

4. In the list of customized parameter templates on the **Customized template** page, click in the **Affiliated project** column for the target customized parameter template <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_482a0c09a8e4fe6f37b3771e19a96be0.png)<sub> </sub></span>.

5. In the **Edit affiliated project** dialog box that appears, select the target project from the **Affiliated project** drop\-down list, and click **OK**.


<span id="DFBZhY7X"></span>
## Subsequent steps

To change the affiliated project of a customized parameter template that is not a global resource, refer to [Project Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).
