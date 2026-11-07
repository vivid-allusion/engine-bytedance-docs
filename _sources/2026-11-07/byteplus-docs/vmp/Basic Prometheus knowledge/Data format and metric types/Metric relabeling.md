---
title: "Metric relabeling"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Metric_relabel"
---

Metric relabeling is an important and frequently used feature in Prometheus. This topic describes the basic usage methods and common examples of metric relabeling to help you quickly get started with and perform metric relabeling.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The following sample code shows the standard format of a metric collected from a target in Prometheus.

```html
http_requests_total{method="POST", handler="/api/v1/vmp", status="200"} 1024
```


You can perform the following operations by using metric relabeling:


* Add, modify, or delete the key or value of a label in the original metric.

* Filter collection targets during service discovery.


<span id=".5Z-656GA55-l6K-G"></span>
## Basic knowledge

Raw job and ServiceMonitor or PodMonitor In most cases, [scrape config](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#scrape_config) is used to configure objects for which you want to collect metrics in Prometheus. In addition to configuring relabeling, you can configure service discovery. For example, if you want to collect the metrics of a Node or a Pod in a Kubernetes environment, you can use `kubernetes_sd_config` to configure service discovery. Prometheus operators are often used in Kubernetes for configuration management and deployment because the configuration of the raw job is relatively complex and inefficient. Prometheus operators implement several custom resource definitions (CRDs), including ServiceMonitor and PodMonitor, for configuring Kubernetes resource metric collection. In fact, the configurations of ServiceMonitor or PodMonitor are converted by Prometheus Operator into the configurations of the Prometheus raw job, which are essentially still the configurations of `kubernetes_sd_config`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you use <a href="https://prometheus-operator.dev/docs/api-reference/api/#monitoring.coreos.com/v1.RelabelConfig">relabelConfig</a> in the raw job or ServiceMonitor/PodMonitor for relabeling configuration, slight differences exist in the format:</div>



* <div data-tips="true" data-tips-type="tip">Fields in the raw job are in <strong>snake_case</strong> format, in which each space in a phrase is replaced with an underscore (_), and all words are written in lowercase.</div>


* <div data-tips="true" data-tips-type="tip">Fields in ServiceMonitor/PodMonitor are in <strong>camelCase </strong>format.</div>



<div data-tips="true" data-tips-type="tip">The preceding differences only exist between <code>sourceLabels</code> and <code>source_labels</code> and between <code>targetLabel</code> and <code>target_label</code>.</div>


Internal labels In Prometheus metrics, a metric name is a label that is named `__metric_name__`. Therefore, a metric can be viewed as a `key-value` pair. The following sample code shows a sample metric name.

```html
{__metric_name__="http_requests_total", method="POST", handler="/api/v1/vmp", status="200"} 1024
```


In addition, some label keys start with double underscores (`__`) to indicate system built\-in labels.  


* `__name__`: the name of the scraped metric

* `__address__`: the host and port of the scrape target, which is in the format of `host:port`

* `__scheme__`: the URI scheme of the scrape target, such as http and https

* `__metrics_path__`: the metrics path of the scrape target

* `__param_<name>`: the value of the first URL parameter passed to the target, where `<name>` is the parameter name

* `__scrape_interval__`: the scrape interval of the target

* `__scrape_timeout__`: the timeout of the target

* `__meta__`: a special set of labels set by the service discovery mechanism

* `__tmp`: a special prefix used for temporarily storing label values before discarding them. 


`__meta__` indicates the built\-in labels configured by service discovery. If you want to use `kubernetes_sd_config` or ServiceMonitor/PodMonitor, refer to the [official documentation of Prometheus](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#kubernetes_sd_config) for more details about built\-in labels.

```html
__meta_kubernetes_node_name
__meta_kubernetes_node_provider_id
__meta_kubernetes_node_label_<labelname>
__meta_kubernetes_node_labelpresent_<labelname>
__meta_kubernetes_node_annotation_<annotationname>
__meta_kubernetes_node_annotationpresent_<annotationname>
__meta_kubernetes_node_address_<address_type>
```


Multiple relabeling stages Prometheus allows you to configure relabeling by using multiple configurations. The most commonly used configurations are `relabel_configs` and `metric_relabel_configs`, which have the same configuration structure and fields but differ in the validity time.

```yaml
scrape_configs:
    - job_name: "test"
    ...
    relabel_configs:
    [ - <relabel_config> ... ]

    metric_relabel_configs:
    [ - <relabel_config> ... ]

remote_write:
    write_relabel_configs:
    [ - <relabel_config> ... ]
```


The following differences exist between the two configurations:


* `relabel_configs` takes effect when targets are being scraped. It is the only configuration that can obtain the built\-in labels from service discovery. At this stage, in addition to processing labels, you can filter the resources of service discovery based on the built\-in labels.

* `metric_relabel_configs`  takes effect after the target metrics are scraped and before the metrics are stored. If you use the prometheus\-agent add\-on to collect metrics in a Vital Kubernetes Engine (VKE) cluster, metric_relabel_configs takes effect before the remote\-write stage when the metrics are being sent to a Vital Managed Service for Prometheus (VMP) workspace.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">System labels that start with a double underscore <code>(__)</code> will be discarded after <code>relabel_configs</code></div>


<span id=".6YWN572u5a2X5q61"></span>
## Configuration fields

The following table describes the configuration fields in `relabel_config`.


| | | | | | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | | | | | | | | |
| | | | | | | | | | | | | | | | | |
| | | | | | | | | | | | | | | | | |
| | | | | | | | | | | | | | | | | |
| | | | | | | | | | | | | | | | | |
| | | | | | | | | | | | | | | | | |
| | | | | | | | | | | | | | | | | |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Pay attention to the default values of the fields. You may not need to specify some fields because the default values of these fields already meet the requirement in some relabeling configurations. For example, the default value of <code>action</code> is <code>replace</code>. If you are not clear about this rule, you may not understand some configurations.</div>


<span id=".6YWN572u56S65L6L"></span>
## Configuration example

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following configuration examples are provided if the original metric is <code>http_requests_total{method="POST", handler="/api/v1/vmp", status="200"} 1024</code>.</div>


<span id="replace"></span>
### replace

Create or overwrite a label Use the following configuration to create or overwrite a label in the original metric. First, obtain the value of the specified source label (`status`) in `source_labels` and then write the value into the target label (`status_code`) in `target_label`.

```yaml
- source_labels: [status]
  target_label: status_code
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The default value of <code>action</code> is <code>replace</code>. Therefore, the <code>action: replace</code> field is not specified in this configuration.</div>


* <div data-tips="true" data-tips-type="tip">Literally, <code>replace</code> means <strong>replace</strong>. It actually takes effect in the following logic:</div>


   * <div data-tips="true" data-tips-type="tip">If the values of <code>target_label</code> and <code>source_labels</code> are the same, <code>source_label</code> is overwritten.</div>


   * <div data-tips="true" data-tips-type="tip">If the key defined by <code>target_label</code> does not exist, a new label will be created by default. The following sample code shows the expected metric, in which a new label <code>status_code</code> is created in the original metric, and the new label value <code>200</code> is the value of the source label <code>status</code>.</div>



```html
http_requests_total{method="POST", handler="/api/v1/vmp", status="200", status_code="200"} 1024
```


Specify the value of a label In this example, `replacement` is used to add a new fixed label. The value is the fixed value in `replacement`. If `replacement` is not configured, the value of the specified label in `source_labels` will be used.

```yaml
- action: replace
  replacement: "success"
  target_label: status_code
```


The following sample code shows the expected metric, in which a new label `status_code` is created in the original metric, and its value is the fixed value `success` configured in `replacement`.

```html
http_requests_total{method="POST", handler="/api/v1/vmp", status="200", status_code="success"} 1024
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default value of <code>replacement</code> is <code>$1</code>. Therefore, you can use <code>replacement</code> with regular expressions to flexibly change labels. For more details, refer to the following sections.</div>


<span id=".bGFiZWwg5YC855qE5ou85o6l"></span>
#### Concatenate label values

Use the following configuration to create a new label in the original metric and obtain the values corresponding to the list of `source_labels`. Then, concatenate the values by using the separator defined by `separator` to generate a new label value.

```yaml
- action: replace
  source_labels: [method, handler]
  separator: "#"
  target_label: url
```


The following sample code shows the expected metric, in which the value of the new label `url` is `POST#/api/v1/vmp`, which is the concatenation result of the values of `method` and `handler` with the separator `#`.

```html
http_requests_total{method="POST", handler="/api/v1/vmp", status="200", url="POST#/api/v1/vmp"} 1024
```


<span id=".5L2_55So5q2j5YiZ6KGo6L6-5byP5L-u5pS5IGxhYmVs"></span>
#### Modify a label by using a regular expression

In addition to being used for specifying fixed values, `replacement` can also be used to achieve more complex changes with `regex`. Configuration example:

```yaml
- action: replace
  source_labels: [method, handler]
  separator: "#"
  regex: "(.*)#(.*)"
  replacement: "$2 $1"
  target_label: url
```


In this example, the label is modified by the following logic:


1. Obtain the values of `method` and `handler` from the metric.

2. Concatenate the obtained values by using the separator defined by `separator` to get `POST#/api/v1/vmp`.

3. According to the regex capture groups, `$1` is `POST`, and `$2` is `/api/v1/vmp`.

4. Reformat the values by using `replacement`. The following sample code shows the expected metric.


```html
http_requests_total{method="POST", handler="/api/v1/vmp", status="200", url="/api/v1/vmp POST"} 1024
```


<span id="keep/drop"></span>
### keep/drop

`keep` and `drop` enable you to filter metrics based on the label value of the metric by using `regex`. If the values of labels in `source_labels` for a type of metric match the `regular expression,`


* `keep`: keeps such metrics and discards other metrics.

* `drop`: discards such metrics and keeps other metrics. For example, in a Kubernetes cluster, you can use the following configuration to discard metrics whose value is test or stage in the built\-in system label `__meta_kubernetes_namespace` during service discovery.


```yaml
- source_labels: [__meta_kubernetes_namespace]
  regex: “test|stage”
  action: drop
```


<span id="labelkeep / labeldrop"></span>
### labelkeep and labeldrop

`labelkeep` and `labeldrop` differ from the previously described `keep and drop` fields. The `label` prefix indicates that they can be used for filtering metrics based on the label key of the metric. For example:

```yaml
- action: labeldrop
  regex: status
```


The following sample code shows the expected metric, in which the `status` label of the original metric is directly discarded.

```html
http_requests_total{method="POST", handler="/api/v1/vmp"} 1024
```


<span id="labelmap"></span>
### labelmap

When you use `replace` to change a label for a metric, you generally need to use `source_labels` to specify a specific label. `labelmap` can perform batch format conversion with `regex` and `replacement`. For example, in the Kubernetes service discovery configuration, multiple built\-in system labels may exist, including:

```yaml
__meta_kubernetes_node_name
__meta_kubernetes_node_provider_id
...
__meta_kubernetes_pod_name
__meta_kubernetes_pod_ip
```


In this case, you can use the following relabeling configuration to store these Kubernetes built\-in system labels in the metrics at the same time.

```yaml
- action: labelmap
  regex: "__meta_kubernetes_(.*)"
  replacement: "k8s_${1}"
```


The following sample code shows the Pod label built\-in system labels, which indicates that the target Pod in Kubernetes service discovery has an `app=foo` label.

```yaml
__meta_kubernetes_pod_label_app: foo
...
```


Use the following relabeling configuration to automatically add the Pod label built\-in system labels to the metrics:

```yaml
- action: labelmap
  regex: __meta_kubernetes_pod_label_(.+)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default value of <code>replacement</code> is <code>$1</code>. Therefore, the value of <code>(.+)</code> in the first regular expression capture group is obtained. The following sample code shows the expected metric.</div>


```html
http_requests_total{method="POST", handler="/api/v1/vmp", status="200", app="foo"} 1024
```
