---
title: "Enabling security control"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/enabling-security-control_"
---

Database Workshop (DBW) supports unified management of database instances, enabling database changes to follow a ticket approval workflow. This simplifies and standardizes database management while improving data management workflows. Before initiating the approval workflow for database instance changes, security control must be enabled for the instance. This topic explains how to enable security control for an instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and an account for RDS for SQL Server have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) and [Creating an account](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-and-managing-account).

* A user has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql). Alternatively, to apply for DBW administrator privileges, refer to [Role permission application](https://docs.byteplus.com/en/docs/DBW/role-permission-request).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After enabling security control, the following operations are supported:

   * On the User management page, grant specified users permissions to enable security control for instances. For detailed steps, refer to [Granting user permissions](https://docs.byteplus.com/en/docs/DBW/Granting_operation_permissions_for_system_roles?type=preview&lang=en).

   * Access instances with security control enabled via password\-free login in the data interaction platform. For detailed steps, refer to [Logging on to the data interaction platform (RDS for SQL Server)](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-rds-for-sql-server).

   * Manage instances with security control enabled through security rule sets. For details, refer to [Security rule set](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__) [management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__?type=preview&lang=en).

* Only the primary account or sub\-users added as DBW administrators can enable security control for instances. Once security control is enabled for an instance, administrators are automatically granted permissions for the current instance, including SQL changes, SQL queries, structural changes, operation and maintenance read\-only and read/write operations for 1 year.

* If the approval workflow for an instance is modified, existing approvals will still follow the previous process, while only newly generated approvals will adopt the updated workflow.

* If you modify the account password of an instance, you must reset the password for the security\-controlled instance. Otherwise, the system will fail to retrieve database information.


<span id=".5byA5ZCv5a6e5L6L5a6J5YWo566h5o6n"></span>
## Enable instance security control


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. In the top\-left corner of the **Instance list** page, switch the instance type to **RDS** for **SQL Server**.

   * Enable security control for the specified instance

      1. Click the pen icon under the **Security control** column of the target instance.

      2. In the **Set security control** dialog box, configure the following parameters.

         
         |**Parameter** |**Description** |
         |---|---|
         |**Security control mode** |Enable security control mode. |
         |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__">Security rule set management</a>.</div><br> |
         |**Instance** **DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
         |**Instance** **Owner** |Select the instance Owner from the drop\-down list. Both administrator and normal user can be assigned as the instance Owner. The instance Owner will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance Owner will automatically serve as the first\-level approver. |
         |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The primary account can approve all tickets by default. For more information on the approval workflow, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management">Approval workflow management</a>.</div><br> |
         |**Database account** |Enter the database account of the instance. |
         |**Database password** |Enter the password for the instance database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you change the database account password for an instance, you must update the corresponding password to the new value on the instance list page within the DBW console.</div><br> |
         

      3. Click **Test connectivity** to verify whether the instance is successfully connected.

      4. Click **OK**.

   * Batch enable instance security control

      All target instances for batch security control enablement must be disabled.

      1. Select the target instance, and choose **Batch security control** \> **Batch enable** on the bottom menu bar.

      2. In the **Enable security control** panel, configure the following parameters.

         
         |**Parameter** |**Description** |
         |---|---|
         |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Security rule set</strong> column to set the security rule set to all selected instances. Once successfully configured, the instances will share the same security rule set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__?type=preview&lang=en">Security rule set management</a>.</div><br> |
         |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Approval workflow</strong> column to set the approval workflow to all selected instances. Once successfully configured, the instances will share the same approval workflow.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The primary account can approve all tickets by default. For more information on the approval workflow, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management">Approval workflow management</a>.</div><br> |
         |**Instance** **DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click Batch next to the <strong>Instance</strong> <strong>DBA</strong> column to assign the instance DBA to all selected instances. Once successfully configured, the instances will share the same instance DBA.</div><br> |
         |**Instance** **Owner** |Select the instance Owner from the drop\-down list. Both administrator and normal user can be assigned as the instance Owner. The instance Owner will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the approval workflow is set to the system default template, the instance Owner will automatically serve as the first\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click Batch next to the <strong>Instance</strong> <strong>Owner</strong> column to assign the instance Owner to all selected instances. Once successfully configured, the instances will share the same instance Owner.</div><br> |
         |**Database account** |Enter the database account of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Database account</strong> column to assign the database account to all selected instances. If batch configuration is required, the database account must be identical for all instances.</div><br> |
         |**Database password** |Enter the password for the instance database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Database password</strong> column to set the database password to all selected instances. If batch configuration is required, the database password must be identical for all instances.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you change the database account password for an instance, you must update the corresponding password to the new value on the instance list page within the DBW console.</div><br> |
         

      3. Click ** One\-click connectivity test** to verify whether the instance is successfully connected.

      4. Click **OK**.

         After enabling security control, you can view the security control status of the target instance as enabled on the instance list page.


<span id=".5L-u5pS55a6e5L6L5a6J5YWo566h5o6n"></span>
## Modify instance security control


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. In the top\-left corner of the **Instance list** page, switch the instance type to **RDS** for **SQL Server**.

   * Modify security control for the specified instance

      1. Click the pen icon under the **Security control** column of the target instance.

      2. In the **Set security control** dialog box, configure the following parameters.

         
         |**Parameter** |**Description** |
         |---|---|
         |**Security control mode** |Enable security control mode. |
         |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__?type=preview&lang=en">Security rule set management</a>.</div><br> |
         |**Instance** **DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
         |**Instance** **Owner** |Select the instance Owner from the drop\-down list. Both administrator and normal user can be assigned as the instance Owner. The instance Owner will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance Owner will automatically serve as the first\-level approver. |
         |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The primary account can approve all tickets by default. For more information on the approval workflow, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management">Approval workflow management</a>.</div><br> |
         |**Database account** |Enter the database account of the instance. |
         |**Database password** |Enter the password for the instance database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you change the database account password for an instance, you must update the corresponding password to the new value on the instance list page within the DBW console.</div><br> |
         

      3. Click **Test connectivity** to verify whether the instance is successfully connected.

      4. Click **OK**.

   * Batch modify instance security control

      All target instances for batch security control editing must be enabled.

      1. Select the target instance, and choose **Batch security control** \> **Batch edit** on the bottom menu bar.

      2. In the **Enable security control** panel, configure the following parameters.

         You can optionally configure **Security rule set**, **Approval workflow**, and **Instance** **DBA** **and Owner**, **Database account and password** as needed.

         
         |**Parameter** |**Description** |
         |---|---|
         |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Security rule set</strong> column to set the security rule set to all selected instances. Once successfully configured, the instances will share the same security rule set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__?type=preview&lang=en">Security rule set management</a>.</div><br> |
         |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Approval workflow</strong> column to set the approval workflow to all selected instances. Once successfully configured, the instances will share the same approval workflow.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The primary account can approve all tickets by default. For more information on the approval workflow, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management">Approval workflow management</a>.</div><br> |
         |**Instance** **DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click Batch next to the <strong>Instance</strong> <strong>DBA</strong> column to assign the instance DBA to all selected instances. Once successfully configured, the instances will share the same instance DBA.</div><br> |
         |**Instance** **Owner** |Select the instance Owner from the drop\-down list. Both administrator and normal user can be assigned as the instance Owner. The instance Owner will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the approval workflow is set to the system default template, the instance Owner will automatically serve as the first\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click Batch next to the <strong>Instance</strong> <strong>Owner</strong> column to assign the instance Owner to all selected instances. Once successfully configured, the instances will share the same instance Owner.</div><br> |
         |**Database account** |Enter the database account of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Database account</strong> column to assign the database account to all selected instances. If batch configuration is required, the database account must be identical for all instances.</div><br> |
         |**Database password** |Enter the password for the instance database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Database password</strong> column to set the database password to all selected instances. If batch configuration is required, the database password must be identical for all instances.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you change the database account password for an instance, you must update the corresponding password to the new value on the instance list page within the DBW console.</div><br> |
         

      3. Click ** One\-click connectivity test** to verify whether the instance is successfully connected.

      4. Click **OK**.


<span id=".5YWz6Zet5a6e5L6L5a6J5YWo566h5o6n"></span>
## Disable instance security control

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When disabling security control, ensure that there are no tickets in the current instance with statuses such as not started, pre\-checking, approving, waiting for execution, or executing. If any such tickets exist, manually complete them before disabling security control.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. In the top\-left corner of the **Instance list** page, switch the instance type to **RDS** for **SQL Server**.

   * Disable security control for the specified instance

      1. Click the pen icon under the **Security control** column of the target instance.

      2. In the **Set security control** dialog box, disable the security control mode.

   * Batch disable instance security control

      All target instances for batch security control disablement must be enabled.

      1. Select the target instance, and choose **Batch security control** \> **Batch disable** on the bottom menu bar.

      2. In the**Batch disable security control** dialog box, click **OK**.
