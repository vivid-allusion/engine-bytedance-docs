---
title: "Collect container logs overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/collect_container_logs_overview"
---

Torch Log Service (TLS) can collect container text logs and standard output from a Kubernetes cluster using a DaemonSet or sidecar. This topic describes how to use a DaemonSet or sidecar to collect container logs from a Kubernetes cluster.

<span id="功能特点"></span>
## Features

TLS LogCollector can collect log files and standard output from containers and upload the collected log data along with the container metadata to a server. When LogCollector collects container logs, the following capabilities are offered:


* It supports general container collection rules.

   * It allows you to specify the container collection scope through the allowlist and denylist of container labels and environment variables.

   * It can upload the container name, image, and other metadata to TLS as log fields along with the collected log data.

* It allows you to specify Kubernetes collection rules. When a container runs in a Kubernetes cluster, LogCollector can offer the following features:

   * It allows you to specify the containers of which the logs are to be collected using Kubernetes namespace names, pod names, and workload types and names.

   * It allows you to specify the container collection scope through the allowlist and denylist of pod labels.

   * It can upload container metadata such as namespaces, pod names, pod UIDs, and pod IP addresses to TLS as log fields.

* It allows you to specify single\-line, multi\-line, delimiter\-based, and other log collection modes and offers compatibility with various collection rules.

* It allows you to specify a log file path in a container for collecting data from that path when you collect container text logs.


<span id="采集方式"></span>
## Collection methods

TLS allows you to collect container logs from a Kubernetes cluster using a DaemonSet or sidecar.


|Collection Method |Description |Document |
|---|---|---|
|DaemonSet |LogCollector is deployed on each node of a Kubernetes cluster to collect all container logs that require collection on each node to a server.<br><br>LogCollector collects all logs on their nodes, which means you can customize it within a limited degree. Therefore, this method is suitable for clusters with limited features.<br><br>It can collect standard output and text logs from containers. |* [Configure a DaemonSet in the console for collecting standard logs from a container](https://docs.byteplus.com/docs/tls/collecte_stdout_daemonset)<br><br>* [Configure a DaemonSet in the console for collecting text logs from a container](https://docs.byteplus.com/docs/tls/collecte_text_logs_daemonSet)<br><br>* [Use CRD to configure a DaemonSet for collecting logs from a container](https://docs.byteplus.com/docs/tls/collecte_logs_daemonSet_CRD) |
|Sidecar |A pod runs a LogCollector container in sidecar mode to collect logs produced by the pod.<br><br>This method features high isolation. Therefore, this method is suitable for multi\-tenant scenarios and scenarios with high collection performance requirements.<br><br>This method can collect container text logs. |* [Configure a sidecar in the console for collecting logs from a container](https://docs.byteplus.com/docs/tls/collect_logs_sidecar_console)<br><br>* [Use CRD to configure a sidecar for collecting logs from a container](https://docs.byteplus.com/docs/tls/collect_logs_sidecar_crd) |


<span id="容器日志采集流程"></span>
## Container log collection process

<span id="daemonset-方式采集流程"></span>
### Collection process of the DaemonSet method

Follow the steps below to install LogCollector and configure container log collection rules.


1. Install LogCollector in a Kubernetes cluster.

   For more information, refer to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet).

2. Create a host group.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you use a host group of the host label type. Specify the host label as the custom label configured when you install LogCollector. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group">Create a label\-based host group</a>.   </div>
   

3. Create log collection rules in the console.

   TLS allows you to collect container text logs and standard output from a Kubernetes cluster using a DaemonSet.

   * [Configure a DaemonSet in the console for collecting standard logs from a container](https://docs.byteplus.com/docs/tls/collecte_stdout_daemonset)

   * [Configure a DaemonSet in the console for collecting text logs from a container](https://docs.byteplus.com/docs/tls/collecte_text_logs_daemonSet)

   * [Use CRD to configure a DaemonSet for collecting logs from a container](https://docs.byteplus.com/docs/tls/collecte_logs_daemonSet_CRD)


<span id="sidecar-方式采集流程"></span>
### Collection process of the sidecar method

Follow the steps below to install LogCollector and configure container log collection rules.


1. Install LogCollector in a Kubernetes cluster.

   For more information, refer to [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar)

2. Create a host group.

   We recommend that you use a host group of the host label type. Specify the host label as the custom label configured when you install LogCollector. For more information, refer to [Create a label-based host group](https://docs.byteplus.com/docs/tls/Create_a_label-based_host_group).

3. Create log collection rules in the console.

   You can collect container text logs using a sidecar. When you create a collection rule, choose the corresponding collection mode based on the text log style without checking the **Container log** option. For more information, refer to:

   * [Configure a sidecar in the console for collecting logs from a container](https://docs.byteplus.com/docs/tls/collect_logs_sidecar_console)

   * [Use CRD to configure a sidecar for collecting logs from a container](https://docs.byteplus.com/docs/tls/collect_logs_sidecar_crd)
