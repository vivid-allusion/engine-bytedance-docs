---
title: "Overview of SSO on the login portal of Cloud Identity"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/Overview-of-SSO-on-the-login-portal-of-Cloud-Identity"
---

<span id="overview-of-sso"></span>
## Overview of SSO

Single sign\-on (SSO) is **a cross\-system authentication solution that allows users to log in to multiple applications and websites with one authentication**.

Cloud Identity offers a login portal independent of the BytePlus console, providing enterprise customers with a personalized login experience and supporting complex permission management for employee SSO.

The login portal supports SSO login based on SAML 2.0 by using the identity system of an enterprise as the identity provider (IdP) and the independent login portal of Cloud Identity as the service provider (SP). It helps you achieve SSO among the identity system of your enterprise or organization, the login portal of Cloud Identity, and the BytePlus console. After logging in to the IdP system, you are redirected and logged in to the login portal of Cloud Identity for a final login to the BytePlus console.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_240614cd02998a4e98b9c1eed8a0e8d9.png) </span>

Through the login portal of Cloud Identity, an enterprise customer only needs to configure the SSO login information between the enterprise identity system and the login portal of Cloud Identity once to ensure SSO login for all BytePlus accounts under the organization.

<span id="procedure-of-sso-login"></span>
## Procedure of SSO login

The login portal of Cloud Identity supports direct SSO login from the enterprise IdP to the login portal and indirect SSO login from the login portal to the enterprise IdP for login and then back to the login portal.

<span id="login-from-the-idp"></span>
### Login from the IdP

Login from the IdP refers to the process where a user who clicks the BytePlus application after authentication by and login to the enterprise IdP is redirected and logged in to the SSO login page of the login portal of Cloud Identity.

After the login, the employee can select an account available to the current user and click Log in to log in to the BytePlus console with the corresponding identity.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5c711c19812d5d378669e394445ee890.png) </span>

<span id="login-from-the-sp"></span>
## Login from the SP

Login from the SP refers to the process where a user who has not logged in, after clicking Log in now on the login portal page of Cloud Identity, is redirected to the enterprise IdP page to send an SSO login request to the IdP.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3532758362187ef667dd690cb13ab6be.png) </span>

After entering their username and password on the login portal of the corresponding IdP, the user is authenticated by and logged in to the IdP. In this example, the third\-party commercial IdP OneLogin is used.

Then, the user is automatically redirected and logged in to the SSO login page of the login portal of Cloud Identity.

After the login, the employee can select an account available to the current user and click Log in to log in to the BytePlus console with the corresponding identity.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_89eaf72e80d9322d0f6cdf0ea4e2502f.png) </span>
