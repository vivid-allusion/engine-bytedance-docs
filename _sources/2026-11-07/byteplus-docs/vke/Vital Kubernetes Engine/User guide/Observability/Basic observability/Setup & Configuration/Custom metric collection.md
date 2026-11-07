---
title: "Custom metric collection"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Custom_metric_collection"
---

Custom metric collection supplements the default collection scope in VKE clusters, enabling the collection of additional metrics or labels needed for your business scenarios. This topic describes how to copy and minimally modify the default collection objects. It also explains how to create VMNodeScrape, ServiceMonitor, or PodMonitor and verify that new metrics are collected.

<span id="M6xdcKky"></span>
## Background

When you enable [cloud-native basic observability](https://docs.byteplus.com/en/docs/vke/Monitoring-overview?lang=en) in a VKE cluster, the system applies default collection configurations to objects such as kubelet, CoreDNS, and CSI components. These configurations cover common monitoring scenarios. The metrics available for collection in the console may not fully match those exposed by the target component. In this case, create a custom VMNodeScrape, ServiceMonitor, or PodMonitor to supplement the collection scope. Typical application scenarios are as follows:


* Collect metrics that are not yet available in the console but are already exposed by the target.

* Maintain a separate collection allowlist for different workloads to avoid impacting the platform's default templates.

* Supplement label rules such as job and node for subsequent aggregation, dashboard display, and alert configuration.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">VKE clusters support configuring custom metric collection rules using CRD resources such as VMNodeScrape and ServiceMonitor. For details about the different resource types and how to configure them, see <a href="https://docs.byteplus.com/en/docs/vke/Service-discovery?lang=en">Service discovery</a>.</div>


<span id="tqsZRh2O"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* If you use an IAM user account to configure the cluster, make sure that the account has permission to view and create custom Kubernetes resources. For details, see [Configuring IAM permissions](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions?lang=en).

* Verify the metric exposure method of the target resource. The supported CRD types vary slightly depending on the exposure method. These include the node, Service, and Pod dimensions.


<span id="M0sHfVfM"></span>
## Procedure

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Do not directly modify the default VMNodeScrape, ServiceMonitor, or PodMonitor collection configurations issued by the system. When you modify or synchronize collection configurations in the console, the system reissues the default configurations. Therefore, the system may overwrite or reset any direct changes to the default configurations.</div>


* <div data-tips="true" data-tips-type="danger">To collect custom metrics, copy an object issued by the platform and create a custom configuration. Then modify the <code>selector</code>, metric allowlist, and label rules as needed. This method isolates custom collection rules from the system's default rules, making future maintenance easier.</div>



<span id="RpRCbzy8"></span>
### Step 1: Export existing configurations


1. [Use kubectl to connect to the cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster?lang=en).

2. Run the following command to view the default collection rules applied by the system.

   ```Bash
   kubectl -n kube-system get vmnodescrape
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also run the <code>kubectl -n kube-system get servicemonitor</code> or <code>kubectl -n kube-system get podmonitor</code> command to view other types of default collection rules.   </div>
   

   The expected output is shown below and includes all default rules for this resource type in the system.

   ```Bash
   NAME                   AGE
   kubelet                5h11m
   kubelet-cadvisor       5h11m
   kubelet-cadvisor-vci   5h11m
   node-exporter          5h11m
   vpc-cni                5h12m
   vpc-cni-cello-cilium   5h12m
   ```
   

3. Select the type of custom collection rule that you want to create, and export the system's default collection rule as a new YAML file. This topic uses the kubelet collection rule as an example. When exporting the rules, rename the file and do not overwrite the original object.

   ```Bash
   kubectl -n kube-system get vmnodescrape kubelet -o yaml > kubelet-custom.yaml
   ```
   


<span id="yhHuPAXH"></span>
### Step 2: Remove redundant fields

The exported YAML file contains many redundant fields. Before configuring the custom collection rule, delete these fields to prevent creation failures or conflicts with the original object. The example is as follows:

```YAML
apiVersion: operator.victoriametrics.com/v1beta1
kind: VMNodeScrape
metadata:
  annotations:
    meta.helm.sh/release-name: container-monitoring
    meta.helm.sh/release-namespace: kube-system
  creationTimestamp: "2026-08-24T02:59:45Z"
  generation: 1
  labels:
    app.kubernetes.io/instance: container-monitoring
    app.kubernetes.io/managed-by: Helm
    app.kubernetes.io/name: kubelet
    app.kubernetes.io/version: 1.22.2
    helm.sh/chart: container-monitoring-1.22.2
    volcengine.vmp: "true"
  name: kubelet
  namespace: kube-system
  resourceVersion: "2***"
  uid: e09ac813-f6fc-44***
spec:
  bearerTokenFile: /var/run/secrets/kubernetes.io/serviceaccount/token
  interval: 15s
...
```



|**Redundant field** |**Handling suggestions** |
|---|---|
|`metadata.creationTimestamp` |This field is the resource creation timestamp on the server and must be deleted. |
|`metadata.resourceVersion` |This field is a server\-generated version number and must be deleted when you create a new object. |
|`metadata.uid` |This field is the unique identifier of the original object and must be deleted. |
|`metadata.generation and metadata.managedFields` |This field is maintained by the control plane. You do not need to retain it and must delete it. |
|`status` |This field indicates the status of the original resource object. If this field exists in the exported YAML, delete it. |


<span id="4rgs5zfk"></span>
### Step 3: Modify key fields

In the exported YAML file, configure the custom collection rule by modifying the following fields as needed. For detailed field configuration instructions, see [Example 1: Custom VMNodeScrape collection rules](https://docs.byteplus.com/en/docs/90/120001#2bte2eli).


|**Key field** |Configuration recommendations |**Description** |
|---|---|---|
|`metadata.name` |The resource name, which must be changed to a new name. |Avoid using the same name as the system's default object. For example, add a `custom-` prefix, a team name, or an application name suffix. |
|`selector` |Narrow the collection scope. |Avoid completely overlapping the collection scope with the system's default object to reduce the risk of duplicate scraping and duplicate time series. |
|`relabelConfigs`/`relabelings` |Modify the job and label rules as needed. |We recommend using a new job name for the custom object to distinguish default collection rules from custom collection rules. |
|`metricRelabelConfigs`/`metricRelabelings` |Adjust the metric allowlist as needed. |To add only a few metrics that are not yet exposed, modify the corresponding keep rule instead of rewriting the entire configuration. |
|`interval`, `port`, `path`, `scheme`, and `tlsConfig` |We recommend keeping the default value. |In general, you do not need to modify these fields. Only adjust them when the exposure method on the target differs from the default object. |


<span id="PcMCSk6B"></span>
### Step 4: Apply and verify the configurations


1. After modifying the custom rule YAML file, run the following command to apply the custom rule to the cluster.

   ```Bash
   kubectl apply -f kubelet-custom.yaml
   ```
   

2. After you apply the custom rule configuration, we recommend checking the following items:

   * Whether the custom object is successfully created.

   * Whether the target count meets expectations.

   * Whether the new metrics can be queried in the query interface or through PromQL.

   * Whether the custom object causes duplicate scraping with the platform's default object.

   For example, use the Explore feature of VMP to verify that the collection rule runs properly and that the corresponding metrics are collected.


<span id="I0fx1eX4"></span>
## Configuration examples

<span id="2bte2eli"></span>
### Example 1: Custom VMNodeScrape collection rules

VMNodeScrape is suitable for node\-level metric collection. In a VKE cluster, kubelet metrics are collected via VMNodeScrape by default. If the default collection scope does not meet your requirements, create an additional custom VMNodeScrape. Retain the node discovery and TLS\-related configurations, and add the required metrics, such as `kubelet_evictions`, in `metricRelabelConfigs`.

```YAML
apiVersion: operator.victoriametrics.com/v1beta1
kind: VMNodeScrape
metadata:
  name: custom-kubelet # The name of the custom collection rule.
  namespace: kube-system # The namespace of the custom collection rule.
  labels: 
    volcengine.vmp: "true" # The labels of the resource for service discovery so that the Agent can discover it.
spec:
  bearerTokenFile: /var/run/secrets/kubernetes.io/serviceaccount/token
  interval: 15s # Collection interval. The system scrapes metrics from all target nodes every 15 seconds.
  scheme: https # kubelet exposes metrics over HTTPS (port 10250) by default. This must be explicitly declared.
  selector: # Filter for the target nodes through Kubernetes Label Selector.
    matchExpressions:
      - key: node.kubernetes.io/instance-type
        operator: NotIn
        values:
          - dcp-node
  tlsConfig:
    caFile: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecureSkipVerify: true
  relabelConfigs:
    - replacement: kubelet-custom # Rewrite the job label of the nodes to kubelet-custom, facilitating subsequent metric filtering by job="kubelet-custom".
      targetLabel: job
    - regex: (.+)
      sourceLabels:
        - __meta_kubernetes_node_name
      targetLabel: node
    - regex: volcengine://(.+)
      sourceLabels:
        - __meta_kubernetes_node_provider_id
      targetLabel: ecs
  metricRelabelConfigs: # Metric filtering configuration.
    - action: keep # Keep metrics.
      sourceLabels: # Filter by metric name. In this example, only metrics matching the regular expression are retained.
        - __name__
      regex: kubelet_running_pods|kubelet_node_name|kubelet_evictions # Specify the metric names to retain or the regular expression. This setting determines the metrics that this collection rule ultimately collects.
```


<span id="3GGzXd8G"></span>
### Example 2: Custom ServiceMonitor collection rules

ServiceMonitor is suitable for components that expose metrics through a Service. In a VKE cluster, CoreDNS metrics are collected through ServiceMonitor by default. If the default collection scope does not meet your requirements, create an additional custom ServiceMonitor. Reuse the selector and port settings from the default configuration, and specify custom job labels and metric allowlists in `metricRelabelConfigs`.

```YAML
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: custom-core-dns # The name of the custom collection rule.
  namespace: kube-system # The namespace of the custom collection rule.
  labels:
    volcengine.vmp: "true" # The labels of the resource for service discovery so that the Agent can discover it.
spec:
  namespaceSelector: # The namespace of the collection object.
    matchNames:
      - kube-system
  selector: # Filter for the target services through Kubernetes Label Selector.
    matchLabels:
      k8s-app: kube-dns
  endpoints:
    - port: metrics # Collection port.
      interval: 15s # Collection interval. The system scrapes metrics from all target services every 15 seconds.
      relabelings: # Rewrite the job label of the target service to core-dns-custom, facilitating metric filtering by job="core-dns-custom".
        - action: replace
          replacement: core-dns-custom
          targetLabel: job
        - action: labeldrop
          regex: service|namespace|container|endpoint
      metricRelabelings: # Metric filtering configuration.
        - action: keep # Keep metrics.
          sourceLabels: # Filter by metric name. In this example, only metrics matching the regular expression are retained.
            - __name__
          regex: coredns_reload_failed_total|coredns_forward_responses_total # Specify the metric names to retain or the regular expression. This setting determines the metrics that this collection rule ultimately collects.
```


<span id="0KofxASb"></span>
### Example 3: Custom PodMonitor collection rules

PodMonitor is suitable for scenarios where metrics are collected directly from Pods. It is typically used for components that do not have a Service or that require separate collection rules at the Pod level. In a VKE cluster, CSI component metrics, such as csi\-ebs, are collected through PodMonitor by default. If the default collection scope does not meet your requirements, create an additional custom PodMonitor. Reuse the Pod selector from the default configuration and add the required metrics in `metricRelabelConfigs`.

```YAML
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: custom-csi-ebs-node # The name of the custom collection rule.
  namespace: kube-system # The namespace of the custom collection rule.
  labels:
    volcengine.vmp: "true" # The labels of the resource for service discovery so that the Agent can discover it.
spec:
  namespaceSelector: # The namespace of the collection object.
    matchNames:
      - kube-system
  selector: # Filter for the target Pods through Kubernetes Label Selector.
    matchLabels:
      app.kubernetes.io/name: csi-ebs-node
  podMetricsEndpoints:
    - port: metrics # Collection port.
      interval: 15s # Collection interval. The system scrapes metrics from all target services every 15 seconds.
      relabelings: # Rewrite the job label of the target Pod to csi-ebs-node-custom, facilitating subsequent metric filtering by job="csi-ebs-node-custom".
        - action: replace
          replacement: csi-ebs-node-custom
          targetLabel: job
        - action: labeldrop
          regex: instance|service|namespace|pod|container|endpoint
      metricRelabelings: # Metric filtering configuration.
        - action: keep # Keep metrics.
          sourceLabels: # Filter by metric name. In this example, only metrics matching the regular expression are retained.
            - __name__
          regex: csi_node_allocatable_volumes|csi_node_allocated_volumes|csi_ebs_xfs_repair_trigger_error_total # Specify the metric names to retain or the regular expression. This setting determines the metrics that this collection rule ultimately collects.
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you configure CSI collection rules, a CSI component may expose multiple ports or metrics from multiple sidecars. In this case, add endpoint configurations in <code>podMetricsEndpoints</code> or create multiple custom objects.</div>


<span id="xgC94Mzr"></span>
## FAQ

<span id="tID0sFPM"></span>
### Why is it not recommended to directly modify the system's default collection rules?

The system's default collection rules are system\-managed objects that are reissued when the console configuration is synchronized, templates are upgraded, or default policies are adjusted. Changes made directly to the default collection rules may be overwritten during the next synchronization. Therefore, direct modification is not suitable as a long\-term solution.

<span id="zvSMfEew"></span>
### Do custom collection rules and the platform's default collection rules collect the same metrics more than once?

If your custom collection rule uses the same `selector` and job labels as the default rule, duplicate scraping or duplicate time series may occur. Therefore, we recommend assigning a custom value to `metadata.name` and adjusting the `selector` and `job` settings as needed.

<span id="tfaMjJp8"></span>
### Which fields should I modify to minimize changes?

We recommend modifying `metadata.name`, `selector`, `job`, and the metric allowlist first. For authentication, TLS, namespaces, and default exposure paths, you can usually inherit the corresponding settings directly from the default collection rules.

<span id="yx67452U"></span>
### How do I verify that new metrics have been successfully collected?

After applying custom collection rules, first check that the objects and collection targets are created. Then query the new metric names in the query interface or by using PromQL. If the query returns time series data as expected, the custom collection configuration has taken effect.
