---
title: "IAM sub-user management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/sub-user-management"
---

This tutorial introduces how to create a BytePlus IAM sub\-user, grant ByteHouse Enterprise privileges to the IAM sub\-user, log in to ByteHouse Enterprise using the sub\-account, and remove ByteHouse Enterprise privileges or delete the IAM sub\-account.

<span id="0fe3d9fb"></span>
# Background information

ByteHouse Enterprise currently supports managing ByteHouse privileges via IAM sub\-users or database users. The differences between the two are described below. IAM sub\-users are part of the ByteHouse privilege model. For more information about users and the ByteHouse privilege model, please see [Access control model](https://docs.byteplus.com/docs/bytehouse/privilege-model).


| |IAM sub\-user |Database Users |
|---|---|---|
|Definition |A user created by the BytePlus main account user using BytePlus Identity and Access Management (IAM). |Database\-level users created in ByteHouse. |
|Scope of application |Cluster or engine level |Database level |
|Login methods |* ByteHouse Enterprise Console<br><br>* API, connection drivers, command line, and connections to ecosystem tools |API, connection drivers, command line, and ecosystem tool connections |
|Use cases |It is applicable to scenarios that require console operations, unified management across products, and similar scenarios. |It is suitable for scenarios that require fine\-grained management of data access and operation privileges within the database. |


The procedure for creating and managing IAM sub\-users is as follows:


1. **Create IAM sub\-users and grant product privileges**: BytePlus primary user creates IAM sub\-users and grants ByteHouse Enterprise product\-level privileges through the BytePlus IAM Access Control Service.

2. **Sync to ByteHouse**: The main account user syncs IAM sub\-users to ByteHouse in the ByteHouse Enterprise Console.

3. **Data authorization**: The primary user grants data privilege in ByteHouse to IAM sub\-users through roles or direct authorization.

4. **Connect to and use ByteHouse**: After you create an IAM sub\-user and complete authorization, the IAM sub\-user uses the URL to log in to the ByteHouse Console and uses the ByteHouse Enterprise Service.

5. If the IAM sub\-user is no longer in use, the main account user can remove the IAM sub\-user's authorization or delete the IAM sub\-user.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c5f4349d01049ab97e5d8d37c5e2f22~tplv-goo7wpa0wc-image.image) </span>

<span id="e5502539"></span>
# Create and use an IAM sub\-user to log in to ByteHouse

**Applicable users**: BytePlus main account users

<span id="c8b39ca4"></span>
## Create IAM sub\-users

**Steps:** 


1. Log in to the BytePlus [IAM Access Control](https://console.byteplus.com/auth/login/) settings page. In the left navigation bar, select **Identity Management** \> **User**, and click the **Create new user** button.

2. Configure user basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43afc3ad7c0f4c39b10c3f3a7f0f6d24~tplv-goo7wpa0wc-image.image) </span>

3. Configure basic privileges. Grant users privilege to use ByteHouse Enterprise.

   * The current system includes the following preset privilege strategies: "ByteHouseCEFullAccess", "ByteHouseCEStandardAccess", "ByteHouseCEReadOnlyAccess", and "ByteHouseCEEngineOnlyAccess". You can assign the corresponding privilege strategies to users to grant them access to ByteHouse Enterprise.

   * For the Restrict To Project Resources option, please make sure to select **Global**. Otherwise, IAM sub\-users will not be able to access ByteHouse.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"ByteHouseCEFullAccess" Strategy: It corresponds to the <strong>System Admin</strong> role defined in ByteHouse <a href="https://docs.byteplus.com/docs/bytehouse/privilege-model">Access control model</a>, granting users all management privileges for ByteHouse Enterprise.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"ByteHouseCEStandardAccess" strategy: It corresponds to the Query User role defined in ByteHouse <a href="https://docs.byteplus.com/docs/bytehouse/privilege-model">Access control model</a> and grants users read privilege on the Default database in ByteHouse Enterprise.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">"ByteHouseCEReadOnlyAccess" policy: No roles or privileges are granted, but users can log in to the ByteHouse Console and view all clusters. Without additional data authorization, it is not possible to view any data in any cluster.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The “ByteHouseCEEngineOnlyAccess” strategy: No roles or privileges, and cannot log in to the ByteHouse Console. However, users can be synced to ByteHouse, authorized, and granted access to the engine.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After creation, the administrator can still adjust the user's roles. For details, see <a href="https://docs.byteplus.com/docs/bytehouse/role-management">Role management</a>.   </div>
   

4. After completing privilege configuration, click **Next** to review the granted privileges. After confirming that they are correct, click **Next** to complete IAM sub\-user creation.

   Copy or save the account number, password, and Console login address of the IAM sub\-user you create, and provide the account number, password, and other relevant information to the intended user.


<span id="998cd741"></span>
## Sync IAM sub\-users and reset passwords


1. Log in to the [ByteHouse Enterprise Console](https://console.byteplus.com/bytehouse-ce). On the **Access control** \> **User** page, sync the IAM sub\-users created in BytePlus IAM to ByteHouse.

   Before performing this action, make sure that the user has been granted the "ByteHouseCEFullAccess", "ByteHouseCEStandardAccess", or "ByteHouseCEReadOnlyAccess" privilege policies.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b0163d6242840449d97c21a0cfc156d~tplv-goo7wpa0wc-image.image) </span>

   ByteHouse currently supports full sync and incremental sync:

   * **Full sync**: This option syncs all IAM sub\-users granted the ByteHouse strategy. The sync time may be long.

   * **Increment sync**: This option manually fetches existing IAM sub\-users quickly. Click **Increment sync**, select the created IAM sub\-user name from the username dropdown list, click **Confirm**, and the system will immediately sync the IAM sub\-user to the ByteHouse user list.

2. After new IAM sub\-users are synced to ByteHouse, it is recommended that you reset the ByteHouse connection password. The password for a new IAM sub\-user is randomly generated by the system. It is recommended that you set a strong password for the IAM sub\-user to ensure account and data security.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/713cce487d3b401b884579b501cbfcf1~tplv-goo7wpa0wc-image.image) </span>


