---
title: "Managing roles"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-roles"
---

You can assign different roles based on the job scope or business needs. Leveraging role groups, admin would be able to quickly manage permissions and policies under different modules across the platform.

<span id="ae875545"></span>
# Business use case

Role management is a cornerstone of professional division of labor within an organization. By defining roles and assigning resource permissions, it streamlines access control and ensures that permissions are automatically inherited when an employee's status changes, such as during a promotion or department transfer.

The system supports both custom\-defined roles and roles synchronized from third\-party data sources. It features static and dynamic roles and leverages Attribute\-Based Access Control (ABAC) to enable flexible and powerful access policies.

Furthermore, the system can automatically maintain role memberships based on predefined rules, significantly improving operational efficiency. These roles can be cascaded and referenced by downstream applications, allowing for more granular control over who can access what. Core features include creating custom roles, configuring dynamic rules, syncing roles from external sources, and comprehensive management capabilities like editing, deleting, searching, importing, and exporting.

<span id="1ee3024c"></span>
# Type of roles


* **Static Role**: A role manually assigned to multiple users by the administrator, typically based on their function or department. Once set, these roles remain unchanged unless the administrator manually adjusts them. SealSuite also supports synchronizing role information from third\-party data sources, eliminating the need to repeatedly configure the relationships between roles and users.

* **Dynamic Role**: A role created by the administrator based on rules set according to user attributes. SealSuite automatically aggregates users who meet the criteria. These roles can be automatically adjusted based on attributes.


<span id="ce96b843"></span>
# Managing static roles

Static roles are suitable for scenarios with well\-defined roles and permission assignments. This method is best suited for scenarios where roles and permissions are relatively stable, as any changes to assigned permissions must be manually implemented.

<span id="0b5a8ee4"></span>
## Adding static roles


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Roles** page, select the **Static** tab:

   * Click **Add** at the bottom of the role list to create a new custom role.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8cc58a0bd2d473ba21b473ee7b43fc0~tplv-goo7wpa0wc-image.image) </span>

   * You can also click **Add from Library** to quickly add roles from the role library. Roles that already exist cannot be selected from the role library.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d431a5f1e9444024873e21c92c4a54e6~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If using user roles for the first time, click <strong>Add Role</strong> in the middle of the page.   </div>
   

4. In the **Add Role** dialog box, follow the instructions provided below, then click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Role Name |Enter the Role Name for identifying this role, names must be unique, with a maximum of 30 Chinese characters. For example, HR, Customer Service, Sales, etc. |
   |Role Description |Enter the role description to understand the functions of this role, with a maximum of 50 Chinese characters. For example: The Administrator is responsible for general and permission management, developers handle software development and maintenance, and testers focus on software testing and quality assurance, among other roles. |
   |Role Type |Select **Static Role**. A Static Role assigns specific roles to various users based on their functions or departments within SealSuite. For example, business, research and development, product manager, etc. |
   |Static Role Scope |Role scope refers to which users are included in the role; you can select designated users or departments. |
   


<span id="3479fe55"></span>
## Adding users to a role

After adding a role, you can add users to that role. The users in the role will have the relevant permissions and policies will be applied to the role.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Static** page, select the corresponding static role from the role list on the left, and click **Add User** in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2a16d7c628d4d6883e62b505b6b9f07~tplv-goo7wpa0wc-image.image) </span>

4. On the **Add User** page, configure relevant parameters, and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Scope** |You can select individual users or departments. |
   |**Effective Time** |Set the expiration period for a user's role. Once the expiration period is exceeded, the user will be removed from the role and no longer possess the relevant permissions and policies of the role.<br><br><br>* **Permanent**: The user permanently holds the role.<br><br>* **Custom**: Custom expiration period for the role. Applicable for scenarios where permission is needed temporarily, such as external collaborators, etc., within a specific time period. |
   


<span id="08d39ceb"></span>
## Modify a user's role expiration period

You can modify the expiration period of a user's role, for example, when the user's role has expired, you can extend the expiration period or change it to permanent.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Static** page, select the corresponding static role from the role list on the left. In the user list for that role, you can modify the role expiration period for a single user or make bulk changes to the role expiration period for multiple users:

   * Individual modification: Select the desired user, click **Edit** in the **Action** column, modify the expiration, and then click **Confirm**.

   * Bulk modification: Select users in bulk, click **Configure Effective Time** in the lower left corner, modify the expiration, and click **Confirm**.


<span id="0ebd5219"></span>
## Editing static roles


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Roles** page, click the **Static** tab, find the specified static role, and click  **···**  on the right side of the role name.

4. Select **Rename** or **Delete role**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19b0b4012b7a4426a1e36b22699773ad~tplv-goo7wpa0wc-image.image) </span>


<span id="5daac144"></span>
# Managing dynamic roles

Dynamic role is suitable for scenarios where there is a need to group users people based on specific characteristics. If you need to manage a large number of enterprise users and find it challenging to accurately pinpoint specific targets for resource control, dynamic role management is a more suitable option. This allows for more flexibility while reducing manual maintenance workload.

