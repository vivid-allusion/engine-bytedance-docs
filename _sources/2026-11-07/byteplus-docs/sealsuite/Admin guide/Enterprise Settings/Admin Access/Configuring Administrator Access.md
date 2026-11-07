---
title: "Configuring Administrator Access"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-administrator_1"
---

To ensure your corporate resources are managed securely, the Admin Access module allows you to define precisely what administrators can see and do. This guide provides detailed instructions for the complete configuration workflow: creating custom roles, defining management scopes for resources, assigning permissions to users, and setting up security alerts.

<span id="6adaab6a"></span>
# Recommended Configuration Workflow

We recommend configuring your administrators in the following order:


1. **Create Admin Roles:**  Roles are the bridge between users and permissions. You can use built\-in roles or create custom ones to define a set of permissions. Assigning roles to users is the foundation of role\-based access control (RBAC).

2. **Define Management Scopes:**  Scopes allow you to group resources (like departments or applications) so you can grant administrators permission to manage only a specific subset of your organization's assets.

3. **Assign Admin Permissions:**  Assign roles and scopes to specific employees, granting them the necessary permissions to manage their designated resources for a defined period.

4. **Configure Admin Alert Policies:**  Set up alerts to be notified of repeated failed login attempts for administrator accounts, helping to prevent security risks.


<span id="f149542e"></span>
# **Step 1: Create an Admin Role**

An admin role is a collection of permissions that defines what an administrator can do. Roles can be either built\-in (pre\-configured by the system) or custom.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Admin Access**.

3. Click the **Admin Role** tab.

4. In the top\-right corner, click **Add Role**.

5. On the **Add Role** page, fill in the following details and click **Finish**.

   
   |**Section** |**Parameter** |**Description** |
   |---|---|---|
   |General |Role Name |A descriptive name for the role (e.g., "Financial Auditor"). Up to 30 characters. Multi\-language support is available. |
   ||Role ID |A unique identifier for the role. |
   ||Role Description |A brief summary of the role's responsibilities. Up to 60 characters. Multi\-language support is available. |
   |Menu Permissions |Menu Permissions |Select the console menus that users with this role will be able to see and access. |
   |Operation Permission |Operation Permission |Select the specific actions that users with this role can perform. Some permissions have dependencies and will be automatically selected. |
   


<span id="7618cb47"></span>
# **Step 2: Define a Management Scope**

Management scopes allow you to group resource objects in SealSuite (such as employees, applications, roles, and tags) so that different administrator roles can manage different resource groups. By segmenting the data resource scope that administrators can operate on, you achieve fine\-grained isolation of sub\-administrator permissions and enforce least\-privilege authorization, preventing unauthorized operations.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Admin Access**.

3. Click the **Admin Scope** tab.

4. In the top\-right corner, click  **+ Add Scope**.

