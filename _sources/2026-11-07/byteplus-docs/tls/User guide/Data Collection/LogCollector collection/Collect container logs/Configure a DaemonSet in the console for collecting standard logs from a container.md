---
title: "Configure a DaemonSet in the console for collecting standard logs from a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/collecte_stdout_daemonset"
---

Torch Log Service (TLS) allows you to collect standard outputs from containers in a Kubernetes cluster using a DaemonSet. This topic describes how to create a collection rule in the TLS console.

<span id="背景信息"></span>
## Background

After the LogCollector plug\-in offered by TLS is installed in containers, LogCollector identifies the containers from which logs are collected based on the container labels and environment variables. Then, it continuously collects standard outputs from the specified containers and upload the collected standard outputs along with the container metadata such as the container name, to the TLS server. LogCollector also supports the breakpoint resume feature. This feature allows LogCollector to seamlessly resume log collection from the last saved checkpoint after a system restart because the checkpoint file periodically saves the collection checkpoint information.

In addition, LogCollector allows you to collect standard outputs from containers in various collection modes, such as single\-line mode and multi\-line mode. Besides the default reserved fields added according to the collection modes, TLS adds the following reserved fields to standard outputs collected by LogCollector and creates indexes for them by default.


|Reserved Field |Description |
|---|---|
|`__container_source__` |Type of a data source. Valid values: stdout and stderr. |
|`__image_name__` |Name of an image. |
|`__container_name__` |Name of a container. |
|`__container_ip__` |IP address of a container or Pod. |
|`__pod_name__` |Pod name. |
|`__pod_uid__` |Unique identifier of a Pod. |
|`__namespace__` |Namespace to which a Pod belongs. |


<span id="前提条件"></span>
## Before you begin


* Install LogCollector in the container from which you want to collect logs. For more information on the procedure, refer to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet).

* Create a host group and add the host of target containers to the group. We recommend that you use a label\-based host group. You can use the custom label that you set when installing LogCollector as the host label. That is, use the value of `${your_labels}` that you set in ConfigMap when installing LogCollector as the label of the hosts in the group. For example, you can use nginx\-log as the label.


<span id="限制说明"></span>
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


<span id="创建-logcollector-采集配置"></span>
## Creating LogCollector collection rules

<span id="步骤一-填写初始配置"></span>
### Step 1: Select a log space


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** page, select a collection mode.

5. Select a project and a topic, and click **Next: Select host group.** 

   The collected log data is stored in the selected topic.


<span id="eba84bee"></span>
### Step 2: Select host groups


1. In the **All host groups** area, select a host group for log collection.

   If there is no host group available in the list, you need to create the host groups first. For specific operations, please refer to [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group), [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group).

2. In the **Selected host group** area, confirm the selection, and click **Next: Collection rule**.


<span id="96ce1c39"></span>
### Step 3: Configure collection rules

<span id="a4c348d8"></span>
#### Configure basic information


1. Complete the basic rule configuration.

   
   |Parameter |Description |
   |---|---|
   |rule name |The **rule name** is the name of the LogCollector collection rule.<br><br>Alternatively, click **Import other collection configurations**, select a collection rule from a specified project in the current account, then import the existing collection rule. You only need to specify a collection rule name. |
   |Container log collection |Select **Enable**. |
   |Collection type |Select **K8s container standard output**. |
   |Collection information |Select the content that must be collected based on your business requirements. You can collect the following types of logs:<br><br><br>* Only collect **standard outputs \- stdout**.<br><br>* Only collect **standard errors \- stderr**.<br><br>* Collect both **standard outputs \- stdout** and **standard errors \- stderr**. |
   

