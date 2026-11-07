---
title: "Introduction to YARN Node Label and best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Introduction_to_YARN_Node_Label_and_best_practices"
---

<span id="_1-基本介绍"></span>
## Basic introduction

YARN (Yet Another Resource Negotiator) Node Label is a mechanism in YARN used to identify Node Manager nodes and manage nodes by "grouping/partitioning" them. By assigning different labels to nodes, YARN can allocate tasks to nodes in specific partitions based on the labels.

The Node Label feature has a wide range of use cases and is commonly used for workload isolation in heterogeneous clusters, multiple scenarios, or computing frameworks.

Currently, all YARN components included in EMR versions support the Node Label feature.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After configuring Node Label, the elastic scaling feature based on load will not function properly due to metric changes.</div>


<span id="_2-node-label"></span>
## Node Label

Currently, a node can only be assigned to a single Node Label, so Node Label can be used to divide the entire YARN cluster into mutually exclusive sets of nodes. By default, nodes belong to the DEFAULT partition (`partition=""`, empty string).

Node Label is divided into two types:


* exclusive: Only containers whose requests match the partition are allowed to be scheduled onto nodes in that partition.

* non\-exclusive: In addition to allocating containers requested for this partition, containers requested for the DEFAULT partition (or containers not specifically assigned to a partition) can also be scheduled onto these nodes when resources are available.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, only the Capacity Scheduler supports partition scheduling with Node Labels.</div>


In general, Node Label is used together with queues. Users need to configure how much resources each queue can use in each partition. You can use scheduler configuration or the node\-label\-expression parameter of the compute engine to schedule task containers in queues to partitions accessible by the queue.

Next, we introduce the basic usage and common practices of Node Label.

<span id="_2-1-node-label-功能开启"></span>
### Enable Node Label functionality


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar, click **Cluster list \> Cluster name** to enter the specific cluster details page.

3. On the cluster details page, click **Service list \> YARN \> Service parameters**, and search for yarn.node\-labels.enabled on the service parameters page.

4. Change the value of yarn.node\-labels.enabled from false to true.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4dd85cb2739f9a7d0f7d51448d065c5d.png) </span>


5. Modify the value of yarn.node\-labels.fs\-store.root\-dir


The default value of yarn.node\-labels.fs\-store.root\-dir is: `/system/yarn/node-labels`. However, to ensure high availability of the cluster and prevent loss of label information if the RM crashes, it is recommended to Save the label information on HDFS. First, create a new directory on HDFS:

```shell
hadoop fs -mkdir -p /yarn/node-labels
```


Then modify this configuration parameter to the actual address on HDFS.

<span id="_2-2-node-label-新建"></span>
### Create a new Node Label

Log in to the ecs node where master\-1\-1 is located and run the following command to obtain all current node labels in yarn:

```shell
yarn cluster --list-node-labels
```


Perform the following operation to create labels.

```shell
yarn rmadmin -addToClusterNodeLabels "streaming,batch"
```


Then run the list command to check that the labels have been created successfully.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ee81b1be2967031ef6145ea0552a1d0.png) </span>

In the cluster details page, click **Access link\>YARN ResourceManager UI** to open the YARN Web UI. Click the "Node Labels" menu on the left. You can see that both labels are now visible in the UI, but from the "Num Of Active NMs" column, you can see that neither has been bound to any node yet.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_831ced72d28556b68e534a0d31005c31.png) </span>

<span id="_2-3-node-label-绑定节点"></span>
### Bind nodes to Node Labels

There are already two worker nodes (core/task), as shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f241f751c3dc7df6015300d97ba7f314.png) </span>

In **Node management\>Node group list**, copy the node group name. For example, bind the "core\-1\-1" node to the "batch" label, and bind nodes starting with "core\-1\-2" to the "streaming" label.

Run the following command to complete the operation:

