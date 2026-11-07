---
title: "Achieving transmission across Volcengine account"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Achieving_transmission_across_Volcengine_account"
---

This topic describes the database types, advantages, and operation steps supported by cross\-Volcengine account data transmission.

## Advantages

Transferring data across accounts not only increases productivity, but also helps you better protect and manage your data. The specific advantages are as follows:

* **Data sharing**: By transferring data across accounts, companies or individuals can share data between different accounts or departments. Improve the work efficiency of project collaboration and data analysis.

* **Security**: Sensitive data can be transferred only between the required accounts and encrypted during transmission, reducing the risk of data leakage.

* **Improve efficiency**: By avoiding duplicate data entry, cross\-account data transmission can improve work efficiency and save time.

* **Disaster recovery**: If there are multiple accounts, problems with one account will not affect other accounts, which helps to build a good data backup and disaster recovery system.

* **Save public network costs**: When transferring data across accounts, there is no need to use the public network for data transmission, so there is no need to bind EIP to the target end, thereby reducing the cost of the public network.

* **Optimize costs**: By optimizing the data transmission method, you can reduce data storage and transmission costs and save expenses.

## Supported database types

The databases that support configuring data transfer across BytePlus accounts are as follows:

> **tip**

> When transferring data across accounts, there are no restrictions on how the target library instance can be accessed.

|**Data transmission type** |**Instance type** |**Access method of the source instance** |
|---|---|---|
|**Data migration** |MySQL |* BytePlus RDS for MySQL<br><br>* BytePlus veDB for MySQL |
||Redis |BytePlus Cache for Redis |
||MongoDB |BytePlus Document Database for MongoDB |
||PostgreSQL |BytePlus RDS for PostgreSQL |
|**Data subscription** |MySQL |* BytePlus RDS for MySQL<br><br>* BytePlus veDB for MySQL |
||PostgreSQL |BytePlus RDS for PostgreSQL |
|**Data synchronization** |MySQL |* BytePlus RDS for MySQL<br><br>* BytePlus veDB for MySQL |
||Redis |BytePlus Cache for Redis |
||MongoDB |BytePlus Document Database for MongoDB |
||PostgreSQL |BytePlus RDS for PostgreSQL |

## Prerequisites

* The source and target instances that need to transfer data across accounts have been created.

* Get the account IDs of the source and target.

## Precautions

Currently only supports cross\-Volcengine account transmission data.

## Procedure

> **tip**

* > This topic takes migrating data of a Volcengine RDS for MySQL instance across Volcengine accounts as an example.

* > This topic uses account A and account B as examples. For example, an enterprise has opened two Volcengine accounts A and B. Due to business requirements, data in Volcengine account A needs to be migrated to Volcengine account B.

