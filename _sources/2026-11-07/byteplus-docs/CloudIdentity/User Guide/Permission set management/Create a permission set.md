---
title: "Create a permission set"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Create-a-permission-set"
---

<span id="scenarios"></span>
## Scenarios

After creating Cloud Identity users, you must grant them permissions to log in to and access different accounts.

When access permissions on BytePlus cloud resources share commonalities, such as network O&M permissions or security management permissions, you can predefine permission sets on Cloud Identity as permission templates for centralized authorization. Cloud Identity synchronizes and distributes permission sets to each account, reducing the permission O&M costs of your enterprise.

<span id="prerequisites"></span>
## Prerequisites


1. You have [activated Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/Activate-Cloud-Identity).

2. You are an organization master account, such as the root user or an authorized IAM user.


<span id="procedure"></span>
## Procedure

The following scenario is used as an example:

> You need to grant standard network resource administrator permissions to the network O&M department.


1. Log in to the BytePlus console by using an authorized IAM sub\-user under the organization administrator account and go to the [Permission sets](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/permissionSet/)page. This page displays the list of all existing permission sets. Click **Create permission set**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_75d877a811915aea61f1872784a301e6.png) </span>


2. On the page that appears, **configure basic information** for the permission set. You need to configure the following fields:

   1. Name: This field is required. It uniquely identifies a permission set.

   2. Description: This field is optional. It describes the business function of a permission set.

   3. Session duration: This field is required. It specifies the maximum duration of the session after a Cloud Identity user logs in to the console with these permissions. The default value is 8 hours.

   4. Initial page to access: This field is optional. It specifies the first console page to which a Cloud Identity user is redirected after the user logs in to the console with these permissions. Enter a real and valid BytePlus console address. If you leave this field empty, users are logged in to the console homepage by default.

      After completing the configuration, click Next.

3. In the **Add policy** step, specify all the permissions to be included in the permission set. You can add permissions in the following two ways:

   1. Select existing predefined system policies for access control. You can add up to 20 predefined system policies to a permission set.

   2. Add custom built\-in policies. You can directly write custom built\-in policies in the visual editor or the JSON editor. After being added, the policies are synchronized to the corresponding account. When the corresponding Cloud Identity user accesses the account, these permissions are granted to the user.

      After completing the configuration, click Submit.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b1cb85193707763e99e70a02b80bada7.png) </span>

<span id="what-to-do-next"></span>
## What to do next

After creating a permission set, you can [configure role access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-role-based-access-authorization) to authorize Cloud Identity users.
