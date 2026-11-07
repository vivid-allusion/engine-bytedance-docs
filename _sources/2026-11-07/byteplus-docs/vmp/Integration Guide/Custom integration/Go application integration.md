---
title: "Go application integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Golang-application-access"
---

Prometheus provides an [official Go library](https://github.com/prometheus/client_golang) to collect and expose monitoring data. This topic describes how to use the library to expose the Go runtime data and use Vital Managed Service for Prometheus (VMP) to collect and display metric data with some basic samples.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about Go client API documentation, refer to <a href="https://pkg.go.dev/github.com/prometheus/client_golang">Prometheus Go client library</a>.</div>


<span id=".5a6J6KOF5L6d6LWW"></span>
## Install dependencies

You can install the relevant dependencies by running the following `go get` command:

```golang
go get github.com/prometheus/client_golang/prometheus
go get github.com/prometheus/client_golang/prometheus/collectors
go get github.com/prometheus/client_golang/prometheus/promhttp
```


<span id=".6L-Q6KGM5pe25oyH5qCH"></span>
## Runtime metrics


1. Create an HTTP service with the path `/metrics`. You can directly use the [Handler](https://pkg.go.dev/github.com/prometheus/client_golang@v1.8.0/prometheus/promhttp#Handler) function provided in [prometheus/promhttp](https://pkg.go.dev/github.com/prometheus/client_golang@v1.8.0/prometheus/promhttp).

   The following section shows a sample Go application, which exposes some default metric data through `http://localhost:2023/metrics`. The metrics include runtime, process, and build metrics.


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



2. Run the following command to start the application:


```golang
go run main.go
```



3. Execute the following command to view metric data during runtime:


```bash
curl http://localhost:2023/metrics
```


<span id=".5bqU55So5bGC5oyH5qCH"></span>
## Application layer metrics


1. The preceding example only exposes some basic built\-in metrics. You need to add metrics at the application layer additionally.

   As shown in the following example, the metric rpc_durations_seconds is exposed, which is used to collect statistics on the Remote Procedure Call (RPC) latency of the service.


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



2. Run the following command to start the application:


```golang
go run main.go
```



3. Execute the following command to view metric data during runtime:


```bash
curl http://localhost:2023/metrics
```


From the output result, you can see the information about the `rpc_durations_seconds` counter, including the help documentation, type information, metric name, and current value.

```bash
# HELP rpc_durations_seconds RPC latency distributions.
# TYPE rpc_durations_seconds summary
rpc_durations_seconds{service="exponential",quantile="0.5"} 7.427294276581254e-07
rpc_durations_seconds{service="exponential",quantile="0.9"} 2.3157390817424027e-06
```


<span id=".55uR5o6nIEdvbGFuZyDlupTnlKjnpLrkvos="></span>
## Monitor the Go application

The preceding example only shows how to use the Go library of Prometheus to expose application metric data. However, the exposed metric data needs to be collected and stored through VMP for data monitoring and alerting.

<span id=".5omT5YyF5bqU55So"></span>
### Package the application


1. A Go application can be packaged into an image through a Dockerfile in the following format. In this way, the Go application can be deployed in a Vital Kubernetes Engine (VKE) cluster.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Dockerfile only serves as an example. You can modify its parameters based on your business requirements.</div>


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



2. After the image is created, it can be uploaded to [CR](https://docs.byteplus.com/en/docs/cr/what-is-cr) for use. You can also use another public cloud or self\-built image registry.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the image pushing method of CR, see <a href="https://docs.byteplus.com/en/docs/cr/Push_and_pull_artifacts">Pushing and pulling images with Docker</a>.</div>


<span id=".6YOo572y5bqU55So"></span>
### Deploy the application

You can use the images from Container Registry to deploy applications in the VKE cluster. Procedure:


1. Log in to the [VKE](https://console.byteplus.com/vke) console.

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster details page.

4. Click **Workload \> Deployment** in the left navigation pane. Click **Create with Yaml** to deploy the application.


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: golang-demo # Specify the name of the application.
  namespace: volcano-metrics # Configure the namespace of the application.
  labels:
    app: golang-demo # Configure the labels of the application.
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
      - name: golang-demo # Specify the container name.
        image: doc-cn-beijing.cr.volces.com/vmp/golang-demo:1.0 # Specify the address and version of the application image.
        ports:
        - containerPort: 2023 # Configure the container port.
```



5. In the left navigation pane of the cluster details page, click **Services and Ingresses** \> **Service**. On the page that appears, click **Create with Yaml** to configure a service for load balancing and service discovery.


```yaml
apiVersion: v1
kind: Service
metadata:
  name: golang-service-demo
  namespace: volcano-metrics # Specify the namespace of the service.
  labels: 
    app: golang-service-demo # Configure the labels of the service.
spec:
  selector:
    app: golang-demo
  ports:
    - protocol: TCP
      port: 2023
      targetPort: 2023
      name: metrics # Specify the service port name.
  type: ClusterIP
```


<span id=".6YWN572u5pyN5Yqh5Y-R546w"></span>
### Configure service discovery

After the application is deployed and works as expected, you can use ServiceMonitor to configure service discovery to allow the collector to collect the metrics of the application. The specific procedure is as follows:


1. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to configure service discovery through ServiceMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml**field.


```Yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: golang-demo    # Enter a unique name.
  namespace: default # Specify the namespace of ServiceMonitor.
  labels: 
    volcengine.vmp: "true" # Configure the labels of ServiceMonitor to allow the labels to be identified by prometheus-agent.
spec:
  endpoints:
  - interval: 30s
    port: metrics # Specify the service port name.
    path: /metrics # Specify the URI path for metric exposure. The value is /metrics by default if it is not specified.
    relabelings:
    - action: replace
      sourceLabels:  [__meta_kubernetes_pod_label_app]
      targetLabel: application
  namespaceSelector:
    matchNames:
    - volcano-metrics # Specify the namespace of the service.
  selector:
    matchLabels:
      app: golang-service-demo # Specify the label value of the service to locate the target service.
```


<span id=".5p-l55yL55uR5o6n5pWw5o2u"></span>
### View monitoring data

You can view metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

You can also use Grafana to read data stored in VMP and create metric dashboards.
