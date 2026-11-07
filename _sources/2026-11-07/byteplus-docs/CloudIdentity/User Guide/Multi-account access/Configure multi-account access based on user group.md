---
title: "Configure multi-account access based on user group"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Configure-multi-account-access-based-on-user-group"
---

<span id="scenarios"></span>
## Scenarios

After creating user groups in Cloud Identity, you can grant multiple organization users the permission to access multiple accounts at a time based on user group.

<span id="prerequisites"></span>
## Prerequisites


1. You have created a user group in [User groups](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userGroup/) in Cloud Identity.

2. You are an organization administrator, such as the root user or an authorized IAM sub\-user.


<span id="procedure"></span>
## Procedure

The following scenario is used as an example:

> Employees in the IT O&M department require IAM user accounts to access the BytePlus account (WorkLoad) within the organization. They can create IAM users within their accounts and log in by using the IAM user account to perform O&M operations.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Make sure that employees in the O&M department are in the IT_maintenance user group.</div>



1. Log in to the BytePlus console by using an authorized IAM sub\-user account under the organization administrator account and go to the [Multi-account access management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/multiAccountAccess/) page. All nodes within the organization are displayed on the left side of the page, and you can select the node to which WorkLoad belongs, select the WorkLoad account, and click **Configure user SSO** under the list.

2. **Specify the user to be authorized** in the pop\-up window. For example, click the user tab and select the IT_maintenance user group. Click Next.

3. Complete **Sync policy configuration**. You can create IAM users with the same usernames under the corresponding accounts to authorize user access permissions. During the creation process, the policies configured in this step will be automatically used to address issues such as duplicate IAM usernames or employee offboarding.



|Policy name |Description |Sample scenario |
|---|---|---|
|**Username conflict** |When the account contains an existing IAM user with the same name as a user in the user group, you can create a new IAM user to replace the existing one, retain both users while adding a username suffix to the new IAM user, or directly bind the IAM user with the username conflict. For more information, refer to [How does the username conflict policy work when granting users SSO permission?](https://docs.byteplus.com/en/docs/CloudIdentity/How-does-the-user-name-conflict-policy-work) |If the employee XiaoShan has an existing IAM user named XiaoShan created in the WorkLoad account, you can create a new IAM user named XiaoShan to replace the existing one, create a new IAM user named XiaoShan\-sso, or bind the user with the username conflict. The IAM user XiaoShan will be associated with the Cloud Identity user XiaoShan and be affected by XiaoShan's onboarding and offboarding status. |
|**Deletion policy** |When a configured user SSO is deleted, the deletion policy allows you to choose whether to retain or remove the synchronized users under the account. **Retaining** synchronized users indicates employees **can still log in** to the corresponding accounts, while **deleting** them indicates employees **can no longer log in** to the corresponding accounts. This policy applies in the following scenarios:<br><br>\- When the permission of an employee with identity source changes due to offboarding, transfer, or other situations, the user SSO task deletion is triggered along with the automatic user deletion by Cloud Identity.<br><br>\- When a Cloud Identity user is removed from a user group, affecting associated user access.<br><br>\- When you manually delete a configured user SSO task while reviewing authorization details for each account in Cloud Identity. |When the employee XiaoShan leaves the IT O&M department, the corresponding Cloud Identity user XiaoShan is removed from the IT_maintenance user group. If XiaoShan has no other access permissions to the WorkLoad account, the IAM user XiaoShan under the WorkLoad account will be either retained or deleted according to the configured deletion policy. If deleted, the IAM user will be removed, and XiaoShan's access permission to the account will be revoked; if retained, the IAM user can still be accessed and used by configuring alternative login methods. |


During policy configuration, you can enter the description for the current user SSO settings and select your preferred policy configuration mode: **batch configuring policies** for all accounts involved in this SSO operation or **configuring policies by account**.

Click Next.


4. View the configuration details. Each user to be authorized will be granted SSO permissions to every designated account according to the synchronization policies you have specified. Click Configure to synchronously create IAM users and configure SSO settings. You can view the configuration task progress and result on the page.


<span id="subsequent-operations"></span>
## Subsequent operations

View account authorization details by referring to [Account authorization details](https://docs.byteplus.com/en/docs/CloudIdentity/Account-authorization-details)

if employees are granted access to multiple accounts.

Refer to [Task management](https://docs.byteplus.com/en/docs/CloudIdentity/Task-management) to address failures.
