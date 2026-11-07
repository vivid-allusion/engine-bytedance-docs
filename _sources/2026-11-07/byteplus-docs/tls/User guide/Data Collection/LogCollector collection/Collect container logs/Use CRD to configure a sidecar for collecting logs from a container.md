---
title: "Use CRD to configure a sidecar for collecting logs from a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/collect_logs_sidecar_crd"
---

When you collect text logs from containers using a sidecar, you can use LogCollector custom resource definition (CRD) to create collection rules. This topic describes how to use a CRD to create a log collection rule for a sidecar.

<span id="背景信息"></span>
## Background

Torch Log Service (TLS) allows you to collect container logs using a sidecar and create collection rules through LogCollector CRD.


* The method of using LogCollector CRD to create collection rules is simple and convenient. However, it requires cost in tool learning. Hence, it is suitable for advanced users who are familiar with Kubernetes and CRDs. For more information on how CRD\-based collection works, refer to [How LogCollector CRD works](https://docs.byteplus.com/docs/tls/how_logcollector_crd_works).

* When you use a sidecar, you can: 1. collect text logs from your container; 2. use all the features supported by LogCollector deployed on physical machines; 3. use various collection modes such as single\-line mode, multi\-line mode, delimiter\-based mode, JSON mode, and full regex\-based mode. Besides the default reserved fields in each collection mode, TLS adds the following reserved fields to container logs collected by LogCollector and creates indexes for them by default.


Reserved fields for container text logs:


|Reserved Field |Description |
|---|---|
|`__image_name__` |Name of an image. |
|`__container_name__` |Name of a container. |
|`__container_ip__` |IP address of a container or Pod. |
|`__pod_name__` |Pod name. |
|`__pod_uid__` |Unique identifier of a Pod. |
|`__namespace__` |Namespace to which a Pod belongs. |


<span id="前提条件"></span>
## Before you begin


* Install LogCollector in a Kubernetes cluster. For more information on the procedure, refer to [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar).

* Install LogCollector CRD in the Kubernetes cluster. For more information on the procedure, refer to [Install LogCollector CRD](https://docs.byteplus.com/docs/tls/install_logCollector_crd).


<span id="限制说明"></span>
## Limits


* The Sidecar mode does not allow you to collect standard output and standard errors from business containers.

* When you collect text logs from a business container using the sidecar mode, collect the logs from the log directory shared by the LogCollector container and the business container. Pay attention to the following:

   * The business container writes logs to the shared directory, and LogCollector periodically scans the log files in the shared directory to collect logs. Therefore, make sure the collection path configured in the console is the path of the log files from the perspective of the LogCollector container.

   * We recommend that you use emptyDir to mount the collection path. For more information on mounting methods, refer to "Deploying LogCollector using a sidecar".

   * This mode can collect data through symbolic links. This can be achieved if the LogCollector container can access the business\-container log files where the symbolic links point.

* If the Pod to which the LogCollector container and the business container belong stops, the LogCollector container stops. Then, the LogCollector container stops collecting logs from the business container. In this case, If latency exists when LogCollector collects logs from the business container, some logs generated before the collection stops may be lost.

* To get container metadata, rely on the environment variables configured in the LogCollector container. LogCollector reads the environment variable LOG_COLLECTOR_ENV_TAGS, splits it into multiple environment variable keys with vertical bars ( | ), reads the values of the keys, and carries the key\-value pairs in logs. Therefore, set the required container metadata in the LogCollector container. Note that only the following metadata can start or end with double underscores ( __ ): `__namespace__`, `__node_ip__`, `__node_name__`, `__pod_ip__`, and `__pod_name__`. If the other metadata starts or ends with double underscores ( __ ), it is ignored during collection.


<span id="088260bf"></span>
## Create LogCollector collection rules

LogCollector CRD uses a YAML file to define and deliver a LogCollector collection rule. After you create and apply this file, TLS automatically creates a LogCollector CR based on the file configuration. The CR corresponds to a LogCollector collection rule and is displayed in the TLS console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Multiple LogCollector CRs with the same projectName, topicName, and RuleName values are considered as the same collection rule. Only the collection rule specified by the CR applied most recently among these CRs takes effect. Make sure that no CRs with the same projectName, topicName, and RuleName values exist. This ensures the desired collection rule takes effect as expected.</div>


To create a LogCollector collection rule:


1. Log on to the Kubernetes cluster where LogCollector CRD is installed.

2. Create a YAML file to specify a collection rule.

   Customize the YAML file name according to your business requirements. This topic uses `access.yaml` as an example.

   ```Bash
   vim access.yaml
   ```
   

3. Edit the YAML file and type the following content into the file.

   ```YAML
   apiVersion: logging.vke.volcengine.com/v1alpha1 # Keep the default setting.
   kind: CollectRule                               # Keep the default setting.
   metadata:
     name: collectrule-sample                      # Name of the LogCollector CR. The name is unique in the current Kubernetes cluster.
   spec:
     projectName: project-name-sample              # Name of the project. If the project does not exist, the system automatically creates a project.
     topicName: topic-name-sample                  # Name of the topic. If the topic does not exist, the system automatically creates a topic.
     lifeCycle: 30                                 # (Optional) Log storage duration. The value takes effect when the system creates a topic.
     shardCount: 2                                 # (Optional) Number of shards. The value takes effect when the system creates a topic.
     hostGroupNames:                               # List of host groups associated with the collection rule.
       - host-group-name-sample1                   # Host group name 1.
       - host-group-name-sample2                   # Host group name 2.
     rule:                                         # Detailed definition of the LogCollector collection rule. For more information, refer to the Sample collection rules section of this topic.
       RuleName: test
       Paths:
         - "/data/nginx/log/*/*/*.log"
       ......
   ```
   

   Customize the parameters in the metadata and spec sections according to your business requirements. The following table describes these parameters.

   
   |**Parameter** |**Data Type** |**Required** |**Description** |
   |---|---|---|---|
   |name |String |Yes |Name of the LogCollector CR. The name is unique in the current Kubernetes cluster. We recommend that you set it to the value of RuleName specified in the rule section for easy identification. |
   |projectName |String |Yes |Name of the project. If the specified project does not exist, the system automatically creates a project. |
   |topicName |String |Yes |Name of the topic. If the specified topic does not exist, the system automatically creates a topic. |
   |hostGroupNames |Array of String |Yes |List of names of host groups associated with the collection rule. If the specified names do not exist, the system automatically creates a host group of the host label type, and the corresponding host label is the host group name. |
   |rule |Object |Yes |For more information on the detailed definition of LogCollector collection rules, supported parameters, and parameter descriptionrefer to [CreateRule](https://docs.byteplus.com/docs/tls/api-createrule). TopicID is not required. The topic associated with the collection rule is determined by the topicName parameter. For more information on the configuration for rule in common scenarios, refer to the **Sample collection rules** section of this topic.<br><br><br>* If the value specified for RuleName does not exist, TLS automatically creates this collection rule. If the value already exists, TLS updates the corresponding collection rule.<br><br>* The specified collection rule is automatically associated with a specified host group. |
   |lifeCycle |Integer |No |The storage duration of logs in a topic specified when the system creates the topic. Expired logs are automatically cleared. Unit: days. Default value: 30. Valid values: 1–3650. The value 3650 means that log data is permanently stored. |
   |shardCount |Integer |No |The number of shards specified when the system creates the topic. Valid values: 1\-10. By default, 1 shard is created. Each shard supports a write capability of 5 MiB/s and 500 operations/s, and a read capability of 20 MiB/s and 100 operations/s. Set an appropriate number of shards when you create a topic. The number of shards cannot be modified after you create its topic. |
   |autoSplit |Boolean |No |Whether to enable the automatic sharding feature when the system creates a topic. It is enabled by default.<br><br><br>* true: TLS performs automatic sharding when the capabilities of existing shards cannot meet the requirements of the volume of written data for five consecutive minutes. This helps meet the business requirements. Note that the number of shards after automatic sharding cannot exceed the upper limit of the feature. New shards generated within the recent 15 minutes after automatic sharding cannot be automatically split.<br><br>* false: The automatic sharding feature is disabled. |
   |maxSplitShard |Integer |No |The upper limit of shards specified when the system creates a topic. Specify the maximum number of shards used after automatic sharding for this parameter. Default value: 10. Valid values: 1–10. |
   |topic |Object |No |When creating a log topic, refer to [CreateTopic](https://docs.byteplus.com/docs/tls/api-createtopic) for detailed definitions of the log topic, supported configuration parameters, and detailed descriptions of the parameters. There is no need to configure `TopicID` and `ProjectId`; the log project to which the log topic belongs is determined by the `projectName` parameter. If the log topic name specified through the `topicName` parameter does not exist, TLS will automatically create the log topic. If the specified log topic name already exists, the log topic will not be updated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>lifeCycle/shardCount/autoSplit/maxSplitShard</code> is specified, and <code>Ttl/ShardCount/AutoSplit/MaxSplitShard</code> is also specified, then the configuration of <code>lifeCycle/shardCount/autoSplit/maxSplitShard</code> takes precedence.</div><br> |
   |index |Object |No |When creating a log topic, refer to [CreateIndex](https://docs.byteplus.com/docs/tls/api-createindex) for detailed definitions of index configurations, supported configuration parameters, and detailed descriptions of the parameters. There is no need to configure `TopicID`; the log topic to which the index belongs is determined by the `topicName` parameter. If the index configuration for the specified log topic does not exist, TLS will automatically create the index configuration. If the index configuration for the specified log topic already exists, it will not be updated. |
   

4. Run the following command to apply the configuration in the`access.yaml` file:

   Replace `access.yaml` with the actual file name as needed.

   ```Bash
   kubectl apply -f access.yaml
   ```
   


<span id="1330e9fd"></span>
## Related operations

<span id="3de0636f"></span>
### Modify collection rules

We recommend that you adjust a collection rule by modifying the YAML file corresponding to your LogCollector CR. After you adjust a collection rule, TLS automatically updates the corresponding LogCollector CR and refreshes the LogCollector collection rule displayed in the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you directly adjust a collection rule in the console, inconsistency between the collection rule information on the LogCollector CR and in the console may exist.</div>


* <div data-tips="true" data-tips-type="tip">Do not modify the values of projectName, topicName, or RuleName in a collection rule. Otherwise, TLS automatically creates a collection rule and assigns a new rule name, project, or topic to it.</div>



The following content describes the recommended procedure. Here, the YAML file named `access.yaml` is taken as an example.


1. Log on to the Kubernetes cluster where LogCollector CRD is installed.

2. Run the following command to edit the specified YAML file and modify the collection rule:

   ```Bash
   vim access.yaml
   ```
   

3. Run the following command to apply the file settings:

   ```Bash
   kubectl apply -f access.yaml
   ```
   


<span id="f8ff9c72"></span>
### Delete collection rules

To delete a LogCollector collection rule, run the following command to delete the corresponding LogCollector CR resource: Replace `*logcollector_cr_name*` with the name of the specified LogCollector CR, such as collectrule\-sample.

```Bash
kubectl delete collectrule logcollector_cr_name
```


<span id="5060f453"></span>
### View collection rule information

After you create and apply a LogCollector collection rule, you can view detailed information on the collection rule through the console or CRD.


* Console: View the corresponding collection rule in the TLS console by project and collection rule name.

* CRD: View a list of LogCollector CRs in the Kubernetes cluster and query the information on the CR by name. Perform the following steps:

   1. Log on to the Kubernetes cluster.

   2. Run the following command to view a list of LogCollector CRs in the current Kubernetes cluster and get the name of the CR you want to view:

      ```Bash
      kubectl get collectrule
      ```
      

      A response similar to the following example is returned.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77ece2e7bf125157bbc8a683e680f83e.png) </span>

   3. Run the following command to view the detailed definition of the LogCollector CR in the spec field of the response. Replace `*logcollector_cr_name*` with the name of the specified LogCollector CR, such as collectrule\-sample.

      ```Bash
      kubectl get collectrule logcollector_cr_name -o yaml
      ```
      


<span id="29c4f1f7"></span>
### View LogCollector CR status

Assume that: 1. You create a LogCollector collection rule through CRD. 2. The rule does not appear in the console or fails to be updated synchronously after you modify the CR. This means the system fails to create or modify the collection rule. To determine the cause of the failure, view the status and description of the LogCollector CR in the Kubernetes cluster.

Run the following command to view the status of the LogCollector CR. Replace `*logcollector_cr_name*` with the name of the LogCollector CR, such as collectrule1.

```Bash
kubectl get collectrule logcollector_cr_name -o yaml
```


The **status** field in the execution result indicates the status of the LogCollector CR. where:


|Field ||Description |
|---|---|---|
|projectId ||The project ID. |
|topicId ||The topic ID. |
|hostGroupIds ||The list of host group IDs. |
|ruleId ||The collection rule ID. |
|status |code |Operation status code of the LogCollector CR.<br><br><br>* 200: The LogCollector collection rule is successfully created or modified.<br><br>* Non\-200 status code: The system failed to create or modify the LogCollector collection rule. |
||message |When the returned code is not 200, this field returns a specific error message. You can troubleshoot the issue based on the message field. |


A response similar to either of the following examples is returned:


* Response that indicates a LogCollector collection rule is successfully created or modified

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10711f1efa3845959e9f0cf7ad84d9a3~tplv-goo7wpa0wc-image.image) </span>

* Response that indicates the system failed to create or modify a LogCollector collection rule

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f630a75cf881f98202c8c3d53aff6bbd.png) </span>


<span id="创建-logcollector-采集配置"></span>
## Sample collection rules

Sample collection rules in common scenarios are as follows. For more information on the parameters in the metadata and spec sections, refer to [Create LogCollector collection rules](https://docs.byteplus.com/docs/tls/collect_logs_sidecar_crd#088260bf).

<span id="分隔符模式采集容器文本日志"></span>
### Collect text logs from containers in delimiter\-based mode

The following example is used to collect logs in the `access.log` file under `/var/logs/app` from business containers. In this example, the delimiter\-based mode is used.

Sample LogCollector collection rule:

```YAML
apiVersion: logging.vke.volcengine.com/v1alpha1
kind: CollectRule
metadata:
  name: collectrule-sample
spec:
  projectName: project-name-sample
  topicName: topic-name-sample
  lifeCycle: 30
  shardCount: 2
  hostGroupNames:
    - host-group-name-sample1
    - host-group-name-sample2
  rule:
    RuleName: test
    LogType: delimiter_log
    LogSample: 2022-01-01 error "this is a error message"
    Paths:
      - /var/logs/app/access.log
    ExtractRule:
      Delimiter: ' '
      Quote: '"'
      Keys:
        - time
        - level
        - message
      UnMatchUpLoadSwitch: true
      UnMatchLogKey: LogParseFailed
```


<span id="json-模式采集容器文本日志"></span>
### Collect text logs from containers in JSON mode

The following example is used to collect logs in the `access.log` file under `/var/logs/app` from business containers. In this example, the JSON mode is used.

Sample LogCollector collection rule:

```YAML
apiVersion: logging.vke.volcengine.com/v1alpha1
kind: CollectRule
metadata:
  name: collectrule-sample
spec:
  projectName: project-name-sample
  topicName: topic-name-sample
  lifeCycle: 30
  shardCount: 2
  hostGroupNames:
    - host-group-name-sample1
    - host-group-name-sample2
  rule:
    RuleName: test
    LogType: json_log
    Paths:
      - /var/logs/app/access.log
    ExtractRule:
      UnMatchUpLoadSwitch: true
      UnMatchLogKey: LogParseFailed
```


<span id="后续步骤"></span>
## Follow\-ups

After a collection rule is created, LogCollector starts to listen for log files from containers and collect logs accordingly. Besides, the log data is saved to the specified topic.

The index feature is disabled by default. To query and analyze the collected log data in the console, enable the index feature for your topics and configure your index.