1. Authorize the trust relationship

   1. Log in to the [IAM](https://console.byteplus.com/iam/identitymanage/user) console using account A at the source end.

   2. Create a role starting with `DTS_`

      1. In the left navigation bar, select **Identity management** \> **Role**.

      2. On the **Role** page, click **Create role**.

      3. On the configuration wizard page of **Create role**’s **Select trusted identity**, configure the following parameters:

         |**Name** |**Description** |
         |---|---|
         |**Select the trusted identity type** |Click **Service**. |
         |**Select service** |Select **IAM** from the drop\-down list. |

      4. Click **Next step**.

      5. On the configuration wizard page of **Create role**’s **Configure role information**, configure the role information as shown in the following table:

         |**Name** |**Description** |
         |---|---|
         |**Role name** |Set the role name. The naming rules for the role are as follows:<br><br><br>* Must start with `DTS_`.<br><br>* It can contain English letters, numbers, and characters. Characters can include English periods (.), hyphens (\-), and underscores (_).<br><br>* Length can not exceed 64 characters. |
         |**Display name** |Optional. Enter the display name for the role, limited to 64 characters. |
         |**Description** |Optional. Enter remarks for the role. |
         |**Tag** |Optional. Click **Add tag**, and enter the tag key and tag value to add tags to the role. |

      6. Click **Next step**.

      7. On the configuration wizard page of **Create role**’s **Add permissions**, configure the following permission policies:

         |**Name** |**Description** |
         |---|---|
         |**Select policy** |Select target policies as needed:<br><br><br>* **`RDSMySQLFullAccess`**: represents full management permissions for RDS for MySQL.<br><br>* **`VedbMysqlFullAccess`**: represents full management permissions for veDB for MySQL.<br><br>* **`RedisFullAccess`**: represents full management permissions for Cache for Redis.<br><br>* **`MongoDBFullAccess`**: represents full management permissions for Document Database for MongoDB.<br><br>* **`RDSPGFullAccess`**: represents full management permissions for RDS for PostgreSQL. |
         |**Scope of effect** |Select **Global**. |

      8. Click **Submit**.

   3. Configure the trust relationship of the role.

      1. In the left navigation bar, select **Identity management** \> **Role**.

      2. On the **Role** page, click the target role name.

      3. On the **Role details** page, click **Trust relationship**.

      4. On the **Trust relationship** tab, click **Edit trust policy**.

      5. Copy the following policy and click **Save**.

         ```json
         {
             "Statement": [
                 {
                     "Effect": "Allow",
                     "Action": [
                         "sts:AssumeRole"
                     ],
                     "Principal": {
                         "IAM": [
                             "trn:iam::dstAccount:role/ServiceRoleForDTS"//dstAccount must be replaced with the target account ID.
                         ]
                     }
                 }
             ]
         }
         ```

2. Creating data migration task

   1. Log in to the Database Transmission Service (DTS) console using target B account.

   2. In the left navigation bar, click **Data migration**.

   3. On the **Data migration list** page, click **Create data migration**.

   4. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

      |**Type** |**Name** |**Description** |
      |---|---|---|
      |None |Configure the **Task name** and **Link specifications** of the migration task as needed. ||
      |**Source database configuration** |**Instance type** |Select **MySQL**. |
      ||**Access method** |Select **BytePlus RDS for MySQL**. |
      ||**region** |Select the region to which the source instance belongs. |
      ||**Cross\-BytePlus account?**  |Select whether to transmit data cross\-account as needed, with the following options:<br><br><br>* **This account**: Selecting this means data transmission occurs only within this account.<br><br>* **Cross\-account**: Selecting this means data transmission occurs between two accounts. |
      ||**Cross\-account ID** |Enter the BytePlus account ID to which the source database belongs. |
      ||**Cross\-account roles** |Enter the IAM role authorized for DTS to access cross\-account resources. |
      ||**MySQL instance** |Select the target instance of RDS for MySQL from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
      ||**Node type** |Select node types as needed, currently supporting **Primary node** and **Read\-only node**.<br><br>> **tip**<br><br><br>> Select read\-only nodes when read\-only nodes are created within the instance. For specific steps on creating a read\-only node, refer to [Read\-only node overview](https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_of_read-only_nodes).<br> |
      ||**MySQL read\-only node** |Select the target read\-only node from the drop\-down list.<br><br>> **tip**<br><br><br>> When a read\-only node is created in the instance and **Node type** selects **Read\-only node**, this parameter can be configured.<br> |
      ||**Database account** |Enter the database account of the source instance. |
      ||**Database password** |Enter the password corresponding to the database account of the source instance. |
      ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
      |**Target database configuration** |Configure the parameter configuration of the target database as required. For more information, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions). ||
      |**None** |Configure the **Project**, **Tag**, and **Billing method** for the migration task as needed. ||

   5. Depending on the source and target instance types, refer to the specific configuration documentation to create a cross\-BytePlus account migration task. For more information, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions).

## Related document

The configuration document for creating data transfer tasks across BytePlus accounts is as follows:

* [Overview of data migration solutions](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions)

* [Overview of data subscription solutions](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions)

* [Overview of data synchronization solutions](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions)

## FAQs

#### **During the data transmission process, can the source and target accounts see each other's instance information?**

After successfully configuring the role and authorizing the trust relationship, the authorized target account can see all the instance information under the source account, but the source cannot see the instance information of the target.

#### After authorizing the trust relationship for the target account, in which region do I need to create a transfer task?

DTS has no geographical restrictions when creating data transfer tasks. When transferring data across accounts, it is recommended to create tasks in the target region.

#### Will cross\-account authorization increase the cost of transferring tasks?

No.
