---
title: "Use CRD to configure a DaemonSet for collecting logs from a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/collecte_logs_daemonSet_CRD"
---

When you collect text logs or standard output from containers using a DaemonSet, you can use LogCollector custom resource definition (CRD) to create a collection rule. This topic describes how to use a CRD to create a collection rule for a DaemonSet.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Torch Log Service (TLS) allows you to collect container logs using a DaemonSet and create collection rules through LogCollector CRD.


* A DaemonSet allows you to collect standard output and text logs from containers. Additionally, it features low resource usage and flexible configurations.

* The method of using LogCollector CRD to create collection rules is simple and convenient. However, it requires cost in tool learning. Hence, it is suitable for advanced users who are familiar with Kubernetes and CRDs. For more information on how CRD\-based collection works, refer to [How LogCollector CRD works](https://docs.byteplus.com/docs/tls/how_logcollector_crd_works).


LogCollector allows you to collect logs from containers in various collection modes, such as single\-line mode and multi\-line mode. Besides the default reserved fields in these collection modes, TLS adds the following reserved fields to container logs collected by LogCollector and creates indexes for them by default.

Reserved fields for container text logs:


|Reserved Field |Description |
|---|---|
|`__image_name__` |Name of an image. |
|`__container_name__` |Name of a container. |
|`__container_ip__` |IP address of a container or Pod. |
|`__pod_name__` |Pod name. |
|`__pod_uid__` |Unique identifier of a Pod. |
|`__namespace__` |Namespace to which a Pod belongs. |


Reserved fields for container standard output:


|Reserved Field |Description |
|---|---|
|`__container_source__` |Type of a data source. Valid values: stdout and stderr. |
|`__image_name__` |Name of an image. |
|`__container_name__` |Name of a container. |
|`__container_ip__` |IP address of a container or Pod. |
|`__pod_name__` |Pod name. |
|`__pod_uid__` |Unique identifier of a Pod. |
|`__namespace__` |Namespace to which a Pod belongs. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Install LogCollector in a Kubernetes cluster. For more information on the procedure, refer to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet).

* Install LogCollector CRD in the Kubernetes cluster. For more information on the procedure, refer to [Install LogCollector CRD](https://docs.byteplus.com/docs/tls/install_logCollector_crd).


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limits


* When you collect standard output from containers, pay attention to the following:

   * The Docker container engine only supports JSON log drivers.

   * If a container matches more than one collection rule, only the latest collection rule takes effect on that container.

* When you collect log files from containers, pay attention to the following:

   * Currently, the collection paths of log files within containers support three mounting methods: no mounting, emptyDir mounting, and hostPath mounting.

   * You cannot set a collection path to a symbolic link because LogCollector cannot access symbolic links to log files within containers. Configure a collection path according to the actual path of a log file within a container.

* After a container stops, LogCollector receives the stop event of the container, then stops collecting logs from the container. If latency exists when LogCollector collects logs from the container, some logs generated before the container stops may not be collected.

* The container engines supported by LogCollector include Docker and Containerd. The limits on access paths corresponding to the preceding container engine types are as follows:

   * Docker: LogCollector accesses the Docker container engine through `/run/docker.sock` of the host. Make sure that this path exists and that LogCollector has the access permissions.

   * Containerd: LogCollector accesses the Containerd container engine through `/run/containerd/containerd.sock` of the host. Make sure that this path exists and that LogCollector has the access permissions.


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
   |rule |Object |Yes |For more information on the detailed definition of LogCollector collection rules, supported parameters, and parameter description, refer to [CreateRule](https://docs.byteplus.com/docs/tls/api-createrule). TopicID is not required. The topic associated with the collection rule is determined by the topicName parameter. For more information on the configuration for rule in common scenarios, refer to the **Sample collection rules** section of this topic.<br><br><br>* If the value specified for RuleName does not exist, TLS automatically creates this collection rule. If the value already exists, TLS updates the corresponding collection rule.<br><br>* The specified collection rule is automatically associated with a specified host group. |
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
### Viewing collection rule information

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


* Response that indicates a LogCollector collection rule is successfully created or modified:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/258ae281f549472da579f2d8bab35301~tplv-goo7wpa0wc-image.image) </span>

* Response that indicates the system failed to create or modify a LogCollector collection rule

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f630a75cf881f98202c8c3d53aff6bbd.png) </span>


