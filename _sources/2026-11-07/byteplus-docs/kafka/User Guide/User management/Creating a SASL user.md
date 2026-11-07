---
title: "Creating a SASL user"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/creating-SASLuser"
---

Message Queue for Kafka is compatible with access control lists (ACLs) of Apache Kafka, managing Simple Authentication and Security Layer (SASL) users. You can grant message sending and receiving permissions to SASL users as needed. This topic describes how to create a SASL user in the console.

<span id="背景信息"></span>
## Background information

Message Queue for Kafka is compatible with ACLs. It supports the SASL mechanism and offers SASL users of the PLAIN and SCRAM types for producing and consuming messages under the PLAIN and SCRAM\-SHA\-256 mechanisms, respectively. After a Simple Authentication and Security Layer (SASL) user is created for a Kafka instance, the Kafka instance provides a SASL endpoint. You can use this endpoint to access the instance only after the data passes the SASL username and password authentication.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For instances created before August 23, 2023, you cannot delete the PLAIN SASL users created automatically with the instances, reset passwords for the users, or create another PLAIN SASL user.</div>


* <div data-tips="true" data-tips-type="tip">The password of a SCRAM SASL user cannot be viewed. Make sure to securely save the password.</div>



<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, click the name of the instance.

4. On the **User Management** tab, click **Create user**.

5. Configure the relevant parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Username |The username of the SASL user. It must meet the following requirements:<br><br><br>* Must be 3 to 64 characters in length.<br><br>* Can only contain letters, digits, hyphens ( \- ), and underscores ( _ ).<br><br>* Cannot be set to admin or monitor.<br><br>* Usernames in the same instance must be unique. |
   |Password type |The password type of a SASL user. Options are:<br><br><br>* **Scram**: SASL user of the SCRAM type<br><br>* **Plain**: SASL user of the PLAIN type<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you create a PLAIN SASL user, it takes 1 minute to take effect. Your patience is appreciated.</div><br> |
   |Password |SASL user password. It must meet the following requirements:<br><br><br>* Must be 8 to 32 characters in length.<br><br>* Must contain at least three of the following: lowercase letters, uppercase letters, digits, and special characters.<br><br>* Special characters are `!@#$%^&*()_+-=`. |
   |Confirm password |Type the password again. |
   |Describe |Description of the SASL user, 1 to 128 characters in length. |
   

6. Specify whether to enable All Permitted for the user.

   All Permitted is similar to default permissions and can be used in conjunction with ACLs.

   * Enabling All Permitted: This user has read and write permissions on all topics and groups in the instance.

   * Disabling All Permitted: This user has no permissions on any topics and groups in the instance. You can grant permissions on specific topics and groups to this user. For more information, refer to [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL).

7. Click **Create**.


<span id="f96c1119"></span>
## Related operations

After creating a SASL user, you can also perform the following operations:


* Modifying the All Permitted permission

   On the **User Management** tab of the target instance, locate the SASL user and toggle the switch in the **All Permitted** column to enable or disable it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Before disabling it, make sure that no running applications use the user for authentication to avoid impacting online business.   </div>
   

* [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL)

   If All Permitted is disabled for the SASL user, you can set fine\-grained permissions through ACLs.

* [Resetting a SASL user password](https://docs.byteplus.com/en/docs/kafka/resetting-SASLuser-password)

* [Viewing a PLAIN SASL user password](https://docs.byteplus.com/en/docs/kafka/viewing-SASLuser-password)

* [Deleting a SASL user](https://docs.byteplus.com/en/docs/kafka/deleting-SASLuser)
