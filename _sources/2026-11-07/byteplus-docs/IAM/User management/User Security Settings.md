---
title: "User Security Settings"
product: "BytePlus IAM"
product_code: "IAM"
source: "https://docs.byteplus.com/en/docs/IAM/user-security-settings"
---

In the security settings of access control, you can set global security rules for IAM users, including:


* Self\-managed settings: whether to allow IAM users to manage their own information, login methods, and other security rules

* IAM user login session: IAM user login session expiration rule;

* IAM user password policy;

* IAM user account protection: Set up login and operation protection for IAM users.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260512035828-1573673009256.png) </span>


&nbsp;

BytePlus account (root user) or IAM users with IAM administrative privileges can perform security settings. After the setting takes effect, it will take effect for all IAM users in this account.

Please note that security settings are sensitive operations, and changes will require a secondary check for sensitive operations. Please be sure to use a user with a secure email address, or an MFA device.

<span id="M7C2x5cU"></span>
## IAM user self\-management settings

Each section of the "Account Management" for IAM users can be set independently:


1. Allow self\-management settings: Allow IAM users to bind or modify secure email, and manage login protection and account protection in account management/security settings

2. Allow management login method: Allow IAM users to bind email and three\-party applications such as Douyin and Feishu as login methods in account management/basic information

3. Allow password management: Allow IAM users to change passwords in account management/security settings. Follow the overall password policy rules

4. Allows management of MFA devices: allows IAM users to bind or unbind MFA devices independently


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260512041619-430328273925.png) </span>

&nbsp;

<span id="dSXsNQUv"></span>
## IAM user login session

Setting the length of a user login session requires a balance between employee user experience and security. Too short an expiration time will affect the user's work. At the same time, it is recommended to set a reasonable no\-operation login expiration time to ensure the security of the account.


1. The time when the login state expires without operation is in minutes, with a minimum of 15 minutes and a maximum of 2880 minutes (ie 48 hours). The system defaults to 120 minutes (2 hours);

2. The maximum login retention time is in minutes, with a minimum of 60 minutes and a maximum of 2880 minutes (48 hours). The system defaults to 1440 minutes (24 hours).


You can set all global login duration for IAM users in Access Control \- User Management \- Security Settings \- Login Duration

<div style="text-align: center">
<img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260717080509-873389025234.png" width="1260px" /></div>


&nbsp;

<span id="MVSzFOlS"></span>
## IAM user password policy

You can set the length of IAM user passwords, including character rules. Set security rules such as the number of retries.

<span id="7TsnEyVl"></span>
## IAM user account security protection

<span id="eWuPPp62"></span>
### Login protection

You can set login protection rules for IAM users.


1. After clicking Open, you can choose to set login protection for each IAM user individually, or set login protection uniformly. **No matter which method you choose, when a IAM user is asked to turn on login protection, your IAM user will verify login protection the next time they log in.**  **If the IAM user has bound the verification method at this time, he can independently bind the secure email/MFA device.** 

   1. When selecting "Unified settings for all IAM users", you can set whether to turn on the operation exemption and the exemption time on the current page. It supports a minimum of 5 minutes and a maximum of 7 days.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260512040355-743208205917.png) </span>

2. When selecting "Separate settings for each IAM user", you need to go to the user management\-user details page to set the login protection separately for each IAM user. You can choose MFA device or secure email as the available verification method. 

3. In the verification method, MFA device is checked by default, and you can also specify secure email as other available login protection methods.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">Please note that in order to simplify your enterprise security management efforts, it is recommended that you configure the same authentication methods available for operational protection.</div>


<span id="ZNHLaDVw"></span>
### 

<span id="D2I7xUOA"></span>
### Operation protection

You can set operation protection rules for IAM users. After clicking Open, you can choose to set the operation protection for each IAM user individually, or set the operation protection uniformly.

Here you can choose MFA devices, secure and secure email as login protection methods.


* When selecting "Unified settings for all IAM users", you can set the operation exemption time on the current page, which supports a minimum of 5 minutes and a maximum of 30 minutes.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260512084044-556527216816.png) </span>


&nbsp;
