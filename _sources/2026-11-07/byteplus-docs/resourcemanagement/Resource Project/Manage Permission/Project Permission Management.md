---
title: "Project Permission Management"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Project_Permission_Management"
---

Once resources are assigned to a project, you can designate an independent administrator for the project, granting the administrator management permissions on resources in the project. This topic introduces how to authorize and manage permissions based on projects.

> To grant project\-based permissions, you need to define the scope of authorization. If no specific scope is set, the default scope is global, meaning the authorization applies to both existing and future related resources within the account.


<span id="viewing-project-authorization"></span>
## Viewing project authorization

You can view project authorization details by using any of the following methods:

<span id="method-1-view-project-authorizations-by-resource-project"></span>
### Method 1: View project authorizations by resource project


1. Log in to [Resource project > Project](https://console.byteplus.com/iam/resourcemanage/project).

2. Click Permission policy to go to the project authorization page.

3. Search for specific authorizations by identity type or identity display name.

> Note: This view only displays identities and policies that have been involved in project permission authorization. To view all policies assigned to a specific identity, refer to Method 2.


<span id="method-2-view-project-authorizations-by-identity"></span>
### Method 2: View project authorizations by identity


1. Log in to [IAM](https://console.byteplus.com/iam).

2. Select the identity you want to check, such as a user, role, or user group.

3. Click the identity name to go to its details page.

4. Go to the Permission tab. If a project restriction exists, the identity has permissions only for the specified project. If no project restriction exists, the identity has permissions for all related resources within the account.


<span id="method-3-view-project-authorizations-by-permission-policy"></span>
### Method 3: View project authorizations by permission policy


1. Log in to [IAM](https://console.byteplus.com/iam).

2. Go to the Policy management page.

3. Click a specific permission policy to view its authorization details.

4. If a project restriction exists, the identity has permissions only for the specified project. If no project restriction exists, the identity has permissions for all related resources within the account.


<span id="granting-project-permission"></span>
## **Granting project permission**

You can grant project\-based IAM permissions using any of the following methods. All three methods offer the same functionality but differ in the management perspective and portal.

<span id="method-1-grant-permissions-by-project"></span>
### **Method 1: Grant permissions by project**


1. Log in to [Resource project > Project](https://console.byteplus.com/iam/resourcemanage/project).

2. Click Permission policy to go to the project authorization page.

3. Click Authorize to go to the permission granting page.

4. Select the identity to be authorized by searching for the identity name or display name, or by filtering identities by identity type. Then, click Next.

5. Search for and select permission policies by policy name or remarks, or by filtering policies by policy type. Then, click Next.

> Note: If a policy is already assigned to the selected identity, you cannot select the policy again. To modify an existing policy, click Modify permission.


6. Confirm the settings and click OK.

7. Complete the authorization.


<span id="method-2-grant-permissions-by-identity"></span>
### **Method 2: Grant permissions by identity**


1. Log in to [IAM](https://console.byteplus.com/iam).

2. Select the identity you want to check, such as a user, role, or user group.

3. Click Add permission to go to the authorization page.

4. Specify to restrict the authorization to a specific project and select permission policies.

5. Click Submit to complete the authorization.


<span id="method-3-grant-permissions-by-permission-policy"></span>
### Method 3: Grant permissions by permission policy


1. Log in to [IAM](https://console.byteplus.com/iam).

2. Go to the Policy management page.

3. Click a specific permission policy and click Authorize to go to the authorization page.

4. Specify to restrict the authorization to a specific project.

5. Select the identity to be authorized.

6. Click Submit to complete the authorization.


<span id="modifying-project-permission"></span>
## **Modifying project permission**

You can modify project permissions using any of the following methods. All three methods offer the same functionality but differ in the management perspective and portal.

<span id="method-1-modify-permissions-by-project"></span>
### **Method 1: Modify permissions by project**


1. Log in to [Resource project > Project](https://console.byteplus.com/iam/resourcemanage/project).

2. Click Permission policy to go to the project authorization page.

3. Click Modify permission to go to the permission policy modification page.

4. Select new policies or remove existing ones and click Next.

5. Confirm the modification and click Next.

6. Review the changes and click Finish.

> Note: If a newly selected policy is globally authorized, its scope will be narrowed from the account level to the project level. This may reduce the permissions of the identity. Proceed with caution to avoid impact on the business operations.


<span id="method-2-modify-permissions-by-identity"></span>
### **Method 2: Modify permissions by identity**


1. Log in to [IAM](https://console.byteplus.com/iam).

2. Select the identity you want to check, such as a user, role, or user group.

3. Click Add permission to go to the authorization page.

4. Click Modify project limit to go to the permission policy modification page.

5. Modify the application scope of the permission policy. If you select Global, the policy applies to the entire account. If you select a specific project, the policy applies only to the project.

6. Click Confirm.


<span id="method-3-modify-permissions-by-permission-policy"></span>
### Method 3: Modify permissions by permission policy


1. Log in to [IAM](https://console.byteplus.com/iam).

2. Go to the Policy management page.

3. Click a specific permission policy and click Authorize to go to the authorization page.

4. Click Modify project limit to go to the permission policy modification page.

5. Modify the application scope of the permission policy. If you select Global, the policy applies to the entire account. If you select a specific project, the policy applies only to the project.

6. Click Confirm.


<span id="remove-project-permissions"></span>
## **Remove project permissions**

To fully remove project permissions from an IAM authorization identity (a user, user group, or role), perform the following steps:


1. Log in to [Resource project > Project](https://console.byteplus.com/iam/resourcemanage/project).

2. Click Permission policy to go to the project authorization page.

3. Locate the identity and click Remove in the Actions column.

> Note: Removing project permissions for the authorized identities or permission policies page only removes the associations between policies and projects. To fully unbind an identity from a project, follow the methods described above.


&nbsp;
