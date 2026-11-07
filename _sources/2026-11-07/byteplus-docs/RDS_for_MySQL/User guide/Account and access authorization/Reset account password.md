---
title: "Reset account password"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/resetting_an_account_password"
---

This topic describes how to reset a database account password.

## Prerequisites

An account has been created for the instance. For more information on specific operations, refer to [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yib5bu66LSm5Y-3).

## Precautions

* Resetting the password may cause the connection to be disrupted which is using the account, proceed with caution.

* When you reset the password of the super account, the permissions of this account are also reset.

* If you have enabled a custom password policy before resetting the account password, the system will verify the reset password in accordance with this policy. To view the effective password policy for the current instance, refer to [View password policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/custom-password-policy?lang=en#Ncd1dWHm).

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

> **tip**

> If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. Click **Accounts** at the top of the page.

6. On the **Accounts** tab, click  **...**  in the **Actions** column of the target account.  **\> Reset password**.

7. In the pop\-up dialog box, enter the password and confirm password. The password must meet the following requirements:

   * The password length is limited to 8~32 characters.

   * The password consists of any three types of characters as follows: uppercase letters, lowercase letters, digits, and special characters.

   * Special characters are `!@#$%^*()_+-=,.&?|/`.

8. Click **OK**.

## Related API

|API |Description |
|---|---|
|[ResetDBAccount](https://docs.byteplus.com/en/docs/RDS_for_MySQL/resetdbaccount) |Call the ResetDBAccount API to reset the Account password. |
