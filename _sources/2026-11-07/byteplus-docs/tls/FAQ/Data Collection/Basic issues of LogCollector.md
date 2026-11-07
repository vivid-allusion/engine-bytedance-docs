---
title: "Basic issues of LogCollector"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Basic-issues-of-LogCollector"
---

This article lists the basic problems of LogCollector.

<span id="74e6d811"></span>
## How to install and upgrade LogCollector?

The relevant reference for installing LogCollector is as follows:


* [Install LogCollector on a host](https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host)

* [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet)

* [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar)


The relevant reference for upgrading LogCollector is as follows:


* [Upgrade LogCollector on a host](https://docs.byteplus.com/docs/tls/upgrade_logcollector_on_a_host)

* [Upgrade LogCollector in a Kubernetes cluster](https://docs.byteplus.com/docs/tls/upgrade_logcollector_in_a_kubernetes_cluster)


<span id="1eda036a"></span>
## How to configure LogCollector to collect logs?


* Collect host logs

   * [Collect logs in Single-line full-text mode](https://docs.byteplus.com/docs/tls/single_line_full_text_mode)

   * [Collect logs in Multi-line full-text mode](https://docs.byteplus.com/docs/tls/multi_line_full_text_mode)

   * [Collect logs in Full regex-based single-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_single_line_mode)

   * [Collect logs in Full regex-based multi-line mode](https://docs.byteplus.com/docs/tls/full_regex_based_multi_line_mode)

   * [Collect logs in Delimiter-based mode](https://docs.byteplus.com/docs/tls/delimiter_based_mode)

   * [Collect logs in NGINX-based mode](https://docs.byteplus.com/docs/tls/nginx_based_mode)

   * [Collect logs in JSON mode](https://docs.byteplus.com/docs/tls/json_mode)

* Capture container logs

   * [Configure a DaemonSet in the console for collecting text logs from a container](https://docs.byteplus.com/docs/tls/collecte_text_logs_daemonSet)

   * [Configure a DaemonSet in the console for collecting standard logs from a container](https://docs.byteplus.com/docs/tls/collecte_stdout_daemonset)

   * [Use CRD to configure a DaemonSet for collecting logs from a container](https://docs.byteplus.com/docs/tls/collecte_logs_daemonSet_CRD)

   * [Use Pod to configure a DaemonSet for collecting logs from a container](https://docs.byteplus.com/docs/tls/Use-Pod-to-configure-a-DaemonSet)

   * [Use CRD to configure a sidecar for collecting logs from a container](https://docs.byteplus.com/docs/tls/collect_logs_sidecar_crd)

   * [Use CRD to configure a sidecar for collecting logs from a container](https://docs.byteplus.com/docs/tls/collect_logs_sidecar_crd)

* acquisition configuration management

   * [LogCollector collection rule management](https://docs.byteplus.com/docs/tls/logcollector_collection_rule_management)


<span id="32e64888"></span>
## Does LogCollector support log rotation?

LogCollector supports log collection in the scenario of log file rotation.


* (Recommended) Rename log file rotation: When a log file reaches a certain size or time limit, the current log file is renamed to a new file name, such as adding a timestamp or serial number. Then a new log file is created and new logs continue to be written into it. For example, if the original log file is `bar.log`, after rotation, log files like `bar.log.1`, `bar.log.2` will be generated.

   LogCollector will automatically recognize the log files before and after rotation to ensure the integrity of the logs.

   If the log file rotation is too frequent and a large number of log files are created by rotation within a short period of time, then LogCollector will only collect 20 rotated log files at the same time. Rotated logs exceeding 20 cannot be collected, which may lead to the situation that some rotated log files are deleted before being collected, resulting in log loss.

* Copytruncate log file rotation: When a log file reaches a certain size or time limit, the current log file is copied into a new log file, such as adding a timestamp or serial number. Then the original log file is emptied and new logs continue to be written into it. For example, if the original log file is `bar.log`, after rotation, log files like `bar.log.1`, `bar.log.2` will be generated.

   * Assume that the configured collection path is `bar.log`. When there is a collection delay in LogCollector, the copytruncate log file rotation will lead to the loss of the logs with delayed collection.

   * Assume that the configured collection path is `bar.log*`. The copytruncate log file rotation will lead to the repeated collection of the logs that have already been collected.


<span id="1402c5b1"></span>
## Log Collection Delay Situation of LogCollector

LogCollector uses a polling mechanism and an event listening mechanism to collect logs. Generally, it will send logs to TLS within 3 seconds.

The collection performance of Logcollector is related to the allocated system resources and the collection mode. For specific details, please refer to [Recommended parameter values](https://docs.byteplus.com/docs/tls/Configure-the-startup-parameters-of-LogCollector#2fdc46f3).

<span id="59c9f6b5"></span>
## How long does it take for the changes to the LogCollector collection configuration to take effect?

After you modify the LogCollector collection configuration in the TLS console, LogCollector will load the new configuration and make it take effect within 1 minute.

<span id="3f56cb34"></span>
## Why is the LogCollector heartbeat IP displayed by the machine group inaccurate?

By default, LogCollector uses the IP address of the first network card as the host machine or container IP address. You can adjust it to read the IP address of the specified network card or obtain the IP address according to a certain order. For detailed instructions, please refer to [Configure an IP address for a host or container](https://docs.byteplus.com/docs/tls/configure_an_ip_address_for_a_host_or_container).

In the Kubernetes scenario, by default, LogCollector will use the Pod IP address as the heartbeat IP address and report it to TLS. If you need to use the node IP address as the LogCollector heartbeat IP address, you can modify the LogCollector daemonset configuration file and add two configuration items: `hostNetwork: true` and `dnsPolicy: ClusterFirstWithHostNet`.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5585e224e47c40f6a1b82d735b58dee7~tplv-goo7wpa0wc-image.image" width="1005px" /></div>
