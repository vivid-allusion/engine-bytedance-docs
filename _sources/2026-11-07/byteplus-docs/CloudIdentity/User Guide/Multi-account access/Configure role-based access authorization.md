---
title: "Configure role-based access authorization"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Configure-role-based-access-authorization"
---

<span id="scenarios"></span>
## Scenarios

After creating Cloud Identity users, you must grant them permissions to log in to and access different accounts.

When access permissions on BytePlus cloud resources share commonalities, such as network O&M permissions or security management permissions, we recommend that you predefine permission sets on Cloud Identity to authorize Cloud Identity users to access different accounts.

This solution enables centralized user authorizations under the management account of Cloud Identity, avoiding authorization management across multiple accounts and simplifying O&M on enterprise personnel permissions.

<span id="prerequisites"></span>
## Prerequisites


1. You have [synchronized a user](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userSync/) to Cloud Identity or [created a user](https://docs.byteplus.com/en/docs/CloudIdentity/Basic-user-management) on Cloud Identity.

2. You have [created a permission set](https://docs.byteplus.com/en/docs/CloudIdentity/Create-a-permission-set).

3. You are an organization administrator, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure

The following scenario is used as an example:

> Xiaoshan, a network O&M engineer at a company, needs to access two BytePlus accounts (WorkLoad and SandBox) of the organization with network O&M administrator permissions to read and write network resources under the two accounts.


1. Log in to the BytePlus console using an authorized IAM sub\-user under the organization administrator account and go to the [Multi-account access](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/multiAccountAccess/) page. The left side of the page displays all nodes within the organization.

2. First, **specify the accounts to access**. On the Role access tab, click Configure role access. Select the nodes where WorkLoad and SandBox reside, select the WorkLoad and SandBox accounts, and click **Configure** under the list.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a73b94de08a58fc43808211bc24a73c6.png) </span>


3. In the pop\-up window, **specify the user to authorize**. Here, specify the Cloud Identity user to whom you want to grant the SSO permission. In this example, select XiaoShan, the username of Xiaoshan in Cloud Identity, and click Next. If you cannot find XiaoShan, you can filter usernames by department. After completing the configuration, click Next.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c2202cde1faa66c9799a71a0356d8b3c.png) </span>


4. In this step, select **a permission set** to specify the permissions that the Cloud Identity user has when accessing BytePlus accounts. For more information about how to create a permission set, refer to [created a permission set](https://docs.byteplus.com/en/docs/CloudIdentity/Create-a-permission-set). Select the necessary access permissions, and click Next.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b2e2c123f7bc49b98af865f8945e556f.png) </span>


5. In this step, you can view the configuration details, including all users to authorize, all accounts to access, and the permission set available during access. Check the configuration, and click **Configure**. You can view the progress and result of each configuration task on the page.


<span id="what-to-do-next"></span>
## What to do next

After authorizing an employee to access multiple accounts, you can [view account authorization details](https://docs.byteplus.com/en/docs/CloudIdentity/Account-authorization-details).

If a failure occurs, you can [Task management](https://docs.byteplus.com/en/docs/CloudIdentity/Task-management) to handle it.

After the authorization is completed, you can distribute the URL of the Cloud Identity portal to the employees. Using this URL, the employees can log in to BytePlus accounts that they have the permission to access.
