---
title: "CreateRule"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-createrule"
---

Call the CreateRule interface to create a collection configuration.

<span id="usage-notes"></span>
## Usage notes


* Before creating a collection configuration, please make sure the following operations are completed:

   * A project and topic have been created.

   * A host group has been created, and the server heartbeat status of the host group is normal.

   * The latest version of LogCollector has been installed on the data source server.

* The call frequency limit of this interface is 20 times/s. An error of ExceedQPSLimit will be reported if the frequency limit is exceeded.

* The **Advanced** parameter is used for extended configuration. After enabling extended configuration, you can customize the advanced behavior of LogCollector, such as the timing of releasing file handles.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If multiple timings for releasing handles are specified, the handle is immediately released and log file monitoring is terminated as soon as any timing requirement is met.   </div>
   

<span id="request-syntax"></span>
## Request syntax


* Request Method: **POST**

* Request URL: **https://tls\-{Region}.bytepluses.com/CreateRule**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|TopicId |String |True |`4a9*********` |The ID of the topic to which the collection configuration belongs. |
|RuleName |String |True |`testname` |The name of the collection configuration. For naming rules, please refer to the [Resource Naming limit](https://docs.byteplus.com/docs/tls/Limits#resource-naming-limit).<br><br>The name must be unique in a topic. |
|Paths |Array of String |False |`/` |The collection path list.<br><br><br>* A maximum of 10 collection paths can be created.<br><br>* Collection paths must be specified as absolute paths, relative paths are not currently supported.<br><br>* When `InputType=0` or `InputType=2`, the collection path supports full match and wildcard pattern matching, the wildcard only supports `**`, `*`, `?`, but only one `**` wildcard can be configured at most.<br><br>* When I`nputType=1`, there is no need to configure the collection path list. |
|ExcludePaths |Array of [ExcludePath](https://docs.byteplus.com/en/docs/38/17245#excludepath) |False |`/` |The blacklist of file paths.<br><br><br>* A maximum of 10 paths can be created.<br><br>* When `InputType=0` or `InputType=2`:<br><br>   * When `Type` is `Path`, Value represents a directory. It supports full matching and wildcard pattern matching, and the wildcard only supports `*`, `?`, and does not support `**` wildcard.<br><br>   * When `Type` is `File`, Value represents a file name. It supports full matching and wildcard pattern matching, and the wildcard supports `**`, `*`, `?`, but only one `**` wildcard can be configured at most.<br><br>* When `InputType=1`:<br><br>   The configuration of the path blacklist is not allowed. |
|LogType |String |False |`delimiter_log` |The collection modes.<br><br><br>* minimalist_log: (Default) collects logs in single line full text mode.<br><br>* json_log: collects logs in JSON mode.<br><br>* delimiter_log: collects logs in delimiter mode.<br><br>* multiline_log: collects logs in multi\-line full text mode.<br><br>* fullregex_log: collects logs in complete regex mode. |
|ExtractRule |Object of [ExtractRule](https://docs.byteplus.com/en/docs/38/17245#extractrule) |False |`/` |The log extraction rules.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>LogType</code> is specified as a type other than minimalist_log or json_log, this parameter is required.</div><br> |
|UserDefineRule |Object of [UserDefineRule](https://docs.byteplus.com/en/docs/38/17245#userdefinerule) |False |`/` |The user\-defined collection rules. |
|LogSample |String |False |`/` |The sample log.<br><br><br>* The maximum length of the sample log is 3000 characters.<br><br>* The content of the sample log must match the collection pattern.<br><br>   * Single\-line full\-text mode and JSON mode do not need to fill in the sample log.<br><br>   * Other modes must fill in the sample log, and the content of the sample log must match the collection pattern. |
|InputType |Integer |False |`2` |The collection types.<br><br><br>* 0: (Default) Host machine log files.<br><br>* 1: Kubernetes container standard output.<br><br>* 2: Log files within Kubernetes. container. |
|ContainerRule |Object of [ContainerRule](https://docs.byteplus.com/en/docs/38/17245#containerrule) |False |`/` |The container collection rules. |


<span id="excludepath"></span>
### ExcludePath


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Type |String |False |`Path` |The types of collection paths.<br><br><br>* File: File name<br><br>* Path: Directory |
|Value |String |False |`/accesslog` |The collection path. Must be specified as an absolute path.<br><br><br>* When `Type` is `Path`, Value represents a directory.<br><br>* When `Type` is `File`, Value represents a file name. |


<span id="extractrule"></span>
### ExtractRule


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Keys |Array of String |False |```Plain Text```<br>```[```<br>```"time",```<br>```"",```<br>```"level",```<br>```"message"```<br>```]```<br> |The list of log field.<br><br><br>* Valid only when `LogType` is `delimiter_log` or `fullregex_log`.<br><br>* Supports the configuration of up to 100 field names.<br><br>* When `LogType` is `delimiter_log`, duplicate field names cannot be configured, and all field names cannot be specified as empty.<br><br>* When `LogType` is `fullregex_log`, duplicate field names cannot be configured, and the field name cannot be specified as empty. |
|Quote |String |False |`"` |The quota. The content wrapped by quota will not be separated but will be parsed as a complete field. It is only valid when `LogType` is `delimiter_log`. |
|TimeKey |String |False |`request_time` |The field name of the log time field. If the specified time field in the log is used as the log timestamp, you need to fill in the `TimeKey` and `TimeFormat`.<br><br>`TimeKey` and `TimeFormat` must appear in pairs. |
|LogRegex |String |False |```Plain Text```<br>```[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)```<br>``````<br> |The entire log needs to match the regular expression.<br><br><br>* Valid only when the collected log type is `fullregex_log`.<br><br>* Must be a legal regular expression. |
|TimeZone |String |False |`%Y-%m-%dT%H:%M:%S,%f` |The time zone, supports host time zone (default) and custom time zone. The custom time zone supports GMT and UTC.<br><br><br>* GMT format: GMT+08:00.<br><br>* UTC format: Asia/Shanghai. |
|Delimiter |String |False |`#` |The log delimiter. Valid only when `LogType` is `delimiter_log`. |
|BeginRegex |String |False |`[(\d+-\d+-\w+:\d+:\d+,\d+)]\s[(\w+)]\s(.*)` |The regular expression that needs to match the first line of the log.<br><br><br>* It is only valid when LogType is either `multiline_log` or `fullregex_log`.<br><br>* It must be a valid regular expression. |
|TimeFormat |String |False |`%Y-%m-%dT%H:%M:%S,%f` |The format for parsing the time field. If a specified time field in the log is used as the log timestamp, you need to fill in `TimeKey` and `TimeFormat`.<br><br><br>* TimeKey and `TimeFormat` must appear in pairs.<br><br>* For how to configure the time format, please refer to [Time Format](https://docs.byteplus.com/docs/tls/time_format). |
|LogTemplate |Object of [LogTemplate](https://docs.byteplus.com/en/docs/38/17245#logtemplate) |False |`{ "Type": "Nginx", "Format": "format main '$remote_addr - $remote_user [$time_local] \"$request\" $request_time $request_length $status $body_bytes_sent \"$http_referer\" \"$http_user_agent\"';" }` |The automatically extract log fields according to the specified log template. |
|UnMatchLogKey |String |False |`LogParseFailed` |When the upload of the parsed log fails, the key name of the failed parsed log is required.<br><br>&nbsp;<br><br>`UnMatchUpLoadSwitch=true` and `UnMatchLogKey` must appear in pairs. |
|FilterKeyRegex |Array of [FilterKeyRegex](https://docs.byteplus.com/en/docs/38/17245#filterkeyregex) |False |`/` |The filter rules list.<br><br><br>* When `LogType` is `minimalist_log` or `multiline_log`, a maximum of 1 filter rule can be configured, and the name of the filter field key must be **content**.<br><br>* When `LogType` is `delimiter_log`, `json_log` or `fullregex_log`, a maximum of 5 filter rules can be configured, and the name of the filter field key cannot be repeated or empty. The regular expression that the log content of the filter field needs to match must be a valid regular expression, and the length limit is 256 characters. |
|TimeExtractRegex |String |False |`[0-9]{0,2}\/[0-9a-zA-Z]+\/[0-9:,]+` |The regular expression for extracting time, used to extract the time value in the `TimeKey` field and parse it into the corresponding collection time. |
|UnMatchUpLoadSwitch |Boolean |False |`true` |Whether to upload the logs of failed analysis. `UnMatchUpLoadSwitch=true` and `UnMatchLogKey` must appear in pairs.<br><br><br>* true: Upload the logs of failed analysis.<br><br>* false: Do not upload the logs of failed analysis. |
|EnableNanosecond |Boolean |False |`true` |Whether to enable the function of nanosecond precision time. After enabling it, the time with nanosecond precision will be parsed and reported when parsing the log time.<br><br><br>* true: Enable nanosecond precision time.<br><br>* false: Disable nanosecond precision time. |


<span id="userdefinerule"></span>
### UserDefineRule


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Fields |JSON Map |False |`{"ClusterID":"dabaad5f-7a10-4771-b3ea-d821f73e****"}` |Add constant fields to the log. The constant fields must follow these restrictions:<br><br><br>* Supports uploading up to 5 constant fields.<br><br>* The field name must not be duplicated or empty. The length limit is 1 to 128 characters, including English letters, numbers, and special characters (`-_./`), and it cannot start with an underscore.<br><br>* The field value must not be empty, with a maximum length of 512 KiB. |
|Plugin |Object of [Plugin](https://docs.byteplus.com/en/docs/38/17245#plugin) |False |`{"processors":[{"json":{"field":"__content__","trim_keys":{"mode":"all","chars":"#"},"trim_values":{"mode":"all","chars":"#"},"allow_overwrite_keys":true,"allow_empty_values":true}` |The configuration of LogCollector plugin. After enabling the plugin configuration, one or more LogCollector handler plugins can be added to parse logs with complex or unstable structure. |
|Advanced |Object of [Advanced](https://docs.byteplus.com/en/docs/38/17245#advanced) |False |`{ "CloseInactive": 10 }` |The extension configuration for LogCollector. |
|RawLogKey |String |False |`__raw__` |The original log field name.<br><br>&nbsp;<br><br>Only takes effect when `EnableRawLog` is set to `true`. The default `RawLogKey` is `__raw__`, indicating that the original log data will be encapsulated in the `__raw__` field and uploaded to Torch Log Service together with the parsed log data. |
|TailFiles |Boolean |False |`true` |The LogCollector collection policy, which specifies whether LogCollector collects incremental logs or full logs. The default is false, indicating that it collects full logs.<br><br><br>* true: Incremental collection. When LogCollector collects logs, it only collects the newly added content within the file. When new logs are written within the monitored log file, it triggers the LogCollector to perform log collection.<br><br>   * For log files being collected for the first time, LogCollector will automatically determine the collection point based on the incremental threshold `TailSizeKb` you specify.<br><br>      * If the size of the new file does not exceed the specified incremental threshold, the first collection will start from the beginning of the new file.<br><br>      * If the size of the new file exceeds the specified incremental threshold, the first collection will start from the position obtained by subtracting the incremental threshold from the end of the new file, that is, only the incremental logs will be collected..<br><br>   * For log files not being collected for the first time, LogCollector determines the collection point based on the Checkpoint and continues collection.<br><br>* false: (default) Full collection. LogCollector starts collecting logs from the beginning of each document, at this time LogCollector will collect historical log data. |
|HostnameKey |String |False |`hostname` |The field name of `hostname`.<br><br>&nbsp;<br><br>Only needs to be set when `EnableHostname` is `true`. |
|EnableRawLog |Boolean |False |`true` |Whether to upload the original log.<br><br><br>* true: Upload the original log.<br><br>* false: (default) Do not upload the original log. |
|ShardHashKey |Object of [ShardHashKey](https://docs.byteplus.com/en/docs/38/17245#shardhashkey) |False |`{ "HashKey": "3C" }` |Rules for routing log shard.<br><br><br>* If this parameter is not set, it means that the default load balancing mode is used to write logs, and the data packet will be written to any currently available Shard.<br><br>* Setting this parameter means that the HashKey routing shard mode is used when collecting logs, and Torch Log Service will write data to the shard containing the specified Key value. |
|ParsePathRule |Object of [ParsePathRule](https://docs.byteplus.com/en/docs/38/17245#parsepathrule) |False |`{ "PathSample": "/data/nginx/log/dabaad5f-7a10/tls/app.log", "Regex": "\\/data\\/nginx\\/log\\/(\\w+)-(\\w+)\\/tls\\/app\\.log", "Keys": ["instance-id", "pod-name"] }` |Analyze the rules for the collection path. After setting the rules, fields will be extracted from the collection path through the regular expressions specified in the rules, and added to the log data as metadata.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When collecting container standard output, this parameter cannot be specified.</div><br> |
|EnableHostname |Boolean |False |`true` |Whether to upload the hostname field, which is off by default.<br><br><br>* True: Add a field in the original log to record the hostname of the log source. At this time, the hostname field name should be specified through the `HostnameKey`.<br><br>* False: (default) Do not add the hostname field. |
|HostGroupLabelKey |String |False |`host_group_label` |The field name used to store machine group Label information. |
|EnableHostGroupLabel |Boolean |False |`true` |Whether to upload the label information of the machine group to torch Log Service.<br><br><br>* true: LogCollector will upload the label information of the machine group to the specified field. You can specify the field name in the **HostGroupLabelKey** parameter.<br><br>* false (default): Do not upload machine group label information. |
|TailSizeKb |Integer |False |`1024` |The backtracking threshold for incremental collection, with the unit of KiB.<br><br>When the collection policy of LogCollector is incremental collection, for the log files being collected for the first time:<br><br><br>* If the size of the new log file does not exceed the value of `TailSizeKb`, the first collection will start from the beginning of the new log file.<br><br>* If the size of the new log file exceeds the value of `TailSizeKb`, the first collection will start from the position after subtracting the value of `TailSizeKb` from the end of the new log file. |
|IgnoreOlder |Integer |False |`7` |Ignore log files that have not been updated for how many hours. The unit is hours. |
|MultiCollectsType |String |False |`RuleID` |Allow collecting log files multiple times.<br><br><br>* Empty: Use the log file ID (including file inode, device, and checksum of the first N bytes) to uniquely identify the log file.<br><br>* RuleID: Use the collection rule ID and the log file ID to uniquely identify the log file.<br><br>* TopicIDRuleName: Use the log topic ID, collection rule name, and log file ID to uniquely identify the log file. |


<span id="containerrule"></span>
### ContainerRule


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|EnvTag |JSON Map |False |```Plain Text```<br>```{```<br>```            "Key1": "Value1",```<br>```            "Key2": "Value2"```<br>```        }```<br> |Whether to add environment variables as log tags to the original log data. When enabled, Torch Log service will add related fields of container environment variables in the log. When setting multiple key\-value pairs, it means adding multiple fields. For example, set `Key` as `source`, set `Value` as `data_source`, if the container contains the environment variable `source=DC`, then a new field `__tag__data_source__: DC` will be added to the log. |
|Stream |String |False |`all` |The collection type.<br><br><br>* stdout: Collect the standard output stdout of the container.<br><br>* stderr: Collect the standard error stderr of the container.<br><br>* all: Collect both the standard output stdout and the standard error stderr of the container simultaneously. |
|KubernetesRule |Object of [KubernetesRule](https://docs.byteplus.com/en/docs/38/17245#kubernetesrule) |False |`{ "NamespaceNameRegex": ".*test.*", "WorkloadType": "Deployment", "WorkloadNameRegex": ".*test.*", "IncludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "ExcludePodLabelRegex": { "Key1": "Value1", "Key2": "Value2" }, "PodNameRegex": ".*test.*", "LabelTag": { "Key1": "Value1", "Key2": "Value2" } }` |The collection rules for kubernetes containers. |
|ContainerNameRegex |String |False |`.*test.*` |The name of the container to be collected. If the container name is not specified, it means all containers in the host group are collected. Regular matching is supported, for example, setting the container name to `^(container-test)$` means collecting all containers named `container-test`. |
|ExcludeContainerEnvRegex |JSON Map |False |```Plain Text```<br>```{```<br>```            "Key1": "Value1",```<br>```            "Key2": "Value2"```<br>```        }```<br> |The container environment variable blacklist is used to specify the containers whose data you want to exclude. When the blacklist is not enabled, it means that all containers are collected. If the container environment variable blacklist is enabled, the `Key` is mandatory and the `Value` is optional.<br><br><br>* If `Value` is empty, it means that all containers that contain the `Key` in the container environment variables are not collected.<br><br>* If `Value` is not empty, it means that only containers with matched key\-value pairs are excluded during collection, that is, only containers that contain the `Key` in the container environment variables and whose value matches the `Value` are excluded. `Value` supports regular matching, for example, set `Key` to module, and set `Value` to `^(tcp\|udp)$`, which means that containers containing `module:tcp`, `module:udp` in the container environment variables are not collected.<br><br>* The logical relationship between multiple key\-value pairs is logical or, that is, as long as the container environment variables meet any key\-value pair, they will be excluded from the collection range.<br><br>* When the container environment variable blacklist is enabled, the `Key` cannot be duplicated. |
|IncludeContainerEnvRegex |JSON Map |False |```Plain Text```<br>```{```<br>```            "Key1": "Value1",```<br>```            "Key2": "Value2"```<br>```        }```<br> |The container environment variables whitelist is used to specify the containers whose data you want to collect. When the whitelist is not enabled, it means that all containers are designated for collection. When the whitelist of container environment variables is enabled, you need to fill in key\-value pairs. `Key` is required, and `Value` is optional.<br><br><br>* If `Value` is empty: Collect all containers that contain `Key` in the container environment variables.<br><br>* If `Value` is not empty: Only collect containers that contain `Key` in the container environment variables and its value matches `Value`. `Value` supports regular matching. For example, set `Key` to module, and set `Value` to `^(tcp\|udp)$`, which means only collect containers that contain `module:tcp`, `module:udp` in the container environment variables.<br><br>* The logical relationship between multiple key\-value pairs is logical or, that is, as long as the container environment variables meet any key\-value pair, they will be listed as the collection range.<br><br>* When the whitelist of container environment variables is enabled, Key cannot be repeated. |
|ExcludeContainerLabelRegex |JSON Map |False |```Plain Text```<br>```{```<br>```            "Key1": "Value1",```<br>```            "Key2": "Value2"```<br>```        }```<br> |The container label blacklist is used to is used to specify the containers whose data you want to exclude. When the blacklist is not enabled, it means that all containers will be collected. If the container label blacklist is enabled, then the `Key` is mandatory, and the Value is optional.<br><br><br>* If the Value is empty, it means that all containers that contain the `Key` in the Container Label will not be collected.<br><br>* If the Value is not empty, it means that only containers that match the key\-value pair will be excluded during collection, only containers that contain the `Key` in the Container Label and whose value matches the Value will be excluded. The Value supports regular matching, for example, if the `Key` is set to `app`, and the Value is set to `^(test1\|test2)$`, it means that containers that contain `app:test1` and `app:test2` in the Container Label will not be collected.<br><br>* The logical relationship between multiple key\-value pairs is a logical or, as long as the container label meets any one of the key\-value pairs, it will be excluded from the collection range.<br><br>* When the Container Label Blacklist is enabled, the Key cannot be duplicated. |
|IncludeContainerLabelRegex |JSON Map |False |`{ "Key1": "Value1", "Key2": "Value2" }` |The container label whitelist is used to specify the containers whose data you want to collect. When the whitelist is not enabled, all containers are collected. When the container label whitelist is enabled, you need to fill in the key\-value pairs. The `Key` is mandatory, and the `Value` is optional.<br><br><br>* If `Value` is empty: Collect all containers that contain the Key in the Container Label.<br><br>* If `Value` is not empty: Only collect containers that contain the Key in the Container Label and its value matches the `Value`. `Value` supports regular matching. For example, setting the Key as "app" and the `Value` as `^(test1\|test2)$` means only collecting containers that contain `app:test1` or `app:test2` in the container label.<br><br>* The logical relationship between multiple key\-value pairs is logical or, that is, as long as the Container Label meets any key\-value pair, it will be listed as the collection range.<br><br>* When the Container Label whitelist is enabled, the Key cannot be repeated. |


<span id="logtemplate"></span>
### LogTemplate


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Type |String |False |`Nginx` |The types of log templates.<br><br><br>* Nginx: Log template of the Nginx type. |
|Format |String |False |`log_format main '$remote_addr - $remote_user [$time_local] "$request" $request_time $request_length $status $body_bytes_sent "$http_referer" "$http_user_agent"';` |The format of a log template. |


<span id="filterkeyregex"></span>
### FilterKeyRegex


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |False |`__content__` |The name of the filter field. |
|Regex |String |False |`.*ERROR.*` |The regular expression required to match the log content of the filtered field. |


<span id="plugin"></span>
### Plugin


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|processors |Array of JSON Map |False |```Plain Text```<br>```{```<br>```            "processors":[```<br>```                {```<br>```                    "json":{```<br>```                        "field":"__content__",```<br>```                        "trim_keys":{```<br>```                            "mode":"all",```<br>```                            "chars":"#"```<br>```                        },```<br>```                        "trim_values":{```<br>```                            "mode":"all",```<br>```                            "chars":"#"```<br>```                        },```<br>```                        "allow_overwrite_keys":true,```<br>```                        "allow_empty_values":true```<br>```                    }```<br>```                }```<br>```            ]```<br>```        }```<br> |The LogCollector plugin. For a list of supported plugins and parameter descriptions, please refer to [LogCollector Plugin Overview](https://docs.byteplus.com/en/docs/tls/plug-ins_Overview). |


<span id="advanced"></span>
### Advanced


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|CloseEOF |Boolean |False |`true` |After reading to the end of the log file, whether to release the handle of the log file. The default is false. |
|CloseRemoved |Boolean |False |`true` |After the log file is removed, whether to release the handle of the log file. The default is false. |
|CloseRenamed |Boolean |False |`true` |After the log file is renamed, whether to release the handle of the log file. The default is false. |
|CloseTimeout |Integer |False |`1800` |The LogCollector monitors the maximum duration of log files. The unit is in seconds, and the default is 0 seconds, which means there is no limit to the duration of the LogCollector's monitoring of log files.<br><br>The LogCollector starts timing when it begins to monitor log files. After exceeding the specified duration, regardless of whether the log file has been read completely, it immediately releases the handle of the log file and ends monitoring. |
|CloseInactive |Integer |False |`10` |The waiting time to release the log file handle. When no new logs are written to the log file beyond the specified time, the handle of this log file is released.<br><br>The unit is in seconds, the value range is 1 to 300 seconds, and the default is 60 seconds. |
|NoLineTerminatorEOFMaxTime |Integer |False |`5` |When LogCollector does not encounter a newline character, the maximum waiting duration is in seconds, with a default of 5 seconds. The timer starts as soon as LogCollector begins reading the log file content. If no newline character is read within the specified duration, the logs in the buffer will be sent. When there is a significant delay in log disk writing, a complete log entry might be split into two parts. You can adjust this parameter based on the disk writing interval of your logs. |


<span id="shardhashkey"></span>
### ShardHashKey


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|HashKey |String |False |`3C` |The HashKey of the log group, used to specify the shard into which the current log group is to be written. The value range for this parameter is [00000000000000000000000000000000\-ffffffffffffffffffffffffffffffff). |


<span id="parsepathrule"></span>
### ParsePathRule


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Keys |Array of String |False |`["instance-id","pod-name"]` |The field name list. Torch Log service will parse the PathSample into multiple fields according to the regular expression, and Keys are used to specify the field name of each field.<br><br><br>* Up to 100 field names can be configured.<br><br>* The field name cannot be empty and cannot be repeated. |
|Regex |String |False |`/var/logs/([a-z]*)_any_([a-z]*)/test.log` |The regular expression used to extract the path field. It must match the collection path example, otherwise it cannot be successfully extracted. |
|PathSample |String |False |`/var/logs/instanceid_any_podname/test.log` |The examples of collection paths in real scenarios.<br><br><br>* The collection path example must be an absolute path.<br><br>* The path example cannot contain wildcards such as `*`, `?`, `**`. |


<span id="kubernetesrule"></span>
### KubernetesRule


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|LabelTag |JSON Map |False |```Plain Text```<br>```{```<br>```                "Key1": "Value1",```<br>```                "Key2": "Value2"```<br>```            }```<br> |After setting the labels, Torch Log service will add new fields related to kubernetes pod labels in the logs. When multiple key\-value pairs are set, it means adding multiple fields. For example, if the `Key` is set to `source`, and the `Value` is set to `data_source`, assuming the Pod contains the Label `source=DC`, a new field `__tag__data_source__: DC` will be added to the log. |
|PodNameRegex |String |False |`.*test.*` |The name of the pod is used to specify the containers to be collected. When the pod name is not specified, it means to collect all containers. The pod name supports regular matching. For example, setting the pod name as `^(http.*)$` means to collect all containers under the pod starting with http. |
|WorkloadType |String |False |`Deployment` |Specify the type of container to be collected by the type of workload, and only one type is supported. When the type is not specified, it means collecting all types of containers. The supported workload types are as follows:<br><br><br>* Deployment: Stateless workload<br><br>* StatefulSet: Stateful workload<br><br>* DaemonSet: Daemon<br><br>* Job: Task<br><br>* CronJob: Scheduled task |
|AnnotationTag |JSON Map |False |```Plain Text```<br>```{```<br>```                "Key1": "Value1",```<br>```                "Key2": "Value2"```<br>```}```<br> |After setting the kubernetes annotations are added as log tags to the original log data. Torch Log service will add related fields of kubernetes pod annotations in the log. When setting multiple key\-value pairs, it means adding multiple fields. For example, set `Key` as `sink`, set `Value` as `data_sink`, suppose pod contains Annotation `sink=ck`, then a new field `__tag__data_sink__: ck` will be added in the log. |
|WorkloadNameRegex |String |False |`.*test.*` |Specify the containers to be collected by the name of the workload. When the workload name is not specified, it means to collect all containers. The workload name supports regular matching. For example, setting the workload name to `^(http.*)$` means to collect all containers under the workload starting with http. |
|NamespaceNameRegex |String |False |`.*test.*` |The name of the kubernetes namespace to be collected. If the namespace is not specified, it means all containers are collected. The name supports regular expression matching. For example, setting the name to `^(tcp\|udp)$` means collecting all containers under the `tcp` and `udp` namespaces. |
|ExcludePodLabelRegex |JSON Map |False |```Plain Text```<br>```{```<br>```                "Key1": "Value1",```<br>```                "Key2": "Value2"```<br>```            }```<br> |Specify the containers not to be collected by the pod label blacklist. If not enabled, all containers will be collected. If you need to set a pod label blacklist, `Key` is required, `Value` is optional.<br><br><br>* If `Value` is empty, it means that all containers containing `Key` in the Pod Label are excluded during collection.<br><br>* If `Value` is not empty, it means that only containers containing `Key` in the pod label and whose value matches `Value` are excluded during collection. `Value` supports regular expression matching, for example, setting `Key` to module, and setting `Value` to `^(tcp\|udp)$`, means that containers containing module:`tcp`, module:`udp` in the pod label are not collected.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between multiple key\-value pairs is logical or, that is, as long as the pod label meets any pair of key values, it will be excluded from the collection range.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the pod label blacklist is enabled, the <code>Key</code> cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When performing regular fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> matches means matching characters starting with <code>http</code>.</div><br> |
|IncludePodLabelRegex |JSON Map |False |```Plain Text```<br>```{```<br>```                "Key1": "Value1",```<br>```                "Key2": "Value2"```<br>```            }```<br> |The pod label whitelist is used to specify the containers whose data you want to collect. When the pod label whitelist is not enabled, it means that all containers are collected. If you need to set up a pod label whitelist, the key is required:<br><br><br>* If `Value` is empty, it means that all containers that include key in the pod label are collected.<br><br>* If `Value` is not empty, it means that only containers that contain key in the pod label and whose value matches `Value` are collected, and regular matching is supported. `Value` supports regular matching, for example, set key to module, set `Value` to `^(tcp\|udp)$`, which means that only containers containing module:`tcp`, module:`udp` in the pod label are collected.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between multiple key\-value pairs is logical <code>or</code>, that is, as long as the pod label meets any key\-value pair, it will be listed as the collection range.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When enabling the pod label whitelist, key cannot be duplicated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When performing regular fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> matches means matching characters starting with <code>http</code>.</div><br> |
|EnableAllLabelTag |Boolean |False |`true` |Whether to add all Kubernetes labels as log tags to the raw log data. When enabled, TLS will add fields related to all labels in the Kubernetes Pod to the logs.<br><br>For example, if a Pod contains the labels `source=DC` and `destination=CS`, the log will add the fields `__tag__source__: DC` and `__tag__destination__: CS`. |
|ExcludePodAnnotationRegex |JSON Map |False | |The Pod annotation blacklist is used to specify containers that will not be collected. If you need to set the Pod annotation blacklist, then the `Key` is required, while the `Value` is optional.<br><br><br>* If the `Value` is empty, it means that all containers under the Pod whose Pod Annotation contains the `Key` will be excluded.<br><br>* If the `Value` is not empty, it means that only the containers under the Pod whose Pod Annotation contains the `Key` and whose value matches the `Value` will be excluded.<br><br>   The default for the `Value` is string matching, that is, only when the `Value` is exactly the same as the value of the Pod annotation will it match. However, if the value starts with `^` and ends with `$`, it is a regex expression match. For example, if the `Key` is set to `app` and the `Value` is set to `^(test1\|test2)$`, it means that it will match the containers under the Pod whose Pod Annotation contains `app:test1` or `app:test2`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between multiple Key\-Value pairs is <strong>OR</strong>, that is, as long as the Pod annotation conforms to any key\-value pair, it will be listed in the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When enabling the Pod annotation blacklist, the <code>Key</code> cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When performing regular fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> matches means matching characters starting with <code>http</code>.</div><br> |
|IncludePodAnnotationRegex |JSON Map |False | |The Pod annotation whitelist is used to specify the containers to be collected. If you need to set the Pod Annotation whitelist, the `Key` is required and the `Value` is optional.<br><br><br>* If the `Value` is empty, it means that all containers under the Pod whose Pod annotation contains the `Key` are matched.<br><br>* If the `Value` is not empty, it means that only the containers under the Pod whose Pod annotation contains the `Key` and whose value matches the `Value` are matched.<br><br>   The default for the `Value` is string matching, that is, only when the `Value` is exactly the same as the value of the Pod annotation will it match. If the value starts with `^` and ends with `$`, it is a regex expression match. For example, if the `Key` is set to `app` and the `Value` is set to `^(test1\|test2)$`, it means that it will match the containers under the Pod whose Pod Annotation contains `app:test1` or `app:test2`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between multiple Key\-Value pairs is 'OR', that is, as long as the Pod Annotation conforms to any key\-value pair, it will be listed in the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When enabling the Pod Annotation whitelist, the <code>Key</code> cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When performing regular fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> matches means matching characters starting with <code>http</code>.</div><br> |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).


|Name |Type |Example |Description |
|---|---|---|---|
|RuleId |String |`fa************` |The ID of the collection configuration. |


<span id="sample-request-1"></span>
## Sample Request 1

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
}
```


<span id="sample-response-1"></span>
## Sample Response 1

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-2"></span>
## Sample Request 2

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
    "LogType": "multiline_log",
    "ExtractRule": {
        "BeginRegex": "\\[([^]]+)].*",
        "FilterKeyRegex": [
            {
                "Key": "__content__",
                "Regex": ".*ERROR.*"
            }
        ]
    },
    "LogSample": "[2018-10-01T10:30:01,000] [INFO] java.lang.Exception: exception happened\n    at TestPrintStackTrace.f(TestPrintStackTrace.java:3)\n    at TestPrintStackTrace.g(TestPrintStackTrace.java:7)\n    at TestPrintStackTrace.main(TestPrintStackTrace.java:16)",
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
}
```


<span id="sample-response-2"></span>
## Sample Response 2

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-3"></span>
## Sample Request 3

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
    "LogType": "delimiter_log",
    "ExtractRule": {
        "Delimiter": "&&",
        "Keys": [
            "time",
            "ip",
            "status",
            "",
            "user-agent"
        ],
        "TimeKey": "time",
        "TimeFormat": "%d/%b/%Y %H:%M:%S",
        "FilterKeyRegex": [
            {
                "Key": "status",
                "Regex": "200"
            }
        ],
        "UnMatchUpLoadSwitch": true,
        "UnMatchLogKey": "LogParseFailed"
    },
    "LogSample": "05/May/2016 13:30:28&&10.200.36.139&&200&&18204&&sdk-go",
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
}
```


<span id="sample-response-3"></span>
## Sample Response 3

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-4"></span>
## Sample Request 4

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
    "LogType": "json_log",
    "ExtractRule": {
        "TimeKey": "time",
        "TimeFormat": "%d/%b/%Y %H:%M:%S",
        "FilterKeyRegex": [
            {
                "Key": "status",
                "Regex": "200"
            }
        ],
        "UnMatchUpLoadSwitch": true,
        "UnMatchLogKey": "LogParseFailed"
    },
    "LogSample": "05/May/2016 13:30:28&&10.200.36.139&&200&&18204&&sdk-go",
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
}
```


<span id="sample-response-4"></span>
## Sample Response 4

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-5"></span>
## Sample Request 5

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
    "LogType": "fullregex_log",
    "ExtractRule": {
        "LogRegex": "([\\s\\S]+),\\s(\\S+),\\s(\\d+),\\s(\\d+),\\s(\\S+).*",
        "Keys": [
            "time",
            "ip",
            "status",
            "size",
            "user-agent"
        ],
        "TimeKey": "time",
        "TimeFormat": "%d/%b/%Y %H:%M:%S",
        "FilterKeyRegex": [
            {
                "Key": "status",
                "Regex": "200"
            }
        ],
        "UnMatchUpLoadSwitch": true,
        "UnMatchLogKey": "LogParseFailed"
    },
    "LogSample": "05/May/2016 13:30:28, 10.200.36.139, 200, 18204, sdk-go",
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
}
```


<span id="sample-response-5"></span>
## Sample Response 5

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-6"></span>
## Sample Request 6

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
    "LogType": "fullregex_log",
    "ExtractRule": {
        "LogRegex": "\\[([^]]+)]\\s\\[(\\w+)]\\s([\\S\\s]+).*",
        "BeginRegex": "\\[([^]]+)].*",
        "Keys": [
            "time",
            "level",
            "message"
        ],
        "TimeKey": "time",
        "TimeFormat": "%Y-%b-dT%H:%M:%S,%f",
        "FilterKeyRegex": [
            {
                "Key": "level",
                "Regex": ".*ERROR.*"
            }
        ],
        "UnMatchUpLoadSwitch": true,
        "UnMatchLogKey": "LogParseFailed"
    },
    "LogSample": "[2018-10-01T10:30:01,000] [INFO] java.lang.Exception: exception happened\n    at TestPrintStackTrace.f(TestPrintStackTrace.java:3)\n    at TestPrintStackTrace.g(TestPrintStackTrace.java:7)\n    at TestPrintStackTrace.main(TestPrintStackTrace.java:16)",
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
}
```


<span id="sample-response-6"></span>
## Sample Response 6

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-7"></span>
## Sample Request 7

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
    "LogType": "fullregex_log",
    "ExtractRule": {
        "LogRegex": "(\\S*)\\s*-\\s*(\\S*)\\s*\\[(\\d+/\\S+/\\d+:\\d+:\\d+:\\d+)\\s+\\S+\\]\\s*\"(\\S+)\\s+(\\S+)\\s+(\\S+)\"\\s*(\\S*)\\s*(\\S*)\\s*(\\S*)\\s*(\\S*)\\s*\"([^\"]*)\"\\s*\"([^\"]*)\".*",
        "Keys": [
            "remote_addr",
            "remote_user",
            "time_local",
            "request_method",
            "request_uri",
            "protocol",
            "request_time",
            "request_length",
            "status",
            "body_bytes_sent",
            "http_referer",
            "http_user_agent"
        ],
        "TimeKey": "request_time",
        "TimeFormat": "%d/%b/%Y:%H:%M:%S",
        "FilterKeyRegex": [
            {
                "Key": "status",
                "Regex": "200"
            }
        ],
        "LogTemplate": {
            "Type": "Nginx",
            "Format": "format main  '$remote_addr - $remote_user [$time_local] \"$request\" $request_time $request_length $status $body_bytes_sent \"$http_referer\" \"$http_user_agent\"';"
        },
        "UnMatchUpLoadSwitch": true,
        "UnMatchLogKey": "LogParseFailed"
    },
    "LogSample": "192.168.1.1 - - [24/Sep/2022:12:23:12 +0800] \"POST /abc.com.testfile HTTP/1.0\" 0.000 129 200 43912736 \"-\" \"Wget/1.11.4 Red Hat modified\"",
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
}
```


<span id="sample-response-7"></span>
## Sample Response 7

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-8"></span>
## Sample Request 8

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
}
```


<span id="sample-response-8"></span>
## Sample Response 8

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-9"></span>
## Sample Request 9

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
    "RuleName": "testname",
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
    },
    "InputType": 1,
    "ContainerRule": {
        "Stream": "all",
        "ContainerNameRegex": ".*test.*",
        "IncludeContainerLabelRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "ExcludeContainerLabelRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "IncludeContainerEnvRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "ExcludeContainerEnvRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "EnvTag": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "KubernetesRule": {
            "NamespaceNameRegex": ".*test.*",
            "WorkloadType": "Deployment",
            "WorkloadNameRegex": ".*test.*",
            "IncludePodLabelRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "ExcludePodLabelRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "PodNameRegex": ".*test.*",
            "LabelTag": {
                "Key1": "Value1",
                "Key2": "Value2"
            }
        }
    }
}
```


<span id="sample-response-9"></span>
## Sample Response 9

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-10"></span>
## Sample Request 10

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
    },
    "InputType": 2,
    "ContainerRule": {
        "ContainerNameRegex": ".*test.*",
        "IncludeContainerLabelRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "ExcludeContainerLabelRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "IncludeContainerEnvRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "ExcludeContainerEnvRegex": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "EnvTag": {
            "Key1": "Value1",
            "Key2": "Value2"
        },
        "KubernetesRule": {
            "NamespaceNameRegex": ".*test.*",
            "WorkloadType": "Deployment",
            "WorkloadNameRegex": ".*test.*",
            "IncludePodLabelRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "ExcludePodLabelRegex": {
                "Key1": "Value1",
                "Key2": "Value2"
            },
            "PodNameRegex": ".*test.*",
            "LabelTag": {
                "Key1": "Value1",
                "Key2": "Value2"
            }
        }
    }
}
```


<span id="sample-response-10"></span>
## Sample Response 10

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="sample-request-11"></span>
## Sample Request 11

```json
POST https://tls-{Region}.bytepluses.com/CreateRule HTTP/1.1
Content-Type: application/json
{
    "TopicId": "706f****-****-****-****-****46aa1f07",
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
        "TimeKey": "time",
        "TimeFormat": "%d/%b/%Y %H:%M:%S",
        "FilterKeyRegex": [
            {
                "Key": "status",
                "Regex": "200"
            }
        ],
        "UnMatchUpLoadSwitch": true,
        "UnMatchLogKey": "LogParseFailed"
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
        }
    }
}
```


<span id="sample-response-11"></span>
## Sample Response 11

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
{
    "RuleId": "faf*************"
}
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument |The parameter is invalid. |
|400 |PathQuotaExceed |Path Quota Exceeded |Exceeded the quota for collection path. |
|400 |ExcludePathQuotaExceed |Exclude Path Quota Exceeded |Exceeded the quota for collection blacklist. |
|400 |ExtractRuleKeyQuotaExceed |ExtractRule Key Quota Exceeded |Exceeded the quota for user\-defined fields in the extraction rules. |
|400 |ExtractRuleFilterKeyRegexQuotaExceed |ExtractRule FilterKeyRegex Quota Exceeded |The extraction rule exceeded the quota for filter rule. |
|409 |RuleAlreadyExist |Rule %s already exist |The collection configuration already exists. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
