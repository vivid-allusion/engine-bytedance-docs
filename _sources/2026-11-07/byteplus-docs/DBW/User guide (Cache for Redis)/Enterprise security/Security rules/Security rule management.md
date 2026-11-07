---
title: "Security rule management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/security_rule_management_redis"
---

This topic describes how to manage security rules on the Database Workshop (DBW) console.

<span id="9KeMhhrY"></span>
### Background

Security control refers to the rules and measures established to protect data and resources in the database system. This feature enables you to implement fine\-grained control over database instances in DBW, such as password\-free login, ticket management, and security rule management. For more information, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management-for-redis?lang=zh).

<span id="FauZHZnT"></span>
### Precautions

Currently, only enabling and disabling security rules in the default security rule set are supported.

<span id="g9YsLolp"></span>
### Enable or disable a security rule

You can enable or disable rules within a security rule set as required.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, filter by **Database type** as **Cache for Redis**, and click **View** in the **Actions** column of the target security rule set.

5. On the target security rule set page, click the switch in the **Enable or not?**  column of the target rule.

6. In **Confirm enable?**  Or **Confirm close?**  dialog box, click **OK**.


<span id="5iHzdSKt"></span>
### Delete a security rule

System rules can not be deleted. Custom security rules can not be restored once deleted. Proceed with caution.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **View** in the **Actions** column of the target security rule set.

5. On the target security rule set page, click **Delete** in the **Actions** column of the target rule.

6. In the **Confirm deletion** dialog box, click **OK**.


<span id="f8xNtoie"></span>
### References


|**Security rule name** |**Effective scenario** |**Enable by default?**  |**Default value** |
|---|---|---|---|
|All users need to check permissions. |SQL window |Enabled |None |


<span id="qlgr0XmE"></span>
### Related operation

Enable security control: When enabling security control for an instance, set the security rule set. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis?lang=zh).
