---
title: "Configuring service discovery with a PodMonitor"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-PodMonitor"
---

After you enable observability in a cluster and install the prometheus\-agent add\-on in the cluster, you can use a PodMonitor to configure custom collection rules. This topic describes how to configure service discovery by using a PodMonitor.

<span id="lofboZdB"></span>
## Verify the demo

You can use the following demo code to integrate a Go application and use a PodMonitor for service discovery. In the following example, Go is used to create an application, and a metric named `rpc_durations_seconds` is exposed in the application to collect statistics on the RPC latency of the service.

```golang
package main

import (
        "math"
        "math/rand"
        "net/http"
        "time"

        "github.com/prometheus/client_golang/prometheus"
        "github.com/prometheus/client_golang/prometheus/collectors"
        "github.com/prometheus/client_golang/prometheus/promhttp"
)

var rpcDurations = prometheus.NewSummaryVec(
        prometheus.SummaryOpts{
                Name:       "rpc_durations_seconds",
                Help:       "RPC latency distributions.",
                Objectives: map[float64]float64{0.5: 0.05, 0.9: 0.01, 0.99: 0.001},
        },
        []string{"service"},
)

func main() {
        // Create a new registry.
        reg := prometheus.NewRegistry()

        // Add Go module build info.
        reg.MustRegister(collectors.NewBuildInfoCollector())
        // Add go runtime metrics and process collectors.
        reg.MustRegister(
                collectors.NewGoCollector(),
                collectors.NewProcessCollector(collectors.ProcessCollectorOpts{}),
        )

        reg.MustRegister(rpcDurations)

        start := time.Now()

        oscillationFactor := func() float64 {
                return 2 + math.Sin(math.Sin(2*math.Pi*float64(time.Since(start))/float64(10*time.Minute)))
        }

        // Periodically record some sample latencies for the three services.
        go func() {
                for {
                        v := rand.Float64() * 0.0002
                        rpcDurations.WithLabelValues("uniform").Observe(v)
                        time.Sleep(time.Duration(100*oscillationFactor()) * time.Millisecond)
                }
        }()

        go func() {
                for {
                        v := (rand.NormFloat64() * 0.0002) + 0.00001
                        rpcDurations.WithLabelValues("normal").Observe(v)
                        time.Sleep(time.Duration(75*oscillationFactor()) * time.Millisecond)
                }
        }()

        go func() {
                for {
                        v := rand.ExpFloat64() / 1e6
                        rpcDurations.WithLabelValues("exponential").Observe(v)
                        time.Sleep(time.Duration(50*oscillationFactor()) * time.Millisecond)
                }
        }()

        http.Handle("/metrics", promhttp.HandlerFor(
                reg, promhttp.HandlerOpts{},
        ))
        http.ListenAndServe(":2023", nil)
}
```


<span id="pW9IK0Bo"></span>
## Prerequisites


