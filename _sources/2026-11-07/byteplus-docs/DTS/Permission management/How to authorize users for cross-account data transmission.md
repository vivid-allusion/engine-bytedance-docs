---
title: "How to authorize users for cross-account data transmission"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission"
---

Database Transmission Service (DTS) supports cross\-account resource migration, synchronization, or subscription between BytePlus accounts. This topic introduces how to grant cross\-account transmission permissions to a BytePlus account in the permission management console.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

This topic uses account A and account B as examples. For instance, a company has activated two BytePlus accounts named A and B, respectively. Due to business requirements, data in BytePlus account A needs to be migrated, subscribed, or synchronized to account B. The specific process is as follows:


1. Account A logs on to the BytePlus IAM console.

2. Account A creates a role in the IAM console.

3. Account A configures the trust relationship of the role.

4. Account B logs on to the DTS console of BytePlus.

5. Account B creates a data transmission task in the DTS console.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered with real name authentication completed. For account registration and real name authentication, refer to [Create account](https://docs.byteplus.com/en/docs/6261/64925) and [Verify account](https://docs.byteplus.com/en/docs/6261/64935).

* The BytePlus account of the destination has authorized DTS to access other cloud resources. For details, refer to Root user permission management.

* The BytePlus cloud account (root user) ID that creates the DTS task on the source end has been obtained.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Do not delete or modify the role's permission policy and trust relationship before the transmission task ends, as this will affect the transmission of the task.

* After configuring the trust relationship, the account on the target side (referred to as B in this document) can view all instances within the source account (referred to as A in this document) when creating a data transmission task.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [IAM](https://console.byteplus.com/iam/identitymanage/user) console using the BytePlus account of the source database.

2. Create a role

   1. In the left navigation bar, select **Identity management** \> **Role**.

   2. On the **Role** page, click **Create role**.

   3. On the configuration wizard page of **Create role**’s **Select trusted identity**, configure the following parameters:

      
      |**Parameter** |**Description** |
      |---|---|
      |**Select the trusted identity type** |Click **Service**. |
      |**Select service** |Select **IAM** from the drop\-down list. |
      

   4. Click **Next step**.

   5. On the configuration wizard page of **Create role**’s **Configure role information**, configure the role information as shown in the following table:

      
      |**Parameter** |**Description** |
      |---|---|
      |**Role name** |Set the role name. The naming rules for the role are as follows:<br><br><br>* Must start with `DTS_`.<br><br>* It can contain English letters, numbers, and characters. Characters can include English periods (.), hyphens (\-), and underscores (_).<br><br>* Length can not exceed 64 characters. |
      |**Display name** |Optional. Enter the display name for the role, limited to 64 characters. |
      |**Description** |Optional. Enter remarks for the role. |
      |**Tag** |Optional. Click **Add tag**, and enter the tag key and tag value to add tags to the role. |
      

   6. Click **Next step**.

   7. On the configuration wizard page of **Create role**’s **Add permissions**, configure the following permission policies:

      
      |**Parameter** |**Description** |
      |---|---|
      |**Select policy** |Select target policies as needed:<br><br><br>* **`RDSMySQLFullAccess`**: represents full management permissions for RDS for MySQL.<br><br>* **`VedbMysqlFullAccess`**: represents full management permissions for NDB for MySQL.<br><br>* **`RedisFullAccess`**: represents full management permissions for Cache for Redis.<br><br>* **`MongoDBFullAccess`**: represents full management permissions for Document Database for MongoDB.<br><br>* **`RDSPGFullAccess`**: represents full management permissions for RDS for PostgreSQL. |
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
                       "trn:iam::<dstAccount>:role/ServiceRoleForDTS"//dstAccount 需替换成目标端的账号 ID。
                   ]
               }
           }
       ]
   }
   ```
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After completing the above configuration, you can create cross\-account migration, subscription, or synchronization in the DTS console:


* [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions)

* [Synchronization solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions)

* [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions)
