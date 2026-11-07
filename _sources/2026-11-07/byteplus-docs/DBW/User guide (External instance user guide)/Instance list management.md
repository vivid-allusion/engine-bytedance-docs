---
title: "Instance list management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/instance-list-management-for-external"
---

This topic describes how to view the list information of target instances and enable security control for instances on the Instance list page.

<span id="n7g6apFG"></span>
## **View instance list information**

<span id="newmuOqa"></span>
### **Prerequisites**

You have connected external or self\-built database instances to Database Workshop DBW. For details, see [External instance management](https://docs.byteplus.com/en/docs/DBW/self-managed-database-administration?lang=en).

<span id="RCt07myA"></span>
### Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click **Instance list**.

3. On the top menu bar, select the project and region.

4. On the **Instance list** page, switch the **Database type** to **Database connected over public network**.

5. On the Instance list page, you can perform the following operations.

   
   |**Actions** |**Description** |
   |---|---|
   |View instance information |In this area, you can view information such as the instance name/ID, database type, security control status, creation time, and status in DBW in the instance list. |
   |Delete instance |If you no longer need to manage your instance in the DBW console, go to the **Actions** column of the target instance and select  **...**  \> **Delete**. In the **Delete instance** dialog box, click **OK**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This deletion only removes the management record of this instance in DBW and does not delete the actual cloud resource entity of the instance.</div><br> |
   |Enabling security control |DBW enables centralized management of database instances. Enabling security control allows database changes to go through a ticket approval process, simplifying and standardizing database management while improving data management workflows. For specific steps and considerations on enabling security control, refer to Enabling security control. |
   |Log on to the data interaction platform |Click **Log in** to log in to the data interaction platform of the corresponding instance. On the data interaction platform, i.e., the SQL window, you can execute various SQL statements and manage databases/table structures. For details, see Log in to the external instance Data interaction platform. |
   


<span id="1DXv0lwr"></span>
## Enabling security control

<span id="0LrDsB2c"></span>
### Prerequisites


* The external instance has been added to the DBW console. For details, see [External instance management](https://docs.byteplus.com/en/docs/DBW/self-managed-database-administration?lang=en).

* A user has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management#.5re75Yqg55So5oi3). Alternatively, to apply for DBW administrator privileges, refer to [Role permission application](https://docs.byteplus.com/en/docs/DBW/role-permission-request).


<span id="GIQsmibU"></span>
### Precautions


* After enabling security control, the following operations are supported:

   * Access instances with security control enabled via password\-free login in the data interaction platform. For detailed steps, see [workspace](https://docs.byteplus.com/en/docs/DBW/data-management-for-external?lang=en) to the [workspace](https://docs.byteplus.com/en/docs/DBW/data-management-for-external?lang=en) [workspace](https://docs.byteplus.com/en/docs/DBW/data-management-for-external?lang=en).

   * Manage instances with security control enabled through security rule sets. For details, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security-rule-management).

* If the approval workflow for an instance is modified, existing approvals will still follow the previous process, while only newly generated approvals will adopt the updated workflow.

* If you modify the account password of an instance, you must reset the password for the security\-controlled instance. Otherwise, the system will fail to retrieve database information.


<span id="MBmYRtoq"></span>
### Enable instance security control


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. On the **Instance list** page, switch the **Database type** to **Database connected over public network**.

   
   <Tabs>
   <Tab zoneid="YG1oMzQzf9" title="Enable security control for the specified instance">
   <TabTitle>Enable security control for the specified instance</TabTitle>
   
   1. Click the pen icon under the **Security control** column of the target instance.
   
   2. In the **Set security control** dialog box, configure the following parameters.
   
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Security control mode** |Enable security control mode. |
   |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For details about MySQL security rule sets, see <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-management">Security rule set management</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For details about PostgreSQL security rule sets, see <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_?lang=en">Security rule set management</a>.</div><br> |
   |**Instance DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver. |
   |**Instance owner** |Select the instance owner from the drop\-down list. Both administrator and normal user can be assigned as the instance owner. The instance owner will have full read and write permissions for the database instance. When the approval workflow is set to the system default template, the instance Owner will automatically serve as the first\-level approver. |
   |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The primary account can approve all tickets by default. For more information on the approval workflow, see <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management">Approval workflow management</a>.</div><br> |
   |**Database account** |Enter the database account of the instance. |
   |**Database password** |Enter the password for the instance database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you change the database account password for an instance, you must update the corresponding password to the new value on the instance list page within the DBW console.</div><br> |
   
   
   
   3. Click **Test connectivity** to verify whether the instance is successfully connected.
   
   4. Click **OK**.
   
   
   </Tab>
   <Tab zoneid="wLa0GgYI2V" title="Batch enable instance security control">
   <TabTitle>Batch enable instance security control</TabTitle>
   
   All target instances for batch security control enablement must be disabled.
   
   
   1. Select the target instance, and choose **Batch security control** \> **Batch enable** on the bottom menu bar.
   
   2. In the **Enable security control** panel, configure the following parameters.
   
   
   
   |**Parameter** |**Description** |
   |---|---|
   |**Security rule set** |Select a security rule from the drop\-down list. Fuzzy search is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Security rule set</strong> column to set the security rule set to all selected instances. Once successfully configured, the instances will share the same security rule set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For details about MySQL security rule sets, see <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-management">Security rule set management</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For details about PostgreSQL security rule sets, see <a href="https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_?lang=en">Security rule set management</a>.</div><br> |
   |**Approval workflow** |Select the target approval workflow from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Approval workflow</strong> column to set the approval workflow to all selected instances. Once successfully configured, the instances will share the same approval workflow.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The primary account can approve all tickets by default. For more information on the approval workflow, see <a href="https://docs.byteplus.com/en/docs/DBW/Approval_workflow_management">Approval workflow management</a>.</div><br> |
   |**Instance DBA** |Select the instance DBA from the drop\-down list. Both administrator and normal user can be assigned as the instance DBA. The instance DBA will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the approval workflow is set to the system default template, the instance DBA will automatically serve as the second\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Instance DBA</strong> next to the <strong>Batch</strong> column to assign the instance DBA to all selected instances. Once successfully configured, the instances will share the same instance DBA.</div><br> |
   |**Instance owner** |Select the instance owner from the drop\-down list. Both administrator and normal user can be assigned as the instance owner. The instance owner will have full read and write permissions for the database instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the approval workflow is set to the system default template, the instance owner will automatically serve as the first\-level approver.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Instance owner</strong> column to assign the instance Owner to all selected instances. Once successfully configured, the instances will share the same instance Owner.</div><br> |
   |**Database account** |Enter the database account of the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Database account</strong> column to assign the database account to all selected instances. If batch configuration is required, the database account must be identical for all instances.</div><br> |
   |**Database password** |Enter the password for the instance database account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Batch</strong> next to the <strong>Database password</strong> column to set the database password to all selected instances. If batch configuration is required, the database password must be identical for all instances.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you change the database account password for an instance, you must update the corresponding password to the new value on the instance list page within the DBW console.</div><br> |
   
   
   
   3. Click **Test connectivity** to verify whether the instance is successfully connected.
   
   4. Click **OK**.
   
   
   </Tab>
   </Tabs>
   

   After enabling security control, you can view the security control status of the target instance as enabled on the instance list page.


<span id="LgoD76Nz"></span>
### Disable instance security control


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, click **Instance list**.

4. On the **Instance list** page, switch the **Database type** to **Database connected over public network**.

   
   <Tabs>
   <Tab zoneid="rRrDM8fm" title="Disable security control for the specified instance">
   <TabTitle>Disable security control for the specified instance</TabTitle>
   
   1. Click the pen icon under the **Security control** column of the target instance.
   
   2. In the **Set security control** dialog box, disable the security control mode.
   
   
   </Tab>
   <Tab zoneid="yPp4dIFZ" title="Batch disable instance security control">
   <TabTitle>Batch disable instance security control</TabTitle>
   
   All target instances for batch security control disablement must be enabled.
   
   
   1. Select the target instance, and choose **Batch security control** \> **Batch disable** on the bottom menu bar.
   
   2. In the**Batch disable security control** dialog box, click **OK**.
   
   
   </Tab>
   </Tabs>
   


&nbsp;
