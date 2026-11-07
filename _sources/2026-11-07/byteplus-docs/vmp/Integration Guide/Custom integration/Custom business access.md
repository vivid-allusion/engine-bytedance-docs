---
title: "Custom business access"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/custom-application-monitoring"
---

This topic takes the Go language as an example to introduce how to configure custom metric tracking for your business, and report, visualize, and alert custom metrics by using Vital Managed Service for Prometheus (VMP).

<span id=".5Lia5Yqh5Z-L54K5"></span>
## Business metric tracking

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the data format and metric type of Prometheus, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Format-of-Prometheus-time-series-data">Format of Prometheus time series data</a>.</div>


<span id=".Q291bnRlciDnsbvlnos="></span>
### Counter

A metric in the counter type increases monotonically and will be reset after service restart. You can use a counter to monitor the numbers of requests, exceptions, user logins, and orders.

The following example shows how to monitor tickets by using the counter type.

```golang
// Ticket
package ticket

import (
        "github.com/prometheus/client_golang/prometheus"
)

// The number of requests.
var requestCounter = prometheus.NewCounterVec(prometheus.CounterOpts{
        Subsystem: "ticket",
        Name:      "request_total",
        Help:      "The total number of ticket requests.",
}, []string{"action"}) // Actions

func init() {
        prometheus.DefaultRegisterer.MustRegister(requestCounter)
}

// Create a ticket.
func Create() {
        requestCounter.With(prometheus.Labels{"action": "create"}).Inc()

        // Create ticket code.
}
```


In this case, the creation rate of tickets can be obtained through the rate() function.

```promql
rate(ticket_request_total{action="create"}[5m])
```


<span id=".R2F1Z2Ug57G75Z6L"></span>
### Gauge type

A gauge is a current value, which can be increased or decreased at the metric scrape time. You can use a gauge to monitor the current memory usage, CPU usage, current number of threads, and queue size.

The following example shows how to monitor tickets by using a gauge.

```golang
// Ticket
package ticket

import (
        "time"

        "github.com/prometheus/client_golang/prometheus"
)

var (
        createConcurrencyCh = make(chan struct{}, 8)
)

// Concurrency control
var (
        createConcurrencyCurrent = prometheus.NewGaugeFunc(prometheus.GaugeOpts{
                Subsystem: "ticket",
                Name:      "concurrent_create_current",
                Help:      "The number of in-flight create ticket requests.",
        }, func() float64 { return float64(len(createConcurrencyCh)) })
        createConcurrencyCapacity = prometheus.NewGaugeFunc(prometheus.GaugeOpts{
                Subsystem: "ticket",
                Name:      "concurrent_create_capacity",
                Help:      "The maximum number of concurrent create ticket requests the server may serve.",
        }, func() float64 { return float64(cap(createConcurrencyCh)) })
)

func init() {
        prometheus.DefaultRegisterer.MustRegister(createConcurrencyCurrent, createConcurrencyCapacity)
}

// Create a ticket.
func Create() {
        t := time.NewTimer(30 * time.Second)

        select {
        case createConcurrencyCh <- struct{}{}:
        case <-t.C:
                // timeout
                return
        }

        defer func() {
                <-createConcurrencyCh
        }()

        // Create ticket code.

}
```


In this case, you can view the concurrency saturation of tickets.

```promql
max_over_time(ticket_concurrent_create_current[1m]) / ticket_concurrent_create_capacity
```


<span id=".SGlzdG9ncmFtIOexu-Weiw=="></span>
### Histogram type

Prometheus calculates sample distribution based on the configured Bucket to generate a histogram, which can be processed subsequently and is generally used for duration monitoring. For example, you can use a histogram to calculate the latencies of P99, P95, and P50 and monitor the numbers of processed items. With histograms, you do not need to use counters to count items. In addition, you can use histograms to monitor metrics such as API response time and database access time.

The following example shows how to monitor the duration of a ticket by using a histogram.

```golang
// Ticket
package ticket

import (
        "time"

        "github.com/prometheus/client_golang/prometheus"
)

// Request duration
var requestDuration = prometheus.HistogramVec(prometheus.HistogramOpts{
        Subsystem: "ticket",
        Name:      "request_duration_seconds",
        Help:      "Request duration distribution in seconds.",
        Buckets:   prometheus.DefBuckets,
}, []string{"action"}) // Actions

func init() {
        prometheus.DefaultRegisterer.MustRegister(requestDuration)
}

// Create a ticket.
func Create() {
        start := time.Now()
        defer requestDuration.With(prometheus.Labels{"action": "create"}).Observe(time.Since(start).Seconds())

        // Create ticket code.
}
```


In this case, you can view the latencies of P95 for the ticket by using a histogram.

```promql
histogram_quantile(0.95, rate(ticket_request_duration_seconds_bucket{action="create"}[5m]))
```


<span id=".U3VtbWFyeSDnsbvlnos="></span>
### Summary type

A summary is similar to a histogram because it also calculates sample distribution. However, a summary uses more client resources and the data cannot be calculated and processed in an aggregated manner subsequently because the summary calculates the distribution (P99/P95/Sum/Count) on the client. You can also use summaries to monitor metrics such as API response time and database access time.

A summary can be used in a similar way to a histogram, so you can directly refer to the histogram usage.

<span id=".5pq06ZyyIFByb21ldGhldXMg5oyH5qCH"></span>
## Expose Prometheus metrics

Use `promhttp.Handler()` to expose the metric tracking data to the HTTP service.

```golang
package main

import (
    "net/http"

    "github.com/prometheus/client_golang/prometheus/promhttp"
)

func main() {
        // Business code

        // Expose Prometheus metrics to an HTTP service.
        http.Handle("/metrics", promhttp.Handler())

        // Business code
}
```


<span id=".5Lia5Yqh6YOo572y"></span>
## Deploy business

After you configure custom metric tracking for your business, you can deploy an application in a VKE cluster or an ECS instance to release the application. After the application is released, you can access VMP to obtain metric data.

<span id=".5pyN5Yqh5Y-R546w"></span>
## service discovery

When your business is deployed in different environments, different service discovery types are supported.


* When your business is deployed in a VKE cluster, you can use PodMonitor or ServiceMonitor for service discovery. For more details, refer to [Service discovery](https://docs.byteplus.com/en/docs/vmp/service-discovery).

* When your business is deployed in an ECS instance, you can use the **integration center** for service discovery. For more details, refer to [ECS integration](https://docs.byteplus.com/en/docs/vmp/ECS-monitoring).


<span id=".5p-l55yL55uR5o6n5pWw5o2u"></span>
## View monitoring data

You can view metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

You can also use self\-built Grafana to read data stored in VMP and create metric dashboards. For more details, refer to the following topics:


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)
