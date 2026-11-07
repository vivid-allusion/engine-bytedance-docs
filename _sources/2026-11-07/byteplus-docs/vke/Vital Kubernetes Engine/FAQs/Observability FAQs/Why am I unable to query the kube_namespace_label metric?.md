---
title: "Why am I unable to query the kube_namespace_label metric?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cannot-query-the-kube_namespace_label-metric"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

After you upgrade the prometheus\-agent add\-on in a cluster to v2.5.0\-vke.1.24 or later, the `kube_namespace_label` metric of kube\-state\-metrics cannot be queried.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

When the prometheus\-agent add\-on is upgraded to v2.5.0\-vke.1.24 or later, the kube\-state\-metrics add\-on is also upgraded to a later version. The changes to the later versions of the kube\-state\-metrics add\-on are as follows:


* Metrics related to `kube_*_annotations` and `kube_*_labels`, which were exposed by default in the earlier versions, are no longer exposed by default in the later versions. Therefore, the corresponding metrics cannot be queried after the upgrade. However, the `kube_pod_labels` metric can still be queried.

* Metrics related to `kube_verticalpodautoscaler_.*` have been deprecated.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><code>*</code> in the preceding metrics indicates a wildcard. For example, <code>kube_*_annotations</code> refers to metrics such as <code>kube_namespace_annotations</code> and <code>kube_pod_annotations</code>.</div>


* <div data-tips="true" data-tips-type="tip">For detailed descriptions of changes to the kube\-state\-metrics add\-on, see <a href="https://github.com/kubernetes/kube-state-metrics/pull/2145">community documentation</a>.</div>


* <div data-tips="true" data-tips-type="tip">This issue only affects v2.5.0\-vke.1.24 and later of the prometheus\-agent add\-on. v2.5.0\-vke.1.20 and later are not affected. For details, see <a href="https://docs.byteplus.com/en/docs/vke/prometheus-agent">Add\-on release records</a>.</div>



<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

If you are using metrics related to `kube_*_annotations` and `kube_*_labels` to create a dashboard, you can use the following solutions:


* Replace `kube_*_annotations` or `kube_*_labels` metrics with the corresponding `kube_*_created` or `kube_*_info` metrics. For example, change the `kube_namespace_label` metric to the `kube_namespace_created` metric.

* Use the latest [official dashboard](https://grafana.com/grafana/dashboards/5225-kubernetes-deployments/) to re\-create your monitoring dashboard.