2. (Optional) Enable **Common container collection rule**.

   General collection rules for container logs specify the content to be collected based on general information about containers and exclude the content that is not to be collected.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <strong>Common container collection rule</strong> and <strong>K8s collection rules</strong> are disabled, the collection scope covers all containers. If both collection rules are enabled, the logical relationship between the rules is <strong>AND</strong>. It means that logs can be collected when the corresponding containers simultaneously meet both rules.   </div>
   

   
   |Parameter ||Description |
   |---|---|---|
   |Container name ||Specify the names of the containers whose logs are to be collected. If you do not specify a container name, TLS collects the logs in all containers of the host group.<br><br>Regular expression matching is supported. For example, if you set this parameter to `^(container-test)$`, TLS collects logs from all containers named `container-test`. |
   |Container Label |Enable whitelisting |The allowlist of container labels specifies the containers whose logs are to be collected based on container labels. If you disable the allowlist, TLS collects logs from all containers.<br><br>When you enable the allowlist of container labels, specify key\-value pairs. Key is required and Value is optional.<br><br><br>* If the Value field is empty, LogCollector collects logs from all containers that have a label with the specified key.<br><br>* Value is not empty: TLS collects logs from the containers of which the labels include the content specified for Key and the label values match the content specified for Value. Value supports regular expression matching. For example, setting Key to app and Value to `^(test1\|test2)$` means TLS collects logs from containers of which the labels include app:test1 and app:test2.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that the containers whose labels match a key\-value pair are included in the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the allowlist of container labels, do not specify the same content for Key.</div><br> |
   ||Enable blacklist |The denylist of container labels specifies the containers whose logs are not to be collected. When you disable the denylist, TLS collects logs from all containers.<br><br>If the denylist of container labels is enabled, Key is required and Value is optional.<br><br><br>* If the Value field is empty, LogCollector does not collect logs from the containers that have a label with the specified key.<br><br>* Value is not empty: TLS does not collect logs from containers whose labels match a key\-value pair. It means TLS does not collect logs from containers whose labels include the content specified for Key and the values match the content specified for Value. You can specify a regular expression in the Value field. For example, setting Key to `app` and Value to `^(test1\|test2)$` means that TLS does not collect logs from containers of which the labels include app:test1 and app:test2.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that the containers whose labels match a key\-value pair are excluded from the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the denylist of container labels, do not specify the same content for Key.</div><br> |
   |Container environment variables |Enable whitelisting |The allowlist of container environment variables specifies the containers whose logs are to be collected based on container environment variables. When you disable the allowlist, TLS collects logs from all containers.<br><br>When you enable the allowlist of container environment variables, specify key\-value pairs. Key is required and Value is optional.<br><br><br>* Value is empty: TLS collects logs from all containers of which the environment variables include the content specified for Key.<br><br>* Value is not empty: TLS collects logs from containers of which the environment variables include the content specified for Key and the values match the content specified for Value. Value supports regular expression matching. For example, setting Key to module and Value to `^(tcp\|udp)$` means that TLS collects logs from the containers of which the environment variables include module:`tcp` and module:`udp`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that containers whose environment variables match a key\-value pair are included in the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the allowlist of container environment variables, do not specify the same content for key.</div><br> |
   ||Enable blacklist |The denylist of container environment variables specifies the containers whose logs are not to be collected. When you disable the denylist, TLS collects logs from all containers.<br><br>If the denylist of container environment variables is enabled, Key is required and Value is optional.<br><br><br>* Value is empty: TLS does not collect logs from all containers of which the environment variables include the content specified for Key.<br><br>* Value is not empty: TLS does not collect logs from containers whose environment variables match a key\-value pair. It means TLS does not collect logs from containers whose environment variables include the content specified for Key and the values match the content specified for Value. You can specify a regular expression in the Value field. For example, setting Key to module and Value to `^(tcp\|udp)$` means that TLS does not collect logs from the containers whose environment variables include module:`tcp` and module:`udp`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that the containers whose environment variables match a key\-value pair are excluded from the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the denylist of container environment variables, do not specify the same content for key.</div><br> |
   |Environment variables log tag ||Specify whether to add environment variables as log tags to the original log data. After this feature is enabled, TLS adds fields related to container environment variables to logs. If you set multiple key\-value pairs, multiple fields are added.<br><br>Assume that: 1. You set Key to source and Value to data_source. 2. A container includes the environment variable `source=DC`. In this case, a field `__tag__data_source__: DC` is added to the logs. |
   

