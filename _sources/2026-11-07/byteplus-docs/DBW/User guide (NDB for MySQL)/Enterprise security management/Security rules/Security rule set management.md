---
title: "Security rule set management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Security_rule_set_management"
---

Security control involves rules and measures established to protect data and resources within the database system. This feature helps you achieve fine\-grained control over database instances in DBW, such as password\-free login instance management, work order management, and security rule management. This topic explains how to manage security rule sets.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The system provides a default security rule set named `vedb_mysql default`, which includes default security rules. For details, refer to [Security rule management](https://docs.byteplus.com/en/docs/DBW/Security_rule_management).

* The default security rule set cannot be deleted and is only viewable. Custom security rule sets cannot be recovered once deleted, so proceed with caution.

* Since security rules are a new feature in DBW, you must set a security rule set for the instance when enabling security control mode. If you enabled security control for an instance before July 9, 2024, you need to reconfigure the instance's security control and bind a security rule set to it; otherwise, some features may become unavailable.


<span id=".5LyY5Yq_"></span>
## Advantages


* **Enhanced control**: Security rule sets allow database administrators to implement fine\-grained control over user activities, such as setting rules that only allow specific users to access the database on specific platforms.

* **Implement the principle of least privilege**: Through security rule sets, the principle of least privilege can be enforced, granting users only the minimum permissions required for the target instance, thereby reducing the risk of users performing high\-risk operations through excessive permissions.

* **Improved standardization**: Clearly defined security rule sets help establish and maintain good database access and usage standards, enhancing the professionalism and security of the database system.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Your account has been added as an administrator of DBW. For detailed steps, refer to [Adding Users](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* A NDB for MySQL cloud database instance has been created and is in the running state. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance).


<span id=".5Yib5bu65a6J5YWo6KeE5YiZ6ZuG"></span>
## Create security rule set


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Enterprise security** \> **Security rules**.

4. On the **Security rule sets** page, click **Create security rule set**.

5. In the **Create security rule set** dialog box, configure the following parameters:

   * **Rule set name**: Customize the security rule set name. The length of the security rule set name cannot exceed 128 characters and does not support spaces.

   * **Database type**: Select the database type as needed, supporting **NDB** ** for MySQL.** 

6. Click **OK**.


<span id=".5bqU55So5a6J5YWo6KeE5YiZ6ZuG"></span>
## Apply security rule set


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, click **Instance list**.

4. In the upper\-left corner of the **Instance list** page, switch the database type to **NDB** ** for MySQL**.

5. On the **Instance list** page, select the pencil icon under the **Security control** column of the target instance.

6. In the **Set security control** dialog box, turn on the security control mode, then select a security rule set from the dropdown under **Security rule set**, and configure other parameters.

7. Click **OK**.


<span id=".5Yig6Zmk5a6J5YWo6KeE5YiZ6ZuG"></span>
## Delete security rule set

Once a security rule set is deleted, it cannot be recovered. Proceed with caution.


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Enterprise security** \> **Security rules**.

4. On the **Security rule sets** page, click the **Delete** option in the **Actions** column of the target security rule set.

5. In the **Confirm deletion?**  dialog box, click **OK**.


<span id=".57yW6L6R5a6J5YWo6KeE5YiZ6ZuG"></span>
## Edit security rule set

Currently, only modifying the name of the security rule set is supported.


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Enterprise security** \> **Security rules**.

4. On the **Security rule sets** page, click the pencil icon in the **Security rule set name** column of the target security rule set to modify the name.

   The name of the security rule set cannot exceed 128 characters and cannot contain spaces.

5. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

If you need to enable, disable, add, or edit security rules within the security rule set, refer to [Security rule management](https://docs.byteplus.com/en/docs/DBW/Security_rule_management).
