---
title: "log-collector"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/log-collector"
---

The log\-collector is a log collection add\-on for clusters. It collects cluster logs and sends them to Torch Log Service (TLS). This topic describes the change history of the log\-collector add\-on.

For more information about this add\-on, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

<span id="PjTmQAq0"></span>
## December 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.3.3 |All versions |Maintained |* It adds support for machine group LogCollector O&M (such as upgrading, degrading, restarting, and updating configurations).<br><br>* The inotify watch directory limit has been expanded to 1000.<br><br>* LogCollector logs include more information.<br><br>* Optimization is made to fix known issues. |None |


<span id="PjTmQAq0"></span>
## November 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.2.9 |All versions |Maintained |The node\-ip is used in reporting heartbeat messages. |None |


<span id="L2ItuuOk"></span>
## July 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.2.7 |All versions |Maintained |* Fixed memory leaks that occurred in data collection scenarios.<br><br>* Allow anonymous collection of AK/SK logs. |None |
|v2.2.6 |All versions |Maintained |* Segmentation faults occurring on some operating systems are resolved.<br><br>* Taint tolerance can be configured by using key\-value pairs. |None |


<span id="tna2E0k5"></span>
## June 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.2.5 |All versions |Maintained |* The processor add\-ons including json_extract, keep_fields, splitselect, and urlparse are supported.<br><br>* Supports configuring the CPU Quota and Memory Limit. |None |
|v2.1.4 |All versions |Maintained |* Fixes the worker leakage issue when more than 20 log files are rotated simultaneously.<br><br>* Fixes the issue where the `%F` time format caused the parsed time to be negative. |None |


<span id="2SLn2WLw"></span>
## May 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.1.3 |All versions |Maintained |* The issue where logs are occasionally repeated when logcollector Pod restarts is fixed.<br><br>* Fixes the out\-of\-order log context issue when close_eof is enabled. |None |


<span id="Ym7aMYYQ"></span>
## April 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.1.2 |All versions |Maintained |Fixes the issue where log file handles may be leaked when log files are truncated. |None |


<span id="N9ZBeMTJ"></span>
## January 2025


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.1.1 |All versions |Maintained |Internal optimizations. |None |


<span id="L3B2kJoC"></span>
## November 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.1.0 |All versions |No longer maintained |* By default, Secret permissions are disabled for the add\-on.<br><br>* The performance is optimized.<br><br>* Files can be collected into multiple topics. |None |


<span id="_2024-08"></span>
## August 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.8 |All versions |No longer maintained |* The authentication method through Secret mounting is supported.<br><br>* The issue where log transmission is blocked when a single standard output log exceeds 10 MB is fixed.<br><br>* More time formats can be parsed. |None |


<span id="_2024-05"></span>
## May 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.4 |All versions |No longer maintained |* The length limit of a single log is changed. If a single log exceeds 512 KB, the extra part is separately sent instead of being truncated and discarded. If a single log exceeds 2 MB, it will not be directly discarded. Instead, it will be truncated into multiple logs before being sent.<br><br>* The time processor add\-on is supported.<br><br>* More time formats can be parsed. |None |


<span id="_2024-04"></span>
## April 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.2 |All versions |No longer maintained |* The specifications of the add\-on can be configured.<br><br>* Supports deployment as a Vital Container Instance (VCI). |None |


<span id="_2024-03"></span>
## March 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v2.0.1 |All versions |No longer maintained |* The `hostname` field can be added.<br><br>* The processor add\-on can be executed by a condition.<br><br>* You can specify custom key names in original logs. |None |


<span id="_2023-11"></span>
## November 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.6 |All versions |No longer maintained |Optimized for stability. |None |


<span id="_2023-09"></span>
## September 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.5 |All versions |No longer maintained |JSON logs can be collected. |None |


<span id="_2023-07"></span>
## July 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.3 |All versions |No longer maintained |Fixes some performance issues. |None |


<span id="_2023-05"></span>
## May 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.2 |All versions |No longer maintained |The issue of Pod collection in short lifecycles is fixed. |None |
|v1.2.1 |All versions |No longer maintained |The add\-on architecture is optimized. |None |


<span id="_2023-03"></span>
## March 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.0 |All versions |No longer maintained |* The format of container log metadata is unified in Vital Kubernetes Engine (VKE) and TLS.<br><br>* After you create a log collection rule, you cannot modify the rule name. This ensures that the tag of the log collection rule remains stable. |None |


<span id="_2023-02"></span>
## February 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.5 |All versions |No longer maintained |The issue of log collection being stuck is fixed. |None |


<span id="_2023-01"></span>
## January 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.4 |All versions |No longer maintained |The issue where logs are repeatedly collected after a pod restarts is fixed. |None |
|v1.1.3 |All versions |No longer maintained |Internal field collection is optimized. |None |


<span id="_2022-09"></span>
## September 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.0 |All versions |No longer maintained |The container log collection rules of VKE are consolidated into TLS. Collection rules are provisioned by TLS in a centralized manner. |The update of existing collection rules is affected. For a detailed description, see [Collecting container logs](https://docs.byteplus.com/en/docs/vke/Collecting-container-logs). |


<span id="_2021-08"></span>
## August 2021


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.0 |All versions |No longer maintained |The first release of the log\-collector add\-on. |None |
