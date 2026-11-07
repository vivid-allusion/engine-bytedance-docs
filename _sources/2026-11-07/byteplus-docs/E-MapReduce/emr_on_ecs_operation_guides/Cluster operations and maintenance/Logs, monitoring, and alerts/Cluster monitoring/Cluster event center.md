---
title: "Cluster event center"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Cluster_event_center"
---

Volcano Engine E\-MapReduce (EMR) integrates with the cloud monitoring event center, providing the capability to monitor EMR cluster events. You can use the event center to view details of events occurring in EMR clusters, and also customize event rules and notification contacts, enabling you to capture critical EMR events in real time and promptly resolve them.

This document describes how to view EMR cluster events and how to customize event rules.

<span id="_1-注意事项"></span>
## **Important notes**


* If you do not find event information for the cloud product in the event center, it means that no events have occurred for the cloud product or the events occurred more than 30 days ago.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Events that have occurred are saved by default for 30 days.   </div>
   

<span id="_2-步骤一：创建告警联系人"></span>
## **Step 1: Create an alert contact**


1. Log in to the [cloud monitoring console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, click **Alert center \> Alert contacts** to enter the alert contact list page.

3. On the list page, click the **Create contact** button.

4. In the **Create contact** popup page, enter the alert contact's **Name**, **Email**, or **Phone**, then click the **Confirm** button to complete contact creation.

5. After setting an email or phone and creating the contact, cloud monitoring will send a verification message to the specified email address or phone number.


<span id="_3-步骤二：创建告警联系组"></span>
## **Step 2: Create an alert contact group**

When creating an alert policy, select the corresponding contact group to receive alert notifications through the contact group.


1. Log in to the [cloud monitoring console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, select **Alert center \> Alert contacts** to enter the alert contact list page.

3. On the list page, click the **Contact group** tab, then click the **Create contact group** button.

4. In the **Create contact group** popup page, enter the contact group's **Name**, **Description**, and **Select contacts**, then click **Confirm**.

   For example, the successfully created contact group is **TESTGroup01**.


<span id="_4-步骤三：创建事件规则"></span>
## **Step 3: Create an event rule**

This scenario creates an event rule to monitor the `Create Instance: In Progress` event for cloud servers. Once this event occurs on a cloud server, Cloud Monitoring will send the event information to the designated alert contacts or alert contact groups through the configured alert channels.


1. Log in to the [Cloud Monitoring Console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, click **Event Center \> Event Rules** to enter the event rules page.

3. On the **Event Rules** page, click the **Create Event Rule** button.

4. On the Create Event Rule page, complete the following configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61c1d0907eff4eaeb7fa392144022909~tplv-goo7wpa0wc-image.image) </span>

   Note:

   Parameters with \* before their names are required, while parameters without \* are optional.

   
   |Configuration items |Note |Example value |
   |---|---|---|
   |Basic information |||
   |\*Name |Custom name used to identify the event rule. Names cannot start with a digit or hyphen, and the length must be between 1 and 128 characters. |Event rule Demo |
   |Description |Enter a description for the event rule to facilitate subsequent management. |Event rule Demo |
   |Event rule |||
   |\*Resource type |Select the name of the cloud product to be monitored from the dropdown list. |E\-MapReduce |
   |\*Event name |After selecting the resource type, the dropdown list will be displayed automatically. You need to manually select one or more event names. |Node group scale\-out failed |
   |\*Effective time |Specify the effective time period for the event rule in days. The Event Center only monitors whether the cloud product triggers the event rule during the specified effective time. |00:00 \- 23:59 |
   |\*Severity |Used to indicate the severity of the event. Supports dropdown selection for setting Severe, Warning, or Notification. |Warning |
   |Delivery method |||
   |\*Delivery channel |The system sends alert notifications through the specified channel. Supports configuring one or more channels among **Email, phone, SMS, alert callbacks, log service**.<br><br>Each delivery method has different additional configuration items. You can configure them as needed:<br><br><br>* Email, phone, SMS: Select one or more contact groups as recipients of alert notifications. You can select up to five contact groups under the same account as recipients. For details on how to create contact groups, see above [Step 2: Create an alert contact group](https://docs.byteplus.com/docs/E-MapReduce/105431#_3-%E6%AD%A5%E9%AA%A4%E4%BA%8C%EF%BC%9A%E5%88%9B%E5%BB%BA%E5%91%8A%E8%AD%A6%E8%81%94%E7%B3%BB%E7%BB%84).<br><br>* Alert callbacks: Enter a publicly accessible URL to receive alert information pushed to this address via a POST request.<br><br>* Log service: Select the corresponding log service topic. For details on topic creation, see [Log topic](https://www.volcengine.com/docs/6470/72004). |Email, phone, SMS methods:<br><br>TESTGroup01 |
   

5. After filling in the event rule configuration information, click the **Confirm** button to complete the event rule configuration.

6. After creation, you can view the information of the created event rules in the list on the **Event Rules** page. When a monitored cloud product triggers an event that meets the conditions, you can receive alert notifications via email, phone, or SMS.

   You can also manage rules on the event rules page, such as enabling, disabling, deleting, or editing rules.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8decd3ec1b0340889bcb6c4ecc0be92b~tplv-goo7wpa0wc-image.image) </span>


<span id="_5-步骤四：查看云产品事件"></span>
## **Step 4: View cloud product events**


1. Log in to the [Cloud Monitoring Console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, click **Event Center \> Cloud Product Events** to enter the cloud product events page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e46f424e7e0147228dcbda867ffcb22f~tplv-goo7wpa0wc-image.image) </span>

3. On the **Cloud Product Events** page, view cloud product event information within the specified time period.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1766625e04e4ada975d94e2d9437c98~tplv-goo7wpa0wc-image.image) </span>

4. On the cloud product events page, you can filter event information by setting the time period, cloud product, and event type:

   * You can quickly select or customize the time period to filter events that occurred within that period.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">By default, queries return event information from the past hour.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The specified time range supports minute\-level precision, with seconds defaulting to 00.      </div>
      

   * You can filter event information by selecting different cloud products and event types.

   * You can view the list of events that meet the filter criteria. The **event** string consists of three parts, formatted as `event source:event type:event content`. For example, for the event `emr:ClusterGroup:extend.ERROR`, the event source is EMR, the event type is cluster group, and the event content is expansion failure.

5. Select a specific event, and click the **Details** button in the **Actions** column on the right. On the **Event Details** page, you can view detailed event information in JSON format.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fd52175cb8a4e4baa6f5eac1942a28f~tplv-goo7wpa0wc-image.image) </span>


