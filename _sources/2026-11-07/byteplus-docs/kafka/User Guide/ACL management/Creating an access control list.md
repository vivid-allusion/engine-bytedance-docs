---
title: "Creating an access control list"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/creating-an-ACL"
---

Message Queue for Kafka is compatible with access control lists (ACLs) of Apache Kafka. You can grant the All Permitted permission or custom permissions on some topics or groups to Simple Authentication and Security Layer (SASL) users, isolating permissions on resources and users.

<span id="38613218"></span>
## Background information

In Apache Kafka, an ACL specifies whether a given operation performed by a particular user of a specified host on a specified resource matches the specified resource pattern. Message Queue for Kafka offers flexible permission policies for SASL users through ACLs, controlling topic and group permissions. ACLs for Kafka instances are enabled by default and cannot be disabled. PLAIN SASL users, created automatically with the instance, only offer credentials for SASL users and are granted the All Permitted permission, thus having read and write access to all topics and groups in the instance. For finer\-grained access control, create a SASL user, and create an ACL on the **ACL Management** tab, to grant permissions on a specific resource to the SASL user.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In Message Queue for Kafka, if the permission type of an ACL is Allow, the designated SASL user is allowed to access certain resources with specified IP addresses.</div>


* <div data-tips="true" data-tips-type="tip">ACLs only apply to SASL users with the All Permitted permission disabled.</div>


* <div data-tips="true" data-tips-type="tip">An existing ACL cannot be modified. If needed, we recommend that you delete it and create a new ACL.</div>



<span id="ed0afb5b"></span>
## Prerequisites


* Make sure that the status of the Kafka instance is **Running**.

* SASL users, topics and groups have been created in advance.


<span id="7c6bb8db"></span>
## Procedure


1. Log into [BytePlus Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, click the name of the desired instance.

4. On the upper\-left corner of the **ACL management** tab, click **Add ACL**.

5. Configure the ACL policy.

   Detailed configuration instructions are as follows:

   
   |**Parameter** |**Description** |
   |---|---|
   |User |The SASL user to which you want to grant permissions. The value can be a specific user or all users. |
   |Resource type |ACL resource types supported by Message Queue for Kafka are:<br><br><br>* **Topic**: message topic.<br><br>* **Group**: consumer group. |
   |Resource namematch type |The matching mode for resources. Options are:<br><br><br>* **Exact match**: the ACL only matches resources with an exact name. In this case, specify a resource name.<br><br>* **Prefix matching**: the ACL matches resources with a specified prefix. In this case, specify a resource name prefix. |
   |Resource name |The resource name matched by the ACL, indicating on which resources with the specified name the user has permissions. The value can be all topics or groups or a specified topic or group.<br><br>Configure this parameter only when **Resource namematch type** is set to **Exact match**. |
   |Resource name prefix |The resource name prefix matched by the ACL, indicating on which resources with the specified name prefix the user has permissions.<br><br>Configure this parameter only when **Resource namematch type** is **Prefix matching**. |
   |IP |The IP address used by the SASL user. The user only has the specified permissions when accessing a specific resource through the specified IP.<br><br>Separate IP addresses with commas ( , ). The value can be an asterisk ( \* ), indicating all addresses can access the resource. |
   |Permission type |The type of permissions that the SASL user has.<br><br><br>* If resource type is Topic, the options are as follows:<br><br>   * **Read**: consumes messages from a topic.<br><br>   * **Write**: writes messages to a topic.<br><br>   * **Create**: creates a topic.<br><br>   * **Alter**: changes the number of partitions.<br><br>   * **Delete**: deletes a topic.<br><br>   * **Describe**: views the details of a topic.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When you select the <strong>Create</strong> permission, its scope is not limited by the resources of the Topic. If you select other permission types at the same time, the scope is limited by the resources of the Topic.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have Read, Write, Change and Delete permissions, you automatically have <strong>View</strong> permission.</div><br><br><br>* If resource type is Group, only the **Read** permission is available, namely the access permission for Group. |
   

6. Click **Add**.


<span id="e92381d1"></span>
## Related operations

After creating an ACL, you can also perform the following operations:


* Viewing an ACL list

   On the **ACL management** tab of the target instance, view the ACL list. You can filter ACLs by user name, resource name or prefix, and IP address.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you set custom permissions when creating a topic, the corresponding ACL is automatically created and displayed in the list.   </div>
   

* [Deleting an access control list](https://docs.byteplus.com/en/docs/kafka/deleting-an-ACL)
