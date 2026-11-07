---
title: "Task management"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Task-management"
---

<span id="scenarios"></span>
## Scenarios

When you configure access permissions for or revoke access permissions from users, you may need to check the configuration history or handle any potential failures. Failure scenarios include:


1. Role access: Failures may occur during the granting or revocation of role access permissions or during the synchronization of permission sets to accounts or permission set cleanup.

2. User access: Failures may occur during the permission authorization for users due to network issues or configuration conflicts. If failures occur, the corresponding authorization failure record will be generated. You can go to Task management \> Failed authorizations to resolve the failure as prompted.


<span id="prerequisites"></span>
## Prerequisites


1. You have configured role access or user access. Otherwise, you must [configure user access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-user-based-access-authorization) or [configure role access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-role-based-access-authorization).

2. You are an organization administrator, such as the root user or an IAM sub\-user with read/write permissions in Cloud Identity.


<span id="procedure"></span>
## Procedure


1. Log in to the BytePlus console by using an authorized IAM sub\-user account under the organization administrator account and go to the [Task management](https://console.bytplus.com/cloudidentity/region:ap-southeast-1/authTaskManagement/) page.

2. On the Role access tab, you can view all task execution records.

   1. For authorization, revocation, synchronization, and synchronized data cleanup tasks, you can check their execution status, including successful and failed.

   2. For failed tasks, you can go to the corresponding page to retry the tasks. However, the related failure records will not be cleared.

3. On the User access tab, you can view the failed authorization records.

   1. For each failed authorization record, you can view the specific failure reason. For example, user conflicts that cannot be automatically resolved exist. To address this issue, you need to clear redundant data or correct relevant configurations before authorization.

   2. For addressed records in the list, you can submit them for task execution again. Unnecessary records can be deleted. Cloud Identity will no longer process authorization for any deleted failure records.
