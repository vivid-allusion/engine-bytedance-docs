---
title: "Enabling security control"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis"
---

Database Workshop (DBW) supports unified management of database instances, enabling database changes to follow a ticket approval workflow. This simplifies and standardizes database management while improving data management workflows. Before initiating the approval workflow for database instance changes, security control must be enabled for the instance. This topic explains how to enable security control for an instance.

<span id="5V8bzBru"></span>
## Prerequisites


* An instance for Cache for Redis has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* A user has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management). Alternatively, to apply for DBW administrator privileges, refer to [Role permission application](https://docs.byteplus.com/en/docs/DBW/role-permission-request).

* Optional. An approval workflow has been created. For detailed steps, refer to [Approval workflow management](https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management?lang=zh).

* Optional. Create a security rule set. For detailed steps, refer to [Security rule management](https://docs.byteplus.com/en/docs/DBW/security_rules_for_redis?lang=zh).


<span id="nFy9UXD3"></span>
## Precautions


* After enabling security control, the following operations are supported:

   * On the User management page, grant specified users permissions to enable security control for instances. For detailed steps, refer to [Granting user permissions](https://docs.byteplus.com/en/docs/DBW/granting_operation_permissions_for_system_roles_for_redis?lang=zh).

   * Manage instances with security control enabled through tickets. For detailed steps, refer to [Creating a ticket](https://docs.byteplus.com/en/docs/DBW/ticket-list-for-redis?lang=zh).

   * Access instances with security control enabled via password\-free login in the data interaction platform. For detailed steps, refer to [Logging on to the data interaction platform (Cache for Redis).](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-cache-for-redis?lang=zh)

   * Manage instances with security control enabled through security rule sets. For details, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security_rules_for_redis?lang=zh).

* Only the primary account or sub\-users added as DBW administrators can enable security control for instances. Once security control is enabled for an instance, administrators are automatically granted permissions for the current instance, including SQL changes, SQL queries, structural changes, operation and maintenance read\-only and read/write operations for 1 year.

* If the approval workflow for an instance is modified, existing approvals will still follow the previous process, while only newly generated approvals will adopt the updated workflow.

* If you modify the account password of an instance, you must reset the password for the security\-controlled instance. Otherwise, the system will fail to retrieve database information.


<span id="QTfMGXCO"></span>
## Enable instance security control


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. On the **Instance list** page, filter database type as **Cache for Redis**.

   
   <Tabs>
   <Tab zoneid="cSsRiy0Dbd" title="Enable security control for the specified instance">
   <TabTitle>Enable security control for the specified instance</TabTitle>
   
   1. Click the pen icon under the **Security control** column of the target instance.
   
   2. In the **Set security control** dialog box, configure the following parameters.
   
      
      |**Parameter** |**Description** |
      |---|---|
      |**Security control mode** |Enable the security control mode button. |
      |**Security rule set** |Select a security rule set from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security_rules_for_redis?lang=zh">Security rule management</a>.</div><br> |
      |**Instance DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br>When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
      |**Instance owner** |Select the instance owner from the drop\-down list. Both administrator and normal user can be assigned as the instance owner. The instance owner will have full read and write permissions for the database instance.<br><br>When the approval workflow is set to the system default template, the instance owner will automatically serve as the first\-level approver. |
      |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The primary account can approve all tickets by default. For more information on the approval workflow, see <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management?lang=zh">Approval workflow management</a>.</div><br> |
      |**Database account** |Enter the database account of the instance. |
      |**Database password** |Enter the password corresponding to the database account.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you modify the database account password for an instance, you must also update the corresponding password to the new value on the instance list page in the DBW console.</div><br> |
      
   
   3. Click **Test connectivity** to verify whether the instance is successfully connected.
   
   4. Click **OK**.
   
   
   </Tab>
   <Tab zoneid="p1SOxSFvKi" title="Batch enable instance security control">
   <TabTitle>Batch enable instance security control</TabTitle>
   
   All target instances for batch security control enablement must be disabled.
   
   
   1. Select the target instance, and choose **Batch security control** \> **Batch enable** on the bottom menu bar.
   
   2. In the **Enable security control** panel, configure the following parameters.
   
      
      |**Parameter** |**Description** |
      |---|---|
      |**Security rule set** |Select the security rule set for the target instance from the drop\-down list in sequence. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to <strong>Security rule set</strong> to batch configure security rule sets for all selected instances. After batch configuration, the security rule sets of the selected instances will remain consistent.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security_rules_for_redis?lang=zh">Security rule set management</a>.</div><br> |
      |**Approval workflow** |Select the approval workflow for the target instance from the drop\-down list in sequence.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Approval workflow</strong> to batch set the approval workflow for all selected instances. After batch setup, the approval workflows for the selected instances will remain consistent.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The primary account can approve all tickets by default. For more information on the approval workflow, see <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management?lang=zh">Approval workflow management</a>.</div><br> |
      |**Instance DBA** |Select the instance DBA for the target instance from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the<strong> Instance DBA</strong> column to assign the instance DBA to all selected instances. After batch setup, the instance DBAs for the selected instances will remain consistent.</div><br> |
      |**Instance owner** |Select the instance owner for the target instance from the drop\-down list in sequence.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the approval workflow is set to the system default template, the instance owner will automatically serve as the first\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Instance owner</strong> column to assign the instance Owner to all selected instances. After batch setup, the instance Owner for the selected instances will remain consistent.</div><br> |
      |**Database account** |Enter the database account of the instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Database account</strong> to batch set the database account for all selected instances. If you need to batch configure database accounts for all instances, the database accounts must be identical for all instances.</div><br> |
      |**Database password** |Enter the password corresponding to the database account.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Database password</strong> column to batch set the database password for all selected instances. If batch configuration is required, the database password must be identical for all instances.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you modify the database account password for an instance, you must also update the corresponding password to the new value on the instance list page in the DBW console.</div><br> |
      
   
   
   
   &nbsp;
   
   3. Click ** One\-click connectivity test** to verify whether the instance is successfully connected.
   
   4. Click **OK**.
   
   
   </Tab>
   </Tabs>
   


After enabling security control, you can view the security control status of the target instance as enabled on the instance list page.

<span id="I8avVM0x"></span>
## Modify instance security control


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. On the **Instance list** page, filter database type as **Cache for Redis**.



<Tabs>
<Tab zoneid="XvzF0loe1J" title="Modify security control for the specified instance">
<TabTitle>Modify security control for the specified instance</TabTitle>

1. Click the pen icon under the Security control column of the target instance.

2. In the Set security control dialog box, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Security control mode** |Enable the security control mode button. |
   |**Security rule set** |Select a security rule set from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security_rules_for_redis?lang=zh">Security rule set management</a>.</div><br> |
   |**Instance DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br>When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
   |**Instance owner** |Select the instance owner from the drop\-down list. Both administrator and normal user can be assigned as the instance owner. The instance owner will have full read and write permissions for the database instance.<br><br>When the approval workflow is set to the system default template, the instance owner will automatically serve as the first\-level approver. |
   |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The primary account can approve all tickets by default. For more information on the approval workflow, see <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management?lang=zh">Approval workflow management</a>.</div><br> |
   |**Database account** |Enter the database account of the instance. |
   |**Database password** |Enter the password corresponding to the database account.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you modify the database account password for an instance, you must also update the corresponding password to the new value on the instance list page in the DBW console.</div><br> |
   

3. Click **Test connectivity** to verify whether the instance is successfully connected.

4. Click **OK**.


</Tab>
<Tab zoneid="vZpbYOVznz" title="Modify security control for batch instances">
<TabTitle>Modify security control for batch instances</TabTitle>

All target instances for batch security control modification must be enabled.


1. Select the target instance, and choose **Batch security control** \> **Batch edit** on the bottom menu bar.

2. In the **Enable security control** panel, configure the following parameters.

   You can check whether to set **Security rule set**, **Approval workflow**, **Instance DBA and Owner**, and **Database account and password** as needed.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Security rule set** |Select the security rule set for the target instance from the drop\-down list in sequence. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to <strong>Security rule set</strong> to batch configure security rule sets for all selected instances. After batch configuration, the security rule sets of the selected instances will remain consistent.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For more information on security rule sets, refer to <a href="https://docs.byteplus.com/en/docs/DBW/security_rules_for_redis?lang=zh">Security rule set management</a>.</div><br> |
   |**Approval workflow** |Select the approval workflow for the target instance from the drop\-down list in sequence.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Approval workflow </strong>to batch set the approval workflow for all selected instances. After batch setup, the approval workflows for the selected instances will remain consistent.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The root user can approve all tickets by default. For more information on the approval workflow, see <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management?lang=zh">Approval workflow management</a>.</div><br> |
   |**Instance DBA** |Select the instance DBA for the target instance from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Instance DBA</strong> column to assign the instance DBA to all selected instances. After batch setup, the instance DBAs for the selected instances will remain consistent.</div><br> |
   |**Instance owner** |Select the instance owner for the target instance from the drop\-down list in sequence.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the approval workflow is set to the system default template, the instance owner will automatically serve as the first\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Instance owner</strong> column to assign the instance Owner to all selected instances. After batch setup, the instance Owner for the selected instances will remain consistent.</div><br> |
   |**Database account** |Enter the database account of the instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Database account</strong> to batch set the database account for all selected instances. If you need to batch configure database accounts for all instances, the database accounts must be identical for all instances.</div><br> |
   |**Database password** |Enter the password corresponding to the database account.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Batch</strong> next to the <strong>Database password</strong> column to batch set the database password for all selected instances. If batch configuration is required, the database password must be identical for all instances.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you modify the database account password for an instance, you must also update the corresponding password to the new value on the instance list page in the DBW console.</div><br> |
   

3. Click ** One\-click connectivity test** to verify whether the instance is successfully connected.

4. Click **OK**.


</Tab>
</Tabs>


<span id="0KTqNXW3"></span>
## Disable instance security control

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When disabling security control, ensure that there are no tickets in the current instance with statuses such as not started, pre\-checking, approving, waiting for execution, or executing. If such tickets exist, manually complete them first, and then disable security control.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. On the **Instance list** page, filter database type as **Cache for Redis**.

   * Disable security control for the specified instance

      1. Click the pen icon under the Security control column of the target instance.

      2. In the Set security control dialog box, disable the security control mode.

   * Batch disable instance security control

      All target instances for batch security control disablement must be enabled.

      3. Select the target instance, and choose **Batch security control** \> **Batch disable** on the bottom menu bar.

      4. In the**Batch disable security control** dialog box, click **OK**.