<span id=".6YWN572u56S65L6L"></span>
## Sample collection rules

Sample collection rules in common scenarios are as follows. For more information on the parameters in the metadata and spec sections, refer to [Create LogCollector collection rules](https://docs.byteplus.com/docs/tls/collecte_logs_daemonSet_CRD#088260bf).

<span id=".6YeH6ZuG5oyH5a6a5bel5L2c6LSf6L2955qE5a655Zmo5qCH5YeG6L6T5Ye6"></span>
### Collecting standard output from containers of a specified workload

The following example is used to collect standard output and standard errors from specific containers. The containers that meet the following requirements are within the collection scope: 1. The workload type is Deployment. 2. The workload name is test\-nginx. 3. The Pod labels include label\-test\-key1:label\-test\-key1 or label\-test\-key2:label\-test\-key2.

Sample LogCollector collection rule:

```yaml
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
    LogType: minimalist_log
    ExtractRule:
      UnMatchUpLoadSwitch: true
      UnMatchLogKey: LogParseFailed
    InputType: 1
    ContainerRule:
      Stream: all
      KubernetesRule:
        WorkloadType: Deployment
        WorkloadNameRegex: test-nginx
        IncludePodLabelRegex:
          label-test-key1: label-test-key1
          label-test-key2: label-test-key2
```


<span id=".6YeH6ZuG5oyH5a6aLW5hbWVzcGFjZS3nmoTlrrnlmajmoIflh4bovpPlh7o="></span>
### Collecting standard output from containers in a specified namespace

The following example is used to collect standard output and standard errors from specific containers. The containers within the collection scope meet the following requirements: 1. The namespace name is namespace\-test\-name. 2. The Pod name is pod\-test\-name. 3. The container name is container\-test\-name.

Sample LogCollector collection rule:

```yaml
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
    LogType: minimalist_log
    ExtractRule:
      UnMatchUpLoadSwitch: true
      UnMatchLogKey: LogParseFailed
    InputType: 1
    ContainerRule:
      Stream: all
      ContainerNameRegex: container-test-name
      KubernetesRule:
        NamespaceNameRegex: namespace-test-name
        PodNameRegex: pod-test-name
```


<span id=".5YiG6ZqU56ym5qih5byP6YeH6ZuG5a655Zmo5paH5pys5pel5b-X"></span>
### Collecting text logs from containers in delimiter\-based mode

The following example is used to collect logs in the `access.log`file under `/var/logs/app` from specific containers. In this example, the delimiter\-based mode is used. The containers within the collection scope meet the following requirements: 1. The namespace name is namespace\-test\-name. 2. The Pod name is pod\-test\-name. 3. The container name is container\-test\-name.

Sample LogCollector collection rule:

```yaml
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
    InputType: 2
    ContainerRule:
      ContainerNameRegex: container-test-name
      KubernetesRule:
        NamespaceNameRegex: namespace-test-name
        PodNameRegex: pod-test-name
```


<span id=".anNvbi3mqKHlvI_ph4fpm4blrrnlmajmlofmnKzml6Xlv5c="></span>
### Collecting text logs from containers in JSON mode

The following example is used to collect logs in the `access.log` file under `/var/logs/app` from specific containers. In this example, the JSON mode is used. Containers within the collection scope meet the following requirements: 1. The namespace name is namespace\-test\-name. 2. The pod name is pod\-test\-name. 3. The container name is container\-test\-name.

Sample LogCollector collection rule:

```yaml
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
    InputType: 2
    ContainerRule:
      ContainerNameRegex: container-test-name
      KubernetesRule:
        NamespaceNameRegex: namespace-test-name
        PodNameRegex: pod-test-name
```


<span id=".5ZCO57ut5q2l6aqk"></span>
## Follow\-ups

After a collection rule is created, LogCollector starts to listen for log files or standard output from containers and collect logs accordingly. Besides, the log data is saved to the specified topic.

The index feature is disabled by default. To query and analyze the collected log data in the console, enable the index feature for your topics and configure your index.
