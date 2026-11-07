---
title: "Recommended alarm rules"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/recommended-alarm-rules"
---

Message Queue for Kafka allows you to configure Vitality Cloud Monitor (VCM) alarm rules, assisting in real\-time tracking of instance running statuses. This topic introduces examples of alarm rule configurations in typical scenarios. We recommend that you refer to these recommended alarm strategies when configuring alarm rules for metrics.

<span id="c22899e8"></span>
## Instance dimension

<span id="ed6d2d9b"></span>
### The disk utilization of an instance exceeds 85%


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition 1 |* Metric Name: CapUtil<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 85% |
   |Alarm level |Notice |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Clean up disk space. You can shorten the message retention period of the topic to expedite message expiration and thus clean up disk space. For more information, refer to [Modifying topic configurations](https://docs.byteplus.com/en/docs/kafka/modifying-topic-configurations).

   * Scale out instance disks. To avoid exceeding the instance disk limit and triggering the automatic message deletion policy, we recommend that you promptly scale out instance disks to increase storage space. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).


<span id="20aa459b"></span>
### Instance disk utilization exceeds 30% and disk skew rate exceeds 30%


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Metric type |Multiple metrics |
   |Trigger condition 1 |* Metric Name: CapUtil<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 30% |
   |Trigger condition 2 |* Metric Name: DiskSkewness<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 30% |
   |Alarm level |Notice |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Scale out instance disks. To avoid filling up the disk of a single broker and impacting future data writes, we recommend that you promptly scale out instance disks to increase storage space. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).

   * Review the business\-side code logic. Modify the data writing method to ensure even data distribution across the brokers of the instance.

   * Rebalance data. In the data rebalancing process, the back\-end service reviews the disk usage difference among all brokers in the cluster and refers to the traffic difference across topic partitions to automatically balance data across all brokers to achieve consistent disk usage.


<span id="332459f2"></span>
### Production traffic exceeds 85% of the specification limit


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: MsgProductionRate<br><br>* Duration: Duration 5 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 85% of the current specification traffic peak. Please refer to [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications) the traffic restrictions of each specification. |
   |Alarm level |Warning |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * For transient traffic peaks, we recommend that you continuously observe the business operation status and resource utilization.

   * If traffic keeps increasing, consider upgrading the instance specification. To avoid exceeding the instance traffic limit and causing production constraints and message accumulation, we recommend that you promptly upgrade the instance type to accelerate message production and consumption. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).


<span id="048af6e8"></span>
### Consumption traffic exceeds 85% of the specification limit


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: MsgConsumptionRate<br><br>* Duration: Duration 5 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 85% of the current specification traffic peak. Please refer to [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications) the traffic restrictions of each specification. |
   |Alarm level |Warning |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * For transient traffic peaks, we recommend that you continuously observe the business operation status and resource utilization.

   * If traffic keeps increasing, consider upgrading the instance specification. To avoid exceeding the instance traffic limit and causing production constraints and message accumulation, we recommend that you promptly upgrade the instance type to accelerate message production and consumption. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).


<span id="c84c6ca9"></span>
### Message production P99 time exceeds the threshold


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: ProductionRequestP99Time<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 100ms |
   |Alarm level |Critical |
   

* Recommendation

   Upon triggering an alarm, we recommend that you review the parameter settings of the client and set appropriate parameter values. After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="09ae2534"></span>
### Message consumption P99 time exceeds the threshold


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: ConsumptionRequestP99Time<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 1s |
   |Alarm level |Critical |
   

* Recommendation

   Upon triggering an alarm, we recommend that you promptly review the business\-side consumption logic to identify factors affecting consumption speed. After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="c84b4b20"></span>
### CPU utilization exceeds 85%


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: CpuUtil<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 85% |
   |Alarm level |Critical |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Verify if client issues cause high CPU utilization, such as the following issues:

      * Kafka version switching causes inconsistency between the Kafka version of the client and the Kafka instance version.

      * A large number of requests exist, but `batch.size` is small for the producer, or a synchronous production mode is set.

      * The compression policy is LZ4.

