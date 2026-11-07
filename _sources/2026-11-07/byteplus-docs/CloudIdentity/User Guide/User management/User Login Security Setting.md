---
title: "User Login Security Setting"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/User_Login_Security_Setting"
---

<span id="oTbjg6K6"></span>
## Scenarios

After you have created cloud identity center users and configured login for the cloud identity portal, enterprise employees can already log in through the portal. You want to enhance your enterprise's security management level by enabling login protection for employee logins to add secondary authentication of employee identities.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="default">Login security configurations only take effect for cloud identity center portal logins</div>


2. <div data-tips="true" data-tips-type="default">Login protection is effective for both account password login and enterprise SSO login</div>



&nbsp;

<span id="AiO47zjX"></span>
## Prerequisites


1. You have activated [Cloud Identity](https://docs.byteplus.com/en/docs/CloudIdentity/Activate\-Cloud\-Identity).

2. You are an organization master account, and you can use root user or authorized IAM user under the master account to login.


&nbsp;

<span id="SA1IFXik"></span>
## Procedure for Administrator


1. Log in to the console and enter the user login settings page.

2. Enable login protection. After enabling, all portal users, regardless of login method, will be required to perform secondary identity verification after login.


<span id="L5iYI5oj"></span>
### <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_430716f9f3809a0d0cb23df1cbd9d8a5.png) </span>

&nbsp;

<span id="GgRMxY1n"></span>
### Procedure for Employee Login

After an employee logs in by accessing the login portal domain and successfully authenticates through account password or enterprise SSO:


1. If the user has no available verification device, they will be required to bind a device during the login process.

2. If the user has available verification devices, they need to complete authentication during the login process.

3. After the user completes login, they can manage security devices by themselves in the portal.


&nbsp;

&nbsp;

<span id="I7Pw5wZX"></span>
## What to do next

&nbsp;

After configuring user login, you can [configure role access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure\-role\-based\-access\-authorization) or [configure user access](https://docs.byteplus.com/en/docs/CloudIdentity/Configure\-user\-based\-access\-authorization) to grant Cloud Identity users permissions to access BytePlus accounts.
