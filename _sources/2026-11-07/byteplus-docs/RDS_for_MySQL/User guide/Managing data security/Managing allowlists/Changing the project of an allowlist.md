---
title: "Changing the project of an allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Changing_the_project_of_an_allowlist"
---

This topic describes the steps to change the affiliated project for historical allowlists.

<span id="LKn2XeqR"></span>
## Background

To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication.

After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar. You can change the affiliated project for historical allowlists in the "Global resources" project.

<span id="9SFYu3FM"></span>
## Precautions


* This topic provides information only about changing the affiliated project for historical allowlists that were automatically assigned to the "Global resources" project after the project\-based authentication feature was launched. To change the affiliated project of an allowlist to another project, refer to [Project Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).

* After an allowlist is assigned to a specified project, sub\-accounts without the privilege for that project cannot operate the resource. Add the corresponding privilege to the sub\-accounts in time. For details on how to add project privilege for a sub\-account, refer to [Project Permission Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management).

* There is a slight latency when modifying the affiliated project of an allowlist. After the modification is complete, wait for a moment and then refresh the page to confirm the result.


<span id="tYHIWoAz"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the region for the parameter template, and select the **All resources** project.

3. In the left\-side navigation pane, click **Allowlists** to go to the **Allowlists** page.

4. On the **Allowlists** page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_482a0c09a8e4fe6f37b3771e19a96be0.png)<sub> </sub></span> icon in the **Affiliated project** column for the target allowlist.

5. In the **Edit affiliated project** dialog box that appears, select the target project from the **Affiliated project** drop\-down list, and click **OK**.


<span id="KwLEOO1J"></span>
## Subsequent steps

To change the affiliated project of an allowlist under a non\-Global resources project, refer to [Project Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).
