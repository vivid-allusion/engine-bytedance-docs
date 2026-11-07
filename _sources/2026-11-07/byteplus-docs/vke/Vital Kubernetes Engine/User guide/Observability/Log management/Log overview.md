---
title: "Log overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Log-overview"
---

Powered by [Torch Log Service (TLS)](https://docs.byteplus.com/en/docs/tls/What_is_TLS), ** ** VKE provides log\-related features, including container log collection, keyword search, and SQL analysis.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

[TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS) supports query and analysis in seconds for large volumes of data, provides efficient and real\-time log processing tools, facilitates the use of log data, and effectively improves O&M capabilities as well as data analysis efficiency.

You can use the log feature to persistently store VKE logs and events in TLS. After a cluster fails, you can also view historical log information in TLS for troubleshooting.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The log feature of VKE is implemented through <a href="https://docs.byteplus.com/en/docs/tls/What_is_TLS">TLS</a>.</div>


* <div data-tips="true" data-tips-type="tip">Related fees will be incurred if you use the features of TLS. For detailed billing instructions, see <a href="https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode">TLS billing instructions</a>.</div>



<span id=".5pel5b-X57G75Z6L"></span>
## Log types

VKE clusters support log collection for multiple resources, such as container logs, add\-on logs, and control plane add\-on logs. By collecting and querying logs, you can understand the running status of basic resources, key add\-ons, and applications in clusters, and perform troubleshooting when failures occur. The following table describes the supported collection objects.


|Collection target |Description |
|---|---|
|Container log |* **Container standard output**: The logs from a container are sent to the standard output device (Stdout) and standard error device (Stderr) of the container. These two standard output devices are the console terminals of the container.<br><br>* **Container file path**: In addition to the container standard output devices, the logs of most applications are written to log files in fixed paths. You can obtain the logs of a specified container by specifying the log file path in the container. For example, VKE outputs GPU Xid\-related information to the log file `/var/log/xid.log` of the pod. You can obtain the GPU Xid log of the pod by using this path. The GPU Xid log allows you to view the time when Xid occurs and view specific details, which facilitates troubleshooting for GPU devices.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can directly view the content of container standard output logs by using the <code>kubectl logs</code> command.</div><br> |
|Add\-on log |The access logs of the ingress\-nginx add\-on can be collected. The system collects the standard output logs of the ingress\-nginx add\-on and sends them to TLS for storage and retrieval. |
|Control plane add\-on log |Control plane add\-on logs primarily apply to the main control plane add\-ons in clusters, which allow you to understand the status and records of the cluster control plane. Add\-ons include kube\-apiserver, kube\-scheduler, kube\-controller\-manager, and etcd. |


<span id=".5pel5b-X5qOA57Si"></span>
## Log retrieval

VKE provides persistent storage and retrieval features for cluster logs by using TLS. For details, see [Log retrieval](https://docs.byteplus.com/en/docs/tls/Query-overview-2).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS also supports features such as log delivery, log consumption, and alerts and monitoring. For details, see <a href="https://docs.byteplus.com/en/docs/tls/What_is_TLS">TLS documentation</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

The log\-collector add\-on required for collecting VKE cluster logs needs to be upgraded to v1.1.0 or later. For add\-on upgrade operations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).
