---
title: "Recommended alarm rules"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Recommended_alarm_rules"
---

The message queue RabbitMQ version supports configuring cloud monitoring alarm rules to help you monitor the instance's operating status in real time. This section introduces examples of alarm rule configurations for typical scenarios. We recommend that you refer to these alarm policies to configure alarm rules for monitoring metrics.

<span id="49287fa6"></span>
## Instance dimension

<span id="1c1f1b02"></span>
### Instance disk usage exceeds 85%


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger conditions |* monitoring metrics: disk usage rate<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: notification<br><br>* threshold: 85% |
   

* Handling Suggestions

   After an alarm triggers, we recommend that you monitor whether the instance's disk usage remains high.

   * If the business peak is brief, continue monitoring.

   * If disk usage continues to rise, we recommend that you promptly expand the disk capacity to reduce usage. For methods to expand disk capacity, please refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications).

      After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="5cb1ecd2"></span>
### Instance memory usage exceeds 85%


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* Monitoring metrics: memory usage<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: 85% |
   

* Handling Suggestions

   After an alarm is triggered, monitor whether the instance's memory usage remains high.

   * If the business peak is brief, continue monitoring.

   * If memory usage continues to rise, upgrade the instance specifications promptly to reduce memory usage. For instructions on upgrading instance specifications, refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications).

      After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="b5a4a05a"></span>
### Instance CPU usage exceeds 85%


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* monitoring metrics: instance CPU usage<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: 85% |
   

* Handling Suggestions

   After an alarm is triggered, promptly upgrade the instance specification to reduce CPU usage. If it is already the highest specification, expanding storage space is recommended. For detailed steps, please refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications). After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="46238e64"></span>
### Excessive instance connections


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* monitoring metrics: number of connections<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: It is recommended to set at 90% of the instance's current computing specification maximum connections. For the maximum connections of each specification, please refer to [Product Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications). |
   

* Handling Suggestions

   After an alarm is triggered, you can first check the monitoring to determine whether the instance connection count remains consistently high. If the peak is occasional, we advice you to continue observation. If the instance connection count remains high for an extended time, use the following methods to investigate.

   * Optimize application usage to ensure each connection only opens necessary channels. Reuse channels as much as possible to control the number of connections.

   * Clean up dormant connections and channels that have been inactive for an extended period. If there are a large number of unused connections and channels, you may consider closing the connections to reduce the number of connections.


After handling, please continue monitoring this metric to confirm if the expected results are achieved.

<span id="a82ba574"></span>
### Excessive usage of instance queue count


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* monitoring metrics: queue count<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: customize according to business requirements, recommended to set at 90% of the current specification's maximum queue size. please refer to [Product Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications) for the maximum queue size of each specification. |
   

* Handling Suggestions

   After triggering an alarm, we recommend that you clear redundant or deletable queues. If there is no removable queue and new queues still need to be continuously created, it is recommended to promptly scale up the instance's computing specifications to increase the number of available queues. For how to upgrade instance specifications, refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications).

   After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="c4449259"></span>
### Instance production and consumption rate is too high.


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* monitoring metrics: instance production consumption rate<br><br>* duration: 3 periods<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: customize according to business needs. The recommendation is to set at 90% of the current specification’s recommended TPS peak. For the recommended TPS peak of each specification, see [Product Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications). |
   

* Handling Suggestions

   If the alarm is triggered, the current instance's level is close to the upper limit of its specifications. If it continues to rise, it may affect business stability. We recommend that you upgrade the instance specifications as recommended. For upgrading details, please refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications).

   After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="c024e26a"></span>
### Unroutable message rate


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |**Configuration** |**value** |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* monitoring metric: Unroutable message rate<br><br>* duration: 3 periods<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: greater than 0 |
   

* Handling Suggestions

   If the alarm is triggered, it indicates that there is no matching queue available for messages to be published to the exchange. This means that messages cannot be routed to any queues and will either be directly discarded or returned to the producer, causing message delivery failures. It is recommended to check the producer configuration.