3. (Optional) Enable **K8s collection rules**.

   Kubernetes collection rules specify the content to be collected based on information about Kubernetes containers and exclude the content that is not to be collected.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <strong>Common container collection rule</strong> and <strong>K8s collection rules</strong> are disabled, the collection scope covers all containers. If both collection rules are enabled, the logical relationship between the rules is <strong>AND</strong>. It means that logs can be collected when the corresponding containers simultaneously meet both rules.   </div>
   

   
   |Parameter ||Description |
   |---|---|---|
   |Namespace ||Specify the names of Kubernetes namespaces based on which collection is performed. If you do not specify this parameter, TLS collects logs from all containers.<br><br>This parameter supports regular expression matching. For example, setting the parameter to `^(tcp\|udp)$`, LogCollector collects logs from all containers in the `tcp` and `udp` namespaces.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using regular expression fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> indicates matching characters starting with <code>http</code>.</div><br> |
   |Workload type ||Specify up to one workload type to determine the containers whose logs are to be collected. If you do not specify this parameter, TLS collects the logs in all types of containers.<br><br>Supported workload types:<br><br><br>* Deployment: stateless workload<br><br>* StatefulSet: stateful workload<br><br>* DaemonSet: daemon<br><br>* Job: task<br><br>* CronJob: scheduled task |
   |Workload name ||Specify workload names to determine the containers whose logs are to be collected. If you do not specify this parameter, TLS collects logs in all containers.<br><br>This parameter supports regular expression matching. For example, if you set the workload name to `^(http.*)$`, LogCollector collects logs from all containers with the workload names starting with http. |
   |Pod Label |Enable whitelisting |The allowlist of Pod labels specifies the containers whose logs are to be collected. If you disable the pod label allowlist, LogCollector collects logs from all containers.<br><br>If you enable the allowlist of Pod labels, Key is required:<br><br><br>* Value is empty: TLS collects logs from all containers of which the Pod labels include the content specified for Key.<br><br>* Value is not empty: TLS collects logs from the containers of which the Pod labels include the content specified for Key and the values match the content specified for Value. In this case, regular expression matching is supported. You can specify a regular expression in the Value field. For example, setting Key to module and Value to `^(tcp\|udp)$` means TLS collects logs from the containers of which the Pod labels include module:`tcp` and module:`udp`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that the containers whose Pod labels match a key\-value pair are included in the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the allowlist of Pod labels, do not specify the same content for Key.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When using regular expression fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> indicates matching characters starting with <code>http</code>.</div><br> |
   ||Enable blacklist |The denylist of Pod labels specifies the containers whose logs are not to be collected. When you disable the denylist, TLS collects logs from all containers.<br><br>If you enable the denylist of Pod labels, Key is required and Value is optional.<br><br><br>* Value is empty: TLS does not collect logs from all containers of which the Pod labels include the content specified for Key.<br><br>* Value is not empty: TLS does not collect logs from the containers of which the Pod labels include the content specified for Key and the values match the content specified for Value. You can specify a regular expression in the Value field. For example, setting Key to module and Value to `^(tcp\|udp)$` means TLS does not collect logs from containers of which the Pod labels include module:`tcp` and module:`udp`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that the containers whose Pod labels match a key\-value pair are excluded from the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the denylist of Pod labels, do not specify the same content for Key.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When using regular expression fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> indicates matching characters starting with <code>http</code>.</div><br> |
   |Pod Annotation |Enable whitelisting |The Pod Annotation whitelist is used to specify the containers whose logs are to be collected. If you need to set the Pod annotation whitelist, the `Key` is required, and the `Value` is optional.<br><br><br>* `Value` is empty: It means that all the containers under the Pod whose Pod annotation contains the `Key` are matched.<br><br>* `Value` is not empty: It means that only the containers under the Pod whose Pod annotation contains the `Key` and whose value matches the `Value` are matched.<br><br>   The `Value` is matched as a string by default, that is, it will be matched only when the `Value` is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with `$`, then it is a regular expression match. For example, when the `Key` is set as `app` and the `Value` is set to `^(test1\|test2)$`, it means that the containers under the Pod whose Pod annotation contains `app:test1` or `app:test2` are matched.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that the containers whose Pod annotations match a key\-value pair are excluded from the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the Pod annotation whitelist, do not specify the same content for Key.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When using regular expression fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> indicates matching characters starting with <code>http</code>.</div><br> |
   ||Enable blacklist |The Pod Annotation blacklist is used to specify the containers whose logs are not to be collected. If you need to set the Pod annotation blacklist, then the `Key` is required and the `Value` is optional.<br><br><br>* `Value` is empty: It means that all the containers under the Pod whose Pod annotation contains the `Key` will be excluded.<br><br>* `Value` is not empty: It means that only the containers under the Pod whose Pod annotation contains the `Key` and whose value matches the `Value` will be excluded.<br><br>   The `Value` is matched as a string by default, that is, it will be matched only when the `Value` is exactly the same as the value of the Pod annotation. If the value starts with `^` and ends with`$`, then it is a regular expression match. For example, when the `Key` is set as `app` and the `Value` is set to `^(test1\|test2)$`, it means that the containers under the Pod whose Pod annotation contains `app:test1` or `app:test2` are matched.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical relationship between key\-value pairs is <strong>OR</strong>. It means that the containers whose Pod annotations match a key\-value pair are excluded from the collection scope.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you enable the Pod annotation whitelist, do not specify the same content for Key.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When using regular expression fuzzy matching, <code>.*</code> must be added. For example, <code>^(http.*)$</code> indicates matching characters starting with <code>http</code>.</div><br> |
   |Pod name matching rule ||Specify Pod names to determine the containers whose logs are to be collected. This parameter is optional. If you do not specify this parameter, TLS collects logs in all containers.<br><br>Regular expression matching is supported. For example, if you set it to `^(http.*)$`, TLS collects logs from all containers under Pods whose names start with http. |
   |Enable All K8s Label Log Tags ||Whether to add all Kubernetes labels as log tags to the original log data. After it is enabled, TLS will add fields related to all labels in the Kubernetes Pod to the logs. For example, if a Pod contains labels `source=DC` and `destination=CS`, then fields `tag__source: DC` and `tag__destination: CS` will be added to the logs. |
   |K8s tag ||Specify whether to add Kubernetes labels as log tags to the original log data. After you enable this parameter, TLS adds Kubernetes Pod label\-related fields to logs. If you set multiple key\-value pairs, TLS adds multiple fields.<br><br>For example, if you set Key to `source` and Value to `data_source`and the pod has the `source=DC` label, LogCollector adds the following new field to the log data: `__tag__data_source__: DC` is added to the logs. |
   |K8s Annotation log tag ||Specify whether to add Kubernetes annotations as log tags to the original log data. After you enable this parameter, TLS adds Kubernetes Pod annotation\-related fields to logs. If you set multiple key\-value pairs, TLS adds multiple fields.<br><br>Assume that: 1. You set Key to sink and Value to data_sink. 2. A Pod includes the annotation `sink=ck`. In this case, a field `__tag__data_sink__: ck` is added to the logs. |
   


