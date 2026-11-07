---
title: "User login settings"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/User-login-settings"
---

<span id="scenarios"></span>
## Scenarios

After creating a user on Cloud Identity, you must configure an effective login method for an employee to log in to BytePlus.

Cloud Identity provides an enterprise\-specific login portal that allows employees to log in. After logging in, an employee can choose an authorized BytePlus account to access cloud resources. **The login portal for enterprises offered by Cloud Identity is a standard login solution that applies to all users in Cloud Identity.**  It supports two login methods, and employees must use at least one of the login methods.


* Use **SSO** to log in from the enterprise identity system to the login portal.

* Use **a username and a password** to directly log in to the login portal.


<span id="prerequisites"></span>
## Prerequisites


1. You have activated [Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/Activate-Cloud-Identity).

2. To configure SSO login, you must have an enterprise identity management platform that supports the standard SAML 2.0 protocol, such as Azure AD, Lark, or SealSuite.

3. You are an organization master account, such as the root user or an authorized IAM user.


<span id="procedure-for-configuring-sso-login"></span>
## Procedure for configuring SSO login


1. Log in to the BytePlus console, and go to the [User login settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userLogin/) page.

2. Currently, only SSO login based on SAML 2.0 is supported. On the current page, upload the metadata file of the identity provider (enterprise identity system). Save the SSO login metadata of Cloud Identity and upload it to the identity provider system. For details, refer to [Configure SAML SSO login](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-SAML-SSO-login).

3. After configuring the SSO login information, you can view your enterprise login portal address at the top of the page. The address can be a custom domain name for the enterprise. After determining the domain name, share it with employees for configuration. Note: A modification can cause a change to the login address for employees. Proceed with caution and make sure all relevant personnel are informed.


An employee can log in by accessing the domain name of the login portal in one of the following two ways:


1. Initiate a login request from the enterprise identity system. After logging in to the enterprise identity system, an employee can send a login request to Cloud Identity to directly log in to its login portal, and then select a BytePlus account to log in to the BytePlus console.

2. Directly access the login portal to initiate a login request from the login portal. An employee is redirected from the login portal to the enterprise identity system for authentication. If the employee has logged in to the enterprise identity system, they are automatically logged in to the login portal of Cloud Identity. Then, the employee can select a BytePlus account to log in to the BytePlus console.


<span id="procedure-for-configuring-username-and-password-based-login"></span>
## Procedure for configuring username and password\-based login


1. Log in to the BytePlus console, and go to the [User login settings](https://console.byteplus.com/cloudidentity/region:ap-southeast-1/userLogin/) page.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_39a7f2242fc36209ca924b710f25526c.png) </span>


2. Enable username and password\-based login.

3. After enabling the feature, you can set login passwords for employees.

   1. For a new user, you can set a password during its creation.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_16026f5d9e324f189851133bbec73ecf.png) </span>

   2. For an existing user, you can reset its password.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ffe827d1f781379e1a9c93d9a45da0a0.png) </span>


Employees can log in by accessing the domain name of the login portal in the following way:


1. Initiate a login request from the enterprise identity system, access the login portal of Cloud Identity, and enter the username and password.


<span id="what-to-do-next"></span>
## What to do next

After configuring user login methods, you can [configure role access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-role-based-access-authorization) or [configure user access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure-user-based-access-authorization) to grant Cloud Identity users permissions to access BytePlus accounts.
