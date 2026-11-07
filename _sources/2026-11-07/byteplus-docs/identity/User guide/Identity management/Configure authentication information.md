---
title: "Configure authentication information"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Configure_authentication_information"
---

To control how users access your application, this guide provides step\-by\-step instructions for configuring authentication methods in your user pool. You will learn how to enable and manage various login options, such as password, SMS, and email, as well as control self\-service registration for new users.

<span id="5701f551"></span>
## Prerequisites

You have created a user pool; for related operations, refer to [Create a user pool](https://docs.byteplus.com/docs/identity/89611).

<span id="7c696789"></span>
## Steps


1. Log in to the BytePlus Agent Identity Console.

2. In the left navigation bar, select **Identity Management \> User Pool**.

3. Click the target user pool name to enter the details page of the specified user pool.

4. Switch to the **Authentication** tab to configure login methods and registration methods.

   * Login methods: Configure which methods users can use to log in to your application.

      
      |Login methods |Description |
      |---|---|
      |Password login |* **Status**: Enabled by default (cannot be disabled).<br><br>* **Note**: This is the most basic login method. Users can log in using SMS verification code or email verification code together with a password. To ensure the basic availability of the account system, the system enforces this by default. |
      |SMS verification code login |* **Status**: Can be enabled/disabled, enabled by default.<br><br>* **Function**: After enabling, users can enter their mobile phone number and receive a verification code to log in (password\-free). Currently, the following two SMS service methods are available:<br><br>   * BytePlus SMS service: Suitable for production environments with high sending volume.<br><br>   * Identity default SMS service: Up to 50 verification messages can be sent per day, suitable for early development or testing environments. |
      |Email login |* **Status**: Can be enabled/disabled, disabled by default.<br><br>* **Function**: When enabled, users can receive a verification code or login link via email to access the system. |
      

   * Registration method management: Control how new users enter your application ecosystem.

      
      |Registration method |Description |
      |---|---|
      |Self\-service registration |* **Status**: Can be enabled or disabled; enabled by default.<br><br>* **Function**:<br><br>   * **When enabled**: Open application. Any visitor accessing the login page can register a new account on their own.<br><br>   * **When disabled**: Closed application. The registration entry will be hidden on the login page. New users must be manually created by an administrator in the Agent Identity console **user pool** or imported via API. |
      


<span id="083ebe6c"></span>
## Quick configuration recommendations


* **Debugging phase**:

   * Password login: Enabled

   * SMS verification code login: Enabled, and use the Identity default SMS service

   * Email login: Enabled

   * Self\-service registration: Enabled

* **Before launch**:

   * Apply for and configure the BytePlus SMS service to ensure sufficient quota.

   * Confirm whether user registration needs to be restricted (open to the public or by internal invitation).
