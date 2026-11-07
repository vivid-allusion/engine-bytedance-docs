---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/kafka_basic_usage"
---

This article introduces some commonly used commands related to the Kafka component of Volcano Engine E\-MapReduce (EMR).

<span id="_1-使用前提"></span>
## 1 **Prerequisites**

The EMR cluster type related to Kafka has already been created for real\-time computing scenarios. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-登录集群"></span>
## 2 **Log in to the cluster**


1. Log in to [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the top menu bar, select the region and project space from the dropdown according to your actual scenario.

3. Click **Cluster list \> Cluster name \> Service list \> Kafka \> Deployment topology** tab to enter the deployment topology of the Kafka component service.

4. Click the ECS ID under the component name (emr\-core\-1 host name) to go to the instance page of the cloud server, then click the **Remote connection** button in the upper right corner.

5. Select a remote connection method (ECS Terminal is recommended), enter the relevant cluster authentication information, and log in to the command line environment of the Kafka cluster to execute relevant commands.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the cluster node group has been assigned a public IP, you can also connect to the cluster via SSH. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/104404">Log in to the cluster</a>.</div>


<span id="_3-常用命令"></span>
## 3 **Common commands**

<span id="_3-1-创建-topic"></span>
### 3.1 Create topic

```shell
/usr/lib/emr/current/kafka/bin/kafka-topics.sh --create --bootstrap-server `hostname -i`:9092 --topic test --replication-factor 3 --partitions 12
```


<span id="_3-2-查看-topic-列表"></span>
### 3.2 View topic list

```shell
/usr/lib/emr/current/kafka/bin/kafka-topics.sh --list --bootstrap-server `hostname -i`:9092
```


<span id="_3-3-查看-topic-状态"></span>
### 3.3 View topic status

```shell
/usr/lib/emr/current/kafka/bin/kafka-topics.sh --describe --bootstrap-server `hostname -i`:9092 --topic test
```


<span id="_3-4-发送消息"></span>
### 3.4 Send message

```shell
/usr/lib/emr/current/kafka/bin/kafka-console-producer.sh --broker-list `hostname -i`:9092 --topic test
1
2
3
```


<span id="_3-5-消费消息"></span>
### 3.5 Consume message

```shell
/usr/lib/emr/current/kafka/bin/kafka-console-consumer.sh --bootstrap-server `hostname -i`:9092 --group testGroup --topic test --from-beginning earliest
```


<span id="_3-6-查看消费列表"></span>
### 3.6 View consumer list

```shell
/usr/lib/emr/current/kafka/bin/kafka-consumer-groups.sh --list --bootstrap-server `hostname -i`:9092
```


<span id="_3-7-查看消费状态"></span>
### 3.7 View consumer status

```shell
/usr/lib/emr/current/kafka/bin/kafka-consumer-groups.sh --bootstrap-server `hostname -i`:9092 --group testGroup --describe
```