```shell
yarn rmadmin -replaceLabelsOnNode "core-1-1.emr-xxx.cn-beijing.emr-volces.com:45454=batch"
yarn rmadmin -replaceLabelsOnNode "core-1-2.emr-xxx5.cn-beijing.emr-volces.com:45454=streaming"
```


On the "Node Labels" page, you can see that both labels are bound to their respective NodeManagers:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4583d9a7ad55612ca6bd26edb31adcc.png) </span>

At the same time, the first column on the "Nodes" list page will also display the corresponding label:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff5f91093cf0e095ac907bb17a397465.png) </span>

<span id="_2-4-node-label-绑定弹性节点"></span>
### Bind elastic nodes to Node Labels

Nodes bound in Node Labels can leverage the elastic scaling capability of the EMR YARN component and the "cluster script" feature of the EMR cluster for elastic scaling. Here is a brief usage guide:


1. On the **Node management** page, click the right side "[新增节点组](https://docs.byteplus.com/docs/E-MapReduce/105443#_4-%E6%96%B0%E5%A2%9E%E8%8A%82%E7%82%B9%E7%BB%84)" to create a task node group:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ef80a6ea66c9048e8e8c5c937a53ae99.png) </span>


2. On the **Cluster script** page, click [Cluster scripts](https://docs.byteplus.com/docs/E-MapReduce/105437) on the right.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f3805d0b4b565065e7875bb8f00cdc1.png) </span>

Copy the content from the **Script location** text box to your local machine and modify the TASK_GROUP and NODE_LABEL variables.


* TASK_GROUP: Prefix of the node group name. The node group name must match the selected **node group**.

* NODE_LABEL: The Node Label to which the user wants to add the node. Before running the script, ensure that the Node Label has been correctly created in the cluster.


```shell
#!/bin/bash

source /etc/profile

# 需人为调整的变量
TASK_GROUP="task-2-"
NODE_LABEL="batch"

# 执行yarn node -list命令并获取输出
output=$(yarn node -list)

# 循环遍历输出的每一行
while IFS= read -r line; do
  # 检查当前行是否以TASK_GROUP开头
  if [[ $line =~ ^$TASK_GROUP.* ]]; then
    # 使用awk提取行的第一部分，即节点名称
    nm_node=$(echo "$line" | awk '{print $1}')

    # 检查是否成功提取了节点名称
    if [[ -n $nm_node ]]; then
      # 执行yarn rmadmin命令，替换节点标签
      yarn rmadmin -replaceLabelsOnNode "$nm_node=$NODE_LABEL"
    fi
  fi
done <<< "$output"
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To ensure that the script can read a series of environment variables, the command "source /etc/profile" is necessary.</div>


<span id="_2-5-脚本验证"></span>
### Script verification

Go to the **Access link\>YARN ResourceManager UI** page to view the mapping between nodes and Node Labels in the current cluster.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1a58946e18bd6c15e57905c975f9bcc.png) </span>

At this point, there is one node under TaskGroup\-2, but it has not been assigned a label. Then, in **Node management**, add [Scale up clusters](https://docs.byteplus.com/docs/E-MapReduce/104396) a node to TaskGroup\-2

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b33256bfd590a32e5aba454ebf2f63ee.png) </span>

After the status of the new node changes from "Initializing" to "Running", go to the **Access link\>YARNResourceManager UI\>Node Label** list to check that both nodes under TaskGroup\-2 have been assigned the "batch" label.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b93011ab190b7f29f0dcdd9b8cb90422.png) </span>

The relevant information in the Node list is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_129d99f97eb9a5674f1e1208d0938d53.png) </span>

On the **Cluster script\>Execution record** page, view the execution record.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_65333f7e2f7547ebffef48ac78ae120f.png) </span>

Click "Execute" to "DEBUG" the script on the existing nodes. After confirming the logic is correct, it can be applied to elastic scaling.

On the **execution record** page, click an individual **execution record** to view the detailed execution record.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fc03b2c3608e78b40e68c711cdfe29f.png) </span>

Execution logs are divided into two categories:


* Script execution logs: Display loaded script information and script content.

* Logs on scaling nodes: Display the standard output stdout/stderr from script execution.


<span id="_2-6-node-label-绑定弹性节点的最佳实践"></span>
### Best practices for binding Node Label to elastic nodes

Node Label can be combined with [Auto scaling](https://docs.byteplus.com/docs/E-MapReduce/105442) capabilities to provide a more flexible and convenient mechanism for assigning Node Labels.

Elastic scaling is one of the advantages of Volcano Engine EMR, and the management of elastic scaling revolves around "TaskGroup". EMR divides scaling nodes into Groups, and scaling rules are also applied to TaskGroups. This is very similar to how YARN introduces Node Label for cluster partitioning and grouping. It is recommended that the logic for using Node Label corresponds to TaskGroup. EMR also supports executing scripts for assigning "Label" on all Nodes within a TaskGroup.

<span id="_2-7-node-label-使用的最佳实践"></span>
### Best practices for Node Label usage

Node Label provides partitioning of nodes, enabling YARN to physically isolate different types of workloads during scheduling. Users are advised to divide and create Node Labels for workloads that differ significantly and must not affect each other.

Common partitioning methods include:


* Different business types:

   * Data ingestion (data lake, data warehouse).

   * Offline ETL.

   * Real\-time ETL.

   * Machine learning (data preprocessing, and so on).

   * AD Hoc

   * ...

* Or heterogeneous node types:

   * High\-performance computing / high\-performance IO.

   * Old specification configuration / new specification configuration.


The above partitioning methods are not absolute; it depends on the user's requirements for business availability. For example, if a user has extremely high SLA requirements for real\-time jobs, it is not recommended to use Node Label isolation. Instead, it is recommended to separate physical clusters. This is because sometimes parameter tuning involves restarting the cluster, which some real\-time workloads cannot tolerate.

<span id="_3-queue"></span>
## Queue

The flexibility of Node Label can be maximized when combined with Queue. This section provides a brief introduction and creation of Queue.

<span id="_3-1-queue-介绍"></span>
### Queue introduction

YARN Queue is a mechanism in YARN for resource management and task scheduling, representing a logical resource pool. In YARN, all tasks must be submitted to a specific Queue, after which YARN's ResourceManager assigns the tasks to appropriate nodes for execution based on factors such as task priority and available resources. YARN Queues can be used to isolate different types of tasks to ensure that different types of tasks can run on different resource pools, thereby improving system reliability and efficiency.

<span id="_3-2-queue-创建"></span>
### Queue creation

<span id="_3-2-1-queue-定义配置项介绍"></span>
#### Introduction to queue configuration items


* On the cluster details page, click **Service List\>YARN\>Service Parameters**, and on the Service Parameters page, search for `capacity-scheduler.xml`.

* The yarn.scheduler.capacity.root.queues parameter is used to define how many Queues exist under the Capacity Scheduler.

> The Queue design in YARN can be a tree structure. Therefore, the standard way to write a Queue is to use dot notation starting from root, such as: root.xxx.xxx


* The yarn.scheduler.capacity..capacity parameter sets the percentage of node resources within the DEFAULT partition that the Queue can access. The sum of the DEFAULT capacities of all direct child items under each parent must equal 100.


<span id="_3-2-2-添加queue"></span>
#### Add queue

Method 1: You can add a queue by modifying the service parameters


* **Service List\>YARN\>Service Parameters**, on the Service Parameters page, click **capacity\-scheduler.xml**

* Add custom parameters yarn.scheduler.capacity.root.queues and yarn.scheduler.capacity..capacity to create a queue


Method 2:

On **Service List\>YARN\>Queue Management,**  click the [YARN queue management](https://docs.byteplus.com/docs/E-MapReduce/109542) button on the right to add a new queue.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08ec59ae962523f3fd538ba5f79c0fdd.png) </span>

After the queue is added successfully, go to **Access Link\>YARN ResourceManager UI**, click the **Scheduler** menu on the left, expand the collapse button in the **Application Queues** panel, and check whether the Queue has been created successfully and whether the capacity allocation is correct.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe0d381bb04e6e0ccc26209d0bb4b7e7.png) </span>

You can see that the relevant queues have already been created in the **DEFAULT** partition. Continue to expand **root.analysis** or **root.warehouse** to check whether the specific capacity allocation is correct. Check that the capacity ratio of **root.warehouse** matches that of the created queue.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7937df317bc7c53123ed19ed705b84c.png) </span>

<span id="_3-3-queue-的最佳实践"></span>
### Queue best practices

The Queue mechanism in YARN is very flexible, and there is no fixed industry standard for how to divide Queues. Considering that its design is a "tree structure", it has certain similarities with the organizational structure of typical enterprises. The recommended practice is to divide queues according to the organizational structure (or similar teams or functions).

For example, this applies to load scenarios such as offline ETL. Many teams are typically involved with this type of workload, for example: data warehouse, business teams, data analytics teams, and machine learning teams (intelligent marketing, intelligent risk control, data mining, and more). It is also possible to further subdivide each Queue into sub\-Queues to accommodate organizational or team relationships, thereby enabling tenant\-level resource management capabilities.

In daily use cases, it is recommended to reserve some buffer resources for the default queue, which can be used for emergencies and fallback after mismatches or omissions.

It is recommended that queues remain sufficiently flat; in most cases, one or two layers are enough (because configuring capacity\-scheduler.xml is very complicated and prone to calculation errors). In some scenarios, you can use XXX_core queue and xxx_elastic queue. The core queue is considered a guaranteed queue and is not elastic.

<span id="_4-queue与node-label结合实现灵活的资源管理"></span>
## Flexible resource management achieved by combining Queue and Node Label

The creation methods and basic functions of Node Label and Queue have already been introduced above. Flexible resource management achieved by combining Queue and Node Label is mainly implemented through Capacity Scheduler.

<span id="_4-1-配置介绍"></span>
### Configuration introduction

The following parameters in the capacity\-scheduler.xml file are related to this:


* yarn.scheduler.capacity..accessible\-node\-labels


Specifies the labels that each Queue can access, separated by commas. For example, "hbase,storm" means the Queue can access the labels hbase and storm.


* yarn.scheduler.capacity..accessible\-node\-labels..capacity


Sets the percentage of node resources within the partition that the Queue can access. The total capacity of all direct child queues under each parent must equal 100. By default, the value is 0.


* yarn.scheduler.capacity..accessible\-node\-labels..maximum\-capacity


Similar to yarn.scheduler.capacity..maximum\-capacity, it is used to configure the maximum capacity for each queue label. The default value is 100.


* yarn.scheduler.capacity..default\-node\-label\-expression


Similar to a value like "hbase", this means: if an application submits a resource request to the queue without specifying a node label, "hbase" will be used as the default node label expression. By default, this value is empty, so the application will obtain containers from unlabeled nodes.

<span id="_4-2-配置示范与演练"></span>
### Configuration demonstration and practice

Take two existing node labels and two queues as an example for actual configuration and practice.

The node labels are "batch" and "streaming" respectively. The workloads for batch and stream processing must be physically isolated to prevent mutual interference.

The queues are "warehouse" and "analysis". The data warehouse and data analytics teams each require a certain proportion of resources on YARN.

Business operation scenario:


* The data warehouse team (queue: warehouse) needs to use 70% of the offline resources (node label: batch) and 80% of the stream processing resources (node label: streaming).

* The data analytics team (queue: analysis) needs to use 30% of the offline resources (node label: batch) and 20% of the stream processing resources (node label: streaming).


Go to **Service List\>YARN\>Service Parameters**, and on the service parameters page, click **capacity\-scheduler.xml**

Configure parameters in the file using XML format to meet the above requirements. The relevant configuration is as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For a child queue to obtain the resource capacity of a node label, its parent queue must first have the resource capacity for that label. It is recommended that the parent queue have 100% resource capacity allocation for these labels.</div>


```xml
<property>
    <name>yarn.scheduler.capacity.root.accessible-node-labels.batch.capacity</name>
    <value>100</value>
</property>
<property>
    <name>yarn.scheduler.capacity.root.accessible-node-labels.streaming.capacity</name>
    <value>100</value>
</property>
```


Configure both queues to access these two Node Labels:

```xml
<property>
    <name>yarn.scheduler.capacity.root.analysis.accessible-node-labels</name>
    <value>batch,streaming</value>
</property>
<property>
    <name>yarn.scheduler.capacity.root.warehouse.accessible-node-labels</name>
    <value>batch,streaming</value>
</property>
```


Allocate capacity, starting with the data warehouse team:

```xml
<property>
    <name>yarn.scheduler.capacity.root.warehouse.accessible-node-labels.batch.capacity</name>
    <value>70</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.warehouse.accessible-node-labels.batch.maximum-capacity</name>
    <value>100</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.warehouse.default-node-label-expression</name>
    <value>batch</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.warehouse.accessible-node-labels.batch.state</name>
    <value>RUNNING</value>
  </property>

  <property>
    <name>yarn.scheduler.capacity.root.warehouse.accessible-node-labels.streaming.capacity</name>
    <value>80</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.warehouse.accessible-node-labels.streaming.maximum-capacity</name>
    <value>100</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.warehouse.accessible-node-labels.streaming.state</name>
    <value>RUNNING</value>
  </property>
```


Then the data analytics team:

```xml
<property>
    <name>yarn.scheduler.capacity.root.analysis.accessible-node-labels.batch.capacity</name>
    <value>30</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.analysis.accessible-node-labels.batch.maximum-capacity</name>
    <value>100</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.analysis.accessible-node-labels.batch.state</name>
    <value>RUNNING</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.analysis.accessible-node-labels.streaming.capacity</name>
    <value>20</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.analysis.accessible-node-labels.streaming.maximum-capacity</name>
    <value>100</value>
  </property>
  <property>
    <name>yarn.scheduler.capacity.root.analysis.accessible-node-labels.streaming.state</name>
    <value>RUNNING</value>
  </property>
```


Basic principle: When `yarn.scheduler.capacity.root.accessible-node-labels.<label>.capacity` is set to greater than 0, the rule is the same as `yarn.scheduler.capacity.<queue-path>.capacity`, requiring the sum of the same partition capacity of direct child queues to be 100.

<span id="_5-yarn-调度验证"></span>
## YARN scheduling verification

Verify the correctness of YARN scheduling by specifying Node Label and queue parameters when YARN schedules Spark APPs.

The Spark task can specify the Node Label by setting the following parameters when submitting:


* spark.yarn.am.nodeLabelExpression

* spark.yarn.executor.nodeLabelExpression


Set the Queue by specifying the `queue` parameter. The job submission command is as follows:

```shell
./bin/spark-submit --class org.apache.spark.examples.SparkPi --master yarn --deploy-mode cluster --driver-memory 1g --executor-memory 2g --conf spark.yarn.am.nodeLabelExpression=batch --conf spark.yarn.executor.nodeLabelExpression=batch --queue=warehouse examples/jars/spark-examples_2.12-3.3.3.jar 10
```


After submitting the job, check the details on **Access Link\>YARN ResourceManager UI**. You can see that the job is scheduled and executed as expected.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee1d80e6d1228f305f21b0d083dd684c.png) </span>

<span id="结论"></span>
## Conclusion

By properly using YARN Node Label and Queue, resource allocation flexibility and efficiency can be improved, better meeting business requirements. In practical applications, reasonable planning and adjustment can be made based on business characteristics and cluster environment to achieve optimal resource utilization.
