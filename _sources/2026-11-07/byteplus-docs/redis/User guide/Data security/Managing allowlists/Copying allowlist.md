---
title: "Copying allowlist"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/copying_a_allowlist"
---

Cache for Redis supports the function of copying allowlists. You can quickly create a new allowlist by copying an existing one. The newly copied allowlist will by default contain all the IP addresses or address segments in the original allowlist as well as those in the security group associated with the allowlist. You can edit and modify the newly copied allowlist before using it. This topic describes how to copy allowlist.

## Prerequisites

Allowlist has been created. For specific procedures, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).

## Precautions

* Cache for Redis can be used with [Database Transmission Service (DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service) and [Database Workshop (DBW)](https://docs.byteplus.com/en/docs/DBW/what-is-database-workbench). To ensure normal access between Redis and DTS or DBW, the system creates corresponding allowlists for them in the Redis allowlist. These system\-built allowlists cannot be edited, modified, or copied.

* When you copy allowlist, the new allowlist only automatically copies all IP addresses or CIDR blocks from the original allowlist and its associated security groups. It does not copy instance information already associated with the original allowlist, or configurations such as whether it is a default allowlist.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, choose **NoSQL Database\> Redis \> Allowlists**.

4. On the **Allowlists** page, locate the target allowlist, and click **Copy** in the **Actions** column on the right.

5. Set the following configurations in the popped\-up dialog box.

   |Parameters |Description |
   |---|---|
   |Allowlist name |The name of the copied allowlist defaults to `<Original_allowlist_name>-replica-Operation Date`.<br><br>For example, if the original allowlist name is `test` and it was copied on November 30, 2024, the name of the copied allowlist defaults to `test-replica-2024-11-30`.<br><br>You can also rename the copied allowlist. The name needs to meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 1 to 128 characters. |
   |Description |The description of the copied allowlist is `<Original_allowlist_name> replica` by default.<br><br>For example, if the original allowlist name is `test`, then the description of the copied allowlist is `test replica` by default.<br><br>You can also reset the description information for the copied allowlist. The length should not exceed 200 characters. |

6. Click **OK**.

   > **tip**

   > If the default name of the copied allowlist exceeds 128 characters or the default description exceeds 200 characters, you need to manually modify the name length or description length before the copying can be successful.
