---
title: "Delete a permission set"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Delete-a-permission-set"
---

<span id="scenarios"></span>
## Scenarios

If you no longer use a permission set, you can delete it. Before you delete a permission set, you must revoke all associated authorizations.

<span id="prerequisites"></span>
## Prerequisites


1. You have [created a permission set](https://docs.byteplus.com/en/docs/CloudIdentity/Create-a-permission-set).

2. You are an organization master account, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure


1. Log in to the BytePlus console by using an authorized IAM sub\-user under the organization administrator account and go to the [Permission sets](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/permissionSet/) page. This page displays the list of all existing permission sets. You can directly delete a permission set without any associated authorization. To delete a permission set with associated authorizations, you must revoke the associated authorizations. This prevents impacts on your business.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_03f91ac26dbbaab90bc68331ea2b5290.png) </span>


2. Click the name of the permission set that you want to delete to go to its details page. At the bottom of the details page, you can view the accounts to which the permission set has been synchronized. Select all accounts, and click **Clear all synchronized data**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_22b33b5820004e6a3cff9e4c9751cfbf.png) </span>


3. On the page that appears, **revoke authorizations**. You can view all existing authorizations and must revoke all of them before clearing the synchronized data. Click **Revoke all authorizations**. Wait until the task is complete, and click **Next**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3aecff6f97d1878beb22824ee9f86ed2.png) </span>


4. In the **Clear synchronized data** step, click **Clear**. Wait until the task is complete, and return to the list page to delete the permission set.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f058ce8a9d7a71b7a5e1969c6af15a86.png) </span>
