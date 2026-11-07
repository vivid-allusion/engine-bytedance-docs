---
title: "Granting RBAC permissions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions"
---

VKE allows you to grant role\-based access control (RBAC) permissions to Identity and Access Management (IAM) users and IAM roles. This topic mainly describes the procedure for granting RBAC permissions.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For an introduction to IAM identities (IAM users and IAM roles), see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management">User management</a> and <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management">Role management</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

Only the following accounts or IAM identities (IAM users or IAM roles) can grant cluster RBAC permissions:


* BytePlus root user (owner): has full permissions on clusters and can directly configure RBAC.

* Cluster creator: Regardless of whether a cluster creator is the root user or an IAM identity, the creator is granted RBAC administrator permissions on the cluster by default.

* Regular IAM users or IAM roles can grant RBAC permissions only when they meet both of the following conditions.

   * The root user or the cluster creator has granted the management permissions for the target cluster in the console or by calling the [GrantPermission](https://docs.byteplus.com/en/docs/vke/GrantPermission) API. Alternatively, they already have the RBAC permissions at the **account cluster level**.

   * A global permission policy, such as IAMFullAccess or IAMReadOnlyAccess, is attached to them.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Permissions related to VKE have been granted to IAM users. For detailed operations, see [Configuring IAM user permissions](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions).

* IAM roles have been created. For detailed operations, see [Managing roles](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management).


<span id=".6YWN572uLWlhbS3nlKjmiLfnmoQtcmJhYy3mnYPpmZA="></span>
## Granting RBAC permissions to IAM users


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Authorizations** \> **User authorization**.

3. On the **User authorization management** page, click **Batch user authorization**.

4. On the **Create user authorization** page, select the target IAM users and grant RBAC permissions to them based on the system prompts.

   
   |Parameter |Description |
   |---|---|
   |User  |In the **All users ** section, select the check boxes before the names of the IAM users to which you want to grant the same RBAC permissions. |
   |Permissions |Grant access permissions to the selected IAM users based on the content in the **Access permission description** section in the console. You can grant access permissions to the users from the following three dimensions:<br><br><br>* Account cluster level: Select **Account All Resources \> Account Cluster Level**. It indicates that the selected IAM user has corresponding permissions on all existing clusters and newly created clusters within the current root user.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only the root user or the IAM user that has <strong>account cluster\-level</strong> permissions can view the <strong>Account Cluster Level</strong> parameter under the Account All Resources parameter.   </div><br>   <br><br>* Cluster level: Select a cluster and all namespaces. It indicates that the selected IAM user has corresponding permissions on all existing and newly added namespaces within the selected cluster.<br><br>* Namespace level: Select a cluster and a namespace. It indicates that the selected IAM user has corresponding permissions on the selected namespace within the selected cluster.<br><br><br>For more information about **access permissions**, see [Description of RBAC permissions and roles](https://docs.byteplus.com/en/docs/vke/RBAC-roles). |
   

5. (Optional) Click **Add permissions** to grant multiple RBAC permissions to the selected IAM users.

6. Click **Confirm**. The RBAC permissions are granted to IAM users.


<span id=".6YWN572uLWlhbS3op5LoibLnmoQtcmJhYy3mnYPpmZA="></span>
## Granting RBAC permissions to the IAM roles


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Authorizations** \> **Role authorization**.

2. On the **Role authorization management** page, enter the name of the IAM role to be granted RBAC permissions in the **Role name** field, and then click **Administrative role permissions**.

   You can obtain the role name on the **User management** \> **Role Management** page of the [IAM console](https://console.byteplus.com/iam).

3. On the **role authorization details page**, click **Add role authorization**. Grant RBAC permissions to the IAM role based on the system prompts.

   
   |Parameter |Description |
   |---|---|
   |Role |The name of the IAM role being configured. You cannot modify the name. |
   |Permissions |Grant cluster\-level and namespace\-level access permissions to the IAM role based on the content in the **Access permission description** section in the console. You can grant access permissions to the role from the following three dimensions:<br><br><br>* Account cluster level: Select **Account All Resources \> Account Cluster Level**. It indicates that the selected IAM role has corresponding permissions on all existing clusters and newly created clusters within the current root user.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only the root user or the IAM role that has <strong>account cluster\-level</strong> permissions can view the <strong>Account Cluster Level</strong> parameter under the Account All Resources parameter.   </div><br>   <br><br>* Cluster level: Select a cluster and all namespaces. It indicates that the selected IAM role has corresponding permissions on all existing and newly added namespaces within the selected cluster.<br><br>* Namespace level: Select a cluster and a namespace. It indicates that the selected IAM role has corresponding permissions on the selected namespace within the selected cluster.<br><br><br>For more information about **access permissions**, see [Description of RBAC permissions and roles](https://docs.byteplus.com/en/docs/vke/RBAC-roles). |
   

4. (Optional) Click **Add permissions** to grant multiple RBAC permissions to the selected IAM role.

5. Click **Confirm**. The RBAC permissions are granted to the IAM role.


<span id="hdYwFmqw"></span>
## Related documentation

[Using the new RBAC permission management system](https://docs.byteplus.com/en/docs/vke/Use_the_new_VKE_RBAC_authorization_system)
