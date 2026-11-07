---
title: "Monitoring Go applications in clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring-Golang-applications-using-Vital-Managed-Service-for-Prometheus"
---

When you deploy a Go application in a VKE cluster, you can use cloud\-native observability to monitor the Go application. This topic describes the methods and steps for monitoring Go applications in clusters.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Prometheus provides an [official Go library](https://github.com/prometheus/client_golang) for collecting and exposing monitoring data. When you develop a Go application, you can use this Go library to expose data related to the Go runtime.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For documentation related to the Go Client API, see <a href="https://pkg.go.dev/github.com/prometheus/client_golang">GoDoc</a>.</div>


<span id=".5a6J6KOF5L6d6LWW"></span>
### Installing dependencies

You can use the `go get` command to install the related dependencies. Example:

```bash
go get github.com/prometheus/client_golang/prometheus
go get github.com/prometheus/client_golang/prometheus/collectors
go get github.com/prometheus/client_golang/prometheus/promhttp
```


<span id=".6L-Q6KGM5pe25oyH5qCH"></span>
### Runtime metrics


1. Create an HTTP service with the path `/metrics`. You can directly use the [Handler](https://pkg.go.dev/github.com/prometheus/client_golang@v1.8.0/prometheus/promhttp#Handler) function provided in [prometheus/promhttp](https://pkg.go.dev/github.com/prometheus/client_golang@v1.8.0/prometheus/promhttp).

   In the following example, `http://localhost:2023/metrics` is used to expose some default metric data of the Go application, including runtime metrics, process metrics, and build\-related metrics.

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
   
           http.Handle("/metrics", promhttp.HandlerFor(
                   reg, promhttp.HandlerOpts{},
           ))
           http.ListenAndServe(":2023", nil)
   }
   ```
   

2. Run the following command to start the application.

   ```bash
   go run main.go
   ```
   

3. Run the following command to view the runtime metric data.

   ```bash
   curl http://localhost:2023/metrics
   ```
   


<span id=".5bqU55So5bGC5oyH5qCH"></span>
### Application layer metrics


1. The preceding example only demonstrates how to expose some basic built\-in metrics. You need to add application layer metrics.

   In the following example, a metric named rpc_durations_seconds is exposed, which is used to collect statistics on the RPC latency of the service.

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
   

2. Run the following command to start the application.

   ```bash
   go run main.go
   ```
   

3. Run the following command to view the runtime metric data.

   ```bash
   curl http://localhost:2023/metrics
   ```
   

   The output displays information about the `rpc_durations_seconds` counter, including documentation, type information, metric name, and current value.

   ```bash
   # HELP rpc_durations_seconds RPC latency distributions.
   # TYPE rpc_durations_seconds summary
   rpc_durations_seconds{service="exponential",quantile="0.5"} 7.427294276581254e-07
   rpc_durations_seconds{service="exponential",quantile="0.9"} 2.3157390817424027e-06
   ```
   


<span id=".55uR5o6nLWdvbGFuZy3lupTnlKjnpLrkvos="></span>
## Example of monitoring Go applications

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

Cloud native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

<span id=".5omT5YyF5bqU55So"></span>
### Packaging the application


1. You can package the preceding Go source code into an image by using a Dockerfile in the following format. This facilitates you in deploying the application in a VKE cluster.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This Dockerfile is for illustration purposes only. You need to modify the parameters based on your business requirements.   </div>
   

   ```bash
   FROM golang:1.19 as builder
   COPY . /go/src/demo
   WORKDIR /go/src/demo
   RUN go env -w GOPROXY=https://goproxy.cn,direct && \
       go mod init && \
       go mod tidy && \
       go mod vendor && \
       go build -v -o /golang-demo
   
   FROM buildpack-deps:bullseye-curl
   RUN mkdir -p /app
   COPY --from=builder /golang-demo /app
   WORKDIR     /app
   ENV TZ Asia/Shanghai
   EXPOSE 2023
   ENTRYPOINT  ["/app/golang-demo"]
   
   ```
   

2. After the image is created, you can upload it to [CR](https://docs.byteplus.com/en/docs/cr/what-is-cr) for use. You can also use other public cloud or self\-built image registries.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For methods of pushing images in CR, see <a href="https://docs.byteplus.com/en/docs/cr/push-and-pull-images">Pushing and pulling images</a>.   </div>
   

<span id=".6YOo572y5bqU55So"></span>
### Deploying the application

You can use the image from CR to deploy the application in the target VKE cluster. The steps are as follows:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation bar, click **Workload \> Deployment**. Click **Create with Yaml**, and deploy the application.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: golang-demo # The name of the application.
     namespace: volcano-metrics # The namespace where the application resides.
     labels:
       app: golang-demo # Application labels.
   spec:
     replicas: 2 # The number of replicas for the application.
     selector:
       matchLabels:
         app: golang-demo
     template:
       metadata:
         labels:
           app: golang-demo
       spec:
         containers:
         - name: golang-demo # The container name.
           image: doc-cn-beijing.cr.volces.com/vmp/golang-demo:1.0 # The address and version of the application image.
           ports:
           - containerPort: 2023 # Specify the container port.
   ```
   

5. In the left navigation bar, click **Services and Ingresses** \> **Service**. On the page that appears, click **Create with Yaml** to configure the service.

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: golang-service-demo
     namespace: volcano-metrics # Specify a namespace for the service.
     labels: 
       app: golang-service-demo # Specify service labels.
   spec:
     selector:
       app: golang-demo
     ports:
       - protocol: TCP
         port: 2023
         targetPort: 2023
         name: metrics # The service port name.
     type: ClusterIP
   ```
   


<span id=".6YWN572u5pyN5Yqh5Y-R546w"></span>
### Configuring service discovery

After the application is deployed and run as expected, you can use a ServiceMonitor to configure service discovery. Specific steps are as follows:


1. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to configure service discovery by using a ServiceMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.

      ```Yaml
      apiVersion: monitoring.coreos.com/v1
      kind: ServiceMonitor
      metadata:
        name: golang-demo    # Enter a unique name.
        namespace: default # Specify a namespace for the ServiceMonitor.
        labels: 
          volcengine.vmp: "true" # Specify ServiceMonitor labels to make it discoverable by prometheus-agent.
      spec:
        endpoints:
        - interval: 30s
          port: metrics # The service port name.
          path: /metrics
          relabelings:
          - action: replace
            sourceLabels:  [__meta_kubernetes_pod_label_app]
            targetLabel: application
        namespaceSelector:
          matchNames:
          - volcano-metrics # The namespace where the service is located.
        selector:
          matchLabels:
            app: golang-service-demo # Specify the label value of the service to locate the target service.
      ```
      


<span id=".5p-l55yL55uR5o6n5pWw5o2u"></span>
### Viewing monitoring data

You can use the Explore feature of VMP to view metric data. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

You can also use Grafana to read data stored in VMP and create metrics dashboards. For more details, see [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).
