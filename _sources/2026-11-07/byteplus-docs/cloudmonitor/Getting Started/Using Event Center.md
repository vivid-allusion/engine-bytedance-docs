---
title: "Using Event Center"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Using-Event-Center"
---

The Event Center of Cloud Monitor enables you to monitor the events of various cloud products. You can use the Event Center to view the event details of integrated cloud products, and also configure custom event rules and event notification contacts. This enables you to capture critical events of cloud products in real time and promptly respond to the events. This topic uses ECS as an example to introduce how to view cloud product events and how to configure custom event rules.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

If you do not query the events of a cloud product by using the Event Center, it indicates that no events have occurred for the cloud product or that the events occurred over 30 days ago.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Occurred events are saved for 30 days by default.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu65ZGK6K2m6IGU57O75Lq6"></span>
## Step 1: Create a contact


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification \> Contacts**.

3. Click **Create contact**.

4. In the **Create contacts** dialog box, specify the **Name** and **Email** or **Phone** parameters of the alert contact and then click **Confirm**.

5. After you configure the email address or phone number and create the contact, Cloud Monitor will send a verification message to the specified email address or phone number.

   The following figure shows the verification message content sent to an email address. You need to click the URL to complete the verification.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65ZGK6K2m6IGU57O757uE"></span>
## Step 2: Create a contact group

When you create an alert policy, select the corresponding contact group to receive alert notifications through the contact group.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification \> Contacts**.

3. Click the **Contact group** tab, and then click **Create contact group**.

4. In the **Create contact group** dialog box, specify the **Name**, **Description**, and **Select contacts** parameters of the contact group and then click **Confirm**.

   For example, the created contact group is `TESTGroup01`.


<span id="a4d13fbc"></span>
## Step 3: Create a callback URL


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Notification** \> **Callback**.

3. On the **Callback address list** page, click **Create callback address**.

4. On the **Create callback address** page, specify the following parameters and then click **Confirm**.

   
   |Parameter |Descriptions |
   |---|---|
   |Callback address name |Specify a custom name for the callback URL to identify the callback URL. Duplicate names are not allowed. |
   |Callback address type |Select the callback URL type. Supported types include **Lark**, **DingTalk**, **WeCom**, and **General callback address**. |
   |Callback address |Enter a publicly accessible URL and then click **Test** to verify the callback URL.<br><br><br>* If the callback URL returns the HTTP status code 200, it indicates that the connectivity test is successful, and the callback URL can receive alerts and event notifications.<br><br>* The connectivity test enforces a one query per second (QPS) limit. |
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65LqL5Lu26KeE5YiZ"></span>
## Step 4: Create an event rule

In this step, you will create an event rule to monitor ECS events that are in the `Create instance: In progress` state. If the ECS event occurs, Cloud Monitor will send the event information to the specified alert contact or contact group through the specified alert channel.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Event Center \> Event Rule**.

3. On the **Event Rule** page, click **Create event rule**.

4. On the Create event rule page, specify the following parameters, and then click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, only the required parameters are specified. You can adjust the configurations based on your business requirements.   </div>
   

   
   |Sections |Parameter |Descriptions |Sample value |
   |---|---|---|---|
   |Basic information |Name |Specify a custom name to identify the event rule. |Event rule Demo |
   ||Description |Specify a custom description for the event rule. |The event rule is used for observing created ECS instances. |
   |Event rule |Resource type |Specify the cloud service to be monitored. |Elastic Compute Service (ECS) |
   ||Event name |After you specify the **Resource type** parameter, the page will automatically display the event drop\-down list of the selected resource type. You need to manually select one or more event names. |`Create instance: In progress` |
   ||Effective time |Specify the effective period of the event rule by day. Event Center only monitors whether the cloud service triggers the event rule during the specified effective period. |`00:00 - 23:59` |
   ||Level |Specify the severity level of the event. Valid values: **Critical**, **Warning**, **Notice**. |Warning |
   |Delivery method |Delivery channel |The system sends alert notifications through specified channels. You can select one or more of the following channels, which include **Email**, **Phone**, **SMS**, **Alert callback**, **Torch Log Service**, and **Message Queue Kafka**. |Email, Phone, and SMS |
   ||Alert contact group |Select one or more contact groups as the recipients of alert notifications. Up to five contact groups within the same account can be selected as recipients. |`TESTGroup01` |
   ||Webhook |Enter an alert callback URL or select one or more created callback URLs.<br><br><br>* You can select created webhook URLs. Up to eight webhook URLs can be selected.<br><br>* You can enter only one webhook URL. |`http://example.com/alert` |
   ||Theme |Select a TLS topic.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you set the Delivery channel parameter to Torch Log Service, Cloud Monitor does not charge you for data. However, after Cloud Monitor delivers data to TLS, TLS will charge you for the data.</div><br> |`Topic1` |
   ||Message queue |Select a topic.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Notifications can be delivered only to topics of Message Queue for Kafka in the China (Beijing) region.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a Kafka instance is bound to an allowlist, only the IP addresses configured in the allowlist can access the instance. Note:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Do not select instances in an allowlist if you set the Delivery channel parameter to Message queue kafka.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">After you select an instance, do not add the instance to an allowlist.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select a Message Queue for Kafka topic for an event rule for the first time, the user named <code>__volcevent_xxxvolc</code> will be automatically created on the <strong>User Management</strong> tab of the topic. Do not delete this user. Otherwise, Cloud Monitor will not be able to deliver messages to this topic.</div><br> |`topicA` |
   

   After the event rule is created, you can view the information of the created event rule on the list on the **Event Rule** page. When an event of a monitored cloud product that meets the specified conditions occurs, you can receive alert notifications through email, phone calls, or SMS messages.


<span id=".5q2l6aqk5Zub77ya5p-l55yL5LqR5Lqn5ZOB5LqL5Lu2"></span>
## Step 5: View cloud product events


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview). 

2. In the left navigation bar, click **Event Center \> Cloud Service Event**.

3. On the **Cloud Service Event** page, specify the following parameters to query ECS events.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2491b275a87299888348a7e1416897ee.png) </span>

   List description:

   * In Section ① in the preceding figure, query events that occurred during the time period from `2024-06-27 14:02:00 to 2024-07-05 14:02:00`.

   * In Section ② in the preceding figure, query **ECS** events that are in the **Start instance: In progress** state.

   * After you configure the preceding query criteria, you can view the occurred events in Section ③.

4. Find a specified system event and click **Details** in the **Actions** column.

   In the **Event details** panel, you can view detailed event information in JSON format, where the `data` field contains detailed information about the cloud product for which the event occurred.
