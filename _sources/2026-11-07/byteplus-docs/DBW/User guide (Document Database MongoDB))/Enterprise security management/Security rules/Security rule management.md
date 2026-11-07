---
title: "Security rule management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/security-rule-management_____"
---

This topic describes how to manage security rules on the Database Workshop (DBW) console.

<span id="4sFd8kur"></span>
## Background

Security control refers to the rules and measures established to protect data and resources in the database system. This feature enables you to implement fine\-grained control over database instances in DBW, such as password\-free login, ticket management, and security rule management. For more information, refer to [Security rule set management](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_____).

<span id="P3Rk7j1j"></span>
## Prerequisites


* Your account has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).

* You have created a security rule set. For detailed steps, refer to [Creating a security rule set](https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_____).


<span id="G1y5YLoC"></span>
## Precautions


* Only SQL statements executed in the SQL window of the data interaction platform will be intercepted and take effect.

* The system provides a default security rule named mongo default. For details on the default security rules included in the default rule set and newly created rule sets, refer to [References](https://docs.byteplus.com/en/docs/DBW/security-rule-management_____).

* System rules do not support deletion and modification, and only support modification and disabling.

* Currently, creating security rules for the **Document Database for MongoDB** database is not supported.


<span id="eJeMJcke"></span>
## Viewing security rules


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the top menu bar of the **Security rule set** page, select **Database type** as **Document Database for MongoDB**.

5. Click **View** in the **Actions** column of the target security rule set.

6. On the target security rule set details page, you can view the following information:

   * View information about the security rule set, including the **Security rule set** **ID**, **Rule set type**, and **Number of associated instances**.

   * View security rule information, including **Data interaction platform**, and **Ticket management** types. You can also view the **Security rule** **ID**, **Security rule name**, **Rule type**, **Enable or not?** , **Last modified time** for each security rule.


<span id="p97PTSQY"></span>
## Enable or disable a security rule

You can enable or disable rules within a security rule set as required.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the top menu bar of the **Security rule set** page, select **Database type** as **Document Database for MongoDB**.

5. Click **View** in the **Actions** column of the target security rule set.

6. On the target security rule set details page, click the switch in the **Enable or not?**  column of the target rule.

7. In the **Are you sure to enable?**  or **Are you sure to disable?**  dialog box, click **OK**.


<span id="44q9KOb2"></span>
## References

The default security rules (system rules) in the security rule set are shown in the table below.

Data interaction platform & Ticket management


|**Security rule name** |**Effective scenario** |**Enable by default?**  |**Default value** |
|---|---|---|---|
|All users need to check permissions. |Data interaction platform |Enabled |None |


<span id="RB70k8gT"></span>
## Related actions

[Enabling security control](https://docs.byteplus.com/en/docs/DBW/MongoDB_Enabling_security_control): When enabling security control for an instance, set the security rule set.
