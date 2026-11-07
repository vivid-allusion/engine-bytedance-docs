---
title: "DescribeHostGroup (Deprecated)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-describehostgroup"
---

TLS provides the new interface [DescribeHostGroupV2](https://docs.byteplus.com/en/docs/tls/DescribeHostGroupV2) to view information about a specific host group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* This interface is limited to 20 requests per second. If the rate limit is exceeded, an ExceedQPSLimit error is returned.

* The following limitations apply to the information returned by this interface: 

   * The maximum number of machines is 10,000, meaning the total HostCount cannot exceed 10,000.

   * The maximum number of collection rules is 1,500, meaning the total RuleCount cannot exceed 1,500.


<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/DescribeHostGroup


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists the parameters specific to this interface and some common parameters. For more details, see [Public parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Query"></span>
### Query


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|HostGroupId |String |Yes |`"c7e0e442-19bf-4fb3-b547-5992fb8b****"` |Host group ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

The table below only lists the return parameters specific to this API. For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostGroupHostsRulesInfo |Object of [HostGroupHostsRulesInfo](https://docs.byteplus.com/en/docs/38/16769#hostgrouphostsrulesinfo) |`/` |Host group information list. |


<span id="hostgrouphostsrulesinfo"></span>
### HostGroupHostsRulesInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostInfos |Array of [HostInfo](https://docs.byteplus.com/en/docs/38/16769#hostinfo) |`/` |Machine information list. |
|RuleInfos |Array of [RuleInfo](https://docs.byteplus.com/en/docs/38/16769#ruleinfo) |`/` |List of linked collection configuration information. |
|HostGroupInfo |Object of [HostGroupInfo](https://docs.byteplus.com/en/docs/38/16769#hostgroupinfo) |`/` |Host group information. |


<span id="hostinfo"></span>
### HostInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Ip |String |`127.0.0.1` |Machine IP address. |
|HeartbeatStatus |Integer |`1` |Agent heartbeat status.<br><br><br>* 0: Heartbeat is normal<br><br>* 1: Heartbeat exception. |
|LogCollectorVersion |String |`1.0.11` |The LogCollector version installed on the machine. |


<span id="ruleinfo"></span>
### RuleInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Paths |Array of String |`["/data/nginx/log/**/access.log"]` |Collection path list. |
|Pause |Integer |`0` |Running status of the collection configuration.<br><br><br>* 0: Running.<br><br>* 1: Paused. |
|RuleId |String |`faf******` |ID of the collection configuration. |
|LogType |String |`delimiter_log` |Collection mode.<br><br><br>* minimalist_log: Single\-line full\-text mode.<br><br>* json_log: JSON mode.<br><br>* delimiter_log: Separator mode.<br><br>* multiline_log: multiline full text mode.<br><br>* fullregex_log: complete regular expression mode. |
|TopicId |String |`4a************` |ID of the log topic to which the collection configuration belongs. |
|RuleName |String |`testname` |Name of the collection configuration. |
|InputType |Integer |`0` |Collection type.<br><br><br>* 0: Host machine log file<br><br>* 1: K8s container standard output<br><br>* 2: Log file in K8s container |
|LogSample |String |`2018-05-22 15:35:53.850 INFO XXXX` |Log sample. |
|TopicName |String |topictestname |Name of the log topic to which the collection configuration belongs. |
|CreateTime |String |`2021-08-18 13:32:23` |Collection configuration creation time. |
|ModifyTime |String |`2021-08-18 13:32:23` |Time when the collection configuration was modified. |
|ExtractRule |Object of [ExtractRule](https://docs.byteplus.com/en/docs/38/16769#extractrule) |`/` |提取规则。 |
|ExcludePaths |Array of [ExcludePath](https://docs.byteplus.com/en/docs/38/16769#excludepath) |`/` |Blacklist for data collection. |
|ContainerRule |Object of [ContainerRule](https://docs.byteplus.com/en/docs/38/16769#containerrule) |`/` |Container collection rules. |
|UserDefineRule |Object of [UserDefineRule](https://docs.byteplus.com/en/docs/38/16769#userdefinerule) |`/` |User\-defined collection rule. |
|RuleType |Integer |1 |Collection rule type identifier, used to distinguish between different types of collection rules. |


<span id="hostgroupinfo"></span>
### HostGroupInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HostCount |Integer |`2` |Number of machines. |
|RuleCount |Integer |`1` |Number of bound collection configurations. |
|AutoUpdate |Boolean |`true` |LogCollector installed on the host group server has auto\-upgrade function. You can choose whether to enable it.<br><br><br>* true: TLS will check for upgrades at the specified time each day. If the requirements are met, LogCollector will upgrade automatically without manual intervention.<br><br>* false: (default) LogCollector does not upgrade automatically. To use a newer version of LogCollector, see [Upgrading LogCollector](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host). |
|CreateTime |String |`2021-08-18 13:32:23` |The creation time of host group. |
|ModifyTime |String |`2021-08-18 13:32:23` |Host group modification time. |
|HostGroupId |String |`0fd**********` |Host group ID. |
|HostGroupName |String |`testname` |Name of the host group. |
|HostGroupType |String |`IP` |The type of host group.<br><br><br>* IP: machine IP.<br><br>* Label: Host identification. |
|UpdateEndTime |String |"02:00" |LogCollector auto\-upgrade end time. |
|HostIdentifier |String |`label` |Machine identifier. |
|IamProjectName |String |`default` |The IAM project to which the host group belongs. |
|ServiceLogging |Boolean |`true` |You can choose whether to enable the LogCollector service log.<br><br><br>* true: enabled.<br><br>* false: (default) disabled. |
|UpdateStartTime |String |"00:00" |Start time for LogCollector auto upgrade.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Required only when AutoUpdate is set to true.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For automatic upgrades, we recommend that you set it during off\-peak business hours. LogCollector may restart during the upgrade, but no logs will be lost.</div><br> |
|AgentLatestVersion |String |"2.3.4" |Latest version of TLS LogCollector released |
|NormalHeartbeatStatusCount |Integer |`1` |Number of machines with normal heartbeat. |
|AbnormalHeartbeatStatusCount |Integer |`1` |Number of machines with heartbeat exceptions. |


<span id="extractrule"></span>
### ExtractRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |`[ "time", "", "level", "msg" ]` |Log field name (Key) list.<br><br><br>* Valid only when LogType is set to delimiter_log or fullregex_log<br><br>* Supports up to 100 field names<br><br>* When LogType is delimiter_log, duplicate field names are not allowed, and all field names cannot be left blank<br><br>* When LogType is fullregex_log, duplicate field names are not allowed, and field names cannot be left blank |
|Quote |String |`"` |Quotation marks. The content enclosed by quotation marks is parsed as a complete field rather than being split. This is valid only when LogType is delimiter_log. |
|TimeKey |String |`request_time` |Name of the log time field. If you use the specified time field in the log as the log timestamp, you must complete TimeKey and TimeFormat.<br><br>TimeKey and TimeFormat must be used together. |
|LogRegex |String |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The entire log must match the regular expression.<br><br><br>* This applies only when the collected log type is fullregex_log.<br><br>* It must be a valid regular expression. |
|TimeZone |String |`GMT+08:00` |Time zone, supporting Host time zone (default) and Custom time zone. Custom time zone supports both GMT and UTC.<br><br><br>* GMT format: GMT+08:00.<br><br>* UTC format: Asia/Shanghai. |
|Delimiter |String |# |Log separator. Valid only when LogType is delimiter_log. |
|BeginRegex |String |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The regular expression that the first line of the log must match.<br><br><br>* Valid only when LogType is set to multiline_log or fullregex_log.<br><br>* Must be a valid regular expression. |
|TimeFormat |String |`%Y-%m-%dT%H:%M:%S,%f` |Format for parsing time fields. If you want to use a specific time field in the log as the log timestamp, you need to specify both TimeKey and TimeFormat.<br><br><br>* TimeKey and TimeFormat must be specified together.<br><br>* Refer to [Time Format](https://docs.byteplus.com/docs/tls/time_format) for instructions on how to configure the time format. |
|LogTemplate |Object of [LogTemplate](https://docs.byteplus.com/en/docs/38/16769#logtemplate) |`{ "Type": "Nginx", "Format": "format main '$remote_addr - $remote_user [$time_local] \"$request\" $request_time $request_length $status $body_bytes_sent \"$http_referer\" \"$http_user_agent\"';" }` |Automatically extract log fields based on the specified log template. |
|UnMatchLogKey |String |`LogParseFailed` |When you upload logs that failed to parse, specify the key name for logs with parsing errors.<br><br>UnMatchUpLoadSwitch=true and UnMatchLogKey must be used together. |
|FilterKeyRegex |Array of [FilterKeyRegex](https://docs.byteplus.com/en/docs/38/16769#filterkeyregex) |`/` |Filter rule list.<br><br><br>* When LogType is minimalist_log or multiline_log, you can configure at most one filter rule, and the field name key must be **content**.<br><br>* When LogType is delimiter_log, json_log, or fullregex_log, you can configure up to five filter rules, and the field names must not be duplicated or empty. The regular expression used to match the content of log fields must be valid and limited to 256 characters. |
|TimeExtractRegex |String |`[0-9]{0,2}\/[0-9a-zA-Z]+\/[0-9:,]+` |Regular expression for extracting time, used to extract the time value from the `TimeKey` field and parse it into the corresponding collection time. |
|UnMatchUpLoadSwitch |Boolean |`true` |Upload failed parsing logs? UnMatchUpLoadSwitch=true and UnMatchLogKey must be used together.<br><br><br>* true: Upload failed parsing logs.<br><br>* false: Do not upload failed parsing logs. |
|EnableNanosecond |Boolean |`true` |Enable nanosecond precision time. When enabled, log time parsing will include and report nanosecond precision.<br><br><br>* true: Enable nanosecond precision time.<br><br>* false: Disable nanosecond precision time. |
|TimeSample |String |`2006-01-02T15:04:05Z07:00` |Time sample. Used to check if the entered time parsing format is correct. |


<span id="excludepath"></span>
### ExcludePath


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |`Path` |Collection path type.<br><br><br>* File: The name of the object you are sharing.<br><br>* Path: Directory. |
|Value |String |`/accesslog` |Collection path. An absolute path must be specified.<br><br><br>* When Type is Path, Value represents a directory.<br><br>* When Type is File, Value represents a file name. |


<span id="containerrule"></span>
### ContainerRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|EnvTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to set environment label as log tag and add it to raw log data. If enabled, TLS will add related container environment variable fields to the logs. If you set multiple key\-value pairs, it means you add multiple fields. For example, set Key to source and Value to data_source. If the container contains the environment variable `source=DC`, a new field `__tag__data_source__: DC` will be added to the log. |
|Stream |String |`all` |Collection details.<br><br><br>* stdout: Collect container standard output (stdout).<br><br>* stderr: Collect container standard error (stderr).<br><br>* all: Collect both container standard output (stdout) and container standard error (stderr). |
|KubernetesRule |Object of [KubernetesRule](https://docs.byteplus.com/en/docs/38/16769#kubernetesrule) |`{ "NamespaceNameRegex": ".*test.*", "WorkloadType": "Deployment", "WorkloadNameRegex": ".*test.*", "IncludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "ExcludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "PodNameRegex": ".*test.*", "LabelTag": { "Key1": "Value1", "Key2": "Value2" } }` |Kubernetes container collection rules. |
|ContainerNameRegex |String |`.*test.*` |Name of container to collect If the container name is not specified, all containers in the host group will be collected. Regular expression matching is supported. For example, if you set the container name to `^(container-test)$`, all containers named `container-test` will be collected. |
|ExcludeContainerEnvRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The container environment variable denylist specifies which containers are excluded from data collection. If the denylist is disabled, all containers will be collected. If you enable the container environment variable denylist, key is required, while value is optional.<br><br><br>* If value is empty, all containers whose environment variables contain the key will be excluded from collection.<br><br>* If value is not empty, only containers whose environment variables match both the key and value are excluded. Value supports regular expression matching. For example, if you set key to module and value to `^(tcp\|udp)$`, containers with environment variables module:`tcp` or module:`udp` are excluded from collection.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`. Any container whose environment variables match any of the pairs will be excluded from collection.<br><br>* When enabling the container environment variable denylist, keys must not be duplicated. |
|IncludeContainerEnvRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Specify which containers to collect by using the container environment variable allowlist. If the allowlist is not enabled, all containers will be collected. To enable the container environment variable allowlist, enter key\-value pairs. Key is required; value is optional.<br><br><br>* If value is empty, all containers containing the key in their environment variables will be collected.<br><br>* If value is not empty, only containers with the key in their environment variables and matching the value will be collected. Value supports regular expression matching. For example, set key to module and value to `^(tcp\|udp)$`. Only containers with environment variables module:`tcp` and module:`udp` will be collected.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`: a container will be included if it matches any Key\-Value pair.<br><br>* When the container environment variable allowlist is enabled, keys can not be duplicated. |
|ExcludeContainerLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The container label denylist is used to specify which containers should not be collected. If the denylist is disabled, all containers are collected. If the container label denylist is enabled, the key field is required and the value field is optional.<br><br><br>* If value is empty, containers with the specified key in their label will not be collected.<br><br>* If value is not empty, only containers whose labels match both the key and value are excluded from collection. Value supports regular expression matching. For example, if you set the key to app and set the value to `^(test1\|test2)$`, containers with labels app:test1 or app:test2 will be excluded from collection.<br><br>* The logic between multiple key\-value pairs is logical `OR`. That is to say, any container whose label matches any of the key\-value pairs will be excluded from collection.<br><br>* When the container label denylist is enabled, the key fields must not be duplicated. |
|IncludeContainerLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |You can specify which containers to collect using container label allowlists. When the allowlist is not enabled, all containers will be collected. When enabling the container label allowlist, you need to fill in key\-value pairs. Key is required; value is optional.<br><br><br>* Value is empty: Collect all containers that contain the key in their container label.<br><br>* Value is not empty: Only collect containers whose label contains the key and whose value matches the value. Value supports regular expression matching. For example, set the key to app and the value to `^(test1\|test2)$`, which means only containers with app:test1 and app:test2 in the container label will be collected.<br><br>* The logical relationship between multiple Key\-Value pairs is `OR`. That is to say, any container Label that matches any Key\-Value pair will be included in the collection.<br><br>* When enabling the container Label allowlist, keys can not be duplicated. |


<span id="userdefinerule"></span>
### UserDefineRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Fields |JSON Map |`{"ClusterID":"dabaad5f-7a10-4771-b3ea-d821f73e****"}` |Add constant fields to logs. Constant fields must follow these restrictions:<br><br><br>* Supports uploading up to 5 constant fields.<br><br>* Field names (keys) must be unique and non\-empty. The length must be between 1 and 128 characters, including English letters, digits, and special characters (`-_./`), and can not start with an underscore.<br><br>* Field values can not be empty and can be up to 512 KiB in size. |
|Plugin |Object of [Plugin](https://docs.byteplus.com/en/docs/38/16769#plugin) |`{"processors":[{"json":{"field":"__content__","trim_keys":{"mode":"all","chars":"#"},"trim_values":{"mode":"all","chars":"#"},"allow_overwrite_keys":true,"allow_empty_values":true}` |LogCollector Plugin configuration. After enabling plugin configuration, you can add one or more LogCollector processor plugins to parse complex or variable\-structured logs. |
|Advanced |Object of [Advanced](https://docs.byteplus.com/en/docs/38/16769#advanced) |`{ "CloseInactive": 10 }` |LogCollector extended configuration. |
|RawLogKey |String |raw |Name of the original log field.<br><br>Applies only when EnableRawLog is set to true. RawLogKey defaults to `__raw__`, meaning the original log data is packaged in the `__raw__` field and uploaded to TLS along with the parsed log data. |
|TailFiles |Boolean |`true` |LogCollector collection policy specifies whether LogCollector collects incremental logs or full logs. The default value is false, which means full log collection.<br><br><br>* true: incremental collection. LogCollector collects only new content added to the file during log collection. When new logs are written to log files within the monitor scope, it triggers LogCollector collection.<br><br>   * For files collected for the first time, LogCollector automatically confirms the collection position based on the incremental threshold you specify in `TailSizeKb`.<br><br>      * If the new file size does not exceed your specified incremental threshold, the first collection starts from the beginning of the new file.<br><br>      * If the new file size exceeds your specified incremental threshold, the first collection starts at the position where the file ends minus the incremental threshold. That is to say, only incremental logs are collected.<br><br>   * For log files that are not being collected for the first time, LogCollector determines the collection position according to the Checkpoint and continues collecting.<br><br>* false: (default) collect all data. LogCollector starts collecting logs from the beginning of each document. In this case, LogCollector will collect historical log data. |
|HostnameKey |String |`hostname` |Hostname field name.<br><br>This setting is required only when EnableHostname is true. |
|EnableRawLog |Boolean |`true` |Upload original log.<br><br><br>* true: Upload original log.<br><br>* false: (default) Do not upload original log. |
|ShardHashKey |Object of [ShardHashKey](https://docs.byteplus.com/en/docs/38/16769#shardhashkey) |`{ "HashKey": "3C" }` |Routing rules for shard logs.<br><br><br>* If this parameter is not set, logs are written in the default load balancing mode, with data packets sent to any available shard.<br><br>* If this parameter is set, logs are collected using the HashKey routing shard mode. TLS will write data to the shard containing the specified Key value. |
|ParsePathRule |Object of [ParsePathRule](https://docs.byteplus.com/en/docs/38/16769#parsepathrule) |`{ "PathSample": "/data/nginx/log/dabaad5f-7a10/tls/app.log", "Regex": "\\/data\\/nginx\\/log\\/(\\w+)-(\\w+)\\/tls\\/app\\.log", "Keys": ["instance-id", "pod-name"] }` |Rules for parsing the collection path. After you set the rules, fields in the collection path will be extracted with the regular expressions specified by the rule and added as metadata to the log data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is not supported when collecting container standard output.</div><br> |
|EnableHostname |Boolean |`true` |This feature determines whether to upload the hostname field. By default, it is disabled.<br><br><br>* true: Adds a field to the raw log to record the log source's hostname. You should specify the hostname field name using HostnameKey at this point.<br><br>* false: (default) Do not add the hostname field. |
|HostGroupLabelKey |String |`host_group_label` |Name of the field used to store host group label information |
|EnableHostGroupLabel |Boolean |`true` |You can select whether to upload the label information of the host group to TLS. By default, it is enabled.<br><br><br>* true: LogCollector uploads the host group's Label information to the specified field. You can specify the field name in the **HostGroupLabelKey** parameter.<br><br>* false (default): The host group Label information is not uploaded. |
|TailSizeKb |Integer |`1024` |The backtrack threshold for incremental collection, measured in KiB. When the LogCollector uses incremental collection strategy, for the first collection of log files:<br><br><br>* If the new log file size does not exceed the value of `TailSizeKb`, the first collection starts from the beginning of the new log file.<br><br>* If the size of the new log file exceeds `TailSizeKb`, the first collection starts at the position after subtracting `TailSizeKb` from the end of the new log file. |
|IgnoreOlder |Integer |`7` |Ignore log files that have not been updated for a certain period; the unit is hours. |
|MultiCollectsType |String |`RuleID` |Allow collecting log files multiple times.<br><br><br>* Empty: Use the log file ID (including file inode, device, and checksum of the first N bytes) to uniquely identify the log file.<br><br>* RuleID: Use both the collection rule ID and log file ID to uniquely identify the log file.<br><br>* TopicIDRuleName: Uniquely identify log files using log topic ID, collection rule name, and log file ID |


<span id="logtemplate"></span>
### LogTemplate


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |`Nginx` |Log template type. Supported types:<br><br><br>* Nginx: Nginx log template type. |
|Format |String |`log_format main '$remote_addr - $remote_user [$time_local] "$request" $request_time $request_length $status $body_bytes_sent "$http_referer" "$http_user_agent"';` |Log template format. |


<span id="filterkeyregex"></span>
### FilterKeyRegex


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Key |String |`__content__` |Name of the filter field |
|Regex |String |`.*ERROR.*` |The log content of the filtered fields must match the regular expression. |


<span id="kubernetesrule"></span>
### KubernetesRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|LabelTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to add Kubernetes Labels as log tags to the raw log data. If enabled, TLS will add Kubernetes Pod Label related fields to the logs. If you set multiple key\-value pairs, multiple fields are added. For example, if you set the key to source and the value to data_source, and the Pod has the label `source=DC`, a new field `__tag__data_source__: DC` will be added to the log. |
|PodNameRegex |String |`.*test.*` |Pod name is used to specify the container to be collected. If the Pod name is not specified, all containers will be collected. Pod names support regular expression matching. For example, set the Pod name to `^(http.*)$` to collect all containers under Pods starting with "http." |
|WorkloadType |String |`Deployment` |Specify the container for collection based on workload type. Only one type can be selected. If no type is specified, containers of all types are collected. Supported workload types:<br><br><br>* Deployment: Stateless workload<br><br>* StatefulSet: Stateful workload<br><br>* DaemonSet: Daemon process<br><br>* Job: Task<br><br>* CronJob: Scheduled SQL task |
|AnnotationTag |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |This feature determines whether to set Kubernetes Annotation to log tags and add it into the raw log data. If enabled, TLS will add Kubernetes Pod annotation fields to the logs. If you set multiple key\-value pairs, multiple fields are added. If you set the key to "sink" and the value to "data_sink", and the Pod has an annotation `sink=ck`, a new field `__tag__data_sink__: ck` will be added to the log. |
|WorkloadNameRegex |String |`.*test.*` |By configuring the workload name, you can specify the container to collect. If no workload name is specified, all containers are collected. Workload names support regular expression matching. For example, if you set the workload name to `^(http.*)$`, all containers under workloads starting with http will be collected. |
|NamespaceNameRegex |String |`.*test.*` |Name of the Kubernetes namespace to be collected. If no Namespace is specified, all containers will be collected. Namespace names support regular expression matching. For example, setting the Namespace name to `^(tcp\|udp)$` will collect all containers in the `tcp` and `udp` namespaces. |
|ExcludePodLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The Pod Label denylist is used to specify which containers should not be collected. If the denylist is disabled, all containers are collected. If you need to set a Pod Label denylist, the key field is required, while the value field is optional.<br><br><br>* If the value field is empty, all containers with the specified key in the Pod Label will be excluded from collection.<br><br>* If the value field is not empty, only containers with the specified key and a value that matches will be excluded from collection. The value field supports regular expressions. For example, if you set key to module and value to `^(tcp\|udp)$`, containers with module:`tcp` and module:`udp` in the Pod Label will not be collected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship between multiple Key\-Value pairs is <code>OR</code>. That is to say, any Pod Label that matches any Key\-Value pair will be excluded from collection.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling the Pod Label denylist, keys can not be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches strings that start with http.</div><br> |
|IncludePodLabelRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |The Pod Label allowlist is used to specify the containers to be collected. If the Pod Label allowlist is not enabled, all containers will be collected. If you need to set the Pod label allowlist, the key field is required.<br><br><br>* If the value is empty, all containers with the key in the Pod label are collected.<br><br>* If the value is not empty, only containers that match the key and the value in Pod Label are collected. Regular expressions are supported. The value supports regular expressions. For example, if you set the key to module and set the value to `^(tcp\|udp)$`, it means only containers with Pod labels module:`tcp` and module:`udp` are collected.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship between multiple key\-value pairs is logical <code>OR</code>. If the Pod label matches any key\-value pair, it will be collected.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling the Pod label allowlist, duplicate keys are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches any string beginning with http.</div><br> |
|EnableAllLabelTag |Boolean |`true` |This feature determines whether to add all Kubernetes labels as log tags to the raw log data. When enabled, TLS will add all related Kubernetes Pod label fields to logs. For example, if a Pod contains the labels `source=DC` and `destination=CS`, the log will include new fields `__tag__source__: DC` and `__tag__destination__: CS`. |
|ExcludePodAnnotationRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Pod Annotation denylist specifies containers that are excluded from collection. If you need to set a Pod Annotation denylist, the key is required and the value is optional.<br><br><br>* If the value is empty, all containers in Pods with the specified key in their Pod Annotation will be excluded.<br><br>* If the value is not empty, only containers in Pods with the specified key and a value matching the specified value in their Pod Annotation will be excluded. By default, value uses string matching. Containers only match if the value is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with `$`, it uses regular expression match. For example, if you set key as app and value as ^(test1\|test2)$, it matches containers within Pods whose Annotation contains app:test1 or app:test2.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship among multiple Key\-Value pairs is logical <strong>OR</strong>. Pods will be included for collection as long as their annotations match any Key\-Value pair.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When enabling Pod Annotation denylist, duplicate Keys are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches strings that start with http.</div><br> |
|IncludePodAnnotationRegex |JSON Map |`{ "Key1": "Value1", "Key2": "Value2" }` |Pod annotation allowlist is used to specify the containers to be collected. If you need to set a Pod annotation allowlist, the key field is required and the value field is optional.<br><br><br>* If the value field is empty, all containers in Pods with the specified key in their annotations will match.<br><br>* If the value field is not empty, containers in Pods whose annotation contains the key and the Key's value matches the value will match. By default, value uses string matching. Containers only match if the value is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with `$`, it uses regular expression match. For example, set the key as "app" and set the value as ^(test1\|test2)$, and then the containers in Pods whose annotation contains app:test1 or app:test2 will match.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The logical relationship among multiple Key\-Value pairs is logical <strong>OR</strong>. Pods will be included for collection as long as their annotations match any Key\-Value pair.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the Pod Annotation allowlist is enabled, the key must not be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For fuzzy regular expression matching, you must add <code>.*</code>. For example, <code>^(http.*)$</code> matches any string that starts with http.</div><br> |


<span id="plugin"></span>
### Plugin


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|processors |Array of JSON Map |`{ "processors":[ { "json":{ "field":"__content__", "trim_keys":{ "mode":"all", "chars":"#" }, "trim_values":{ "mode":"all", "chars":"#" }, "allow_overwrite_keys":true, "allow_empty_values":true } } ] }` |LogCollector plugin. For the list of supported plugins and their parameter descriptions, see [LogCollector plugin overview](https://docs.byteplus.com/en/docs/tls/plug-ins_Overview). |


<span id="advanced"></span>
### Advanced


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|CloseEOF |Boolean |`true` |After reading to the end of the log file, release the handle of the log file. The default value is false. |
|CloseRemoved |Boolean |`true` |After the log file is removed, decide whether to release its file handle. The default value is false. |
|CloseRenamed |Boolean |`true` |Whether to release the handle of the log file after it is renamed. The default value is false. |
|CloseTimeout |Integer |`1800` |Maximum duration for monitoring log files with LogCollector. Measured in seconds. The default value is 0 seconds, which means there is no time limit for LogCollector to monitor log files. LogCollector starts timing when it begins monitoring a log file. When the specified duration is exceeded, it immediately releases the file handle and ends monitoring, even if the log file has not been completely read. |
|CloseInactive |Integer |`10` |Wait time to release the log file handle. If no new logs are written within the specified time, the log file handle is released. Unit: seconds. Range: 1–300 seconds. Default: 60 seconds. |
|NoLineTerminatorEOFMaxTime |Integer |`5` |Maximum waiting time when LogCollector does not read a newline character. Unit: seconds. Default: 5s. LogCollector starts timing when it begins reading the log file. If no newline is detected within the specified period, the logs in the buffer will be sent. If the interval between file writes is long, a complete log entry may be split and written to disk separately. Adjust this setting based on your log write intervals. |


<span id="shardhashkey"></span>
### ShardHashKey


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|HashKey |String |`3C` |The HashKey of the log group is used to specify the shard for writing logs in the current log group. The value range for this parameter is [00000000000000000000000000000000\-ffffffffffffffffffffffffffffffff). |


<span id="parsepathrule"></span>
### ParsePathRule


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Keys |Array of String |`["instance-id","pod-name"]` |Field name list. TLS will use regular expressions (Regex) to parse path samples (PathSample) into multiple fields. Keys specify the name for each field.<br><br><br>* You can configure up to 100 field names.<br><br>* Field names can not be empty or duplicated. |
|Regex |String |`/var/logs/([a-z]*)_any_([a-z]*)/test.log` |Regular expression used to extract path fields. It must match the sample collection path; otherwise, extraction fails. |
|PathSample |String |`/var/logs/instanceid_any_podname/test.log` |Sample collection path for actual scenarios.<br><br><br>* The collection path sample must be an absolute path.<br><br>* The path sample must not contain wildcards `*`, `?`, or `**`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/DescribeHostGroup?HostGroupId=faf6d************ HTTP/1.1
Content-Type: application/json
```


<span id=".6L-U5Zue56S65L6L"></span>
## Return example

For example, in collection mode, the entire line is treated as full text.

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "HostGroupHostsRulesInfo": {
        "HostGroupInfo": {
            "HostGroupId": "0fda*************",
            "HostGroupName": "mgn1",
            "HostGroupType": "IP",
            "HostCount": 2,
            "NormalHeartbeatStatusCount": 1,
            "AbnormalHeartbeatStatusCount": 1,
            "RuleCount": 1,
            "AutoUpdate": true,
            "UpdateStartTime": "00:00",
            "UpdateEndTime": "02:00",
            "AgentLatestVersion": "1.0.8",
            "CreateTime": "2021-08-18T13:32:23Z",
            "ModifyTime": "2021-08-18T13:32:23Z",
            "ServiceLogging": true,
            "IamProjectName": "default"
        },
        "HostInfos": [
            {
                "Ip": "127.0.0.1",
                "LogCollectorVersion": "logcollector-1.0.3",
                "HeartbeatStatus": 0
            },
            {
                "Ip": "127.0.0.2",
                "LogCollectorVersion": "logcollector-1.0.3",
                "HeartbeatStatus": 1
            }
        ],
        "RuleInfos": [
            {
                "TopicId": "faf6*********",
                "TopicName": "tn1",
                "RuleId": "faf6*********",
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
                    },
                    "TailFiles": false
                },
                "CreateTime": "2021-08-18T13:32:23Z",
                "ModifyTime": "2021-08-18T13:32:23Z"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

The following table lists error codes related to the interface and business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) documentation.


|**HTTP status code** |**Error Code** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Invalid parameter. |
|404 |RuleNotExist |Rule %s does not exist |Collection configuration does not exist. |
|404 |HostNotExist |Host of HostGroup %s does not exist |The machine does not exist. |
|404 |TopicNotExist |Topic %s does not exist |The log topic does not exist. |
|404 |HostGroupNotExist |HostGroup %s does not exist |Host group does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |
