---
title: "Announcement on upgrading the allowlist and parameter template features"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Announcement_on_upgrading_the_allowlist_and_parameter_template_features"
---

We are planning to upgrade the allowlist and parameter template features to enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services.

<span id="jOHRYw26"></span>
## Upgrade details

Project\-based authentication will be available for allowlists and parameter templates.

<span id="bAqJOxbR"></span>
## Upgrade time

The upgrade will be rolled out by region from late January to early February 2026.

<span id="0xLf0zo4"></span>
## Business impact and response


* **Scope of impact**


All existing and newly created allowlists and custom parameter templates.


* **Business impact**


After the project\-based authentication feature is released, the procedures for creating or modifying allowlists and customized parameter templates change as follows:


   * After the project\-based authentication feature is released, you can specify an affiliated project when creating new allowlists and parameter templates. Only accounts with the required project privileges can manage the allowlists or parameter templates within the project.

   * Existing allowlists and customized parameter templates created before the release of the project authentication feature are automatically assigned to the "Global resources" project. To view and modify allowlists and parameter templates under the "Global resources" project, select the "All resources of the account" project in the top navigation bar. You can change the affiliated project for existing allowlists and parameter templates under the "Global resources" project. For details, refer to [Changing the project of a parameter template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Changing_the_project_of_a_parameter_template) and[ Changing the project of an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Changing_the_project_of_an_allowlist).

* **Solutions**

   **This upgrade does not affect the running of instances.**  However, if you use a IAM user account to manage RDS for MySQL resources, you may be unable to query or modify allowlists and parameter templates due to insufficient privileges. If this occurs, you can:

   * Use a root user account to adjust the projects of historical allowlists and parameter templates.

   * Use a root user account to grant IAM user accounts the privilege to manage resources.


<span id="G6a9MZOC"></span>
## Next steps

None. If you have any questions or need further support during use, you can contact our customer support team at any time.
