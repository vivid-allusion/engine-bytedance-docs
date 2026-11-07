---
title: "Custom metric labels"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Customing_metrics_labels"
---

Vital Kubernetes Engine (VKE) allows you to define custom metric labels within clusters to improve the flexibility and information richness of the monitoring system. This topic describes how to configure custom metric labels.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5oyH5qCH5ZKM5qCH562-"></span>
### Metrics and labels

In the Prometheus monitoring system, metrics can have multiple labels attached. These labels are used to group and distinguish data in greater detail. Each label consists of a key and a value, which enriches the dimensionality of metrics and makes it easier to monitor and analyze specific scenarios.

For example, when monitoring the CPU usage of multiple servers, you can use labels to denote the ID or location of each server, as in `cpu_usage{server_id="ecs1", location="datacenter1"}`.  In this case, you can not only view the overall CPU usage but also filter by labels to get the CPU usage of a specific server or data center.

Labels enable highly flexible data querying, filtering, or aggregation. You can use them to perform comparative analysis, calculate sums or averages, and generate other statistical metrics. This is extremely helpful for understanding and optimizing system performance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details about metrics and labels, see <a href="https://docs.byteplus.com/en/docs/vmp/Format-of-Prometheus-time-series-data">Format of Prometheus time series data</a>.</div>


<span id=".6Ieq5a6a5LmJ5qCH562-"></span>
### Custom labels

In addition to the default labels included in metrics, you often need custom labels to enhance the flexibility and information richness of the monitoring system. For example:


1. **Environment differentiation**. When you deploy the same application in development, test, and production environments, labels (such as `env="production"` or `env="development"`) can distinguish metric data from different environments. This allows you to aggregate and easily view metrics from multiple environments in a single Prometheus instance, and quickly identify which environment is experiencing issues.

2. **Service instance differentiation**. When multiple instances of the same service are running, labels (such as `instance="server1"` or `instance="server2"`) can be used to identify each service instance. This helps monitor the performance of individual instances, identify unbalanced load allocation, or detect failures in specific instances.

3. **Version tracking**. During software deployment or updates, you can use labels (for example, `version="1.0"` or `version="1.1"`) to track the performance of different application versions. This helps development teams understand how new versions impact performance or compare performance differences between versions.

4. **Geographic location tagging**. For distributed services, geographic labels (such as `region="cn-beijing-1"` and `region="cn-beijing-2"`) enable monitoring of performance across regions and analysis of key metrics like response time and availability between geographic locations.

5. **Business\-related information**. You can use business\-level labels (such as `customer="customerA"` and `project="projectX"`) to segment monitoring data. This allows teams to view resource usage for specific customers or projects, supporting cost analysis and resource optimization for business units.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Adding custom labels to metrics doubles the number of active time series in the workspace within a short period (1 hour). Confirm in advance that the VMP workspace bound to the cluster has sufficient specifications to handle the increased number of active time series. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/workspaces-types">Workspace specifications</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A  Vital Kubernetes Engine (VKE) cluster has been created and cloud native observability has been enabled for the cluster. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The prometheus\-agent add\-on has been installed and upgraded to v2.6.0\-vke.1.24 or v2.6.0\-vke.1.20 or later. For details, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/prometheus-agent).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console ](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Configurations** \> **ConfigMap**. On the page that appears, click **Create with Yaml** to create a ConfigMap.


```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: additional-monitoring-config # Configuration item name, fixed value, please do not modify
  namespace: kube-system # The namespace of the ConfigMap. This field has a fixed value. Do not modify it.
data:
  external-labels: |-
    k1: v1
    k2: v2
    
  # k1: v1 is a user-defined metric label.
  # The length of the label key cannot exceed 256 bytes.
  # The label key must match the [a-zA-Z_][a-zA-Z0-9_]* regex pattern.
  # The length of the label value cannot exceed 2,048 bytes.
  # The label value must be valid UTF-8 characters.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This configuration is a global configuration. After a custom metric label is configured for the cluster, all metrics collected by the prometheus\-agent add\-on in the cluster will include this label.</div>


* <div data-tips="true" data-tips-type="tip">This configuration modifies the <code>global</code> parameter in <a href="https://prometheus.io/docs/prometheus/latest/configuration/configuration/#configuration-file">native Prometheus settings</a>. Only some parameters are supported for this configuration. For details, see <strong>Global prometheus\-agent parameters</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Upgrading the prometheus\-agent add\-on does not overwrite this configuration.</div>


* <div data-tips="true" data-tips-type="tip">If you specify built\-in labels such as <code>_cloud_product</code> and <code>cluster</code> in this configuration, they will not take effect.</div>



<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

In the [VMP console ](https://console.byteplus.com/prometheus), use the Explore feature to quickly query cluster metric data. You can view the custom labels in the metrics.

<span id=".5Y-C6ICD5L-h5oGv"></span>
## References

<span id=".cHJvbWV0aGV1cy1hZ2VudC3lhajlsYDphY3nva7lj4LmlbA="></span>
### Global prometheus\-agent parameters

Only some native Prometheus parameters are supported, as shown in the table below. Unmentioned parameters are not supported.


|Parameters |Supported |Default configuration |
|---|---|---|
|external_labels |Yes |None |
|remote_write |Yes |None |
