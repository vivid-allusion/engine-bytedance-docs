---
title: "Custom password policy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Custom_password_policy"
---

RDS for MySQL supports custom password policies to improve database security. This topic describes how to set the password policy.

## Prerequisites

The database kernel version must meet the following requirements:

* MySQL 5.7 instances: The kernel version must be MySQL 5.7.44_20260815 and above.

* MySQL 8.0 instances: The kernel version must be MySQL 8.0.43_20260815 and above.

* MySQL 8.4 instances: The kernel version must be MySQL 8.4.7_20260815 and above.

> **tip**

> You can view the kernel minor version of an instance by [Viewing instance information](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details). If your instance does not meet the requirements, you can [Upgrade instance kernel minor version](https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version).

## Precautions

* **Regardless of how you set the custom password policy, passwords must always comply with the following policies:**

   * **The password length is 8~32 characters.**

   * **The password must contain any three of uppercase letters (A~Z), lowercase letters (a~z), digits (0~9), and special characters (!@#$%^\*()_+\-=,.&?|/).**

* When configuring a custom password policy, the password length verification rule is that **`the minimum password length must be greater than or equal to the number of digits + 2 × the number of upper and lower case letters + the number of special characters`**. Otherwise, the system automatically adjusts the minimum length to the result of this formula.

* When the password strength level is medium or high, the password must contain at least any three of uppercase letters, lowercase letters, digits, and special characters. Since specifying a dictionary file is not supported currently, the verification rules for medium strength and high strength are the same.

* The custom password policy takes effect only when creating new accounts or resetting passwords for existing accounts. It does not verify or force changes to the passwords of existing accounts.

* After the custom password policy is disabled, new account creation or password resets for existing accounts are only bound by basic password rules. Existing passwords of current accounts remain unaffected.

* Password policies can be set when creating a new instance or modified for existing instances, but batch configuration of password policies for existing instances is not supported.

* If you have manually installed the password plugin (validate_password), MySQL will automatically take over and manage this plugin after you perform password policy operations.

## Enable password policy

### Set for a new instance

Password policies can be set when creating an instance. For specific operations, see [Create an Instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1?lang=en).

### Set for an existing instance

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project to which the instance belongs is not set, this operation should select the project as **All resources**.

   3. On the left navigation bar, click **Instances** to go to the **Instances** page.

4. Click the name of the target instance on the **Instance list** page to go to the **Instance information** page.

5. On the **Instance information** page, click the **Accounts** tab.

6. In the upper\-right corner of the page, enable the **Password policy**, and set the following parameters in the displayed **Password policy** dialog box:

|**Parameter** |**Description** |
|---|---|
|Password strength level |Password strength level. Values are as follows:<br><br><br>* Low (default): Only the password length is verified.<br><br>* Medium: The password length, uppercase letters, lowercase letters, digits and special characters are verified.<br><br>* High: The password length, uppercase letters, lowercase letters, digits, special characters and dictionary file are verified.<br><br><br>> **tip**<br><br><br>> Since specifying a dictionary file is not supported currently, the verification rules for medium strength and high strength are the same.<br> |
|Minimum password length |The minimum length of the password. The default value is 8, and the value range is 8~256.<br><br>> **tip**<br><br><br>> The configurable range of this parameter is dynamically adjusted according to the current values of the Minimum number of digits, Minimum number of upper‑lowercase letters, and Minimum number of special characters parameters.<br> |
|Minimum number of digits |The number of digits that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br>> The configurable range of this parameter is dynamically adjusted according to the current values of the Minimum password length, Minimum number of upper‑lowercase letters, and Minimum number of special characters parameters.<br> |
|Minimum number of upper‑lowercase letters |The minimum number of uppercase letters and lowercase letters that the password must contain respectively. The default value is 1, and the value range is 0~256. For example, when this parameter is set to 2, the password must contain at least 2 uppercase letters and 2 lowercase letters, meaning a total of at least 4 letters.<br><br>> **tip**<br><br><br>> The configurable range of this parameter is dynamically adjusted according to the current values of the Minimum password length, Minimum number of digits, and Minimum number of special characters parameters.<br> |
|Minimum number of special characters<br><br> |The number of special characters that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br>> The configurable range of this parameter is dynamically adjusted based on the current values of Minimum password length, Minimum number of digits, and Minimum number of upper‑lowercase letters.<br> |

7. After setting the parameters, click **OK**.

## View password policy

1. On the **Summary** page, click the **Accounts** tab.

2. Hover over **Password policy** in the upper\-right corner of the page to view the password policy for the current instance.

## Modify password policy

1. On the **Summary** page, click the **Accounts** tab.

2. Hover over **Password policy** in the upper\-right corner of the page and click **Edit** in the pop\-up card.

3. In the pop\-up **Password policy** dialog box, set the following parameters:

|**Parameter** |**Description** |
|---|---|
|Password strength level |Password strength level. Values are as follows:<br><br><br>* Low (default): Only the password length is verified.<br><br>* Medium: The password length, uppercase letters, lowercase letters, digits and special characters are verified.<br><br>* High: The password length, uppercase letters, lowercase letters, digits, special characters and dictionary file are verified.<br><br><br>> **tip**<br><br><br>> Since specifying a dictionary file is not supported currently, the verification rules for medium strength and high strength are the same.<br> |
|Minimum password length |The minimum length of the password. The default value is 8, and the value range is 8~256.<br><br>> **tip**<br><br><br>> The **configurable range** of this parameter is dynamically adjusted according to the **current values** of the Minimum number of digits, Minimum number of upper‑lowercase letters, and Minimum number of special characters parameters.<br> |
|Minimum number of digits |The number of digits that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br>> The configurable range of this parameter is dynamically adjusted according to the current values of the Minimum password length, Minimum number of upper‑lowercase letters, and Minimum number of special characters parameters.<br> |
|Minimum number of upper‑lowercase letters |The minimum number of uppercase letters and lowercase letters that the password must contain respectively. The default value is 1, and the value range is 0~256. For example, when this parameter is set to 2, the password must contain at least 2 uppercase letters and 2 lowercase letters, meaning a total of at least 4 letters.<br><br>> **tip**<br><br><br>> The configurable range of this parameter is dynamically adjusted according to the current values of the Minimum password length, Minimum number of digits, and Minimum number of special characters parameters.<br> |
|Minimum number of special characters<br><br> |The number of special characters that the password must contain. The default value is 1, and the value range is 0~256.<br><br>> **tip**<br><br><br>> The configurable range of this parameter is dynamically adjusted based on the current values of Minimum password length, Minimum number of digits, and Minimum number of upper‑lowercase letters.<br> |

4. After setting the parameters, click **OK**.

## Disable the password policy

1. On the **Summary** page, click the **Accounts** tab.

2. In the upper\-right corner of the page, disable the **Password policy**, and in the pop\-up **Confirm disabled password policy** dialog box, click **Confirm disabled**.
