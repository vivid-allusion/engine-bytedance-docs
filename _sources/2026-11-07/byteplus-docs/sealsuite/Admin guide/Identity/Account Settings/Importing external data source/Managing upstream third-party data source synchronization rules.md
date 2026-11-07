---
title: "Managing upstream third-party data source synchronization rules"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-upstream-third-party-data-source-synchronization-rules"
---

After creating an upstream synchronization third\-party data source, you can manage the synchronization rule for the data source in the account source details, including those for users, departments, and roles. The synchronization rules can help you better cope with changes in various organizational structures and data sources, offering a more reliable data synchronization solution.

<span id="f196b7a0"></span>
# Prerequisites

An upstream synchronization third\-party data source has been created. For specific operations, please refer to [Integrating third-party data sources](https://docs.byteplus.com/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-).

<span id="bb8230ab"></span>
# User synchronization policy

User synchronization rules are a flexible solution for synchronizing data and status, designed to handle situations where users and their data statuses change in upstream third\-party data sources. The user synchronization rules of SealSuite include:


* **User synchronization mapping rule**: Field mapping is used for enterprises to independently specify the data that needs to be synchronized, where mobile phone number and email are the unique identifiers used to match users. Currently, deleting the mapping relationship between these two fields is not supported.

* **User status mapping**: When the user status of the upstream data source changes and is synchronized to SealSuite, you can customize the configuration to map the user status to SealSuite. For example, if upstream updates the user status but you do not want to synchronize the updates on SealSuite, you can turn off the update function.

1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page, click the **Directory Sync** tab.

4. (Optional) To view the data sources for a specific unit, click **Effective Unit** in the upper\-right corner and make your selection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d7d356b59e04b0dbbe6e99344aeae02~tplv-goo7wpa0wc-image.image) </span>

5. In the **Data source list**, click the data source that you want to edit. You will be redirected to the account source details page.

6. On the **Advanced Settings** tab of the **Account source details** page, click **Edit** to modify sync rule content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/108a2f248e4843c788813f9643912999~tplv-goo7wpa0wc-image.image) </span>