* If high CPU utilization is not caused by client issues, we recommend that you promptly upgrade the instance specification to improve the processing performance of the instance. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications). After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="43b24f38"></span>
### Memory utilization exceeds 95%


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: MemUtil<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 95% |
   |Alarm level |Critical |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

* For transient traffic peaks, we recommend that you continuously observe the business operation status and resource utilization.

* Verify if the instance reaches the thresholds of the current instance type, such as transactions per second (TPS). If any maximum value allowed by the instance type is reached, we recommend that you upgrade the instance specification to improve the processing performance of the instance. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications). After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="2d182999"></span>
### IP connection count exceeds the threshold

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each Kafka instance has a maximum of 20,000 IP connections. We recommend that you set an alarm for IP connections exceeding 90%.</div>



* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: ConnectionsPerIP<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 18000 |
   |Alarm level |Notice |
   

* Recommendation

   Upon triggering an alarm, we recommend that you modify the IP connection count as needed. After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="61ed2c49"></span>
### Insufficient remaining available partitions in the instance


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: InstanceAvailablePartition<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Minimum value<br><br>* Comparison method: <<br><br>* threshold: Set it according to business requirements, and it is recommended to set it to 50. |
   |Alarm level |* If topics are typically created through the console, it is recommended to set it to **Notice**.<br><br>* If topics are usually created through OpenAPI, it is recommended to set it to **Warning**. |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Clean up idle resources. Verify if any idle partitions exist. If any, we recommend that you promptly clean up them.

   * If the alarm persists after the cleanup, considering buying additional partitions or upgrading the instance specification. During business peak hours, the number of partitions surges in a short period. To avoid insufficient partitions affecting the business processing bandwidth of the instance, we recommend that you buy partitions or upgrade the instance specification in advance to reserve a sufficient number of partitions. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).


<span id="aa7c06b4"></span>
### Insufficient remaining available consumer groups in the instance


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Instance |
   |Trigger condition |* Metric Name: InstanceAvailableGroup<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Minimum value<br><br>* Comparison method: <<br><br>* threshold: Set it according to business requirements, and it is recommended to set it to 50. |
   |Alarm level |* If groups are typically created through the console, it is recommended to set it to **Notice**.<br><br>* If groups are usually created through OpenAPI, it is recommended to set it to **Warning**. |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Clean up idle resources. Verify if any idle consumer groups exist. If any, we recommend that you promptly clean up them. You can also enable the automatic group deletion feature so that the back\-end service automatically cleans up idle groups. For more information, refer to [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) and [Deleting a group](https://docs.byteplus.com/en/docs/kafka/deleting-group).

   * If the alarm persists after the cleanup, considering buying additional partitions or upgrading the instance specification. During business peak hours, the number of partitions surges in a short period. To avoid insufficient partitions affecting the business processing bandwidth of the instance, we recommend that you buy partitions or upgrade the instance specification in advance to reserve a sufficient number of partitions. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).


<span id="be771a98"></span>
## Broker dimension

<span id="a8de835b"></span>
### Broker disk utilization exceeds 85%


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Broker |
   |Trigger condition |* Metric Name: DiskUtil<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 85% |
   |Alarm level |Notice |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

* Clean up disk space. You can shorten the message retention period of the topic to expedite message expiration and thus clean up disk space. For more information, refer to [Modifying topic configurations](https://docs.byteplus.com/en/docs/kafka/modifying-topic-configurations).

* Scale out instance disks. To avoid exceeding the instance disk limit and triggering the automatic message deletion policy, we recommend that you promptly scale out instance disks to increase storage space. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).

* If disk utilization exceeds the threshold on only some brokers and the disk skew rate is high for the instance, data is imbalanced across brokers.


<span id="1559b518"></span>
### Message production P99 time exceeds the threshold


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Broker |
   |Trigger condition |* Metric Name: ProductionRequestP99Time<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 100ms |
   |Alarm level |Critical |
   

