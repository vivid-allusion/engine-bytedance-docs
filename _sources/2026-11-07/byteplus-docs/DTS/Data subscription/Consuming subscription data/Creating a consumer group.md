---
title: "Creating a consumer group"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group"
---

After successfully creating a data subscription task, create a consumer group in the DTS console or through the open\-source Kafka SDK based on the consumer type. This topic describes how to create a consumer group for built\-in middleware on the Database Transmission Service (DTS) console.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

A consumer group is a set of consumers with the same consumer group ID. When a Topic is consumed by multiple consumers in the same consumer group, each message is delivered to only one consumer to achieve load balancing of consumption. With consumer groups, you can ensure that the messages of a Topic are consumed in parallel.

After creating the data subscription task, data and schema updates in the database are delivered as message data to the designated consumer. You must also create the corresponding consumer group to consume the data. The methods to create consumer groups differ by consumer type as follows:


* Built\-in middleware: Create a consumer group through DTS. For details, refer to the [Procedure](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group#.5pON5L2c5q2l6aqk) section in this topic.

* Self\-owned middleware:

   * Kafka connected over express network: Create a consumer group ("Group") using the open\-source Kafka SDK. For details, refer to [Kafka documentation](https://kafka.apache.org/documentation/).

   * Message queue Kafka: Create a consumer group ("Group") using the Message Queue for Kafka SDK. After creation, you can view the Group list in the Message Queue for Kafka console. For details, refer to [Message Queue for Kafka SDK references](https://docs.byteplus.com/en/docs/kafka/Apache-Java-SDK-overview).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* You only need to create a consumer group on the DTS console when the **Subscription data delivery** is **Subscription built\-in middleware**. For other types, refer to [Background](https://docs.byteplus.com/en/docs/DTS/adding_a_consumer_group#.6IOM5pmv5L-h5oGv) to select the corresponding method to create a consumer group.

* A single data subscription task supports the creation of up to 20 consumer groups. By creating multiple consumer groups, the goal of repeated data consumption can be achieved.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Create a data subscription task on demand. For detailed steps, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

* The data subscription task must be **In progress**.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. You can access the create consumer group dialog box through two methods.

   * **Method 1**

   On the **Data subscription list** page, select the target data subscription task and click **New consumer group**.

   * **Method 2**

      1. On the **Data subscription list** page, click the target data subscription task name.

      2. On the page of the target data subscription task, click **Data consumption**.

      3. On the **Data consumption** tab, click **Create new consumer group**.

5. In the **Create new consumer group** dialog box, configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Consumer group name** |Custom consumer group name. It is recommended to set a name related to your business for easier future queries. Naming rules are as follows:<br><br><br>* The length must be between 2 to 32 characters.<br><br>* It consists of digits, uppercase letters, lowercase letters, underscores (_), and hyphens (\-). |
   |**Account** |Set the consumer group account. The account naming rules are as follows:<br><br><br>* The length must be between 2 and 16 characters.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of numbers, uppercase letters, lowercase letters, and underscores (_). |
   |**Password** |Set the account and password of the consumer group. The password rules are as follows:<br><br><br>* The length must be between 8 and 32 characters.<br><br>* It contains at least three of the following: uppercase letters, lowercase letters, digits, and special characters. Special characters are `_#!@$%^&*()+=-`. |
   |**Confirm password** |Enter the consumer group account password again. |
   

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[CreateSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/createsubscriptiongroup) |Call the CreateSubscriptionGroup API to create a subscription consumer group. |
|[DescribeSubscriptionGroup](https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroup) |Call the DescribeSubscriptionGroup API to query the subscription message group. |
|[DescribeSubscriptionGroups](https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroups) |Call the DescribeSubscriptionGroups API to query the consumer group list. |
|[DescribeSubscriptionGroupProgress](https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroupprogress) |Call the DescribeSubscriptionGroupProgress API to query the progress of the subscription consumer group. |