5. On the **Add Scope** page, fill in the following details and click **Finish**.

   
   |**Section** |**Parameter** |**Description** |
   |---|---|---|
   |General |Name |Enter a name for the management resource scope, up to 30 characters. Click the multilingual button on the right to set the name in different languages. |
   ||Description |Enter a description for the management resource scope, up to 60 characters. Click the multilingual button on the right to set the description in different languages. |
   |Unit scope |User Scope |Restrict administrators to managing employee permissions only within specified departments, departments and their sub\-departments, or specific roles. This isolates personnel management permissions, ensuring that administrators only manage employees within their designated scope of authority.<br><br>> Notes: The **Role** scope currently only applies to the Data Security module. |
   ||Application Scope |Restrict administrators to configuring and managing permissions only for specified business applications. |
   ||Role Scope |Restrict administrators to managing only the specified roles (for example, they can only manage the Intern role and no other roles).<br><br>> Notes: This feature currently only applies to the Role Management and Single Sign\-On modules. |
   ||Manage tag scope |Restrict administrators to managing only resources associated with specified tags. This achieves resource permission isolation at the tag level, allowing different administrators to manage resources under their respective tags.<br><br><br>* **All**: Selected by default. Grants the administrator access to resources under all tags.<br><br>* **Partial tags**: Opens a tag selector after selection, allowing you to choose one or more tags from the tag library for fine\-grained authorization.<br><br>> Notes:<br><br>> 1. Tag\-based visibility control currently applies only to the **Data Security** and **Assets** (Device Group) modules.<br><br>> 2. To assign **Partial tags** to an administrator, make sure the corresponding resource tags have been created in the **Tag Library** in advance. For detailed instructions, see [Managing the tag Library](https://docs.byteplus.com/docs/sealsuite/managing-the-tag-library). |
   


<span id="5a657df5"></span>
# **Step 3: Assign Admin Permissions to a User**

This step assigns a role and a scope to a specific employee.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Admin Access**. You can assign permissions in two ways:

   * **From the Admin Role Tab:** 

      1. Find the role you want to assign and click **Add Admin User** in its row.

      2. In the dialog, select the users, the management scope they can manage, and the effective time. Click **Confirm**.

   * **From the Admin Permission Tab:** 

      1. Click **Add Admin User** in the top\-right corner.

      2. In the dialog, select the role name, the users, the management scope they can manage, and the effective time. Click **Confirm**.


<span id="e65a8e75"></span>
# **Step 4: Configure Admin Alert Policies**

Set up security alerts to be notified when an admin account experiences multiple consecutive failed login attempts.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Admin Access**.

3. On the **Settings** tab, set the threshold for failed login attempts and check the box to enable alert notifications.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ede25c95013e4637b84d14b892ca258d~tplv-goo7wpa0wc-image.image) </span>

4. Click **Notification** in the top\-right corner.

5. On the **Edit Notification** page, configure your desired notification channels and click **Effective now**.

   You can choose to send alerts via SMS, email, or a third\-party IM integration.

   
   |**Channel** |**Description** |
   |---|---|
   |SMS |Enter up to 5 mobile numbers, separated by the `Enter` key. |
   |Email Notification |Enter up to 5 email addresses, separated by the `Enter` key. |
   |IM Notification |Select a pre\-configured IM bot from the drop\-down list. If you need to add a new one, click **New Integration**. For instructions, see [Manage third-party IM](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#7e2d6168). |
   


<span id="2352714d"></span>
# **Configuring Multi\-Factor Authentication (MFA) for Sensitive Admin Actions**

For enhanced security, you can require administrators to perform multi\-factor authentication before executing high\-risk operations.

**Sensitive actions include:** 


* Bulk exporting users and departments.

* Exporting the device list.

* Disabling an MFA authentication scenario.

* Creating an API Access Key.

* Editing MDM policies or executing MDM scripts.

* Adding or editing endpoint firewall policies.

* Distributing software.

* Viewing the details of Agent interaction tasks.

* Adding or editing admin roles or permissions.

* Modifying this MFA setting itself.


**How to Configure**


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Admin Access**.

3. On the **Settings** tab, enable the **When Administrators Perform Sensitive Operations, They Need Identity Authentication** toggle.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only a Super Administrator can enable or disable this feature and must perform MFA to do so. Other administrators can only adjust the authentication methods when the feature is already on.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4317f4d89b0439990a602fbe576c5e3~tplv-goo7wpa0wc-image.image) </span>

4. Configure the authentication methods:

   * Click **Edit** to set a **Primary Authentication Method** (required, single choice: MFA, SMS, or Email) and one or more **Backup Authentication Methods** (optional).

   * Set the **MFA Exemption Period** (5\-30 minutes). After a successful MFA verification, the admin will not be prompted again within this time frame.


<span id="368481bc"></span>
# **Next Steps**

After adding an administrator, you can modify their role or scope at any time to reflect organizational changes. To learn how, see [Editing Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-editing-or-deleting-administrator).