<span id="82c160a6"></span>
## Adding dynamic role


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Roles** page, select the **Dynamic** tab.

4. Click **Add** at the bottom of the role list to create a new custom role.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69d730c370294680a8214978155d500a~tplv-goo7wpa0wc-image.image) </span>

5. In the **Add Role** dialog box, complete configuration according to the instructions below and click **Next Step**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Role Name |Enter the Role Name for identifying this role, names must be unique, with a maximum of 30 Chinese characters. For example, HR, Customer Service, Sales, etc. |
   |Role Description |Enter the role description to understand the functions of this role, with a maximum of 50 Chinese characters. For example: The Administrator is responsible for general and permission management, developers handle software development and maintenance, and testers focus on software testing and quality assurance, among other roles. |
   |Role Type |Select **Dynamic Role**. When you choose a dynamic role, SealSuite will automatically aggregate users according to the rules you set. For example, automatically match the corresponding roles based on user attributes such as country, city, sequence, etc. |
   

6. On the **Configuring Dynamic Role Rules** page, complete configuration according to the instructions below, and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Parameter |Define the basic conditions for the dynamic rule. Each parameter is identified by a letter (A, B, C...).<br><br>Click  **+ Add New Parameter** to define multiple conditions. |
   |Logical Expression |Set the combination status for parameters, and link each parameter using an operator. The supported operators are as follows:<br><br><br>* **Operators**: `!`, `in`, `not in`, `>`, `>=`, `==`, `!=`, `<`, `<=`, `+`, `-`, `*`, `/`, `&&`, `\|\|`<br><br>* **Functions**: `begin_of_date()`, `end_of_date()`<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Example Scenario:   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To create a dynamic role for employees whose last day is today, you could define Parameter <code>A</code> as the employee's termination date and Parameter <code>B</code> as the current time. The expression would be: <code>B-begin_of_date(A)>=0 && end_of_date(A)-B>=0</code>.   </div><br>    |
   |Allowlist |Click on **Allowlist**. Once selected, you can choose from user or department criteria. The selected effect users will automatically be added to the role, regardless of whether the rule is triggered or not. |
   |Blocklist |Click on **Blocklist**. Once selected, you can choose from user or department criteria. No matter if the rule is triggered, the selected users will not be added to the role. |
   


<span id="dfdfd1d2"></span>
## Editing dynamic roles


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Roles** page, click the **Dynamic** tab to find the specified dynamic role, you can:

   * Rename role: Click **Rename**.

   * Delete role: Click **Delete**. After deleting the role, all users in the role will be removed, and the role's policy will become ineffective.

   * Change dynamic rules: Click **Edit dynamic rules** to modify the dynamic rules, allowlist, and blocklist of the role.

   * Manual Update: Click **Manual Update** to update the role list.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6531f536d32457daf83788810549ca6~tplv-goo7wpa0wc-image.image) </span>


<span id="b21f0026"></span>
# Importing static roles

You can import static roles in bulk and set users in the static role. You can also use this feature to bulk import users for existing roles.


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Roles** page, click **Import** in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea587e1627304a479ef4b1233e2e17c6~tplv-goo7wpa0wc-image.image) </span>

4. Download the role import template and fill in the required parameters according to the template instructions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If only <strong>roles</strong> are filled in the import template, only roles are created after import, and no users are added to the roles.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <strong>Role + User information</strong> is populated in the import template, the corresponding user will be added to the role after it is created.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">User ID and other user information need to be consistent with the user information in the SealSuite Admin Console. For details, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/docs-managing-members">Managing users</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For imported users, the expiration period of their role is permanent by default.   </div>
   

5. Upload the role import template, and click **Start**.


<span id="e50ff8b4"></span>
# Exporting all roles


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Identity** \> **Roles**.

3. On the **Roles** page, click **Export** in the top right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7b25b30f07049d39ad1aae4e1b36a47~tplv-goo7wpa0wc-image.image) </span>

4. In the **Export role** dialog box, choose **All roles** or **Selected role**, and click **Next Step**.

   * **All roles**: Export all roles in the current user roles list.

   * **Selected role**: Choose the specified range of roles for export.

5. Choose the columns for the export role and click **Next Step**.

6. Confirm export role data, choose an export format **CSV file (.csv)**  or **Excel file (.xlsx)** , and click **Confirm**.

   You can view the list of exported files in the top right corner of the page, and choose to **Download** or **Ignore**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61d8052c835f4482a963bee760556e73~tplv-goo7wpa0wc-image.image) </span>


<span id="d9008f5a"></span>
# Related documentation

[Integrating third-party data sources](https://docs.byteplus.com/docs/sealsuite/docs-importing-data-from-third-party-upstream-sources-)

[Configuring custom attributes](https://docs.byteplus.com/docs/sealsuite/docs-configuring-custom-attributes)
