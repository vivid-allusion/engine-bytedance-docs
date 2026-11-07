---
title: "Security rule management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/security-rule-management__"
---

This topic describes how to manage security rules on the Database Workshop (DBW) console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Security control refers to the rules and measures established to protect data and resources in the database system. This feature enables you to implement fine\-grained control over database instances in DBW, such as password\-free login, ticket management, and security rule management. For more information, refer to [management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__)[management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__)[management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Your account has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* You have created a security rule set. For detailed steps, refer to [Creating a security rule set](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management__#.5Yib5bu65a6J5YWo6KeE5YiZ6ZuG).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only SQL statements executed in the SQL window of the data interaction platform will be intercepted and take effect.

* Ensure that no conflicts exist among the security rules enabled in the security rule set. Otherwise, the security rules bound to your instance may become invalid.

* Custom security rules are not supported. Only the default security rules included in the system security rule set are supported. Refer to [Reference content](https://docs.byteplus.com/en/docs/64/72576#.5Y-C6ICD5YaF5a65).

* System rules do not support deletion and modification, and only support modification and disabling.

* Currently, only enabling and disabling security rules are supported. Creating security rules is not supported.


<span id=".5ZCv55So5oiW5YWz6Zet5a6J5YWo6KeE5YiZ"></span>
## Enable or disable a security rule

You can enable or disable rules within a security rule set as required.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Corporate security** \> **Security rule**.

3. On the top menu bar, select the region.

4. On the **Security rule set** page, click **View** in the **Actions** column of the target security rule set.

5. On the target security rule set page, click the switch in the **Enable or not?**  column of the target rule.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f60428f9c5689ec82c999663521063fd.png) </span>

6. In **Confirm enable?**  Or **Confirm close?**  dialog box, click **OK**.


<span id=".5Y-C6ICD5YaF5a65"></span>
## Reference content

The default security rules (system rules) in the security rule set are shown in the table below.


|**Security rule name** |**Effective scenario** |**Enable by default?**  |**Default value** |
|---|---|---|---|
|Prohibit direct execution of `CREATE_TABLE` in the database interaction platform. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `DROP_TABLE` in the database interaction platform. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `TRUNCATE` in the database interaction platform. |Data interaction platform |Enabled |None |
|Forbid direct execution of `INSERT` in the database interaction platform. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `UPDATE` in the database interaction platform. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `DELETE` in the database interaction platform. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `ALTER_TABLE` in the database interaction platform. |Data interaction platform |Enabled |None |
|Prohibit direct execution of `KILL` in the data interaction platform. |Data interaction platform |Enabled |None |
|Prohibit direct creation of stored procedures in the database interaction platform. |Data interaction platform |Enabled |None |
|`SELECT` statements are not recommended to use `*`. |Data interaction platform |Not enabled |None |
|`SELECT` statements are not recommended to use `HAVING` clause. |Data interaction platform |Not enabled |None |
|`SELECT` statements are not recommended to use `UNION`. |Data interaction platform |Not enabled |None |
|Reverse queries `(NOT IN / NOT LIKE)` are not recommended in the `WHERE` condition. |Data interaction platform |Not enabled |None |
