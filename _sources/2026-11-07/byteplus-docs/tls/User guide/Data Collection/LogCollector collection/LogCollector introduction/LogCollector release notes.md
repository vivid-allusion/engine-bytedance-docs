---
title: "LogCollector release notes"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/logcollector_release_notes"
---

This topic describes the main features of each version of LogCollector.

<span id=".54mI5pys57G75Z6L"></span>
## Version types

Torch Log Service offers the following LogCollector version types:


|Version Type |Description |
|---|---|
|Beta |The test version of LogCollector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Beta version is only available for the customers who are in the allowlist for canary release. If you want to use this version LogCollector, contact sales.</div><br> |
|Latest official version |The latest official version of LogCollector is a version released to the public. The latest official version features stable and reliable performance. To download and install the latest official version of LogCollector, refer to [Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host).<br><br>To upgrade to the latest version:<br><br><br>* If the automatic upgrade feature is enabled for a host group, Torch Log Service (TLS) automatically upgrades LogCollector installed on the hosts in the group to the latest version.<br><br>* If the automatic upgrade feature is not enabled, you must manually upgrade the version.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To ensure the service quality and performance of LogCollector, we recommend that you use the latest official version of LogCollector.</div><br> |
|Historical versions |The previously published versions. TLS does not allow you to download a historical version of LogCollector. |


<span id=".54mI5pys5YiX6KGo"></span>
## Version list