7. Modify the rule according to the following instructions, and click **Save** to complete the modification.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The functional changes under the <strong>User status mapping</strong> section take effect after the next synchronization task.   </div>
   

   
   |**Rule** |**Function** |**Description** |
   |---|---|---|
   |**User synchronization mapping rule** |Synchronization mapping |In the **Edit Mapping Relationship** dialog box, you can add, delete, or modify mappings. Two methods are supported: **Data Field Mapping** and **Expression Mapping**. For the supported expression syntax, refer to the [Expression Syntax](https://docs.byteplus.com/docs/sealsuite/configuring-data-source-mappings#4e89f04d). If you need to add custom attributes, please refer to [Configuring custom attributes](https://docs.byteplus.com/docs/sealsuite/docs-configuring-custom-attributes).<br><br>**Note**: Mobile phone number and email are the only identifiers used to match users. Currently, deleting the mapping relationship between these two fields is not supported. |
   |**User status mapping** |Create employees |This function is enabled by default. After this function is enabled, when an employee is created upstream, the employee and its information are created simultaneously. When the function is disabled, SealSuite will not be able to create an employee when upstream creates an employee. |
   ||After creating an employee, the employee status is |Select **Not Activated** or **Lock User**:<br><br><br>* **Not Activated**: This function is enabled by default. After an employee is created, the employee status is inactive.<br><br>* **Lock User**: After this function is enabled and an employee is created, the employee is in the suspended state and cannot log in to SealSuite. You need to restore the employee status to unactivated, so that employees can log in to SealSuite. |
   ||Update staff |This function is enabled by default. Once enabled, SealSuite will synchronize and update the employees as well as their information when there are updates in the upstream data source. Once disabled, SealSuite does not update employees from the upstream data source. |
   ||After deleting the employee, the employee status is |Select **leave**, **reserve** or **Lock User**:<br><br><br>* **leave**: This function is enabled by default. When an employee is deleted in the upstream data source, SealSuite marks the employee as terminated. After resignation, the employee will not be able to log in to SealSuite.<br><br>* **reserve**: When an employee is deleted in the upstream data source, SealSuite will retain the employee's information, and the employee's status may be normal use, inactive or suspended.<br><br>* **Lock User**: When an employee is deleted in the upstream data source, SealSuite will suspend the use of the employee account. |
   ||After creating an employee, set the initial password rule |Select to generate different random passwords or set a unified password:<br><br><br>* **Generate different random passwords**: This function is enabled by default. After creating employees, SealSuite generates different random initial passwords for each employee, ensuring that each employee has their own password.<br><br>* **Set a unified password**: After creating employees, you can set a unified password for all employees. Before setting a password, the mandatory password change function must be enabled, otherwise the unified password setting cannot be saved. For more information, please refer to [Configuring account security policies](https://docs.byteplus.com/docs/sealsuite/docs-configuring-account-security-policies).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To enable this function, please contact SealSuite technical support.</div><br> |
   


<span id="059dd82c"></span>
# Department synchronization policy

The department synchronization rules are a solution used to address situations that may arise when departments or higher\-level departments in upstream third\-party data sources change. The department synchronization rules of SealSuite include:


* **Department state mapping**: When the department status in the upstream data source changes and is synchronized to SealSuite, you can customize the configuration mapping to SealSuite's department status. For example, if a department is deleted in the upstream data source, you can select:

   * **Keep all departments**: When upstream third\-party data sources delete or clean up department data, resulting in departments without employees on SealSuite, you can choose to retain these departments. This can preserve the department's historical records and structure for queries or analysis later.

   * **Remove departments without users**: If you believe that departments without employees are no longer of practical significance or need not be retained, you can choose to have SealSuite automatically clean up these departments to keep the organizational structure concise and clear.

* **Department Advanced Strategy**: When selecting the synchronization range in SealSuite, if you select a department but do not select its superior department, SealSuite automatically adds all of its parent departments to ensure that the hierarchical relationship between departments is complete and accurate.

1. Log in to the Admin Console.

2. In the left navigation bar, select **Identity** \> **Account Setup**.

3. On the **Account Setup** page, click the **Directory Sync** tab.

4. In the Data source list, click the data source that you want to edit. You will be redirected to the account source details page.

5. On the **Advanced Settings** tab of the **Account source details** page, click **Edit** to modify sync rule content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38544ae00d96412fb0320e2324fcf092~tplv-goo7wpa0wc-image.image) </span>

6. Modify the rule according to the following instructions, and click **Save** to complete the modification.

   
   |**Rule** |**Function** |**Description** |
   |---|---|---|
   |**Department state mapping** |Create department |This function is enabled by default. Once enabled, SealSuite synchronizes the department creation and its information when a department is created upstream. Once disabled, SealSuite does not create departments when they are created upstream. |
   ||update department |This function is enabled by default. Once enabled, SealSuite updates the department and its information simultaneously when upstream updates the department. Once disabled, SealSuite does not update the department when it is updated upstream. |
   ||delete Department |After the upstream department data is deleted or cleared and synchronized with SealSuite, SealSuite will **Keep all departments** by default. You can choose to switch to **Remove departments without users** mode. In this mode, when upstream removes departments, if there are no employees in the department, the corresponding department will be automatically removed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule is supported only for manual and automatic synchronization.</div><br> |
   |**Department Advanced Strategy** |Department level completion rule |This function is disabled by default. You can choose to enable the **Department level completion rule**. When this rule is enabled, if you select a department in the synchronization range without selecting its parent department, SealSuite automatically includes all parent departments to ensure the hierarchy is complete.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This rule is supported only for manual and automatic synchronization.</div><br> |
   


<span id="77f8d331"></span>
# Role synchronization policy

If your upstream data source includes role attributes, SealSuite can automatically create corresponding roles and assign members. This allows administrators to mirror upstream permission structures, automating the link between business identity and security policy.

<span id="a7a4ecd2"></span>
### Compatibility Matrix


|**Data Source** |**Sync Roles** |**Sync User Groups** |**Note** |
|---|---|---|---|
|**Feishu / Lark** |✅ |✅ |Full support for roles and groups. |
|**DingTalk / Authing** |✅ |❌ |Syncs roles only. |
|**WeCom** |❌ |❌ |WeCom does not provide a "Role" attribute. |
|**LDAP** |❌ |❌ |Requires manual definition of role attributes via extended attribute mapping. |


<span id="0b1691ec"></span>
### Procedure


1. Log in to the Admin Console.

2. Navigate to **Identity** \> **Account Setup** \> **Directory Sync**.

3. In the source list, click the name of the source you want to configure.

4. Navigate to the **Advanced Settings** tab on the **Account Source Details** page.

5. Locate the **Role Synchronization Policy** section and click **Edit**.



|**Feature** |**Description** |
|---|---|
|**Synchronize roles** |Disabled by default. When enabled, SealSuite imports role attributes from the upstream source. |
|**Synchronize user group** | **(Feishu/Lark only)** .<br><br>**Sync to Roles**: Select **Sync to Roles** to automatically generate SealSuite roles based on Feishu/Lark User Groups.<br><br><br>* **Prerequisite**: Ensure the Feishu/Lark `user_id` is mapped to the SealSuite `third_party_user_id` in the **User Synchronization Mapping Policy**, otherwise, group members cannot be synced.<br><br>* **Use Case**: Ideal for complex organizations or cross\-departmental collaboration. Instead of manual maintenance, SealSuite automatically updates role membership based on Feishu/Lark groups, allowing for precise security controls (e.g., DLP auditing, network authorization). |


<span id="2f8c88b8"></span>
# Data Protection Policy

To prevent data loss caused by network instability or configuration errors during synchronization, it is recommended to enable the **Data Protection Rule**. For detailed instructions, see [Configuring data protection rules for sync tasks](https://docs.byteplus.com/docs/sealsuite/configuring-data-protection-rules-for-sync-tasks).