<span id="402db396"></span>
## Grant database table privileges to users

<span id="977d21b1"></span>
### **Prerequisites**


* Only users with the SystemAdmin role can perform this action.

* The SystemAdmin user or BytePlus primary user already has the highest privilege, so additional authorization cannot be granted.


<span id="fb4b494e"></span>
### Grant privilege through roles


1. In the ByteHouse Enterprise Console, on the \*\*Access control \*\*\> **User** page, click **User name** to view the details page.

2. In the "Grant Roles" settings item, click **Grant roles** to grant roles to the user. If you have not yet set up Roles, you can refer to [Role management](https://docs.byteplus.com/docs/bytehouse/role-management).

3. Select the scope for granting privileges and the roles to which privileges will be granted, and adjust the Admin Option. The Admin Option privilege refers to whether a user is allowed to grant the privileges they have received to other users.

   To grant a user role privileges for multiple clusters, click **Add** to add more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/796ad97a76c841a09e40f48f14cf1fdd~tplv-goo7wpa0wc-image.image) </span>

4. After adding a role, click **Submit**. Role authorization takes effect immediately. You can view the granted privileges in Grant roles, User profile, and Privileges.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72724c3b5492489998c553d60c26ab9d~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) After authorization, if you need to adjust the role privileges granted to the user, go to the 'Grant Roles' settings, click **Edit**, and after making adjustments, click **Submit**.

   The following privileges can be adjusted:

   * Adjust the granted cluster scopes, corresponding roles, and Admin Option.

   * Click **Add** to continue adding clusters and role authorizations.

   * Delete cluster authorization: Hover the mouse over the corresponding cluster row, then click the **Delete** button.


<span id="494abf5f"></span>
### Authorize


1. In the ByteHouse Enterprise Console, on the \*\*Access control \*\*\> **User** page, click **User name** to view the details page.

2. Scroll to the bottom of the page. In the **Privileges** settings section, click **Grant privileges directly**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5fe76f2a83d422dbe9055651d5bb723~tplv-goo7wpa0wc-image.image) </span>

3. On the Authorization Page, select the data privilege type, cluster, database, and privilege point to be assigned. To grant privileges for multiple databases, click **Add** to continue adding databases and privilege points. For details on privilege specifications, please refer to [Description of grantable database and table privileges](https://docs.byteplus.com/docs/bytehouse/privilege-model#e75a2c67).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33d3fa5a94934663a3a56c4074e25984~tplv-goo7wpa0wc-image.image) </span>

4. After privileges have been added, click **Confirm**. The authorization will take effect immediately, and you can view the granted privileges in the **Direct grant** tab of **User Parameters** and **Privileges**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6507f27e13d4466ba27d6cfa48cafd5~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) After authorization, if you need to adjust the granted privileges, do so in the "Privileges" settings. Adjustable privileges are as follows:

   * Increase authorization: Click **Grant privileges directly**, and refer to Step 3 and Step 4 to increase authorization.

   * Revoke privilege

      * Method 1: Expand clusters and databases. Click the **Delete** button next to the database to remove the privilege for the corresponding database.

      * Mode 2: Click **Revoke privileges directly**. In the popup window, select Type, Cluster, Database, and Privilege, then click **Confirm**.