* Cloud native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The demo code has been packaged as an image and uploaded to CR. For details, see [Go application integration](https://docs.byteplus.com/en/docs/vmp/Golang-application-access).

* The target cluster has been connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="2dL8f4px"></span>
## Procedure

<span id="7Mw1hoJT"></span>
### Step 1: Deploy the application

You can use the image from CR to deploy the application in the target VKE cluster. The steps are as follows:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the configuration page of the cluster.

3. In the left navigation bar, click **Workload \> Deployment**. Click **Create with Yaml**, and deploy the application.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: golang-demo # Specify a name for the application.
     namespace: volcano-metrics # Specify the namespace where the application resides.
     labels:
       app: golang-demo # Specify application labels.
   spec:
     replicas: 2 # Specify the number of replicas for the application.
     selector:
       matchLabels:
         app: golang-demo
     template:
       metadata:
         labels:
           app: golang-demo
       spec:
         containers:
         - name: golang-demo # Specify a name for the container.
           image: doc-cn-beijing.cr.volces.com/vmp/golang-demo:1.0 # Specify the address and version of the application image.
           ports:
           - name: metric-port # Specify a name for the container port.
             containerPort: 2023 # Specify the container port.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The image address in this example is only for demonstration purposes. You need to replace it with your actual image address.   </div>
   

<span id="dNojLaiE"></span>
### Step 2: Configure a PodMonitor


1. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** and configure a PodMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.


```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover # Specify a name for the PodMonitor.
  namespace: volcano-metrics # Specify a namespace for the PodMonitor.
  labels: 
    volcengine.vmp: "true" # Specify PodMonitor labels to make it discoverable by prometheus-agent.
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port # Specify the container port name.
    path: /metrics # Specify the container metric path. The default value is /metrics if it is left empty.
    relabelings: # Configure metric relabeling. If not required, this can be omitted.
    - targetLabel: environment 
      action: replace # In this example, add the environment="Production" label.
      replacement: Production
  namespaceSelector:
    matchNames: 
    - volcano-metrics # Specify the namespace where the container resides.
  selector: 
    matchLabels:
      app: golang-demo # Specify the container label value to locate and select the target pod.
```



2. Click **Confirm**.


<span id="rK6Q2h65"></span>
## Validating results


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Explore** to go to the Explore page.

4. In the upper\-right corner, specify the **Workspace** from which metrics will be queried.In the **Query** text box, enter `up{job="volcano-metrics/golang-demo-discover"}` to verify if the corresponding pod has been discovered as expected.


<span id="G9C3jfnA"></span>
## Advanced configuration

<span id="ji3d0UXa"></span>
### Specify a custom name for the job

By default, the name of the job discovered through the PodMonitor is `<namespace>/<name>`. In this example, the default job name is `volcano-metrics/golang-demo-discover`. You can specify a custom name for the job based on your business requirements.

<span id="TEcySnXk"></span>
#### Method 1

You can use the `jobLabel` field in the PodMonitor to change the job name to the value of a specified pod label. In this example, you can change the job name to the value of the label `app: golang-demo`. As a result, the job name is `golang-demo`.

```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover
  namespace: volcano-metrics
  labels: 
    volcengine.vmp: "true"
spec:
  jobLabel: app # Specify the label name of the pod.
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port
    path: /metrics
  namespaceSelector:
    matchNames: 
    - volcano-metrics
  selector: 
    matchLabels:
      app: golang-demo
```


The expected result is as follows: You can query metrics by using the job name `golang-demo`.

<span id="S6lvJc6u"></span>
#### Method 2

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This method prevails over Method 1.</div>


You can use the `spec.podMetricsEndpoints.N.relabelings` field in the PodMonitor to configure relabeling and specify a custom job name.

```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover
  namespace: volcano-metrics
  labels: 
    volcengine.vmp: "true"
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port
    path: /metrics
    relabelings: # Configure metric relabeling.
    - targetLabel: job
      action: replace
      replacement: jobname-demo # Specify a custom job name.
  namespaceSelector:
    matchNames: 
    - volcano-metrics
  selector: 
    matchLabels:
      app: golang-demo
```


The expected result is as follows: You can query metrics by using the job name `jobname-demo`.

<span id="ivwSkiac"></span>
### Adding pod labels to metrics

By default, pod labels are not added to metrics. You can use the `spec.podTargetLabels` field in the PodMonitor to add pod labels to metrics.

```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover
  namespace: volcano-metrics
  labels: 
    volcengine.vmp: "true"
spec:
  jobLabel: app
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port
    path: /metrics
  namespaceSelector:
    matchNames: 
    - volcano-metrics
  podTargetLabels: # Add the required pod labels to metrics.
    - app
    - app.kubernetes.io/component
  selector: 
    matchLabels:
      app: golang-demo
```


The expected result is as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Prometheus metric labels can only contain uppercase and lowercase letters, digits, and underscores (_). Therefore, any other characters in the pod label name will be automatically replaced with underscores (_). For example, <code>app.kubernetes.io/component</code> will change to <code>app_kubernetes_io_component</code>.</div>


<span id="rmg5b55F"></span>
### Metric relabeling

You can use metric relabeling to add, modify, or delete metric labels before metrics are collected or pushed to managed Prometheus workspaces. You can configure metric relabeling by using the following two methods:


* Use `relabelings`:

   * Modify or filter target labels before target collection.

   * Modify or filter target labels during service discovery.

* Use `metricRelabelings`:

   * Modify or filter metric labels after data collection.

   * Delete specific metrics after data collection.

   * Typical scenarios include deleting unnecessary metrics, renaming metric labels, and adding new metric labels.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about PodMonitor relabeling, see the <a href="https://prometheus-operator.dev/docs/api-reference/api/#monitoring.coreos.com/v1.RelabelConfig">official documentation</a>. You can view the relabeling process and debug relabeling configurations by using the <a href="https://relabeler.promlabs.com/">relabeling tool</a>.</div>


<span id="8h5vgxqk"></span>
#### Adding global labels

If you want to add a specified label to all collected metrics, you can specify the `spec.podMetricsEndpoints.N.relabelings` parameter. For example, use the following configuration to add the label key\-value pair `label: value` to all collected metrics.

```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover
  namespace: volcano-metrics
  labels: 
    volcengine.vmp: "true"
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port
    path: /metrics
    relabelings: # Configure metric relabeling to add global labels.
    - targetLabel: label
      action: replace 
      replacement: value
  namespaceSelector:
    matchNames: 
    - volcano-metrics
  selector: 
    matchLabels:
      app: golang-demo
```


<span id="jvzYZNke"></span>
#### Retaining specified metrics

If you want to write only specified metrics, you can configure `action: keep`. For example, use the following configuration to retain only metrics whose names match the regular expression `vmagent_remotewrite.*`.

```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover
  namespace: volcano-metrics
  labels: 
    volcengine.vmp: "true"
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port
    path: /metrics
    metricRelabelings:  # Retain metrics that match the specified regular expression.
    - action: keep 
      regex: vmagent_remotewrite.*
      sourceLabels:
      - __name__
  namespaceSelector:
    matchNames: 
    - volcano-metrics
  selector: 
    matchLabels:
      app: golang-demo
```


<span id="zyf4IP0T"></span>
#### Deleting metrics

If you do not want to write some metrics, you can discard these metrics by configuring `action: drop`. For example, use the following configuration to discard the `vmagent_daily_series_limit_rows_dropped_total` metric.

```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover
  namespace: volcano-metrics
  labels: 
    volcengine.vmp: "true"
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port
    path: /metrics
    metricRelabelings:  # Delete specified metrics.
    - action: drop
      regex: vmagent_daily_series_limit_rows_dropped_total # Metrics to be deleted. Regular expressions are supported.
      sourceLabels:
      - __name__
  namespaceSelector:
    matchNames: 
    - volcano-metrics
  selector: 
    matchLabels:
      app: golang-demo
```


<span id="yVu2yk4G"></span>
#### Modifying the value of a label

You can configure `action: replace` to modify the value of a label. For example, use the following configuration to remove the `/api/v1` prefix for the path label value. As a result, `path: /api/v1/targets` will change to `path: /targets`.

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: golang-demo-discover
  namespace: volcano-metrics
  labels: 
    volcengine.vmp: "true"
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port
    path: /metrics
    relabelings: # Use regular expressions to modify label values.
    - action: replace
      regex: /api/v1:(.*)
      replacement: $1
      sourceLabels:
      - path
      targetLabel: path
  namespaceSelector:
    matchNames: 
    - volcano-metrics
  selector: 
    matchLabels:
      app: golang-demo
```
