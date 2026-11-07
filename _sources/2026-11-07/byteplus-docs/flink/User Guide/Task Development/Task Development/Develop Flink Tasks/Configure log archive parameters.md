---
title: "Configure log archive parameters"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Configure_log_archive_parameters"
---

The logging service provided by Flink itself is rather limited. To support more flexible operations such as keyword and key\-value pair (KV) queries, log statistics, and log alarms for business logs, export runtime logs to the BytePlus log service TLS, thereby providing stronger support for monitoring and troubleshooting Flink tasks.

<span id="1730ab9c"></span>
## Functional Limitations

Currently, only Flink versions 1.16\-byted and above support Flink log TLS export tasks; earlier versions do not support log exporting.

<span id="0dcdf9a4"></span>
## Operation Steps


1. Log in to [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, use the search box to perform a fuzzy search based on the project name, and then click on the project block to enter the project.

4. In the project's left navigation bar, select **Task Development**, then click on the target task within the target folder.

5. In the task editing area on the right, select the "Open Log Archiving" function from the pop\-up drawer of **Logs**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ab4affbe7784b5ebf61de9a01baeed8~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Root Log Level |Customize the selection of the root log's log level.<br><br>All logs above this level will be automatically exported globally. To reduce TLS storage costs, you can choose to export logs at the desired log level on demand. The current supported log levels are: TRACE, DEBUG, INFO, WARN, ERROR, FATAL. |
|Category Log Level |Supports custom log level settings based on class modules.<br><br>Exports will be carried out according to the logging level of a specific class. The priority is class log level \> root log level.<br><br>> Note: The class name must be the full path name of the class, such as com.bytedance.MyClass |
|TLS Custom Parameters |* topicId: The target Topic for log writing. Refer to [Log Topic](https://docs.byteplus.com/en/docs/tls/Managing_topics).<br><br>* region: The region of the TLS service. Refer to [TLS service address](https://docs.byteplus.com/en/docs/tls/endpoint).<br><br>* accessKeyId: The Access Key ID for accessing TLS. Please note that this access account needs to have TLS write permissions enabled.<br><br>* accessKeySecret: Access the TLS with the Access Key Secret.<br><br>* endpoint: The address of the TLS service. You can refer to the [TLS service address](https://docs.byteplus.com/en/docs/tls/endpoint). |
