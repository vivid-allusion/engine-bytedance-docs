---
title: "Log in to the Cloud Identity portal to access BytePlus cloud resources"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Log-in-to-the-Cloud-Identity-portal"
---

<span id="scenarios"></span>
## Scenarios

Cloud Identity users can log in to the Cloud Identity portal to view their access permissions granted to BytePlus accounts. They can also log in as IAM roles or users to access the cloud resources under BytePlus accounts.

<span id="prerequisites"></span>
## Prerequisites


1. You have configured a valid user login method by completing the [user login settings](https://docs.byteplus.com/en/docs/CloudIdentity/User-login-settings).

2. You are a Cloud Identity user.


<span id="procedure"></span>
## Procedure


1. Obtain **the URL of the Cloud Identity portal**.

   Log in to the BytePlus console by using an authorized IAM sub\-user under the organization administrator account and go to the [User login settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userLogin/) page. At the top of the page, an organization administrator can customize the employee login URL as needed and then copy and distribute the URL to the corresponding employees.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6af5e4153505a34229dca5e217b4ccb3.png) </span>


2. **Log in to the Cloud Identity portal**.

   After obtaining the URL in Step 1, a user can access the URL and log in to the Cloud Identity portal by using the methods configured by an administrator.

   * **SSO login.** 

      After accessing the portal URL, a user can click Log in now to go to the login page of the enterprise identity system to complete the login. A user who has already logged in to the enterprise identity system is directly redirected back to the portal URL to complete the login.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_77dc02ca14126bac1f1e4998d581bcd7.png) </span>

   * **Username and password\-based login.** 

      After accessing the portal URL, a user can enter the username and password set by an administrator to complete the login. The user can also reset the password based on the settings configured by the administrator.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_619e814421d1cf33cc08e839ed40315a.png) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If both login methods are enabled, a user can choose either of them as needed.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6bb86efc31f306e5fd50b0ede194b8e1.png" width="550px" /></div>



3. **Access BytePlus cloud resources**.

   After logging in to the portal, a Cloud Identity user can view the access permissions granted by an administrator.

   1. **Log in with specific role access**. If an administrator has granted role access to a user, the user can view the accounts that they can log in to on the following page. After expanding an account, the user can view the permissions that they have after logging in to the account. After clicking Log in, the user can log in to the corresponding BytePlus account as an IAM role. Permissions associated with the IAM role are the same as those in the permission set.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c8274e69b2ddade7bd12a0d0b6652967.png) </span>

      After logging in, you can view your currently logged\-in role identity in the upper\-right corner of the top navigation bar in the BytePlus console.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_06f139797f3c37d60fa1ef23cb38b7a7.png) </span>

   2. **Log in as the current user**. If an administrator has granted user access to a user, the user can view the accounts that they can log in to on the following page. After clicking Log in, the user logs in to the BytePlus account as the corresponding IAM user under the account. Permissions associated with the IAM user are subject to access control permissions under the account.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0da268fce2edad8d672bbb6871b899cc.png) </span>After logging in, you can view your currently logged\-in role identity in the upper\-right corner of the top navigation bar in the BytePlus console.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c2c5738ec1e14533834ce86d4eab8be8.png) </span>