<span id="07508e1d"></span>
### Message backlog


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, please refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* monitoring metric: consumable message count<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: notification<br><br>* threshold: customize based on business needs |
   

* Handling Suggestions

   If the alarm is triggered, we recommend that you monitor whether the instance's disk usage remains high.

   * If the business peak is brief, continue monitoring.

   * If messages accumulate significantly over time, we recommend that you investigate the cause by checking relevant metrics, such as whether the production rate greatly exceeds the consumption rate. After identifying the cause of message accumulation, you can alleviate the issue through the following methods:

      * Add consumers: increasing consumers can speed up message consumption and relieve backlog issues.

      * Scale the queue: increasing queue capacity can ease message backlog but may consume more instance resources.

   After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="2e8b493b"></span>
### Node online rate is less than 100%


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, please refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* Monitoring metric: node online rate<br><br>* duration: 3 continuous cycles<br><br>* Value method: minimum<br><br>* Comparison method: <<br><br>* Alarm level: severe alarm<br><br>* Threshold: 100% |
   

* Handling Suggestions

   If the alarm is triggered, it indicates unexpected node disconnections in the instance. Contact technical support through the [Ticket System](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000257) for assistance in troubleshooting.


<span id="245f591f"></span>
## Node Dimension

<span id="296682fa"></span>
### Node disk usage exceeds 85%


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, please refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Node |
   |Trigger conditions |* monitoring metrics: disk usage rate<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: 85% |
   

* Handling Suggestions

   After the alarm triggers, please monitor whether the node's disk usage remains high and check the consumption logic.

   * If the business peak is brief, continue monitoring.

   * If disk usage continues to rise, we recommend that you promptly expand the disk capacity to reduce usage. To expand disk capacity, please refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications).

   * If insufficient consumption capacity causes message backlog, disk usage rises. Please check if the consumption status and progress meet expectations.

   After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="b0be4a6e"></span>
### Node memory usage exceeds 85%


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Instance |
   |Trigger conditions |* Monitoring metrics: memory usage<br><br>* duration: 3 continuous cycles<br><br>* value method: maximum<br><br>* comparison method: \><br><br>* Alarm level: warning<br><br>* threshold: 85% |
   

* Handling Suggestions

   After an alarm triggers, we suggest that you promptly upgrade the instance specifications to reduce memory usage. If it is already the highest specification, expanding storage space is recommended. For detailed steps, please refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications).

   After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="8b2cf55c"></span>
### Node memory high watermark


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Node |
   |Trigger conditions |* monitoring metric: node memory high water mark<br><br>* duration: 1 continuous cycle<br><br>* value method: maximum<br><br>* comparison: \>=<br><br>* Alarm level: severe alarm<br><br>* Threshold: 1 |
   

* Handling Suggestions

   An alarm triggers when the available memory usage on a single node reaches 100% (equivalent to 40% of the actual physical memory). The backend service will automatically pause data writing. Please upgrade the instance specifications promptly to reduce memory usage. If it is already the highest specification, expanding storage space is recommended. For detailed steps, please refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications).

   After handling, please continue monitoring this metric to confirm if the expected results are achieved.


<span id="0c37bf98"></span>
### Node disk high watermark


* Alarm rule configuration

   The core configurations of alarm rules are as follows. For steps to create alarm rules, refer to [Setting Alarm Rules](https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules).

   
   |Configuration |value |
   |---|---|
   |dimension |Node |
   |Trigger conditions |* monitoring metric: disk high watermark<br><br>* duration: 1 continuous cycle<br><br>* value method: maximum<br><br>* comparison: \>=<br><br>* Alarm level: severe alarm<br><br>* Threshold: 1 |
   

* Handling Suggestions

   An alarm indicates that the disk usage of a single node in the instance has reached 100%. The backend service will automatically pause data writing. We suggest that you expand storage space promptly. For detailed steps, please refer to [Upgrading Instance Specifications](https://docs.byteplus.com/en/docs/rabbitmq/Upgrade_instance_specifications). after handling, please continue monitoring this metric to confirm if the expected results are achieved.
