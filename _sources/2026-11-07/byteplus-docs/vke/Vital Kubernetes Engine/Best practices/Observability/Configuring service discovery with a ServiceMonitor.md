---
title: "Configuring service discovery with a ServiceMonitor"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-Service-discovery-through-ServiceMonitor"
---

After you enable observability in a cluster and install the prometheus\-agent add\-on there, you can use a ServiceMonitor to configure custom collection rules. This topic describes how to set up service discovery with a ServiceMonitor.

<span id="kmUM8jdb"></span>
## Verify the demo

You can use the following demo code to integrate a Go application and use a ServiceMonitor for service discovery. In the following example, Go is used to create an application, and a metric named `rpc_durations_seconds` is exposed in the application to collect statistics on the RPC latency of the service.

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


<span id="JwUauUWP"></span>
## Prerequisites


* Cloud native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The demo code has been packaged as an image and uploaded to CR. For details, see [Go application integration](https://docs.byteplus.com/en/docs/vmp/Golang-application-access).

* The target cluster has been connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="iXghfKPW"></span>
## Procedure

<span id="edwMLEAs"></span>
### Step 1: Deploy an application and service

You can use the image from CR to deploy the application in the target VKE cluster. The steps are as follows:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the cluster name to enter the cluster configuration page.

4. In the left navigation bar, click **Workload \> Deployment**. Click **Create with Yaml**, and deploy the application.

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
           - containerPort: 2023 # Specify the container port.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The image address in this example is only for demonstration purposes. You need to replace it with your actual image address.   </div>
   

5. In the left navigation bar of the cluster management page, click **Services and Ingresses** \> **Service**. On the page that appears, click **Create with Yaml** to configure the service for load balancing and service discovery.

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: golang-service-demo
     namespace: volcano-metrics # Specify the namespace where the service is located.
     labels: 
       app: golang-service-demo # Specify service labels.
   spec:
     selector:
       app: golang-demo
     ports:
       - protocol: TCP
         port: 2023
         targetPort: 2023
         name: metrics # Specify a name for the service port.
     type: ClusterIP
   ```
   


<span id="fGI89bAT"></span>
### Step 2: Configure a ServiceMonitor


1. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to configure a collection rule by using a ServiceMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.

      ```yaml
      apiVersion: monitoring.coreos.com/v1
      kind: ServiceMonitor
      metadata:
        name: golang-demo-discover # Specify a name for the collection rule.
        namespace: default # Specify a namespace for the ServiceMonitor.
        labels: 
          volcengine.vmp: "true" # Specify ServiceMonitor labels to make it discoverable by prometheus-agent.
      spec:
        endpoints:
        - port: metrics # Specify a name for the service port.
          relabelings: # Configure metric relabeling. If not required, this can be omitted.
          - targetLabel: environment 
            action: replace # In this example, add the environment="Production" label.
            replacement: Production
        namespaceSelector:
          matchNames:
          - volcano-metrics # Specify the namespace where the service is located.
        selector:
          matchLabels:
            app: golang-service-demo # Specify the label value of the service to locate and select the target service.
      ```
      

2. Click **Confirm**.


<span id="3HMiWACG"></span>
## Validating results


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, click **Explore** to go to the Explore page.

4. In the upper\-right corner, specify the **Workspace** from which metrics are to be queried, and in the **Query** text box, enter `up{job="golang-service-demo"}` to check whether the corresponding service has been discovered as expected.


&nbsp;