* Recommendation

   Upon triggering an alarm, we recommend that you review the parameter settings of the client and set appropriate parameter values. After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="53113f2c"></span>
### Message consumption P99 time exceeds the threshold


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Broker |
   |Trigger condition |* Metric Name: ConsumptionRequestP99Time<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 1s |
   |Alarm level |Warning |
   

* Recommendation

   Upon triggering an alarm, we recommend that you promptly review the business\-side consumption logic to identify factors affecting consumption speed. After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="45211f6e"></span>
### CPU utilization exceeds 85%


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Broker |
   |Trigger condition |* Metric Name: CpuUtil<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 85% |
   |Alarm level |Warning |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Verify if client issues cause high CPU utilization, such as the following issues:

      * Kafka version switching causes inconsistency between the Kafka version of the client and the Kafka instance version.

      * A large number of requests exist, but `batch.size` is small for the producer, or a synchronous production mode is set.

      * The compression policy is LZ4.

   * If high CPU utilization is not caused by client issues, we recommend that you promptly upgrade the instance specification to improve the processing performance of the instance. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications). After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="a78290e1"></span>
### Memory utilization exceeds 95%


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Broker |
   |Trigger condition |* Metric Name: MemUtil<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 95% |
   |Alarm level |Warning |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * For transient traffic peaks, we recommend that you continuously observe the business operation status and resource utilization.

   * Verify if the instance reaches the thresholds of the current instance type, such as transactions per second (TPS). If any maximum value allowed by the instance type is reached, we recommend that you upgrade the instance specification to improve the processing performance of the instance. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications).


<span id="08e3f80e"></span>
### Broker connection count exceeds the threshold

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each Kafka instance has a maximum of 20,000 IP connections. We recommend that you set an alarm for IP connections exceeding 90%.</div>



* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Broker |
   |Trigger condition |* Metric Name: ConnectionsCount<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: 18000 |
   |Alarm level |Notice |
   

* Recommendation

   Upon triggering an alarm, we recommend that you modify the IP connection count as needed. After handling, continue monitoring the metric to verify if the expected effect is achieved.


<span id="5f5d89bf"></span>
## Message accumulation dimension of the partition

<span id="c4351e28"></span>
### Message accumulation in partitions


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |PartitionAccum |
   |Trigger condition |* Metric Name: Partition Message accumulation<br><br>* Duration: Duration 1 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: Set up according to business requirements |
   |Alarm level |Warning |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Review if the instance traffic is approaching its specification limit to determine whether an urgent scale\-out is needed, preventing the traffic from exceeding the specification limit and causing message accumulation.

   * Examine the production environment to determine whether the consumer client encounters consumption issues that cause consumption accumulation. If the consumer client has a performance issue, promptly add consumers or improve the consumption efficiency of individual consumers.


<span id="3301d92c"></span>
## Consumer group dimension

<span id="ea9f6a6c"></span>
### Message accumulation in a consumer group


* Alarm rule configurations

   The core configurations for alarm rules are as follows. For more information, refer to [Setting an alarm rule](https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule).

   
   |Parameter |Value |
   |---|---|
   |Dimension |Group |
   |Trigger condition |* Metric Name: GroupMsgAccum<br><br>* Duration: Duration 3 cycles<br><br>* Value Mode: Maximum value<br><br>* Comparison method: \><br><br>* threshold: Set up according to business requirements |
   |Alarm level |Notice |
   

* Recommendation

   Upon triggering an alarm, you can handle it by using the following methods. After handling, continue monitoring the metric to verify if the expected effect is achieved.

   * Review if the instance traffic is approaching its specification limit to determine whether an urgent scale\-out is needed, preventing the traffic from exceeding the specification limit and causing message accumulation.

   * Examine the production environment to determine whether the consumer client encounters consumption issues that cause consumption accumulation. If the consumer client has a performance issue, promptly add consumers or improve the consumption efficiency of individual consumers.
