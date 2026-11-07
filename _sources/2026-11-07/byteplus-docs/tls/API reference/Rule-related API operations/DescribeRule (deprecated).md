---
title: "DescribeRule (deprecated)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describerule"
---

TLS provides a new API [DescribeRuleV2](https://docs.byteplus.com/en/docs/tls/DescribeRuleV2) to view specified collection configuration information.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* This API has a rate limit of 20 requests/second. If exceeded, an ExceedQPSLimit error will be returned.

* The following limitations apply to the information returned by this interface: 

   * The maximum number of machines is 10,000, meaning the total number of HostCounts cannot exceed 10,000.

   * The maximum number of machine groups is 100, meaning the number of HostGroupInfo instances cannot exceed 100.


<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request address: https://{tls\-endpoint}/DescribeRule


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists parameters specific to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|RuleId |String |Yes |`faf6d529-e75e-457f-a23a-9c4203a6dff3xx` |ID of the collection configuration |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

The following table lists only the parameters specific to this API. For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|ProjectId |String |`c7***********` |ID of the project that owns the collection configuration. |
|ProjectName |String |`testname` |Name of the project to which the collection configuration belongs. |
|TopicId |String |`4a**********` |ID of the log topic to which the collection configuration belongs |
|TopicName |String |`testname` |Name of the log topic associated with the collection configuration. |
|RuleInfo |Object of [RuleInfo](https://docs.byteplus.com/en/docs/38/17248#ruleinfo) |`/` |Information about the collection configuration. |
|HostGroupInfos |Array of [HostGroupInfo](https://docs.byteplus.com/en/docs/38/17248#hostgroupinfo) |`/` |Information about the host group bound to the collection configuration. |


<span id="ruleinfo"></span>
### RuleInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Paths |Array of String |`["/data/nginx/log/**/access.log"]` |Collection path list. |
|Pause |Integer |`0` |Status of the collection configuration.<br><br><br>* 0: Running.<br><br>* 1: Paused. |
|RuleId |String |`faf******` |ID of the collection configuration. |
|LogType |String |`delimiter_log` |Collection mode.<br><br><br>* minimalist_log: Single\-line full text mode.<br><br>* json_log: JSON mode.<br><br>* delimiter_log: Separator mode.<br><br>* multiline_log: Multi\-line full text mode.<br><br>* fullregex_log: Complete regular expression mode. |
|TopicId |String |`4a************` |ID of the log topic to which the collection configuration belongs. |
|RuleName |String |`testname` |Name of the collection configuration. |
|InputType |Integer |`0` |Collection type.<br><br><br>* 0: Host log file<br><br>* 1: K8s container standard output<br><br>* 2: Log file inside K8s container |
|LogSample |String |`2018-05-22 15:35:53.850 INFO XXXX` |Log sample. |
|TopicName |String |topictestname |Name of the log topic to which the collection configuration belongs |
|CreateTime |String |`2021-08-18 13:32:23` |Collection configuration creation time. |
|ModifyTime |String |`2021-08-18 13:32:23` |Time of collection configuration modification. |
|ExtractRule |Object of [ExtractRule](https://docs.byteplus.com/en/docs/38/17248#extractrule) |`/` |Extraction rules. |
|ExcludePaths |Array of [ExcludePath](https://docs.byteplus.com/en/docs/38/17248#excludepath) |`/` |Collection denylist. |
|ContainerRule |Object of [ContainerRule](https://docs.byteplus.com/en/docs/38/17248#containerrule) |`/` |Container collection rule. |
|UserDefineRule |Object of [UserDefineRule](https://docs.byteplus.com/en/docs/38/17248#userdefinerule) |`/` |User\-defined collection rules. |
|RuleType |Integer |1 |Type identifier for the collection rule, used to distinguish different rule types. |


<span id="hostgroupinfo"></span>
### HostGroupInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostCount |Integer |`2` |Number of machines. |
|RuleCount |Integer |`1` |Number of bound collection configurations. |
|AutoUpdate |Boolean |`true` |LogCollector installed on the host group server has auto\-upgrade function. You can choose whether to enable it.<br><br><br>* true: TLS checks for upgrades daily during a specified time window. If conditions are met, LogCollector is upgraded automatically with no manual action required.<br><br>* false: (Default) LogCollector will not upgrade automatically. To use a newer version of LogCollector, refer to [LogCollector upgrade](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host). |
|CreateTime |String |`2021-08-18 13:32:23` |The creation time of the host group. |
|ModifyTime |String |`2021-08-18 13:32:23` |Time of host group modification. |
|HostGroupId |String |`0fd**********` |ID of the host group. |
|HostGroupName |String |`testname` |Name of the host group. |
|HostGroupType |String |`IP` |The type of host group.<br><br><br>* IP: Machine IP.<br><br>* Label: Host identification. |
|UpdateEndTime |String |"02:00" |End time of LogCollector automatic upgrade. |
|HostIdentifier |String |`label` |Machine identifier. |
|IamProjectName |String |`default` |The IAM project to which the host group belongs. |
|ServiceLogging |Boolean |`true` |You can choose whether to enable the LogCollector service log.<br><br><br>* true: Enable.<br><br>* false: (Default) Disabled. |
|UpdateStartTime |String |"00:00" |The start time for LogCollector automatic upgrade.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This setting is required only when AutoUpdate is true.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For automatic upgrades, we recommend that you set it during off\-peak business hours. LogCollector may restart during the upgrade, but no logs will be lost.</div><br> |
|AgentLatestVersion |String |"2.3.4" |The latest version number of LogCollector released by TLS. |
|NormalHeartbeatStatusCount |Integer |`1` |Number of machines with normal heartbeat. |
|AbnormalHeartbeatStatusCount |Integer |`1` |Number of machines with abnormal heartbeat. |


<span id="extractrule"></span>
### ExtractRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |`[ "time", "", "level", "msg" ]` |Log field name (Key) list.<br><br><br>* Valid only when LogType is delimiter_log or fullregex_log.<br><br>* Supports configuring up to 100 field names.<br><br>* When LogType is delimiter_log, duplicate field names cannot be configured and all field names cannot be left empty.<br><br>* When LogType is fullregex_log, duplicate field names cannot be configured and field names cannot be left empty. |
|Quote |String |`"` |Quotation marks. Content wrapped by quotation marks will not be separated, but will be parsed as a complete field. Valid only when LogType is set to delimiter_log. |
|TimeKey |String |`request_time` |The field name for the log time field If you use a specific time field in the log as the timestamp, you must fill in both TimeKey and TimeFormat<br><br>TimeKey and TimeFormat must be used together |
|LogRegex |String |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The regular expression that the entire log entry must match.<br><br><br>* Effective only when the log type being collected is fullregex_log.<br><br>* Must be a valid regular expression. |
|TimeZone |String |`GMT+08:00` |Time zone, supports host time zone (default) and custom time zone. Custom time zone supports both GMT and UTC.<br><br><br>* GMT format: GMT+08:00.<br><br>* UTC format: Asia/Shanghai. |
|Delimiter |String |# |Log separator. Valid only when LogType is delimiter_log. |
|BeginRegex |String |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The regular expression to match the first line of the log.<br><br><br>* Applies only when LogType is multiline_log or fullregex_log.<br><br>* Must be a valid regular expression. |
|TimeFormat |String |`%Y-%m-%dT%H:%M:%S,%f` |Time field parsing format. If you use a specified time field in the log as the log timestamp, you must provide both TimeKey and TimeFormat.<br><br><br>* TimeKey and TimeFormat must be used together.<br><br>* See [Time Format](https://docs.byteplus.com/docs/tls/time_format) for instructions on configuring the time format. |
|LogTemplate |Object of [LogTemplate](https://docs.byteplus.com/en/docs/38/17248#logtemplate) |`{ "Type": "Nginx", "Format": "format main '$remote_addr - $remote_user [$time_local] \"$request\" $request_time $request_length $status $body_bytes_sent \"$http_referer\" \"$http_user_agent\"';" }` |Automatically extract log fields using the specified log template. |
|UnMatchLogKey |String |`LogParseFailed` |When uploading logs that failed to be parsed, this is the key name for logs that failed to be parsed.<br><br>UnMatchUpLoadSwitch=true and UnMatchLogKey must be used together. |
|FilterKeyRegex |Array of [FilterKeyRegex](https://docs.byteplus.com/en/docs/38/17248#filterkeyregex) |`/` |Filter rule list.<br><br><br>* When LogType is minimalist_log or multiline_log, you can configure a maximum of one filter rule, and the filter field name key must be **content**.<br><br>* When LogType is delimiter_log, json_log, or fullregex_log, you can configure up to five filter rules, and the filter field name key cannot be duplicated or empty. The regular expression used to match the log content in the filter field must be valid and no longer than 256 characters. |
|TimeExtractRegex |String |`[0-9]{0,2}\/[0-9a-zA-Z]+\/[0-9:,]+` |Regular expression for extracting time, used to extract the time value from the `TimeKey` field and parse it as the corresponding collection time. |
|UnMatchUpLoadSwitch |Boolean |`true` |Whether to upload logs that failed to be parsed. UnMatchUpLoadSwitch=true and UnMatchLogKey must be used together.<br><br><br>* true: Upload logs that failed to be parsed.<br><br>* false: Do not upload logs that failed to be parsed. |
|EnableNanosecond |Boolean |`true` |Enable nanosecond precision time. When enabled, log time will be parsed and reported with nanosecond precision.<br><br><br>* true: Enable nanosecond precision time.<br><br>* false: turn off nanosecond precision time. |
|TimeSample |String |`2006-01-02T15:04:05Z07:00` |Time sample. Used to check whether the provided time parsing format is correct. |


<span id="excludepath"></span>
### ExcludePath


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |`Path` |Type of collection path.<br><br><br>* File: File name.<br><br>* Path: Directory. |
|Value |String |`/accesslog` |Collection path. Must specify as an absolute path.<br><br><br>* When Type is Path, Value represents a directory.<br><br>* When Type is File, Value represents a file name. |


<span id="containerrule"></span>
### ContainerRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|EnvTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to set environment label as log tag and add it to raw log data. If enabled, TLS will add related container environment variable fields to the logs. If you set multiple key\-value pairs, it means you add multiple fields. For example, set Key as source and Value as data_source. If the container includes the environment variable `source=DC`, a new field `__tag__data_source__: DC` will be added to the log. |
|Stream |String |`all` |Collection details.<br><br><br>* stdout: Collects standard output from the container.<br><br>* stderr: Collects standard error from the container.<br><br>* all: Collects both standard output and standard error from the container. |
|KubernetesRule |Object of [KubernetesRule](https://docs.byteplus.com/en/docs/38/17248#kubernetesrule) |`{ "NamespaceNameRegex": ".*test.*", "WorkloadType": "Deployment", "WorkloadNameRegex": ".*test.*", "IncludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "ExcludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "PodNameRegex": ".*test.*", "LabelTag": { "Key1": "Value1", "Key2": "Value2" } }` |Kubernetes container collection rules. |
|ContainerNameRegex |String |`.*test.*` |Name of container to collect If the container name is not specified, all containers in the host group will be collected. Supports regex matching. For example, set the container name to `^(container-test)$` to collect all containers named `container-test`. |
|ExcludeContainerEnvRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The container environment variable denylist specifies which containers are excluded from data collection. If the denylist is disabled, all containers will be collected. If you enable the container environment variable denylist, key is required, while value is optional.<br><br><br>* If value is empty, all containers whose environment variables contain the key will be excluded from collection.<br><br>* If value is not empty, only containers whose environment variables match both the key and value are excluded. Value supports regular expression matching. For example, if you set key to module and value to `^(tcp\|udp)$`, containers with environment variables module:`tcp` or module:`udp` are excluded from collection.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`. Any container whose environment variables match any of the pairs will be excluded from collection.<br><br>* When enabling the container environment variable denylist, keys must not be duplicated. |
|IncludeContainerEnvRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Specify which containers to collect by using the container environment variable allowlist. If the allowlist is not enabled, all containers will be collected. To enable the container environment variable allowlist, enter key\-value pairs. Key is required; value is optional.<br><br><br>* If value is empty, all containers containing the key in their environment variables will be collected.<br><br>* If value is not empty, only containers with the key in their environment variables and matching the value will be collected. Value supports regular expression matching. For example, set key to module and value to `^(tcp\|udp)$`. Only containers with environment variables module:`tcp` and module:`udp` will be collected.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`: a container will be included if it matches any Key\-Value pair.<br><br>* When the container environment variable allowlist is enabled, keys can not be duplicated. |
|ExcludeContainerLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The container label denylist is used to specify which containers should not be collected. If the denylist is disabled, all containers are collected. If the container label denylist is enabled, the key field is required and the value field is optional.<br><br><br>* If value is empty, containers with the specified key in their label will not be collected.<br><br>* If value is not empty, only containers whose labels match both the key and value are excluded from collection. Values support regular expression matching. For example, setting the key to app and the value to `^(test1\|test2)$` means containers labeled app:test1 or app:test2 will not be collected.<br><br>* The logic between multiple key\-value pairs is logical `OR`. That is to say, any container whose label matches any of the key\-value pairs will be excluded from collection.<br><br>* When the container label denylist is enabled, the key fields must not be duplicated. |
|IncludeContainerLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |You can specify which containers to collect using container label allowlists. When the allowlist is not enabled, all containers will be collected. When enabling the container label allowlist, you need to fill in key\-value pairs. Key is required; value is optional.<br><br><br>* Value is empty: Collect all containers that contain the key in their container label.<br><br>* Value is not empty: Only collect containers whose label contains the key and whose value matches the value. Value supports regular expression matching. For example, set the key to app and the value to `^(test1\|test2)$`. This means only the containers with the container label app:test1 or app:test2 will be collected.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`. That is to say, any container Label that matches any Key\-Value pair will be included in the collection.<br><br>* When enabling the container Label allowlist, keys can not be duplicated. |


<span id="userdefinerule"></span>
### UserDefineRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Fields |JSON Map |`{"ClusterID":"dabaad5f-7a10-4771-b3ea-d821f73e****"}` |Add constant fields to logs. Constant fields must follow these restrictions:<br><br><br>* Supports uploading up to 5 constant fields.<br><br>* Field names (keys) must be unique and non\-empty. The length must be between 1 and 128 characters, including English letters, digits, and special characters (`-_./`), and can not start with an underscore.<br><br>* Field values can not be empty and can be up to 512 KiB in size. |
|Plugin |Object of [Plugin](https://docs.byteplus.com/en/docs/38/17248#plugin) |`{"processors":[{"json":{"field":"__content__","trim_keys":{"mode":"all","chars":"#"},"trim_values":{"mode":"all","chars":"#"},"allow_overwrite_keys":true,"allow_empty_values":true}` |Plugin configuration for LogCollector After enabling plugin configuration, you can add one or more LogCollector processor plugins to parse logs with complex or irregular structures. |
|Advanced |Object of [Advanced](https://docs.byteplus.com/en/docs/38/17248#advanced) |`{ "CloseInactive": 10 }` |LogCollector extended configuration. |
|RawLogKey |String |raw |Original log field name.<br><br>Effective only when EnableRawLog is set to true. RawLogKey defaults to `__raw__`, meaning the original log data will be encapsulated in the `__raw__` field and uploaded to TLS along with the parsed log data. |
|TailFiles |Boolean |`true` |LogCollector collection policy specifies whether LogCollector collects incremental logs or full logs. The default value is false, meaning full log collection.<br><br><br>* true: Incremental collection. LogCollector collects only new content added to the file during log collection. When new logs are written to log files within the monitor scope, it triggers LogCollector collection.<br><br>   * For first\-time collected log files, LogCollector uses your specified incremental threshold `TailSizeKb` to automatically locate the collection position.<br><br>      * If the new file size does not exceed your specified incremental threshold, the first collection starts from the beginning of the new file.<br><br>      * If the new file size exceeds your specified incremental threshold, the first collection starts at the position where the file ends minus the incremental threshold. That is to say, only incremental logs are collected.<br><br>   * For log files not collected for the first time, LogCollector determines the collection position based on the Checkpoint and continues collecting.<br><br>* false: (Default) Full log collection. LogCollector starts collecting logs from the beginning of each document. In this case, LogCollector will collect historical log data. |
|HostnameKey |String |`hostname` |hostname field name.<br><br>Only required when EnableHostname is set to true. |
|EnableRawLog |Boolean |`true` |Upload original log.<br><br><br>* true: Upload original log.<br><br>* false: (default) Do not upload original log. |
|ShardHashKey |Object of [ShardHashKey](https://docs.byteplus.com/en/docs/38/17248#shardhashkey) |`{ "HashKey": "3C" }` |Rules for routing log shards.<br><br><br>* If this parameter is not set, logs are written using the default load balancing mode. Data packets are stored in any available shard.<br><br>* If this parameter is set, logs are routed to shards using the HashKey mode. TLS writes data to shards containing the specified key value. |
|ParsePathRule |Object of [ParsePathRule](https://docs.byteplus.com/en/docs/38/17248#parsepathrule) |`{ "PathSample": "/data/nginx/log/dabaad5f-7a10/tls/app.log", "Regex": "\\/data\\/nginx\\/log\\/(\\w+)-(\\w+)\\/tls\\/app\\.log", "Keys": ["instance-id", "pod-name"] }` |Parse collection path rules. After setting the rules, fields will be extracted from the collection path using the specified regular expressions in the rules and added as metadata to the log data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is not supported when collecting container standard output.</div><br> |
|EnableHostname |Boolean |`true` |This feature determines whether to upload the hostname field. By default, it is disabled.<br><br><br>* true: Add a field in the original log to record the hostname of the log source. Specify the hostname field name using HostnameKey.<br><br>* false: (default) Do not add the hostname field. |
|HostGroupLabelKey |String |`host_group_label` |The field name used to store host group label information. |
|EnableHostGroupLabel |Boolean |`true` |You can select whether to upload the label information of the host group to TLS. By default, it is enabled.<br><br><br>* true: LogCollector uploads the label information of the host group to the specified field You can specify the field name using the **HostGroupLabelKey** parameter<br><br>* false (default): The label information of the host group is not uploaded |
|TailSizeKb |Integer |`1024` |Backtracking threshold for incremental collection, measured in KiB. When the LogCollector collection strategy is incremental, for the first collection of a log file:<br><br><br>* If the new log file size does not exceed the `TailSizeKb` value, the first collection starts from the beginning of the new log file.<br><br>* If the new log file size exceeds the `TailSizeKb` value, the first collection starts at the position where the end of the new file minus the `TailSizeKb` value. |
|IgnoreOlder |Integer |`7` |Ignore log files not updated for a certain period; the unit is hours. |
|MultiCollectsType |String |`RuleID` |Collect log files multiple times.<br><br><br>* Empty: Use the log file ID (including file inode, device, and checksum of the first N bytes) to uniquely identify the log file.<br><br>* RuleID: Use the collection rule ID and log file ID to uniquely identify the log file.<br><br>* TopicIDRuleName: Use the log topic ID, collection rule name, and log file ID to uniquely identify the log file. |


<span id="logtemplate"></span>
### LogTemplate


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |`Nginx` |Type of log template. The following types are supported:<br><br><br>* Nginx: Log templates for Nginx. |
|Format |String |`log_format main '$remote_addr - $remote_user [$time_local] "$request" $request_time $request_length $status $body_bytes_sent "$http_referer" "$http_user_agent"';` |Log template format. |


<span id="filterkeyregex"></span>
### FilterKeyRegex


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Key |String |`__content__` |Name of the filter field. |
|Regex |String |`.*ERROR.*` |The log content in filtered fields must match the regular expression. |


<span id="kubernetesrule"></span>
### KubernetesRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|LabelTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to add Kubernetes Labels as log tags to the raw log data. If enabled, TLS will add Kubernetes Pod Label related fields to the logs. If you set multiple key\-value pairs, multiple fields are added. For example, set the key to source and the value to data_source. If the Pod includes the label `source=DC`, the log will have a new field `__tag__data_source__: DC`. |
|PodNameRegex |String |`.*test.*` |Pod name is used to specify the target container for collection. If you do not specify the Pod name, all containers are collected. Pod name supports regex matching. For example, if you set the Pod name to `^(http.*)$`, it collects all containers under Pods whose names start with "http". |
|WorkloadType |String |`Deployment` |Specify the container for collection based on workload type. Only one type can be selected. If no type is specified, containers of all types are collected. Supported workload types:<br><br><br>* Deployment: Stateless workload<br><br>* StatefulSet: Stateful workload<br><br>* DaemonSet: Daemon process<br><br>* Job: Task<br><br>* CronJob: Scheduled SQL task |
|AnnotationTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to set Kubernetes Annotation to log tags and add it into the raw log data. If enabled, TLS will add Kubernetes Pod annotation fields to the logs. If you set multiple key\-value pairs, multiple fields are added. If you set the key to "sink" and the value to "data_sink", and the Pod has an annotation `sink=ck`, a new field `__tag__data_sink__: ck` will be added to the log. |
|WorkloadNameRegex |String |`.*test.*` |By configuring the workload name, you can specify the container to collect. If no workload name is specified, all containers are collected. Workload names support regular expression matching. For example, if you set the workload name to `^(http.*)$`, all containers under workloads starting with http will be collected. |
|NamespaceNameRegex |String |`.*test.*` |Name of the Kubernetes namespace to be collected. If no Namespace is specified, all containers will be collected. Namespace names support regular expression matching. For example, setting the Namespace name to `^(tcp\|udp)$` collects all containers under the `tcp` and `udp` namespaces. |
|ExcludePodLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The Pod Label denylist is used to specify which containers should not be collected. If the denylist is disabled, all containers are collected. If you need to set a Pod Label denylist, the key is required, and the value is optional.<br><br><br>* If the value field is empty, all containers with the specified key in the Pod Label will be excluded from collection.<br><br>* If the value field is not empty, only containers with the specified key and a value that matches will be excluded from collection. The value field supports regular expressions. For example, if you set key to module and value to `^(tcp\|udp)$`, containers with module:`tcp` and module:`udp` in the Pod Label will not be collected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship between multiple Key\-Value pairs is <code>OR</code>. That is to say, any Pod Label that matches any Key\-Value pair will be excluded from collection.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling the Pod Label denylist, keys can not be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches any string that starts with "http".</div><br> |
|IncludePodLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The Pod Label allowlist is used to specify the containers to be collected. If the Pod Label allowlist is not enabled, all containers will be collected. If you need to set the Pod label allowlist, the key field is required.<br><br><br>* If the value is empty, all containers with the key in the Pod label are collected.<br><br>* If the value is not empty, only containers that match the key and the value in Pod Label are collected. Regular expressions are supported. The value supports regular expressions. For example, if you set the key to module and set the value to `^(tcp\|udp)$`, it means only containers with Pod labels module:`tcp` and module:`udp` are collected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship between multiple key\-value pairs is logical <code>OR</code>. If the Pod label matches any key\-value pair, it will be collected.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling the Pod label allowlist, duplicate keys are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches strings that start with "http".</div><br> |
|EnableAllLabelTag |Boolean |`true` |This feature determines whether to add all Kubernetes labels as log tags to the raw log data. When enabled, TLS will add all related Kubernetes Pod label fields to logs. For example, if a Pod contains the label `source=DC` and `destination=CS`, new fields `__tag__source__: DC` and `__tag__destination__: CS` will be added to the log. |
|ExcludePodAnnotationRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Pod Annotation denylist specifies containers that are excluded from collection. If you need to set a Pod Annotation denylist, the key is required and the value is optional.<br><br><br>* If the value is empty, all containers in Pods with the specified key in their Pod Annotation will be excluded.<br><br>* If the value is not empty, only containers in Pods with the specified key and a value matching the specified value in their Pod Annotation will be excluded. By default, value uses string matching. Containers only match if the value is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with `$`, it uses regular expression match. For example, if you set key as app and value as ^(test1\|test2)$, it matches containers within Pods whose Annotation contains app:test1 or app:test2.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship among multiple Key\-Value pairs is logical <strong>OR</strong>. Pods will be included for collection as long as their annotations match any Key\-Value pair.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling Pod Annotation denylist, duplicate Keys are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches strings that start with "http".</div><br> |
|IncludePodAnnotationRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Pod annotation allowlist is used to specify the containers to be collected. If you need to set a Pod annotation allowlist, the key field is required and the value field is optional.<br><br><br>* If the value field is empty, all containers in Pods with the specified key in their annotations will match.<br><br>* If the value field is not empty, containers in Pods whose annotation contains the key and the Key's value matches the value will match. By default, value uses string matching. Containers only match if the value is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with `$`, it uses regular expression match. For example, set the key as "app" and set the value as ^(test1\|test2)$, and then the containers in Pods whose annotation contains app:test1 or app:test2 will match.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship among multiple Key\-Value pairs is logical <strong>OR</strong>. Pods will be included for collection as long as their annotations match any Key\-Value pair.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the Pod Annotation allowlist is enabled, the key must not be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> will match strings that start with http.</div><br> |


<span id="plugin"></span>
### Plugin


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|processors |Array of JSON Map |`{ "processors":[ { "json":{ "field":"__content__", "trim_keys":{ "mode":"all", "chars":"#" }, "trim_values":{ "mode":"all", "chars":"#" }, "allow_overwrite_keys":true, "allow_empty_values":true } } ] }` |LogCollector plugin. For the supported plugin list and parameter descriptions, see [LogCollector Plugin Overview](https://docs.byteplus.com/en/docs/tls/plug-ins_Overview). |


<span id="advanced"></span>
### Advanced


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|CloseEOF |Boolean |`true` |After reading to the end of the log file, release the handle for that log file. The default value is false. |
|CloseRemoved |Boolean |`true` |Release the handle of the log file after it is removed. The default value is false. |
|CloseRenamed |Boolean |`true` |After the log file is renamed, release the handle for that log file. The default value is false. |
|CloseTimeout |Integer |`1800` |Maximum monitoring duration for LogCollector log files. Measured in seconds. The default value is 0 seconds, which means LogCollector does not restrict the monitoring duration of log files. When LogCollector starts monitoring a log file, timing begins. If the specified duration is exceeded, LogCollector immediately releases the log file handle and stops monitoring, whether the log file has been fully read or not. |
|CloseInactive |Integer |`10` |Wait time before releasing log file handle. If no new log entries are written to the log file within the specified time, the log file handle will be released. The unit is seconds. The valid range is 1–300 seconds, with a default value of 60 seconds. |
|NoLineTerminatorEOFMaxTime |Integer |`5` |Maximum wait time when LogCollector does not read a newline character. Unit: seconds. Default is 5s. LogCollector starts timing when it begins reading the log file. If no newline character is found within the specified time, it sends the logs in the buffer. If the interval between file writes is long, a complete log entry may be split into two parts when written to disk. Adjust this parameter according to your log write interval. |


<span id="shardhashkey"></span>
### ShardHashKey


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HashKey |String |`3C` |HashKey of the log group, used to specify which shard to write to. The value range for this parameter is [00000000000000000000000000000000\-ffffffffffffffffffffffffffffffff). |


<span id="parsepathrule"></span>
### ParsePathRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |`["instance-id","pod-name"]` |Field name list. TLS will use a regular expression (Regex) to parse a path sample (PathSample) into multiple fields. Keys specify the field name for each field.<br><br><br>* You can configure up to 100 field names.<br><br>* Field names can not be empty or duplicated. |
|Regex |String |`/var/logs/([a-z]*)_any_([a-z]*)/test.log` |Regular expression used to extract path fields. It must match the sample collection path; otherwise, extraction fails. |
|PathSample |String |`/var/logs/instanceid_any_podname/test.log` |Example of a collection path from an actual scenario.<br><br><br>* The collection path sample must be an absolute path.<br><br>* The path sample must not contain wildcards `*`, `?`, or `**`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeRule?RuleId=faf HTTP/1.1
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

For example, using single\-line full text mode.

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ProjectId": "c7e0e442-19bf-4fb3-b547-5992fb8b****",
    "ProjectName": "testname",
    "TopicId": "4a9bd4bd-53f1-43ff-b88a-64ee1be5****",
    "TopicName": "testname",
    "RuleInfo": {
        "TopicId": "4a9bd4bd-53f1-43ff-b88a-64ee1be5****",
        "TopicName": "testname",
        "RuleId": "faf6d529-e75e-457f-a23a-9c4203a6df****",
        "RuleName": "testname",
        "Paths": [
            "/data/nginx/log/*/*/*.log"
        ],
        "ExcludePaths": [
            {
                "Type": "File",
                "Value": "/data/nginx/log/*/*/exclude.log"
            },
            {
                "Type": "Path",
                "Value": "/data/nginx/log/*/exclude/"
            }
        ],
        "LogType": "minimalist_log",
        "ExtractRule": {
            "FilterKeyRegex": [
                {
                    "Key": "__content__",
                    "Regex": ".*ERROR.*"
                }
            ]
        },
        "LogSample": "2018-05-22 15:35:53.850 INFO XXXX",
        "UserDefineRule": {
            "ParsePathRule": {
                "PathSample": "/data/nginx/log/dabaad5f-7a10/tls/app.log",
                "Regex": "\\/data\\/nginx\\/log\\/(\\w+)-(\\w+)\\/tls\\/app\\.log",
                "Keys": [
                    "instance-id",
                    "pod-name"
                ]
            },
            "ShardHashKey": {
                "HashKey": "3C"
            },
            "EnableRawLog": true,
            "RawLogKey": "raw",
            "Fields": {
                "ClusterID": "dabaad5f-7a10-4771-b3ea-d821f73e****"
            },
            "Advanced": {
                "CloseInactive": 10
            }
        }
    },
    "HostGroupInfos": [
        {
            "HostGroupId": "bcb20377-7e48-4e90-968b-922eb259****",
            "HostGroupName": "testname",
            "HostGroupType": "Label",
            "HostIdentifier": "label",
            "HostCount": 2,
            "NormalHeartbeatStatusCount": 1,
            "AbnormalHeartbeatStatusCount": 1,
            "RuleCount": 1,
            "CreateTimestamp": "2021-08-18 13:32:23",
            "ModifyTimestamp": "2021-08-18 13:32:23"
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The table below lists the error codes related to this interface and its business logic. For common error codes, refer to the [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument |Invalid parameter. |
|404 |RuleNotExist |Rule %s does not exist |Collection configuration does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
