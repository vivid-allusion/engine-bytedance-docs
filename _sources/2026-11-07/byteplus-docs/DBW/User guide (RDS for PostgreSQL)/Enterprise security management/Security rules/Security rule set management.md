---
title: "Security rule set management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/security-rule-set-management_"
---

Security control refers to the rules and measures established to protect data and resources in the database system. Security rule sets enable you to implement fine\-grained control over database instances in DBW, such as password\-free login, ticket management, and security rule management. This topic describes how to manage security rule sets.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The system provides a default security rule set named `postgres default`. For the default security rules it contains, refer to [Security rule management](https://docs.byteplus.com/en/docs/DBW/security-rule-management_?type=preview&lang=en).

* The default security rule set can not be deleted and can only be viewed. Custom security rule sets can not be recovered after deletion. Proceed with caution.


<span id=".5LyY5Yq_"></span>
## Advantages


* **Enhanced control**: Security rule sets allow database administrators to refine control over user activities, such as setting rules that only allow specific users to access the database on specific platforms.

* **Implement the Principle of Least Privilege (PoLP)** : With security rule sets, you can implement the PoLP by assigning users only the minimum permissions required for the target instance, thereby reducing the risk of users performing high\-risk operations through permissions.

* **Improved standardization**: A clearly defined security rule set helps build and maintain good database access and usage specifications, and improves the professionalism and security of the database system.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance and account for RDS for PostgreSQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account).

* Your account has been added as an administrator of DBW. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).


<span id=".5Yib5bu65a6J5YWo6KeE5YiZ6ZuG"></span>
## Create a security rule set


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **Create security rule sets**.

5. In the **Create security rule sets** dialog box, configure the following parameters:

   * **Rule set name**: Customize the security rule set name. The security rule set name can not exceed 128 characters, and must not contain spaces.

   * **Database type**: Select **RDS for PostgreSQL** from the drop\-down list.

6. Click **OK**.


<span id=".5bqU55So5a6J5YWo6KeE5YiZ6ZuG"></span>
## Apply a security rule set


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, click **Instance list**.

4. In the upper\-left corner of the **Instance list** page, switch the database type to **RDS for PostgreSQL**.

5. On the **Instance list** page, find the target instance and click the pen icon in the **Security control** column.

6. In the **Set security control** dialog box, turn on the switch for the security control mode, select a security rule set from the **Security rule set** drop\-down list, and then configure other parameters.

7. Click **OK**.


<span id=".5Yig6Zmk5a6J5YWo6KeE5YiZ6ZuG"></span>
## Delete a security rule set

A deleted security rule set cannot be recovered. Proceed with caution.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click **Delete** in the **Actions** column of the target security rule set.

5. In the **Are you sure to delete?**  dialog box, click **OK**.


<span id=".57yW6L6R5a6J5YWo6KeE5YiZ6ZuG"></span>
## Edit a security rule set

Currently, only modification of the security rule set name is supported.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Corporate security** \> **Security rule**.

4. On the **Security rule set** page, click the pen icon in the **Security rule set name** column of the target security rule set to modify its name.

   The security rule set name can not exceed 128 characters, and must not contain spaces.

5. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

To enable, disable, add, or edit security rules in the security rule set, refer to [Security rule management](https://docs.byteplus.com/en/docs/DBW/security-rule-management_?type=preview&lang=en).
