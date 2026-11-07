---
title: "DescribeRuleV2"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/DescribeRuleV2"
---

Call the DescribeRuleV2 API to query details of the collection rule, excluding host group information.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeRuleV2


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique parameters for this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|RuleId |String |Yes |`faf6d529-e75e-457f-a23a-9c4203a6dff3xx` |ID of the collection configuration. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the parameters unique to this API. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|CsAccountChannel |String |internal_channel_001 |The account channel identifier associated with the collection rule is used for internal system identification and management. |
|ProjectId |String |c7e0e442\-19bf\-4fb3\-b547\-5992fb8b\*\*\*\* |The project ID to which the collection configuration belongs. |
|ProjectName |String |testname |Name of the project to which the collection configuration belongs. |
|RuleInfo |Object of [RuleInfo](https://docs.byteplus.com/en/docs/38/83205#ruleinfo) |/ |Information about the collection configuration. |
|TopicId |String |4a\*\*\*\*\*\*\*\*\*\*\*\* |ID of the log topic to which the collection configuration belongs. |
|TopicName |String |topictestname |Name of the log topic to which the collection configuration belongs. |
|allowDelete |Boolean |true |Allow deletion of this collection rule<br><br><br>* `true`: Deletion is allowed<br><br>* `false`: Deletion is not allowed |
|allowEdit |Boolean |true |Allow editing this collection rule.<br><br><br>* `true`: Editing allowed.<br><br>* `false`: Editing not allowed. |


<span id="ruleinfo"></span>
### RuleInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Paths |Array of String |`["/data/nginx/log/**/access.log"]` |Collection path list. |
|Pause |Integer |`0` |Collection configuration status.<br><br><br>* 0: Running.<br><br>* 1: Paused. |
|RuleId |String |`faf******` |ID of the collection configuration. |
|LogType |String |`delimiter_log` |Collection mode<br><br><br>* minimalist_log: single\-line full text mode<br><br>* json_log: JSON mode<br><br>* delimiter_log: separator mode<br><br>* multiline_log: multi\-line full text mode<br><br>* fullregex_log: complete regular expression mode |
|TopicId |String |`4a************` |ID of the log topic to which the collection configuration belongs |
|RuleName |String |`testname` |Name of the collection configuration. |
|InputType |Integer |`0` |Collection type.<br><br><br>* 0: Host machine log file<br><br>* 1: K8s container standard output<br><br>* 2: Log file in K8s container |
|LogSample |String |`2018-05-22 15:35:53.850 INFO XXXX` |Log example. |
|TopicName |String |topictestname |Name of the log topic to which the collection configuration belongs. |
|CreateTime |String |`2021-08-18 13:32:23` |Collection configuration creation time. |
|ModifyTime |String |`2021-08-18 13:32:23` |Collection configuration modification time. |
|ExtractRule |Object of [ExtractRule](https://docs.byteplus.com/en/docs/38/83205#extractrule) |`/` |Extraction rule. |
|ExcludePaths |Array of [ExcludePath](https://docs.byteplus.com/en/docs/38/83205#excludepath) |`/` |Blacklist collection list. |
|ContainerRule |Object of [ContainerRule](https://docs.byteplus.com/en/docs/38/83205#containerrule) |`/` |Container collection rule. |
|UserDefineRule |Object of [UserDefineRule](https://docs.byteplus.com/en/docs/38/83205#userdefinerule) |`/` |User\-defined collection rules. |
|RuleType |Integer |1 |This is the identifier for the rule type, used to distinguish between different types of collection rules. |


<span id="extractrule"></span>
### ExtractRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |`[ "time", "", "level", "msg" ]` |List of log field names (Key).<br><br><br>* Valid only when LogType is delimiter_log or fullregex_log.<br><br>* You can configure up to 100 field names.<br><br>* When LogType is delimiter_log, you cannot configure duplicate field names or set all field names to empty.<br><br>* When LogType is fullregex_log, you cannot configure duplicate field names or set any field name to empty. |
|Quote |String |`"` |Quotation marks. Content wrapped by quotation marks will not be separated but will be parsed as a complete field. Valid only when LogType is delimiter_log. |
|TimeKey |String |`request_time` |Name of the log time field. If you use a specific time field in the log as the log timestamp, you must set both TimeKey and TimeFormat.<br><br>TimeKey and TimeFormat must be provided together. |
|LogRegex |String |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The regular expression required for the entire log.<br><br><br>* This is only valid when the collected log type is fullregex_log.<br><br>* This must be a valid regular expression. |
|TimeZone |String |`GMT+08:00` |Time zone: supports Host time zone (default) and Custom time zone Custom time zone supports both GMT and UTC<br><br><br>* GMT format: GMT+08:00.<br><br>* UTC format: Asia/Shanghai. |
|Delimiter |String |# |Log separator. Applies only when LogType is set to delimiter_log. |
|BeginRegex |String |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |Regular expression required to match the first line of the log<br><br><br>* Only available when LogType is set to multiline_log or fullregex_log<br><br>* Must be a valid regular expression |
|TimeFormat |String |`%Y-%m-%dT%H:%M:%S,%f` |Time field parsing format. If you want to use a specific time field in the log as the log timestamp, you need to specify both TimeKey and TimeFormat.<br><br><br>* TimeKey and TimeFormat must appear as a pair<br><br>* For instructions on configuring the time format, see [Time format](https://docs.byteplus.com/docs/tls/time_format) |
|LogTemplate |Object of [LogTemplate](https://docs.byteplus.com/en/docs/38/83205#logtemplate) |`{ "Type": "Nginx", "Format": "format main '$remote_addr - $remote_user [$time_local] \"$request\" $request_time $request_length $status $body_bytes_sent \"$http_referer\" \"$http_user_agent\"';" }` |Automatically extract log fields based on the specified log template. |
|UnMatchLogKey |String |`LogParseFailed` |When uploading logs that fail to parse, the key name for the failed logs.<br><br>UnMatchUpLoadSwitch=true and UnMatchLogKey must be used together. |
|FilterKeyRegex |Array of [FilterKeyRegex](https://docs.byteplus.com/en/docs/38/83205#filterkeyregex) |`/` |Filter rule list.<br><br><br>* When LogType is minimalist_log or multiline_log, you can configure only one filter rule. The key name of the filter field must be **content**.<br><br>* When LogType is delimiter_log, json_log, or fullregex_log, you can configure up to five filter rules. The key names in the filter fields must be unique and cannot be empty. The regular expression that the filter field content needs to match must be valid and limited to 256 characters. |
|TimeExtractRegex |String |`[0-9]{0,2}\/[0-9a-zA-Z]+\/[0-9:,]+` |Regular expression for extracting time, used to extract the time value from the `TimeKey` field and parse it as the corresponding collection time. |
|UnMatchUpLoadSwitch |Boolean |`true` |Upload logs that failed to parse. UnMatchUpLoadSwitch=true and UnMatchLogKey must appear together.<br><br><br>* true: Upload logs that failed to parse.<br><br>* false: Do not upload logs that failed to parse. |
|EnableNanosecond |Boolean |`true` |Enable nanosecond precision time function. When enabled, log time is parsed and reported with nanosecond precision.<br><br><br>* true: Enable nanosecond precision time.<br><br>* false: Disable nanosecond precision time. |
|TimeSample |String |`2006-01-02T15:04:05Z07:00` |Time example.<br><br>Checks if the entered time parsing format is correct. |


<span id="excludepath"></span>
### ExcludePath


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |`Path` |Collection path type.<br><br><br>* File: The name of the object you are sharing.<br><br>* Path: Directory. |
|Value |String |`/accesslog` |Collection path. An absolute path is required.<br><br><br>* When Type is Path, Value refers to a directory.<br><br>* When Type is File, Value refers to a file name. |


<span id="containerrule"></span>
### ContainerRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|EnvTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to set environment label as log tag and add it to raw log data. If enabled, TLS will add related container environment variable fields to the logs. If you set multiple key\-value pairs, it means you add multiple fields. For example, set the key to source and the value to data_source. If the container includes the environment variable `source=DC`, a new field `__tag__data_source__: DC` will be added to the log. |
|Stream |String |`all` |Collection details<br><br><br>* stdout: Collect container standard output \- stdout.<br><br>* stderr: Collect container standard error \- stderr.<br><br>* all: Collect both container standard output \- stdout and container standard error \- stderr. |
|KubernetesRule |Object of [KubernetesRule](https://docs.byteplus.com/en/docs/38/83205#kubernetesrule) |`{ "NamespaceNameRegex": ".*test.*", "WorkloadType": "Deployment", "WorkloadNameRegex": ".*test.*", "IncludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "ExcludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "PodNameRegex": ".*test.*", "LabelTag": { "Key1": "Value1", "Key2": "Value2" } }` |Kubernetes container collection rule. |
|ContainerNameRegex |String |`.*test.*` |Name of container to collect If the container name is not specified, all containers in the host group will be collected. Supports regular expressions. For example, set the container name to `^(container-test)$` to collect all containers named `container-test`. |
|ExcludeContainerEnvRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The container environment variable denylist specifies which containers are excluded from data collection. If the denylist is disabled, all containers will be collected. If you enable the container environment variable denylist, key is required, while value is optional.<br><br><br>* If value is empty, all containers whose environment variables contain the key will be excluded from collection.<br><br>* If value is not empty, only containers whose environment variables match both the key and value are excluded. Value supports regular expression matching. For example, if you set key to module and value to `^(tcp\|udp)$`, containers with environment variables module:`tcp` or module:`udp` are excluded from collection.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`. Any container whose environment variables match any of the pairs will be excluded from collection.<br><br>* When enabling the container environment variable denylist, keys must not be duplicated. |
|IncludeContainerEnvRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Specify which containers to collect by using the container environment variable allowlist. If the allowlist is not enabled, all containers will be collected. To enable the container environment variable allowlist, enter key\-value pairs. Key is required; value is optional.<br><br><br>* If value is empty, all containers containing the key in their environment variables will be collected.<br><br>* If value is not empty, only containers with the key in their environment variables and matching the value will be collected. Value supports regular expression matching. For example, set key to module and value to `^(tcp\|udp)$`. Only containers with environment variables module:`tcp` and module:`udp` will be collected.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`: a container will be included if it matches any Key\-Value pair.<br><br>* When the container environment variable allowlist is enabled, keys can not be duplicated. |
|ExcludeContainerLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The container label denylist is used to specify which containers should not be collected. If the denylist is disabled, all containers are collected. If the container label denylist is enabled, the key field is required and the value field is optional.<br><br><br>* If value is empty, containers with the specified key in their label will not be collected.<br><br>* If value is not empty, only containers whose labels match both the key and value are excluded from collection. Value supports regular expression matching. For example, set the key to app and the value to `^(test1\|test2)$`, which means containers with app:test1 or app:test2 in their labels will not be collected.<br><br>* The logic between multiple key\-value pairs is logical `OR`. That is to say, any container whose label matches any of the key\-value pairs will be excluded from collection.<br><br>* When the container label denylist is enabled, the key fields must not be duplicated. |
|IncludeContainerLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |You can specify which containers to collect using container label allowlists. When the allowlist is not enabled, all containers will be collected. When enabling the container label allowlist, you need to fill in key\-value pairs. Key is required; value is optional.<br><br><br>* Value is empty: Collect all containers that contain the key in their container label.<br><br>* Value is not empty: Only collect containers whose label contains the key and whose value matches the value. Value supports regular expression matching. For example, if you set the key as app and set the value as `^(test1\|test2)$`, it means only containers with the label app:test1 or app:test2 will be collected.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`. That is to say, any container Label that matches any Key\-Value pair will be included in the collection.<br><br>* When enabling the container Label allowlist, keys can not be duplicated. |


<span id="userdefinerule"></span>
### UserDefineRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Fields |JSON Map |`{"ClusterID":"dabaad5f-7a10-4771-b3ea-d821f73e****"}` |Add constant fields to logs Constant fields must follow these restrictions:<br><br><br>* Supports uploading up to 5 constant fields.<br><br>* Field names (keys) must be unique and non\-empty. The length must be between 1 and 128 characters, including English letters, digits, and special characters (`-_./`), and can not start with an underscore.<br><br>* Field values can not be empty and can be up to 512 KiB in size. |
|Plugin |Object of [Plugin](https://docs.byteplus.com/en/docs/38/83205#plugin) |`{"processors":[{"json":{"field":"__content__","trim_keys":{"mode":"all","chars":"#"},"trim_values":{"mode":"all","chars":"#"},"allow_overwrite_keys":true,"allow_empty_values":true}` |Plugin configuration for LogCollector. After enabling plugin configuration, you can add one or more LogCollector processor plugins to parse logs with complex or dynamic structures. |
|Advanced |Object of [Advanced](https://docs.byteplus.com/en/docs/38/83205#advanced) |`{ "CloseInactive": 10 }` |LogCollector extended configuration. |
|RawLogKey |String |raw |Original log field name.<br><br>This setting only applies when EnableRawLog is set to true. The RawLogKey defaults to `__raw__`, meaning the raw log data will be encapsulated in the `__raw__` field and uploaded to TLS along with the parsed log data. |
|TailFiles |Boolean |`true` |LogCollector collection policy specifies whether LogCollector collects incremental logs or full logs. The default value is false, indicating collection of all logs.<br><br><br>* true: Collect incrementally. LogCollector collects only new content added to the file during log collection. When new logs are written to log files within the monitor scope, it triggers LogCollector collection.<br><br>   * For first\-time collection, LogCollector automatically confirms the collection position based on the incremental threshold `TailSizeKb` you specified.<br><br>      * If the new file size does not exceed your specified incremental threshold, the first collection starts from the beginning of the new file.<br><br>      * If the new file size exceeds your specified incremental threshold, the first collection starts at the position where the file ends minus the incremental threshold. That is to say, only incremental logs are collected.<br><br>   * For files collected not for the first time, LogCollector determines the collection position based on the Checkpoint and continues collecting.<br><br>* false: (Default) Collect all logs. LogCollector starts collecting logs from the beginning of each document. In this case, LogCollector will collect historical log data. |
|HostnameKey |String |`hostname` |hostname field name.<br><br>Required only when EnableHostname is set to true. |
|EnableRawLog |Boolean |`true` |Whether to upload the original log.<br><br><br>* true: Upload the original log.<br><br>* false: (Default) Do not upload the original log. |
|ShardHashKey |Object of [ShardHashKey](https://docs.byteplus.com/en/docs/38/83205#shardhashkey) |`{ "HashKey": "3C" }` |Rules for routing log shard partitioning.<br><br><br>* If this parameter is not set, logs are written using the default load balancing mode, and packets are sent to any available shard.<br><br>* If you set this parameter, the logs are collected using the HashKey routing shard mode, and TLS will write data to the shard that contains the specified key value. |
|ParsePathRule |Object of [ParsePathRule](https://docs.byteplus.com/en/docs/38/83205#parsepathrule) |`{ "PathSample": "/data/nginx/log/dabaad5f-7a10/tls/app.log", "Regex": "\\/data\\/nginx\\/log\\/(\\w+)-(\\w+)\\/tls\\/app\\.log", "Keys": ["instance-id", "pod-name"] }` |Parse collection path rules. After setting the rules, extract fields from the collection path specified by the regular expression and add them as metadata to the log data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is not supported when collecting container standard output.</div><br> |
|EnableHostname |Boolean |`true` |This feature determines whether to upload the hostname field. By default, it is disabled.<br><br><br>* true: Adds a field to the original log to record the source hostname. At this stage, you should specify the hostname field name via HostnameKey.<br><br>* false: (default) Does not add the hostname field. |
|HostGroupLabelKey |String |`host_group_label` |Field name for storing host group Label information. |
|EnableHostGroupLabel |Boolean |`true` |You can select whether to upload the label information of the host group to TLS. By default, it is enabled.<br><br><br>* true: LogCollector uploads host group label information to the specified field. You can specify the field name in the **HostGroupLabelKey** parameter.<br><br>* false (default): Host group label information is not uploaded. |
|TailSizeKb |Integer |`1024` |Backtracking threshold for incremental collection, measured in KiB.<br><br>When the LogCollector uses the incremental collection strategy, for the first collection of a log file:<br><br><br>* If the new log file size does not exceed `TailSizeKb`, the first collection starts from the beginning of the new log file.<br><br>* If the new log file size exceeds `TailSizeKb`, the first collection starts at the position where the file ends minus `TailSizeKb`. |
|IgnoreOlder |Integer |`7` |Ignore log files that have not been updated for a specified period, in hours. |
|MultiCollectsType |String |`RuleID` |Log files can be collected multiple times.<br><br><br>* Empty: The log file is uniquely identified using its log file ID, which includes the file's inode, device, and the checksum of the first N bytes.<br><br>* RuleID: Use the collection rule ID and log file ID to uniquely identify the log file.<br><br>* TopicIDRuleName: Use the log topic ID, collection rule name, and log file ID to uniquely identify the log file. |


<span id="logtemplate"></span>
### LogTemplate


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |`Nginx` |Type of log template. Supported types:<br><br><br>* Nginx: Log template for Nginx. |
|Format |String |`log_format main '$remote_addr - $remote_user [$time_local] "$request" $request_time $request_length $status $body_bytes_sent "$http_referer" "$http_user_agent"';` |Log template format. |


<span id="filterkeyregex"></span>
### FilterKeyRegex


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Key |String |`__content__` |Name of the filter field. |
|Regex |String |`.*ERROR.*` |The regular expression that must be matched in the log content of the filtered field. |


<span id="kubernetesrule"></span>
### KubernetesRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|LabelTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to add Kubernetes Labels as log tags to the raw log data. If enabled, TLS will add Kubernetes Pod Label related fields to the logs. If you set multiple key\-value pairs, multiple fields are added. For example, if you set the Key as source and the Value as data_source, and the Pod contains the Label `source=DC`, then the log will include a new field `__tag__data_source__: DC`. |
|PodNameRegex |String |`.*test.*` |Pod name is used to specify the containers to collect If no Pod name is specified, all containers will be collected Pod name supports regular expressions. For example, set the Pod name to `^(http.*)$` to collect all containers under Pods that start with "http" |
|WorkloadType |String |`Deployment` |Specify the container for collection based on workload type. Only one type can be selected. If no type is specified, containers of all types are collected. Supported workload types:<br><br><br>* Deployment: Stateless workload<br><br>* StatefulSet: Stateful workload<br><br>* DaemonSet: Daemon process<br><br>* Job: Task<br><br>* CronJob: Scheduled SQL task |
|AnnotationTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to set Kubernetes Annotation to log tags and add it into the raw log data. If enabled, TLS will add Kubernetes Pod annotation fields to the logs. If you set multiple key\-value pairs, multiple fields are added. If you set the key to "sink" and the value to "data_sink", and the Pod has an annotation `sink=ck`, a new field `__tag__data_sink__: ck` will be added to the log. |
|WorkloadNameRegex |String |`.*test.*` |By configuring the workload name, you can specify the container to collect. If no workload name is specified, all containers are collected. Workload names support regular expression matching. For example, if you set the workload name to `^(http.*)$`, all containers under workloads starting with http will be collected. |
|NamespaceNameRegex |String |`.*test.*` |Name of the Kubernetes namespace to be collected. If no Namespace is specified, all containers will be collected. Namespace names support regular expression matching. For example, setting the namespace name to `^(tcp\|udp)$` means collecting all containers in the `tcp` namespace and `udp` namespace. |
|ExcludePodLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The Pod Label denylist is used to specify which containers should not be collected. If the denylist is disabled, all containers are collected. If you need to set a Pod Label denylist, the key field is required, while the value field is optional.<br><br><br>* If the value field is empty, all containers with the specified key in the Pod Label will be excluded from collection.<br><br>* If the value field is not empty, only containers with the specified key and a value that matches will be excluded from collection. The value field supports regular expressions. For example, if you set key to module and value to `^(tcp\|udp)$`, containers with module:`tcp` and module:`udp` in the Pod Label will not be collected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship between multiple Key\-Value pairs is <code>OR</code>. That is to say, any Pod Label that matches any Key\-Value pair will be excluded from collection.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling the Pod Label denylist, keys can not be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches strings that start with "http".</div><br> |
|IncludePodLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The Pod Label allowlist is used to specify the containers to be collected. If the Pod Label allowlist is not enabled, all containers will be collected. If you need to set the Pod label allowlist, the key field is required.<br><br><br>* If the value is empty, all containers with the key in the Pod label are collected.<br><br>* If the value is not empty, only containers that match the key and the value in Pod Label are collected. Regular expressions are supported. The value supports regular expressions. For example, if you set the key to module and set the value to `^(tcp\|udp)$`, it means only containers with Pod labels module:`tcp` and module:`udp` are collected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship between multiple key\-value pairs is logical <code>OR</code>. If the Pod label matches any key\-value pair, it will be collected.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling the Pod label allowlist, duplicate keys are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches any string that starts with http.</div><br> |
|EnableAllLabelTag |Boolean |`true` |This feature determines whether to add all Kubernetes labels as log tags to the raw log data. When enabled, TLS will add all related Kubernetes Pod label fields to logs.<br><br>For example, if the Pod contains `source=DC` and `destination=CS` labels, the log will include the fields `__tag__source__: DC` and `__tag__destination__: CS`. |
|ExcludePodAnnotationRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Pod Annotation denylist specifies containers that are excluded from collection.<br><br>If you need to set a Pod Annotation denylist, the key is required and the value is optional.<br><br><br>* If the value is empty, all containers in Pods with the specified key in their Pod Annotation will be excluded.<br><br>* If the value is not empty, only containers in Pods with the specified key and a value matching the specified value in their Pod Annotation will be excluded.<br><br><br>By default, value uses string matching. Containers only match if the value is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with `$`, it uses regular expression match. For example, if you set key as app and value as ^(test1\|test2)$, it matches containers within Pods whose Annotation contains app:test1 or app:test2.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship among multiple Key\-Value pairs is logical <strong>OR</strong>. Pods will be included for collection as long as their annotations match any Key\-Value pair.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling Pod Annotation denylist, duplicate Keys are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches characters starting with http.</div><br> |
|IncludePodAnnotationRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Pod annotation allowlist is used to specify the containers to be collected.<br><br>If you need to set a Pod annotation allowlist, the key field is required and the value field is optional.<br><br><br>* If the value field is empty, all containers in Pods with the specified key in their annotations will match.<br><br>* If the value field is not empty, containers in Pods whose annotation contains the key and the Key's value matches the value will match.<br><br><br>By default, value uses string matching. Containers only match if the value is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with `$`, it uses regular expression match. For example, set the key as "app" and set the value as ^(test1\|test2)$, and then the containers in Pods whose annotation contains app:test1 or app:test2 will match.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship among multiple Key\-Value pairs is logical <strong>OR</strong>. Pods will be included for collection as long as their annotations match any Key\-Value pair.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the Pod Annotation allowlist is enabled, the key must not be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches values starting with "http".</div><br> |


<span id="plugin"></span>
### Plugin


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|processors |Array of JSON Map |`{ "processors":[ { "json":{ "field":"__content__", "trim_keys":{ "mode":"all", "chars":"#" }, "trim_values":{ "mode":"all", "chars":"#" }, "allow_overwrite_keys":true, "allow_empty_values":true } } ] }` |LogCollector plugin. For the list of supported plugins and parameter descriptions, see [LogCollector Plugin Overview](https://docs.byteplus.com/en/docs/tls/plug-ins_Overview). |


<span id="advanced"></span>
### Advanced


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|CloseEOF |Boolean |`true` |After reading to the end of the log file, release the file handle. The default value is false. |
|CloseRemoved |Boolean |`true` |Release the handle of the log file after it is removed. The default value is false. |
|CloseRenamed |Boolean |`true` |After the log file is renamed, its handle will be released or not The default value is false. |
|CloseTimeout |Integer |`1800` |Maximum duration LogCollector monitors log files. Unit: seconds. The default is 0 seconds, which means there is no limit on how long LogCollector monitors log files.<br><br>&nbsp;<br><br>LogCollector starts timing when it begins monitoring a log file, and releases the file handle immediately after exceeding the specified duration, regardless of whether the log file has been fully read. |
|CloseInactive |Integer |`10` |Waiting time to release the log file handle. If no new logs are written to the log file after the specified time, the handle for the log file is released.<br><br>&nbsp;<br><br>The unit is seconds. Valid values range from 1 to 300 seconds, and the default is 60 seconds. |
|NoLineTerminatorEOFMaxTime |Integer |`5` |Maximum wait time for LogCollector when no line break is detected.<br><br>The unit is seconds, with a default value of 5s.<br><br>LogCollector starts timing when it begins reading the log file. If no newline character is found within the specified duration, the buffered logs will be sent.<br><br>If the interval between log file writes is large, a complete log entry may be split and written in two parts. You can adjust this parameter according to your log write interval. |


<span id="shardhashkey"></span>
### ShardHashKey


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HashKey |String |`3C` |The HashKey of the log group, used to specify the shard that the current log group will be written to This parameter value must be in the range [00000000000000000000000000000000\-ffffffffffffffffffffffffffffffff) |


<span id="parsepathrule"></span>
### ParsePathRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |`["instance-id","pod-name"]` |Field name list. TLS will use regular expressions (Regex) to parse the path sample (PathSample) into multiple fields. Keys specify the name of each field.<br><br><br>* You can configure up to 100 field names.<br><br>* Field names can not be empty or duplicated. |
|Regex |String |`/var/logs/([a-z]*)_any_([a-z]*)/test.log` |Regular expression for extracting path fields. It must match the sample collection path; otherwise, extraction fails. |
|PathSample |String |`/var/logs/instanceid_any_podname/test.log` |Sample collection paths for real scenarios.<br><br><br>* The collection path sample must be an absolute path.<br><br>* The path sample must not contain wildcards `*`, `?`, or `**`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeRuleV2?&RuleId=faf6d529-e75e-457f-a23a-9c4203a6dff3xx HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "CsAccountChannel": "internal_channel_001",
    "ProjectId": "c7e0e442-19bf-4fb3-b547-5992fb8b****",
    "ProjectName": "testname",
    "RuleInfo": {
        "Paths": [
            "/data/nginx/log/**/access.log"
        ],
        "Pause": 0,
        "RuleId": "faf******",
        "LogType": "delimiter_log",
        "TopicId": "4a************",
        "RuleName": "testname",
        "RuleType": 1,
        "InputType": 0,
        "LogSample": "2018-05-22 15:35:53.850 INFO XXXX",
        "TopicName": "topictestname",
        "CreateTime": "2021-08-18 13:32:23",
        "ModifyTime": "2021-08-18 13:32:23",
        "ExtractRule": {
            "Keys": [
                "time",
                "",
                "level",
                "msg"
            ],
            "Quote": "\"",
            "TimeKey": "request_time",
            "LogRegex": "[(\\d+-\\d+-\\w+:\\d+:\\d+,\\d+)]\\s[(\\w+)]\\s(.*)",
            "TimeZone": "GMT+08:00",
            "Delimiter": "#",
            "BeginRegex": "[(\\d+-\\d+-\\w+:\\d+:\\d+,\\d+)]\\s[(\\w+)]\\s(.*)",
            "TimeFormat": "%Y-%m-%dT%H:%M:%S,%f",
            "TimeSample": "2006-01-02T15:04:05Z07:00",
            "LogTemplate": {
                "Type": "Nginx",
                "Format": "format main  '$remote_addr - $remote_user [$time_local] \"$request\" $request_time $request_length $status $body_bytes_sent \"$http_referer\" \"$http_user_agent\"';"
            },
            "UnMatchLogKey": "LogParseFailed",
            "FilterKeyRegex": [
                {
                    "Key": "__content__",
                    "Regex": ".*ERROR.*"
                }
            ],
            "EnableNanosecond": true,
            "TimeExtractRegex": "[0-9]{0,2}\\/[0-9a-zA-Z]+\\/[0-9:,]+",
            "UnMatchUpLoadSwitch": true
        },
        "ExcludePaths": [
            {
                "Type": "Path",
                "Value": "/accesslog"
            }
        ],
        "ContainerRule": {
            "EnvTag": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "Stream": "all",
            "KubernetesRule": {
                "LabelTag": {
                    "Key1": "Value1",
                    "Key2": "Value2"
                },
                "PodNameRegex": ".*test.*",
                "WorkloadType": "Deployment",
                "AnnotationTag": {
                    "Key1": "Value1",
                    "Key2": "Value2"
                },
                "EnableAllLabelTag": true,
                "WorkloadNameRegex": ".*test.*",
                "NamespaceNameRegex": ".*test.*",
                "ExcludePodLabelRegex": {
                    "Key1": "Value1",
                    "Key2": "Value2"
                },
                "IncludePodLabelRegex": {
                    "Key1": "Value1",
                    "Key2": "Value2"
                },
                "ExcludePodAnnotationRegex": {
                    "Key1": "Value1",
                    "Key2": "Value2"
                },
                "IncludePodAnnotationRegex": {
                    "Key1": "Value1",
                    "Key2": "Value2"
                }
            },
            "ContainerNameRegex": ".*test.*",
            "ExcludeContainerEnvRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "IncludeContainerEnvRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "ExcludeContainerLabelRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "IncludeContainerLabelRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            }
        },
        "UserDefineRule": {
            "Fields": {
                "ClusterID": "dabaad5f-7a10-4771-b3ea-d821f73e****"
            },
            "Plugin": {
                "processors": [
                    {
                        "json": {
                            "field": "__content__",
                            "trim_keys": {
                                "mode": "all",
                                "chars": "#"
                            },
                            "trim_values": {
                                "mode": "all",
                                "chars": "#"
                            },
                            "allow_overwrite_keys": true,
                            "allow_empty_values": true
                        }
                    }
                ]
            },
            "Advanced": {
                "CloseEOF": true,
                "CloseRemoved": true,
                "CloseRenamed": true,
                "CloseTimeout": 1800,
                "CloseInactive": 10,
                "NoLineTerminatorEOFMaxTime": 5
            },
            "RawLogKey": "raw",
            "TailFiles": true,
            "TailSizeKb": 1024,
            "HostnameKey": "hostname",
            "IgnoreOlder": 7,
            "EnableRawLog": true,
            "ShardHashKey": {
                "HashKey": "3C"
            },
            "ParsePathRule": {
                "Keys": [
                    "instance-id",
                    "pod-name"
                ],
                "Regex": "\\/data\\/nginx\\/log\\/(\\w+)-(\\w+)\\/tls\\/app\\.log",
                "PathSample": "/data/nginx/log/dabaad5f-7a10/tls/app.log"
            },
            "EnableHostname": true,
            "HostGroupLabelKey": "host_group_label",
            "MultiCollectsType": "RuleID",
            "EnableHostGroupLabel": true
        }
    },
    "TopicId": "4a************",
    "TopicName": "topictestname",
    "allowDelete": true,
    "allowEdit": true
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [Public Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more information.
