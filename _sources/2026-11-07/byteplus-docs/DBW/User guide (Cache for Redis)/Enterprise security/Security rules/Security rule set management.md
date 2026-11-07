---
title: "Security rule set management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/security-rule-set-management-for-redis"
---

Security control refers to the rules and measures established to protect data and resources in the database system. Security rule sets enable you to implement fine\-grained control over database instances in DBW, such as password\-free login, ticket management, and security rule management. This topic describes how to manage security rule sets.

<span id="Um5Ff9gP"></span>
### Precautions


* The system provides a default security rule set named redis default. For default security rules included in the security rule sets, refer to [Security rule management](https://docs.byteplus.com/en/docs/DBW/security_rule_management_redis?lang=zh).

* The default security rule set can not be deleted and can only be viewed. Custom security rule sets can not be recovered after deletion. Proceed with caution.


<span id="lhcwp9Zl"></span>
### Advantages


* **Enhanced control**: Security rule sets allow database administrators to refine control over user activities, such as setting rules that only allow specific users to access the database on specific platforms.

* **Implement the Principle of Least Privilege (PoLP)** : With security rule sets, you can implement the PoLP by assigning users only the minimum permissions required for the target instance, thereby reducing the risk of users performing high\-risk operations through permissions.

* **Improved standardization**: A clearly defined security rule set helps build and maintain good database access and usage specifications, and improves the professionalism and security of the database system.


<span id="3iTcVYUH"></span>
### Prerequisites


* An instance for Cache for Redis has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* Your account has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management?lang=zh).


<span id="098UfoAl"></span>
### Create a security rule set


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **Create security rule sets**.

5. In the **Create security rule sets** dialog box, configure the following parameters:

   * **Rule set name**: Customize the security rule set name. The security rule set name can not exceed 128 characters, and must not contain spaces.

   * **Database type**: Select the database type as needed, supporting **Cache for Redis**.

6. Click **OK**.


<span id="1iJ2mT3B"></span>
### Apply a security rule set


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, click **Instance list**.

4. In the upper\-left corner of the **Instance list** page, switch the database type to **Cache for Redis**.

5. On the **Instance list** page, find the target instance and click the pen icon in the **Security control** column.

6. In the **Set security control** dialog box, turn on the switch for the security control mode, select a security rule set from the **Security rule set** drop\-down list, and then configure other parameters.

7. Click **OK**.


<span id="KGs4Z9Uu"></span>
### Delete a security rule set

A deleted security rule set cannot be recovered. Proceed with caution.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **Delete** in the **Actions** column of the target security rule set.

5. In **Confirm deletion?**  dialog box, click **OK**.


<span id="b1mALEgr"></span>
### Edit a security rule set

Currently, only modification of the security rule set name is supported.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click the pen icon in the **Security rule set name** column of the target security rule set to modify its name.


The security rule set name cannot exceed 128 characters and must not contain spaces.

<span id="kAO2hHvW"></span>
### Next steps

To enable, disable, add, or edit security rules in the security rule set, refer to [Security rule management](https://docs.byteplus.com/en/docs/DBW/security_rule_management_redis?lang=zh).
