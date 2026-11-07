---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/kafka_advanced_usage"
---

This article introduces advanced usage of the Kafka component in Volcano Engine E\-MapReduce (EMR), enabling you to use Kafka in greater depth.

<span id="扩容"></span>
# Cluster scaling

You can perform Kafka cluster scaling operations on the cluster management page in the EMR console.

After scaling open\-source Kafka by adding new brokers, traffic does not automatically migrate to the new brokers. There are generally two ways to migrate traffic to the new brokers.


* Partition expansion: Use a script to directly expand partitions. For example, if there were previously 12 partitions, you can expand to 24 partitions. New partitions will be assigned to new brokers according to the policy, which is the simplest method. The drawback is that the old partitions remain on the old brokers, resulting in unbalanced traffic across the cluster.

* Reassign: This method migrates partition data to the new brokers, and the steps are relatively complex.


<span id="_1-扩分区"></span>
## 1 Partition expansion

Run the following command to perform partition expansion:

```shell
/usr/lib/emr/current/kafka/bin/kafka-topics.sh --alter --zookeeper {zookeeper_connect} --topic {topic} --partitions {num}
```


<span id="_2-reassign-进行数据均衡"></span>
## 2 Reassign for data balancing

If the number of existing partitions already exceeds 24 and the data volume is large, consider using the following method for balancing.

Script: kafka\-reassign\-partitions.sh, which has three main operations:


* \-\-generate: Generate a partition reassignment plan

* \-\-execute: Execute the partition reassignment plan

* \-\-verify: Verify the partition reassignment result


<span id="_2-1-选择要处理的-topic"></span>
### 2.1 Select the topic to process

Save the information of the topic to be processed to a JSON file in the following format. For example, if the topic to be processed is test, Save the topic information as topic_test.json, with the following content:

```json
{
    "topics":
    [
        {
            "topic": "test"
        }
    ],
    "version": 1
}
```


<span id="_2-2-生成分区重分配计划"></span>
### 2.2 Generate a partition reassignment plan

<span id="_2-2-1-获取执行计划"></span>
#### 2.2.1 Obtain the execution plan

You can refer to the following command.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The broker identifier in the \-\-broker\-list parameter is the broker.id value. Fill in all broker.id values for the cluster to generate the recommended partition information.</div>


```shell
sh bin/kafka-reassign-partitions.sh --zookeeper {zookeeper_connect}  --topics-to-move-json-file {topic_test.json} --broker-list "1001,1002,1003,1004,1005,1006" --generate
```


<span id="_2-2-2-保存目标分区信息"></span>
#### 2.2.2 Save the target partition information

After running the generate command, there will be two JSON data files:


* The first is the Current partition replica assignment, which is the current assignment.

* The other is the Proposed partition reassignment configuration, which is the recommended assignment and the file to be saved.


Save the **recommended assignment** as a JSON file, for example: **topic_test_reassignment.json**

<span id="_2-3-执行分区重分配计划"></span>
### 2.3 Execute the partition reassignment plan

```shell
sh bin/kafka-reassign-partitions.sh --zookeeper {zookeeper_connect} --reassignment-json-file  {topic_test_reassignment.json} --execute
```


<span id="_2-4验证分区重分配结果"></span>
### 2.4 Verify the partition reassignment result

```shell
sh bin/kafka-reassign-partitions.sh --zookeeper {zookeeper_connect} --reassignment-json-file  {topic_test_reassignment.json}  --verify
```


If all results show 'successfully', the operation is successful. If the data volume is large, you may need to wait for a period of time.

<span id="_3-创建时绑定了公网-ip-的-kafka-集群在扩容-core-节点后需要做的配置操作"></span>
## 3 Configuration operations required after scaling Core nodes in a Kafka cluster that was bound to a public IP at creation

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section applies to EMR 3.4.X and earlier software stack versions. For EMR 3.5.0 and later software stack versions, these configuration steps are not required.</div>


When a Kafka cluster is created, if the Core node group where the Broker resides is bound to a public IP, Kafka Broker parameters such as advertised.listeners are automatically configured, allowing Kafka Broker to be accessed via the public IP (port: 19092) and the internal network address (port: 9092).

After expanding the Core nodes in a Kafka cluster, to continue accessing Kafka Broker via the public IP address, perform the following steps:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After expanding the Core nodes in a Kafka cluster, if the following steps are not performed, Kafka Broker can still be accessed via the internal network address.</div>



1. Bind a public IP to all newly expanded Core nodes.

2. In **Cluster list \> Kafka cluster name \> Service list \> Kafka service name \> Service parameters**, modify the configuration parameter of the Kafka service for this cluster: **kafka_broker_hostname_eip_map_str**. The value of this parameter is a JSON string that contains the mapping from the hostname of each Kafka Broker node to its public IP address. Add the mapping from the hostname to the public IP address for the newly expanded Core nodes in the value of this parameter.

3. Restart the Kafka Broker component under the newly expanded Core nodes in the Kafka service center.


After successfully completing the above steps, you can continue to access Kafka Broker via the public IP address.
