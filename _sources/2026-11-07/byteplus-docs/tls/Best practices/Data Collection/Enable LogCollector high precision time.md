---
title: "Enable LogCollector high precision time"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Enable-LogCollector-high-precision-time"
---

LogCollector supports enabling high\-precision time to extract the nanosecond portion of the original log time content. This topic describes how to enable the LogCollector high\-precision time feature.

<span id="31830e2d"></span>
## application scenario

By default, TLS collects and stores logs with millisecond accuracy to accommodate a wide range of log management and analysis scenarios. However, in fields such as real\-time monitoring of financial transactions and performance analysis of ultra\-low latency systems, nanosecond\-level monitoring accuracy is a key factor in value transaction analysis, service response, and troubleshooting.

In order to meet such high\-precision time management requirements, TLS supports the ability to easily enable nanosecond time accuracy when collecting logs through LogCollector, ensuring that every minor time change can be captured and analyzed, providing a solid foundation for decision\-making.

<span id="814f4c62"></span>
## Log sample

```Plain
URL_REQUEST,https://clientservices.googleapis.com/chrome-variations/seed?osname=win&channel=stable&milestone=86,2024-06-19 12:27:35.822222222
```


<span id="24b6fd1d"></span>
## Before you begin


* Create a project and a topic. For more information, refer to [Create a project](https://docs.byteplus.com/docs/tls/Managing_projects#%E5%88%9B%E5%BB%BA%E6%97%A5%E5%BF%97%E9%A1%B9%E7%9B%AE) and [Create a topic](https://docs.byteplus.com/docs/tls/Managing_topics#%E5%88%9B%E5%BB%BA%E6%97%A5%E5%BF%97%E4%B8%BB%E9%A2%98).

* Create a host group and make sure that the heartbeat statuses of the hosts in the host group are in normal state. For more information, refer to [Create an IP address-based host group](https://docs.byteplus.com/docs/tls/Create_an_IP_address-based_host_group) or [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group).

* Install the latest version of LogCollector on the log source server. For more information, refer to [Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).


<span id="570bea6c"></span>
## Procedure

You can extract the time in the log through the LogCollector or LogCollector plug\-in and resolve it to nanosecond time.

<span id="4db1b936"></span>
### LogCollector

This example uses Delimiter\-based mode as an example, and you need to complete the relevant configuration in the collection configuration. Important parameter configuration examples are as follows. For other specific instructions and related operations, please refer to [Collect logs in Delimiter-based mode](https://docs.byteplus.com/docs/tls/delimiter_based_mode).


1. Complete Delimiter\-based mode related configuration.

   According to the log sample, set the **separator** to a **comma** , and set the key for each value in the **Extract result**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f181f8488d7c4d21a6824f0b0c4b3c92~tplv-goo7wpa0wc-image.image) </span>

2. Complete log time related configuration.

   1. Disable the **use collection time**.

   2. Set the **Time key name** to **starttime**.

      **starttime** is the key name you specified for the time content in the previous step.

   3. Check **Enable nanosecond time accuracy**.

      After checking **Enable nanosecond time accuracy** in the collection configuration, it supports parsing the log time to nanosecond precision.

   4. Set the **time conversion format** to `% Y-% m-% d% H:% M:% S.% f` based on the time content in the sample log.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9fe7fa1ae814faf9ee0fd1689f0619b~tplv-goo7wpa0wc-image.image) </span>


Once the logs are collected and indexed, you can view the collected logs by selecting **nanosecond query accuracy** on the query and analysis page, where the log time is nanosecond precision.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ae32f91ce634ec7aa6930d57a3943cb~tplv-goo7wpa0wc-image.image) </span>

<span id="ea946fe4"></span>
### LogCollector plugin

When collecting text logs through LogCollector, it supports parsing the specified fields of the collected log data through the LogCollector plug\-in, so you can also use the LogCollector time parsing plug\-in to enable nanosecond time accuracy  functions.

This example takes single\-line full\-text mode as an example, and you need to complete the relevant configuration in the collection configuration. Important parameter configuration examples are as follows. For other specific instructions and related operations, please refer to [Collect logs in Single-line full-text mode](https://docs.byteplus.com/docs/tls/single_line_full_text_mode).


1. Select **Collection mode** as **single\-line**.

2. In the **Use collection time** parameter, check **Enable**.

3. In the **Plugin configuration** parameters, check **Enable** and enter the following steps.

   When collecting in single\-line full\-text mode, each line of the original log will be stored in the `__content__` field. You can use the time parsing plug\-in to extract the time content in the original log. For details, please refer to [Time parsing](https://docs.byteplus.com/docs/tls/Time-parsing).

   ```SQL
   {
       "processors":[
           {
               "strp_time": {
                   "field": "__content__",
                   "format": "%Y-%m-%d %H:%M:%S.%f",
                   "time_zone": "GMT+08:00",
                   "extract_regex": "\\[(\\d{4}\\-\\d{2}\\-\\d{2}T\\d{2}:\\d{2}:\\d{2},\\d{3})\\]",
                    "enable_nanosecond": true
               }
           }
       ]
   }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81a34d31ada7434d99cfcc31c3be20f7~tplv-goo7wpa0wc-image.image) </span>


Once the logs are collected and indexed for the reserved fields `__content__` are enabled, you can view the collected logs by selecting **nanosecond query accuracy** on the query and analysis page, where the log time is nanosecond precision.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b492cad73244eacb9474371afbdc6ef~tplv-goo7wpa0wc-image.image) </span>