<span id="4020a2b1"></span>
#### Configure Log Format


1. Set **Collection policy**.

   The collection policy specifies whether LogCollector collects incremental logs or full logs. By default, incremental logs are collected.

   
   |Parameter |Description |
   |---|---|
   |Full |LogCollector collects logs from the start of each file, collecting historical log data. |
   |increment |LogCollector only collects new content in files. When new logs are written to log files within the monitoring range, it triggers LogCollector to collect logs.<br><br><br>* For the first\-time collection of a log file, LogCollector will automatically determine the collection position based on the incremental threshold you specify.<br><br>   * If the size of the new file does not exceed the specified incremental threshold, LogCollector collects logs from the beginning of the new file.<br><br>   * If the size of the new file exceeds the specified incremental threshold, LogCollector collects logs from a position that is the file's end minus the incremental threshold, thus collecting only the incremental logs.<br><br>* For log files that are not being collected for the first time, LogCollector will determine the collection position based on the Checkpoint and continue collecting from there. |
   

2. Set **Collection mode**.

   The collection mode determines how LogCollector parses log files. You can select an appropriate collection mode based on your actual business scenario and configure the log parsing rules for the mode. For more information, refer to **Step 6: Specify a collection mode** in the document for the collection mode.

   * [Collect logs in Single-line full-text mode](https://docs.byteplus.com/docs/tls/single_line_full_text_mode)

   * [Collect logs in Multi-line full-text mode](https://docs.byteplus.com/docs/tls/multi_line_full_text_mode)

   * [Collect logs in Full regex-based multi-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_multi_line_mode)

   * [Collect logs in Full regex-based single-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_single_line_mode)

   * [Collect logs in Delimiter-based mode](https://docs.byteplus.com/docs/tls/delimiter_based_mode)

   * [Collect logs in NGINX-based mode](https://docs.byteplus.com/docs/tls/nginx_based_mode)

   * [Collect logs in JSON mode](https://docs.byteplus.com/docs/tls/json_mode)

3. Select whether to use the collection time.

   * **Acquisition point in time**: Use the system time of the server where the LogCollector is located when the log is collected as the log time.

   * **Custom time**: Extract the time that comes with the original log as log time. The relevant configuration is as follows:

      
      |Parameter |Description |
      |---|---|
      |Time key name |The name of the time field. |
      |Time regular |If you only parse part of the contents of a time field, you can use a regular expression to extract it. |
      |Time accuracy |After checking **Enable nanosecond time accuracy**, you can extract timestamps with nanosecond accuracy. For detailed instructions, please refer to [Enable LogCollector high precision time](https://docs.byteplus.com/docs/tls/Enable-LogCollector-high-precision-time). |
      |Time conversion format |Set the time conversion format according to the extracted time content. For example `01/March/2024 20:15:02`, you can configure the **time conversion format** to `% d/% b/% Y:% H:% M:% S`. For more information, refer to [Time format](https://docs.byteplus.com/docs/tls/time_format).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the time conversion format is filled in incorrectly and the time cannot be parsed correctly, the collection time shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">By default, LogCollector collection time can be accurate to milliseconds, that is, when configuring the time conversion format, it supports configuration to milliseconds. If no millisecond resolution is specified in the time conversion format, the millisecond portion is automatically filled with 0.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After checking <strong>Enable nanosecond time accuracy</strong> in the collection configuration, it supports parsing the log time to nanosecond precision.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add a time zone to the log time and the original log time contains the time zone, you can add the time zone format (% z) to the <strong>time conversion format</strong> to extract the time zone. Alternatively, you can add a fixed time zone format (+ 08:00) to the <strong>time conversion format</strong> and select the appropriate <strong>time zone attribute</strong> .</div><br><br><br>   <div data-tips="true" data-tips-type="tip">For example <code>2024-03-03 15:00:00 + 08:00</code>, you can set the <strong>time conversion format</strong> to <code>% Y-% m-% d% H:% M:% S% z</code>, or set the <strong>time conversion format</strong> to <code>% Y-% m-% d% H:% M:% S + 08:00</code>and select the corresponding <strong>time zone attribute.</strong>   </div><br>    |
      |Time zone attribute |Set the time zone. Select UTC if you want to support daylight or winter time; otherwise, select GMT. |
      

4. Select whether to ignore the files that have not been updated.

   Once enabled, when the update time of the log file is not within the time range you specified, LogCollector will ignore this file and not perform collection.


<span id="befe7f67"></span>
#### Configure plugin

Enable **Plugin configuration**.

If complex and unstructured business logs cannot be parsed using common log collection modes like JSON, you can use LogCollector plug\-ins to process the collected logs. For more information, refer to [LogCollector plug-ins Overview](https://docs.byteplus.com/docs/tls/plug-ins_Overview).

<span id="9a8d2cd9"></span>
#### Advanced settings


1. Enable **Advanced Settings**.

   Configure advanced settings as needed. We recommend that you keep the default settings unless otherwise needed.

   
   |Parameter |Description |
   |---|---|
   |Filter |Specify whether to enable log field filter rules. By default, it is disabled. After enabled, use regular expressions to set filter rules. Only logs that exactly match the regular expressions are collected, helping you collect valuable log data. |
   |Upload parsing failure log |Specify whether to upload logs that failed to be parsed. By default, it is disabled.<br><br><br>* Enable: All logs that failed to be parsed are uploaded to TLS, with a specified field acting as the key and the original log content as the value. The key can be specified using **Failure log key name**. The default key is `LogParseFailed`.<br><br>* Disable: Logs that failed to be parsed are not uploaded to TLS. |
   |Upload hostname field |Specify whether to upload the hostname field. This parameter is disabled by default.<br><br><br>* If you enable the parameter, a field is added to the original log to record the hostname of the log source. Specify the field name for **Hostname** . Default value: `hostname`.<br><br>* If you disable this parameter, the `hostname` field is not added. |
   |Parse collection path |Extract fields from the collection path using regular expressions, then add the fields as metadata to log data. By default, this feature is disabled.<br><br>After enabled, set **Sample collection path**, **Extract regular expression**, and **Extract result**.<br><br><br>* **Sample collection path**: Specify an example of the collection path in actual scenarios.<br><br>   * The example must be an absolute path.<br><br>   * The example cannot include the following wildcards: single asterisk`*`, question mark `?`, and double asterisks `**`.<br><br>* **Extract regular expression**: Specify a regular expression used to extract fields from the path. To successfully extract fields, it must match the collection path example.<br><br>* **Extract result**: It displays each field value parsed and extracted by TLS from the path example based on the regular expression. You must specify a key for each field.<br><br>   * Up to 100 keys can be configured.<br><br>   * Each key must be unique and cannot be empty. |
   |HashKey Routing Shard |Specify a HashKey to write data to a shard that meets the range requirements. By default, this feature is disabled.<br><br><br>* Enable: Use the HashKey Routing Shard mode for data collection. In this mode, data is written to the specified shard in sequence. This is suitable for scenarios requiring sequential data writes and consumption. In this case, you must set the HashKey. Then, TLS writes the data to the shard containing that key value. The HashKey value range is [00000000000000000000000000000000–ffffffffffffffffffffffffffffffff).<br><br>* Disable: Use the load\-balanced mode for data collection. In this mode, data packets are written to an available shard in a load\-balanced manner. This is suitable for scenarios where data consumption and writes are irrelevant to shards, such as scenarios not requiring a sequential order. |
   |Upload original log |Specify whether to upload raw log data as a field to TLS. It is disabled by default.<br><br><br>* Enable: Raw log data is encapsulated in a specified field, and uploaded to TLS together with the parsed log data. The field key can be specified using **Raw log key name**. The default key is `raw`, and the actual corresponding log field is `__raw__`.<br><br>* Disable: No raw log field is added. |
   |Upload constant field |After enabled, LogCollector encapsulates the specified field keys and values in each log entry. The following limits apply to constant fields:<br><br><br>* Up to 5 constant fields can be uploaded.<br><br>* Each field key must be unique and cannot be empty. The key must be 1 to 128 characters in length. It can contain letters, digits, and the following special characters: `-_./` It cannot start with an underscore ( _ ).<br><br>* Each value cannot be empty, with a maximum length of 512 KiB. |
   |Upload Host Group Label |Whether to upload the label information of the host group to TLS.<br><br><br>* Enable: LogCollector will upload the label information of the host group to the specified field. You can specify the field name in the **Host Group Label Key Name**, the default value is `host_group_label`.<br><br>* Disable: Do not upload the label information of the host group. |
   |Allows multiple file collections |By default, a log file can only match one collection rule and be collected into one topic. After completing this configuration, it enables a log file to match multiple collection rules simultaneously. For more information, please refer to [File logs or standard output can be collected multiple times simultaneously](https://docs.byteplus.com/docs/tls/file-repeatedly-collected). |
   |Extended configuration |Specify the extended configuration of LogCollector in JSON object format. Currently, the supported parameters include CloseInactive, CloseRemoved, CloseRenamed, CloseEOF, and CloseTimeout. For more information on the parameters, refer to [CreateRule](https://docs.byteplus.com/docs/tls/api-createrule).<br><br>For example, the configuration below means that the file handle is released if any of the following occurs: 1. No log data is written to the log file for 10 seconds. 2. The log file is removed or renamed. 3. LogCollector reads to the end of the file. 4. The monitoring duration of the log file exceeds 30 minutes.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/213bf60ab3ed4bcd9db3ce9a768cd92b~tplv-goo7wpa0wc-image.image) </span> |
   

2. Confirm the collection rule, then click **Next step**.


<span id="步骤三-更新索引"></span>
### Step 4: Update indexes


1. Update indexes.

   Follow the prompts on the page to set or update indexes as needed. You can also click **Import existing index configuration** to import the index of other topics.

   * If no index is set for this topic, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2)to set an index.

   * If an index is set for this topic, determine whether to update the index based on the log fields parsed by the collection rules.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The updated index settings take effect on data written after the update. For more information on instructions and limits related to query and analysis, refer to <a href="https://docs.byteplus.com/docs/tls/Query-overview-2">Query overview</a>and <a href="https://docs.byteplus.com/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

2. Confirm the index configuration and click **Submit**.


<span id="后续步骤"></span>
## Follow\-ups

After creating the collection configuration, LogCollector will collect logs and save them to the specified log topic. You can perform query and analysis operations in the log topic.
