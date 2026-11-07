---
title: "Account authorization details"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Account-authorization-details"
---

<span id="account-authorization-details"></span>
# Account authorization details

<span id="scenarios"></span>
## Scenarios

After you configure user access on the Multi\-account access management page, you can view the access authorization details of each account.

<span id="prerequisites"></span>
## Prerequisites


1. You have configured user access. Otherwise, you must [configure user access](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/multiAccountAccess/).

2. You are an organization master account, such as the root user or an authorized IAM user with read/write permissions in Cloud Identity.


<span id="procedure"></span>
## Procedure


1. Log in to the BytePlus console by using an authorized IAM sub\-user account under the organization administrator account and go to the [Multi-account access management](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/multiAccountAccess/) page. Click the name of the account displayed in the list to enter the account authorization details page.

2. You can view the basic information of the account on the account authorization details page, which is consistent with the account information in the organization. You can also view the configured user access. If you want to revoke the access permission from an employee, delete the corresponding user access authorization task.

3. On the account authorization details page, you can click **Set as admin** in the Action column to set an authorized Cloud Identity user as the administrator and grant its IAM users the AdministratorAccess permission. In this case, the Cloud Identity user has the permissions of an administrator. Authorization tasks can be assigned to IAM users for convenience. You can click **Remove admin** in the Action column to revoke the administrator permission from the user.


<span id="what-to-do-next"></span>
## What to do next

To proceed with access permission configuration, refer to [Configure user access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-user-based-access-authorization).
