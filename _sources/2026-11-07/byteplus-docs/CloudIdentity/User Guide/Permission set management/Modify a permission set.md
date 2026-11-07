---
title: "Modify a permission set"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Modify-a-permission-set"
---

<span id="scenarios"></span>
## Scenarios

After creating a permission set, you can modify it to change its content. The changes must be synchronously updated to the authorized accounts.

<span id="prerequisites"></span>
## Prerequisites


1. You have [created a permission set](https://docs.byteplus.com/en/docs/CloudIdentity/Create-a-permission-set).

2. You are an organization master account, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure

The following scenario is used as an example:

> You need to add the VPCFullAccess permission to the NetWorkAdmin permission set. This permission is granted to relevant users under the network O&M department, allowing these users to access all accounts under the organization.


1. Log in to the BytePlus console by using an authorized IAM user under the organization master account and go to the [Permission sets](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/permissionSet/) page. This page displays the list of all existing permission sets. You can view the information of all permission sets, including their authorization status and synchronization status. Click the name of the NetWorkAdmin permission set to go to its details page.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6c4cacb1662db1d2e2f2b23a9b01ca79.png) </span>


2. On the details page, you can click to modify the basic information, including the description, session duration, and initial page to access. The changes take effect immediately after you click Submit. Users who log in with the new access permissions after the submission are affected, while users who have logged in before the submission are not affected.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a8117160d0811eaace8a8b8a0750e563.png) </span>


3. On the details page, view existing predefined system managed policies and click **Add**.

   1. On the page that appears, **select a system managed policy**. In this case, search for and select VPCFullAccess, and click Add.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0b566462620ef54ec1be81a83b3c7ce9.png) </span>


2. Synchronize the change to all authorized accounts with one click to ensure the authorization rules of each account accessed from Cloud Identity are synchronously updated. Click **Synchronize**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c4413915d1249964ed9949651b33c5ab.png) </span>


4. On the details page, you can also delete existing predefined system policies or create or modify custom built\-in policies. After modifying the permission set, synchronously update the changes to all authorized accounts.


<span id="what-to-do-next"></span>
## What to do next

After modifying a permission set, you can

[configure role-based access authorization](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-role-based-access-authorization) to authorize Cloud Identity users.
