---
title: "Configure user-based access authorization"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Configure-user-based-access-authorization"
---

<span id="configure-user-access"></span>
# Configure user access

<span id="scenarios"></span>
## Scenarios

After creating Cloud Identity users, you must grant them permissions to log in to and access different accounts.

<span id="prerequisites"></span>
## Prerequisites


1. You have created a Cloud Identity user. Otherwise, go to configure [user synchronization settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/) or refer to [Basic user management](https://docs.byteplus.com/en/docs/CloudIdentity/Basic-user-management).

2. You are an organization administrator, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure

The following scenario is used as an example:

> The employee XiaoShan requires access to two BytePlus accounts (WorkLoad and SandBox) within the organization. He/She can create IAM users within the corresponding accounts separately and log in by using the IAM user account through User SSO to perform operations.


1. Log in to the BytePlus console by using an authorized IAM sub\-user account under the organization administrator account and go to the [Multi-account access management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/multiAccountAccess/) page. All nodes within the organization are displayed on the left side of the page, and you can select the nodes to which WorkLoad and SandBox belong, select the WorkLoad and SandBox accounts, and click **Configure user SSO** under the list.

2. **Specify the user to be authorized** in the pop\-up window. The user must be a Cloud Identity user to whom SSO permissions are to be granted. In this example, for the employee XiaoShan, whose Cloud Identity username is XiaoShan, select XiaoShan in this step and click Next. If you cannot find XiaoShan, you can filter usernames by department.

3. Complete **synchronization policy configuration**. User SSO is implemented by synchronously creating IAM users with the same username within the corresponding accounts. This process automatically configures the appropriate SSO method for your IAM users. When creating IAM users and configuring SSO methods, the policies configured in this step will be automatically used to address issues such as duplicate IAM usernames or employee offboarding.



|Policy name |Description |Sample scenario |
|---|---|---|
|**Username conflict** |When the account contains an existing IAM user with the same name as the one you are creating, you can create a new IAM user to replace the existing one, retain both users while adding a username suffix to the new IAM user, or directly bind the IAM user with the username conflict. For more information, refer to [How does the username conflict policy work when granting users SSO permission?](https://docs.byteplus.com/en/docs/CloudIdentity/How-does-the-user-name-conflict-policy-work) |When the employee XiaoShan already has an existing IAM user named XiaoShan created in the WorkLoad account, you can create a new IAM user named XiaoShan to replace the existing one, create a new IAM user named XiaoShan\-sso, or bind the user with the username conflict. The IAM user XiaoShan will be associated with the Cloud Identity user XiaoShan and be affected by XiaoShan's onboarding and offboarding status. |
|**Deletion policy** |When a configured user SSO is deleted, the deletion policy allows you to retain or remove the synchronized users under the account. **Retaining** synchronized users indicates that employees **can still log in** to the corresponding accounts, while **deleting** them indicates that employees **can no longer log in** to the corresponding accounts. This policy applies in the following scenarios:<br><br>\- When the permission of an employee with identity source changes due to offboarding, transfer, or other situations, the user SSO task deletion is triggered along with the automatic user deletion by Cloud Identity.<br><br>\- When a Cloud Identity user is removed from a user group, associated user access permissions are affected.<br><br>\- When you manually delete a configured user SSO task while reviewing authorization details for each account in Cloud Identity. |When XiaoShan resigns from the company, his Cloud Identity user XiaoShan shall be deleted. In this case, you can delete or retain the IAM users in both the WorkLoad and SandBox accounts. If deleted, XiaoShan will no longer have permissions to log in to the corresponding accounts; if retained, the IAM users can still be accessed and used by configuring alternative login methods. |


During policy configuration, you can enter the description for the current user SSO settings and select your preferred policy configuration mode: **batch configuring policies** for all accounts involved in this SSO operation or **configuring policies by account**.

Click Next.


4. View the configuration details. Each user to be authorized will be granted SSO permissions to every designated account according to the sync policies you have specified. Click Configure to synchronously create IAM users and configure SSO settings. You can view the configuration task progress and result on the page.


<span id="what-to-do-next"></span>
## What to do next

If employees are granted access permissions to multiple accounts, and you want to designate an employee as the account administrator, you can click Set as admin on the page or grant the employee administrator permission by referring to [Account authorization details](https://docs.byteplus.com/en/docs/CloudIdentity/Account-authorization-details) to grant its IAM users the AdministratorAccess permission. In this case, authorization tasks can be assigned to IAM users for convenience.

View account authorization details by referring to [Account authorization details](https://docs.byteplus.com/en/docs/CloudIdentity/Account-authorization-details) if employees are granted access permissions to multiple accounts.

Refer to [Task management](https://docs.byteplus.com/en/docs/CloudIdentity/Task-management) to address failures.

After authorization is completed, you can distribute the Cloud Identity portal URL to employees. Using this URL, employees can log in to their authorized BytePlus accounts.
