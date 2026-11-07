---
title: "Use LogCollector plug-ins to process logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Use_LogCollector_plug-ins_to_process_logs"
---

When collecting text logs using LogCollector, you can use LogCollector plug\-ins to process certain specified fields in the collected log data, such as parsing log fields based on regular expressions. This topic describes how to use LogCollector plug\-ins to process log data.

<span id="背景信息"></span>
## Background

In scenarios with intricate log structures or variable log data formats, when configuring LogCollector collection rules for collecting text logs, you can enable and configure plug\-ins for processing log data. When processing the collected log data, Torch Log Service (TLS) executes the processing logic in sequence according to the plug\-in configurations. For example, parses log fields based on the specified regular expression.

When creating a collection rule for such a scenario, you can select a collection mode for splitting and parsing the structure of the first layer of the original log data, then uses a LogCollector plug\-in to further split and parse the specified fields. LogCollector allows you to add one or more plug\-ins, and it runs the plug\-ins in the order in which they are configured.

<span id="前提条件"></span>
## Before you begin


* Create a project and a topic. For more information, refer to [Create a project](https://docs.byteplus.com/docs/tls/Managing_projects#%E5%88%9B%E5%BB%BA%E6%97%A5%E5%BF%97%E9%A1%B9%E7%9B%AE) and [Create a topic](https://docs.byteplus.com/docs/tls/Managing_topics#%E5%88%9B%E5%BB%BA%E6%97%A5%E5%BF%97%E4%B8%BB%E9%A2%98).

* Create a host group and make sure that the heartbeat statuses of the hosts in the host group are in normal state. For more information, refer to [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group)or [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group).

* Install the latest version of LogCollector on the log source server. For more information, refer to [Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).


<span id="操作步骤"></span>
## Procedure

<span id="_1-填写采集配置"></span>
### 1. Configure a collection rule


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Common Functions** \> **Log Collection**.

4. In the **LogCollector** pane, select a collection mode based on your business requirements and the type and data structure of the logs that you want to collect, and configure a collection rule.

   Complete the basic settings including the collection rule name, collection path, and collection mode, and confirm the advanced settings. For more information on how to configure a plug\-in, refer to [2. Configure plug-ins](https://docs.byteplus.com/docs/tls/Use_LogCollector_plug-ins_to_process_logs#_2-%E5%A1%AB%E5%86%99%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE). For more information on how to configure the basic settings for different collection modes, refer to the following documents.

   * [Collect logs in Single-line full-text mode](https://docs.byteplus.com/docs/tls/single_line_full_text_mode)

   * [Collect logs in Multi-line full-text mode](https://docs.byteplus.com/docs/tls/multi_line_full_text_mode)

   * [Collect logs in Full regex-based single-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_single_line_mode)

   * [Collect logs in Full regex-based multi-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_multi_line_mode)

   * [Collect logs in Delimiter-based mode](https://docs.byteplus.com/docs/tls/delimiter_based_mode)

   * [Collect logs in NGINX-based mode](https://docs.byteplus.com/docs/tls/nginx_based_mode)

   * [Collect logs in JSON mode](https://docs.byteplus.com/docs/tls/json_mode)


<span id="_2-填写插件配置"></span>
### 2. Configure plug\-ins

When creating and configuring a collection rule, select **Enable** in the **Plugin configuration** pane, then configure plug\-ins.

The plug\-in configuration must be in JSON format. Each plug\-in is defined by a complete JSON object. The key is `processors` and the value is a JSON Object array. Each Object represents a LogCollector plug\-in configuration. For more information on the plug\-ins supported by LogCollector and their configuration methods, refer to [List of plug-ins](https://docs.byteplus.com/docs/tls/plug-ins_Overview#%E6%8F%92%E4%BB%B6%E5%88%97%E8%A1%A8).

<span id="日志样例"></span>
## Examples

For example, an original log entry of an application is as follows:

```Plain
Click Here&&36&&bold&&text1&&250&&100&&#center#&&sun1.opacity = (sun1.opacity / 100) * 90;
```


When using the single\-line full\-text mode to collect the above log entry, TLS encapsulates the full text of the log entry into a field. The final log data saved on the server is as follows:

```Plain
__content__:Click Here&&36&&bold&&text1&&250&&100&&#center#&&sun1.opacity = (sun1.opacity / 100) * 90;
__path__:net/log/net_log_event.log
__source__:192.0.0.1
```


The `__content__` field can be further split using a delimiter. That is, you enable the plug\-in processing feature and use the delimiter plug\-in to extract the content in the `__content__` field in delimiter\-based mode.

The plug\-in configuration is as follows:

```json
{
    "processors":[
        {
            "delimiter": {
                "field": "__content__",
                "delimiter": "&&",
                "keys": [
                    "data",
                    "size",
                    "style",
                    "name",
                    "hOffset",
                    "vOffset",
                    "alignment",
                    "onMouseUp"
                ],
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
```


The data in `__content__` field after processing is as follows:

```Plain
"data": "Click Here"
"size": "36"
"style": "bold"
"name": "text1"
"hOffset": "250"
"vOffset": "100"
"alignment": "center"
"onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
```