<span id="_6-事件规则列表"></span>
## Event rule list

When the resource type is E\-MapReduce, the supported event rule list is as follows:


|**Dimension** |**Event name** |
|---|---|
|Cluster |Cluster creation failed |
||Cluster creation succeeded |
||Cluster release failed |
||Cluster release succeeded |
||Node group scale\-out failed |
||Node group scale\-out succeeded |
||Node group scale\-in failed |
||Node group scale\-in succeeded |
||Node group disk expansion failed |
||Node group disk expansion and contraction succeeded |
||Elastic scaling failed |
||Elastic scaling partially succeeded |
||Elastic scaling trigger exception |
||Elastic scaling trigger denied |
||Elastic scaling trigger succeeded |
||Elastic scaling succeeded |
|Service |Airflow \- Schedule process status abnormal |
||Airflow \- Webserver process status abnormal |
||Airflow \- Worker process status abnormal |
||BookKeeper \- Bookie process status abnormal |
||DolphinSchedule \- AlertServer process status abnormal |
||DolphinSchedule \- ApiServer process status abnormal |
||DolphinSchedule \- MasterServer process status abnormal |
||DolphinSchedule \- WorkerServer process status abnormal |
||Doris \- BE process status abnormal |
||Doris \- FE process status abnormal |
||Flume \- FlumeAgent process status abnormal |
||GTS \- Server process status abnormal |
||HBase \- HMaster process status abnormal |
||HBase \- HRegion process status abnormal |
||HDFS \- Datanode process status abnormal |
||HDFS \- JournalNode process status abnormal |
||HDFS \- Namenode process status abnormal |
||HDFS \- Secondary NameNode process status abnormal |
||HDFS \- ZKFC process status abnormal |
||Hive \- Hive Metastore process status abnormal |
||Hive \- Hiveserver2 process status abnormal |
||HUE \- Server process status abnormal |
||Impala \- Catalogd process status abnormal |
||Impala \- Impalad process status abnormal |
||Impala \- Statestored process status abnormal |
||Kafka \- Broker process status abnormal |
||Knox \- Gateway process status abnormal |
||Kudu \- Master process status abnormal |
||Kudu \- TServer process status abnormal |
||Kyuubi \- Kyuubi process status abnormal |
||MapReduce2 \- HistoryServer process status abnormal |
||OpenLDap \- Nss process status abnormal |
||OpenLDap \- Slapd process status abnormal |
||OpenLDap \- Dashboard process status abnormal |
||OpenLDap \- Server process status abnormal |
||Ossa \- Gateway process status abnormal |
||Ossa \- Server process status abnormal |
||Presto \- Coordinator process status abnormal |
||Presto \- Worker process status abnormal |
||Pulsar \- Manager process status abnormal |
||Pulsar \- Broker process status abnormal |
||Ranger \- Admin process status abnormal |
||Ranger \- UserSync process status abnormal |
||Spark \- Livy process status abnormal |
||Spark \- HistoryServer process status abnormal |
||StarRocks \- BE process status abnormal |
||StarRocks \- FE process status abnormal |
||Trino \- Coordinator process status abnormal |
||Trino \- Worker process status abnormal |
||YARN \- ResourceManager process status abnormal |
||YARN \- NodeManager health status abnormal |
||Zookeeper process status abnormal |
