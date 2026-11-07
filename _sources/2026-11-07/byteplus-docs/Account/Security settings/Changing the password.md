---
title: "Changing the password"
product: "BytePlus Account"
product_code: "Account"
source: "https://docs.byteplus.com/en/docs/Account/changing-the-password"
---

<span id="U379JLQc"></span>
## Change Password

<span id="uPumDAXr"></span>
### Operation Steps


1. Navigate to the [account account settings page](https://console.byteplus.com/user/security/), click ** Password Policy \- Password \- Edit** to enter the password modification process.<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515083257-366586615914.png) </span>

2. Changing password is a sensitive operation that requires secondary identity verification. Select an appropriate verification method in the identity verification pop\-up window to complete authentication.

3. After identity verification, enter a new password to finish the modification. The new password must comply with the password complexity rules: 

   1. Length should be 8\-32 characters

   2. Only supports letters, numbers, and special characters (except spaces)

   3. It must contain at least 3 types ofcharacters.


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515084225-1333784832070.png) </span>

&nbsp;


---



<span id="D2Iuztht"></span>
## Password Security Rule Settings

Navigate to the [account account settings page](https://console.byteplus.com/user/security/), click **Modify Rules** under **Login Password** to adjust relevant rules. The configurable password rules include:


* Modify password length rules

* Modify password validity period

* Set historical password rules

* Password retry limit rules


<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260515084408-369365679105.png) </span>

&nbsp;

<span id="pVnd6myf"></span>
### Password Complexity/Length Rules


* **Password Length**: Mandatory 8–32 characters; the minimum character limit can be customized.

* **Password Complexity**:The complexity requirement is non\-configurable.

   * Length should be 8\-32 characters

   * Only supports letters, numbers, and special characters (except spaces)

   * It must contain at least 3 types ofcharacters.


<span id="XKfvAb0A"></span>
### Password Validity Period

Administrators can set a password validity period (0–90 days; 0 days means no expiration limit). Once expired, users must reset their password upon next login.

<span id="g2AHMDAh"></span>
### Password History Check

When resetting a password, the system will check that the new password is not identical to previously used ones. The default checks the last 3 passwords; the check limit can be customized to 3–5 historical passwords.

<span id="vGQDFwff"></span>
### Account Lockout

Configure the maximum password retry attempts within 1 hour and the corresponding lockout duration.

Example: After 3 incorrect password attempts within one hour, the account will be locked for 60 minutes and cannot log in.


* Allowed incorrect attempts: configurable from 3 to 5 times

* Lockout duration: configurable from 10 to 60 minutes