<span id="b33e3e89"></span>
## IAM sub\-user login

<span id="65515088"></span>
### Console access

**Applicable users**: BytePlus IAM sub\-users

**Steps:** 


1. Access the IAM user login link provided by the administrator, and log in using the correct username and password.

2. After logging in to the ByteHouse Enterprise Console, you can use functions such as operations and maintenance management, data management, query, and others online.


<span id="79647ec1"></span>
### Connect via third\-party tools

**Applicable to**: BytePlus IAM sub\-users

ByteHouse Enterprise also provides, by default, support for data integration via graphical interface tools (such as DataGrip, DBeaver, and others), as well as common development tools (such as [ClickHouse Client](https://docs.byteplus.com/docs/bytehouse/clickhouse-client), [JDBC](https://docs.byteplus.com/docs/bytehouse/jdbc), [Python Driver](https://docs.byteplus.com/docs/bytehouse/python-driver), and others). You can view connection commands and instructions in the ByteHouse Console at **Cluster management** \> **Cluster list** \> **Cluster** \> **Connect** tab, or refer to the [official documentation](https://docs.byteplus.com/en/docs/bytehouse/connection) to complete configuration and connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92216a787b2b4cd99cbc34ea5605502e~tplv-goo7wpa0wc-image.image) </span>

<span id="e30da5b5"></span>
# Remove/delete IAM sub\-users

If you need to remove an IAM sub\-user in ByteHouse Enterprise, you can remove that user's ByteHouse data privileges and product privileges. You may also delete the BytePlus IAM sub\-user as needed. This section describes the impact of deleting and removing privilege actions as follows:


|Delete actions |Impact |
|---|---|
|Delete IAM sub\-users in the ByteHouse Enterprise Console |This action will delete users who were synced from BytePlus IAM access control to ByteHouse, and also delete their data privileges in ByteHouse.<br><br><br>* After deletion, the IAM sub\-user still has ByteHouse product privileges.<br><br>* If this IAM sub\-user is re\-synced, they can access the ByteHouse Enterprise Console, but will not have any ByteHouse data privileges. If data access is required, privileges must be granted again.<br><br>* If the IAM sub\-user will no longer use the ByteHouse Enterprise Service in the future, you can go to the BytePlus IAM Access Control page to remove the ByteHouse Enterprise Privieges. |
|Remove ByteHouse Enterprise product privileges in the BytePlus IAM Access Control page |After the privilege is deleted, the user will no longer be able to access ByteHouse Enterprise. |
|Delete IAM sub\-users on the BytePlus IAM Access Control Page |Delete all BytePlus Service privileges granted to IAM sub\-users. |


**Applicable user**: BytePlus main account users

**Steps:** 


1. Delete a ByteHouse Enterprise user.

   Log in to the ByteHouse Enterprise Console, go to **Access control** \> **the User page**, and click the **Delete** button on the right side of the user row. After deletion, the ByteHouse data privileges granted to the IAM sub\-user will remain. You need to go to the BytePlus IAM access control page to remove the relevant ByteHouse privileges. After syncing IAM sub\-user information, the user can still log in to ByteHouse Enterprise via the ByteHouse Enterprise Console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/320e64aa54154170b84ed91199675896~tplv-goo7wpa0wc-image.image) </span>

2. Remove ByteHouseCE\-related privilege policies granted to IAM sub\-user accounts in BytePlus.

   Log in to the BytePlus [IAM Access Control](https://console.byteplus.com/auth/login/) settings page. In the left navigation bar, select **Identity Management** \> **User**, search for the specified user, and click **Username** to enter the user details page. On the **Privilege** tab, search for ByteHouseCE, then click the **Remove privilege** button in the corresponding privilege row.

3. (Optional) Delete IAM subusers. **If there are no other BytePlus services that need to be retained under the IAM sub\-user, you can delete the BytePlus IAM sub\-user as needed.**  Log in to the BytePlus [IAM Access Control](https://console.byteplus.com/auth/login/) settings page. In the left navigation pane, select **Identity Management** \> **User**, then click the **Delete** button on the right side of the user row.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Deleting <strong>a BytePlus IAM sub\-user</strong> may affect the normal use of other BytePlus services under this account. Please proceed with caution.   </div>
