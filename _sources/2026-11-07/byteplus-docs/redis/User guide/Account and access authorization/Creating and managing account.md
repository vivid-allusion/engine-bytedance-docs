---
title: "Creating and managing account"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/manage-account"
---

Cache for Redis supports creating multiple accounts. You can select different roles when creating an account, with each role supporting different permissions. This helps you achieve refined database management and enhances data security.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

Each Redis instance can have up to 100 accounts by default. If you need to create more accounts, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to modify relevant parameters.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Accounts** tab.

5. On **Accounts**tab, click **Create account**.

6. In the pop\-up dialog box, configure the following parameters.

   |Parameters |Description |
   |---|---|
   |Username |The account name must meet the following conditions:<br><br><br>* It starts with a lowercase letter and ends with a lowercase letter or number.<br><br>* The length should be 2 to 16 characters.<br><br>* It consists of only lowercase letters, digits, and underscores (_). |
   |Role |Set permissions assigned to this account. You can choose either the default role or a custom role you created:<br><br><br>* Default roles<br><br>   * **Administrator**: Permission to use all commands on all keys.<br><br>   * **NotDangerous**: Permission to use all commands other than `dangerous` commands on all keys.<br><br>   * **ReadWrite**: Permission to use all commands other than `admin` commands on all keys.<br><br>   * **ReadOnly**: Permission to use all `read` commands on all keys.<br><br>   * **NotWrite**: Permission to use all commands other than `write` commands on all keys.<br><br>* Custom roles<br><br>   You can select a custom role after you create one. To create a role, refer to [Creating role](https://docs.byteplus.com/en/docs/redis/create-role). |
   |Password |Set the password for this account, which must meet the following conditions:<br><br><br>* The length is 8~64 characters.<br><br>* It contains at least two of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>* It supports the following special characters:<br><br>   ```Plain Text```<br>```   ()`~!@#$%^&*-+=_\|{}[];<>,.?```<br>```   ```<br>    |
   |Confirm password |Enter the password again for confirmation. |
   |Description |The account's remark information, which should be 0~256 characters in length. |

7. Click **OK**.

   > **tip**

   > The new account is expected to take effect within one minute. You can check the status of the new account on the account list page to see if it has been changed to **Available**.

## Subsequent operations

Based on business needs, you can choose the following steps to manage accounts:

> **tip**

* > The dafault account cannot update roles or delete accounts.

* > Before performing any of the following operations, ensure that the instance associated with the account is in the running state. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

* > Also make sure the account status is **Available** before updating roles, resetting passwords, or changing description.

* **Update role**

   In the **Actions** column of the target account, click ** Update role**, then in the pop\-up dialog box, choose the desired permissions and click **OK**.

* **Reset password**

   For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password).

* **Modify description**

   In the **Description** column of the target account, click the ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) icon, then in the pop\-up dialog box, modify the description and click **OK**.

* **Delete account**

   In the **Actions** column of the target account, select  **...**   **\> Delete account**. Then, click **OK** in the pop\-up dialog box.

## Relevant APIs

|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/redis/createdbaccount) |Call the CreateDBAccount API to create an account for a specified Redis instance. |
|[ListDBAccount](https://docs.byteplus.com/en/docs/redis/listdbaccount) |Call the ListDBAccount API to query the information of specified accounts or all accounts for a Redis instance, including the account name and account role. |
|[ModifyDBAccount](https://docs.byteplus.com/en/docs/redis/modifydbaccount) |Call the ModifyDBAccount API to modify the information of a specified account, including the account role, password, and description. |
|[DeleteDBAccount](https://docs.byteplus.com/en/docs/redis/deletedbaccount) |Call the DeleteDBAccount API to delete a specified account. |
|[DescribeDBInstanceAclCommands](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcommands) |Call the DescribeDBInstanceAclCommands API to query the list of commands supported by the specified command category in target Redis instance. |
|[DescribeDBInstanceAclCategories](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories) |Call the DescribeDBInstanceAclCategories API to query the command categories supported by target Redis instance. |
