---
title: "Data security"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Data_security"
---

This section introduces the data security capabilities provided by message queue for RabbitMQ and reliability risks in certain scenarios.

<span id="75b52b11"></span>
## Data reliability

BytePlus message queue for RabbitMQ offers various deployment strategies and security capabilities to comprehensively protect user data security and availability.


* Multiple availability zone deployment

   The message queue for RabbitMQ supports single and multiple availability zone deployments, allowing users to choose freely based on business needs when creating instances. Instances deployed across multiple available zones offer stronger disaster recovery capabilities, fully ensuring cluster data reliability and service availability. If high data reliability is required, it is recommended to choose the multiple availability zone deployment mode.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Cross\-available zone deployment improves availability but may cause network latency of 2ms to 3ms.   </div>
   

* Cluster deployment

   The Message Queue for RabbitMQ enhances data reliability through the clustered deployment method of instances. Compared to stand alone instances, clustered instances can configure data redundancy copies, ensuring business recovery in seconds when nodes need to be restarted for upgrades. If you want to ensure business stability in such scenarios, it is recommended to choose the clustered version and use multiple\-replica type queues.

* Data persistence

   The message queue for RabbitMQ supports configurable data persistence to address potential data loss in fault scenarios. For the configuration method of data persistence, please refer to [Configure data persistence](https://docs.byteplus.com/en/docs/rabbitmq/Configure_data_persistence).


<span id="e42deb54"></span>
## Reliability risk

The message queue for RabbitMQ ensures user data security in various aspects. During use, be aware of the data security protection measures necessary to mitigate risks such as reduced availability and data loss.


|Risky operations |Note |
|---|---|
|Using a standalone instance |The message queue for RabbitMQ supports both standalone version and cluster version instances. After choosing to purchase a cluster version instance, you can choose to [Create quorum queue](https://docs.byteplus.com/en/docs/rabbitmq/Create_quorum_queue) and create redundant copies of the queues. This ensures data consistency and service availability in the event of network issues or failures of a few nodes.<br><br>Standalone instance does not have the capability to configure mirrored queues, **so it has lower availability than cluster versions**. |
|Non\-configured data persistence |In a production environment, low\-probability exceptional events happen inevitably. The message queue RabbitMQ version provides high reliability. Therefore, users with strong reliability requirements should place strong emphasis on their own data reliability. Please refer to [Configure data persistence](https://docs.byteplus.com/en/docs/rabbitmq/Configure_data_persistence).<br><br>If non\-configured data achieves persistence, there is a risk of data loss in certain extreme abnormal situations or when extensions trigger an active instance restart. |
|High water mark of resources |When a node of the message queue for RabbitMQ instance reaches a resource high watermark threshold (disk remaining capacity <= 2GiB, memory usage 100%), it triggers the blocking of writing flow to this node. It may lead to failure in message production and limited message consumption, reducing the availability of the RabbitMQ instance.<br><br>The message queue for RabbitMQ provides monitoring metrics such as instance and node resources for you to monitor your instance resource levels at any time. It also offers a recommended configuration alert rule list to help you preemptively avoid potential risks. For detailed information, please refer to [View monitoring data](https://docs.byteplus.com/en/docs/rabbitmq/View_monitoring_data) and [Recommended alarm rules](https://docs.byteplus.com/en/docs/rabbitmq/Recommended_alarm_rules). |
