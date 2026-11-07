---
title: "Configure a sidecar in the console for collecting logs from a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/collect_logs_sidecar_console"
---

Torch Log Service (TLS) allows you to collect text logs from containers in a Kubernetes cluster using a Sidecar. This topic describes how to create a collection rule in the console.

<span id="背景信息"></span>
## Background

LogCollector allows for collecting text logs from containers using a Sidecar and uploading the collected log data along with the container metadata to the TLS server.

When collecting text logs from containers using a Sidecar, LogCollector offers the following features:


* It supports all the features of LogCollector deployed on physical machines, and various collection modes such as single\-line mode, multi\-line mode, delimiter \-based mode, JSON mode, and full regex\-based mode.

* In addition to the default reserved fields added according to the collection modes, LogCollector can also add container metadata, such as the namespace, pod name, and pod IP address, to the collected log data. Then, it uploads the data to TLS and automatically creates indexes for the fields by default.

   The additional reserved fields are as follows.

   
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


* Install LogCollector in the container from which you want to collect logs. For more information, refer to [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar).

* Create a host group and add the host of target containers to the group.

   We recommend that you use a host group of the host label type. You can set the host labels to the custom labels configured when you install LogCollector. Make sure the labels match the values of `${your_labels}` in the ConfigMap. For example, you can set a host label to nginx\-log. For more information, refer to [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group).


<span id="限制说明"></span>
## Limits


* The Sidecar mode does not allow you to collect standard output and standard errors from business containers.

* When you collect text logs from a business container using the sidecar mode, collect the logs from the log directory shared by the LogCollector container and the business container. Pay attention to the following:

   * The business container writes logs to the shared directory, and LogCollector periodically scans the log files in the shared directory to collect logs. Therefore, make sure the collection path configured in the console is the path of the log files from the perspective of the LogCollector container.

   * We recommend that you use emptyDir to mount the collection path. For more information on mounting methods, refer to "Deploying LogCollector using a sidecar".

   * This mode can collect data through symbolic links. This can be achieved if the LogCollector container can access the business\-container log files where the symbolic links point.

* If the Pod to which the LogCollector container and the business container belong stops, the LogCollector container stops. Then, the LogCollector container stops collecting logs from the business container. In this case, If latency exists when LogCollector collects logs from the business container, some logs generated before the collection stops may be lost.

* To get container metadata, rely on the environment variables configured in the LogCollector container. LogCollector reads the environment variable LOG_COLLECTOR_ENV_TAGS, splits it into multiple environment variable keys with vertical bars ( | ), reads the values of the keys, and carries the key\-value pairs in logs. Therefore, set the required container metadata in the LogCollector container. Note that only the following metadata can start or end with double underscores ( __ ): `__namespace__`, `__node_ip__`, `__node_name__`, `__pod_ip__`, and `__pod_name__`. If the other metadata starts or ends with double underscores ( __ ), it is ignored during collection.


<span id="创建-logcollector-采集配置"></span>
## Create LogCollector collection rules

<span id="步骤一-填写初始配置"></span>
### Step 1: Select a log space


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** page, select a collection mode.

5. Select a project and a topic, and click **Next: Select host group.** 

   The collected log data is stored in the selected topic. You can query and analyze log data by topic. If no suitable topic is available, create a topic as prompted.


<span id="2999fb8d"></span>
### Step 2: Select host groups


1. In the **All host groups** area, select a host group for log collection.

   If there is no host group available in the list, you need to create the host groups first. For specific operations, please refer to [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group), [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group).

2. In the **Selected host group** area, confirm the selection, and click **Next: Collection rule**.


<span id="2829e700"></span>
### Step 3: Configure collection rules

The collection mode determines how LogCollector parses log files. You can select an appropriate collection mode based on your actual business scenario and configure the log parsing rules for the mode. You can use of the following log collection modes to collect container logs using a sidecar. For more information on how to configure a log collection rule, refer to the corresponding document.


* [Collect logs in Single-line full-text mode](https://docs.byteplus.com/docs/tls/single_line_full_text_mode)

* [Collect logs in Multi-line full-text mode](https://docs.byteplus.com/docs/tls/multi_line_full_text_mode)

* [Collect logs in Full regex-based multi-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_multi_line_mode)

* [Collect logs in Full regex-based single-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_single_line_mode)

* [Collect logs in Delimiter-based mode](https://docs.byteplus.com/docs/tls/delimiter_based_mode)

* [Collect logs in NGINX-based mode](https://docs.byteplus.com/docs/tls/nginx_based_mode)

* [Collect logs in JSON mode](https://docs.byteplus.com/docs/tls/json_mode)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To using the sidecar mode, do not enable <strong>Container log collection</strong>.</div>


<span id="步骤三-更新索引"></span>
### Step 4: Update indexes


1. Update indexes.

   Follow the prompts on the page to set or update indexes as needed. You can also click **Import existing index configuration** to import the index of other topics.

   * If no index is set for this topic, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2) to set an index.

   * If an index is set for this topic, determine whether to update the index based on the log fields parsed by the collection rules.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The updated index settings take effect on data written after the update. For more information on instructions and limits related to query and analysis, refer to <a href="https://docs.byteplus.com/docs/tls/Query-overview-2">Query overview</a>and <a href="https://docs.byteplus.com/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

2. Confirm the index configuration and click **Submit**.


<span id="后续步骤"></span>
## Follow\-ups

After creating the collection configuration, LogCollector will collect logs and save them to the specified log topic. You can perform query and analysis operations in the log topic.
