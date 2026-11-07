---
title: "Resetting password"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/reset-password"
---

This topic describes how to modify or reset the database account password on the Redis console.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Accounts** tab.

5. On the **Accounts** tab, click **Update password** in the **Actions** column of the target account.

6. Enter the password and confirm it in the pop\-up dialog box, and click **OK**.

   > **tip**

   > The new password must meet the following conditions:

   * > The length is 8~64 characters.

   * > It contains at least two of the following: uppercase letters, lowercase letters, digits, and special characters.

   * > It supports the following special characters:

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```plain
   ()`~!@#$%^&*-+=_|{}[];<>,.?
   ```
      </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[ListDBAccount](https://docs.byteplus.com/en/docs/redis/listdbaccount) |Call the ListDBAccount API to query the information of specified accounts or all accounts for a Redis instance, including the account name and account role. |
|[ModifyDBAccount](https://docs.byteplus.com/en/docs/redis/modifydbaccount) |Call the ModifyDBAccount API to modify the information of a specified account, including the account role, password, and description. |