|Version Number |Version types |Release notes |
|---|---|---|
|2.3.5 |Latest official version |Solved the issue where collecting symbolic links failed when multiple collection rules separately enforced to collect both symbolic links and real files. |
|2.3.4 |Historical version |Fixed a crash caused by segmentation faults on certain operating systems. |
|2.3.3 |Historical version |Resolved an issue where Cpu/Mem values were reported as 0 in the service logs. |
|2.3.2 |Historical version |* Optimizes LogCollector upgrade and downgrade operations, along with other maintenance tasks.<br><br>   * Adds manual LogCollector upgrade and downgrade functionality in the console.<br><br>   * Adds batch restart host group functionality in the console.<br><br>   * Adds functionality to configure LogCollector in the console.<br><br>   * Updates the entry point for configuring automatic LogCollector upgrades.<br><br>* Internal optimization. |
|2.2.9 |Historical version |Internal optimization. |
|2.2.7 |Historical version |Internal optimization. |
|2.2.5 |Historical version |* Adds JSON extraction plugin.<br><br>* Adds field segmentation and recombination plugin.<br><br>* Adds URL parsing plugin<br><br>* Adds field retention plugin |
|2.2.0 |Historical version |* Optimized some plugins to support conditional processors.<br><br>* Optimized the deployment scripts and installation scripts for Kubernetes scenarios, enabling LogCollector installation via the Helm method.<br><br>* Container collection now supports Pod Annotation filtering.<br><br>* Improved the collection performance of single\-line and multi\-line regular expression collection modes.<br><br>* Supports customizing the maximum length of a single log entry.<br><br>* The time parsing processor now supports customizing the year.<br><br>* Supports more operating systems. |
|2.1.1 |Historical version |Internal optimizations. |
|2.1.0 |Historical version |* It supports that the standard output of log files or containers can be simultaneously matched and collected by multiple collection rules.<br><br>* Dynamically configure the handle release time according to the graceful exit configuration of Pods.<br><br>* Internal optimizations. |
|2.0.0 |Historical version |* The LogCollector Daemon process has been added, which is used to manage and control the LogCollector process, hot\-load the LogCollector configuration files, report the LogCollector panic information, and other related tasks.<br><br>* The Checkpoint storage mechanism has been optimized.<br><br>* The incremental collection has been optimized by ignoring the limitation that the incremental collection only takes effect when LogCollector is deployed for the first time.<br><br>* The collection performance has been optimized.<br><br>* The resource consumption has been optimized.<br><br>* Internal optimizations. |
|1.0.52 |Historical version |* It supports collecting all Labels of Kubernetes Pods.<br><br>* Internal optimizations. |
|1.0.50 |Historical version |* Support reporting the **Label** field of the machine group.<br><br>* Support parsing nanosecond time. |
|1.0.48 |Historical version |* Optimize the installation and deployment steps of LogCollector.<br><br>* Single log length limit changes.<br><br>   The maximum length of a single log is 512 KiB. If it exceeds 512 KiB, the log will be split into multiple strips for collection.<br><br>* Added time resolution plugin.<br><br>* More time conversion formats are supported when parsing time.<br><br>* Internal optimization. |
|1.0.44 |Historical version |Internal optimization. |
|1.0.42 |Historical version |Internal optimization. |
|1.0.40 |Latest official version |* The hostname field is supported.<br><br>* Internal optimization. |
|1.0.38 |Historical versions |* Conditions can be set for triggering plug\-ins.<br><br>* The name of the field that is used to store original logs can be replaced with a custom name.<br><br>* Collects standard outputs from containers and is compatible with the container services of Huawei Cloud and Tencent Cloud. |
|1.0.36 |Historical versions |Internal optimization. |
|1.0.34 |Historical versions |* The inotify mechanism can be used to detect log files.<br><br>* Quote characters can be used in the delimiter\-based collection mode, the delimiter\-based field extractor, and the KV\-based field extractor.<br><br>* The desensitize plug\-in and replace plug\-in are supported. |
|1.0.30 |Historical versions |* The issues of duplicated log collection or missed log collection due to inode reuse are resolved.<br><br>* PCRE regular expressions are supported.<br><br>* Internal optimization. |
|1.0.28 |Historical versions |The authentication logic for LogCollector deployed in VKE and VCI environments is optimized. |
|1.0.26 |Historical versions |* Metadata placeholders can be contained in collection paths and denylists of collection paths.<br><br>* Wait queues are supported for log rotation scenarios. By default, a wait queue can contain up to 20 log entries.<br><br>* Internal optimization. |
|1.0.24 |Historical versions |Internal optimization. |
|1.0.23 |Historical versions |* The `ip_policy` parameter can be configured in the YAML configuration file to specify the policy of getting the IP address of the current host or container.<br><br>* Internal optimization for the automatic upgrade logic and other features. |
|1.0.22 |Historical versions |The occasional issue of repeated collection of inactive log files is resolved. |
|1.0.21 |Historical versions |* Potential file handle leaks in log rolling scenarios are resolved.<br><br>* The performance is optimized. |
|1.0.18 |Historical versions |* Double asterisks ( `**` ) can be contained in collection paths when collecting logs from containers.<br><br>* The add_kvs plug\-in is supported.<br><br>* Pod annotations can be connected when collecting logs from containers. |
|1.0.17 |Historical versions |* Potential deadlock issues in log rolling scenarios are resolved.<br><br>* The issue that causes container initialization log collection failures is resolved. |
|1.0.15 |Historical versions |Internal optimization. |
|1.0.14 |Historical versions |The issue related to automatic upgrade is resolved. |
|1.0.12 |Historical versions |* LogCollector plug\-ins and extension configurations are supported.<br><br>* Download links are fixed.<br><br>* Service logs and incremental logs can be collected.<br><br>* Other internal optimizations. |
|1.0.10 |Historical versions |The following issue is resolved: In scenarios where LogCollector collects logs from physical machines, it fails to collect the log if the file handle exceeds the system limit. |
|1.0.9 |Historical versions |* Constant fields can be uploaded.<br><br>* Internal optimization. |
|1.0.8 |Historical versions |\*LogCollector on hosts can be automatically upgraded.<br><br><br>* NGINX\-based log collection mode is supported.<br><br>* Original logs can be uploaded. |
|1.0.7 |Historical versions |Internal performance optimization. |
|1.0.6 |Historical versions |HashKey\-based shard routing is supported. |
|1.0.5 |Historical versions |* Regex\-based collection path parsing is supported, and the fields parsed from collection paths are recorded in log metadata.<br><br>* Internal performance optimization. |
|1.0.4 |Historical versions |LogCollector can be installed in Kubernetes clusters to collect text logs and standard outputs from containers using DaemonSets. |
|1.0.3 |Historical versions |* LogCollector can be installed in a custom directory.<br><br>* Authentication parameters such as the parameters specifying your AccessKey pair can be configured in a script. |
|1.0.2 |Historical versions |Internal performance optimization. |
|1.0.1 |Historical versions |* Text logs can be collected in single\-line full\-text mode, delimiter\-based mode, and other modes. To collect logs in other modes, contact Technical Support.<br><br>* Traffic control, resumable collection, and other features are supported.<br><br>* The inputs section is removed from the `filebeat.yml` configuration file template, and no sample collection rules are offered. |
