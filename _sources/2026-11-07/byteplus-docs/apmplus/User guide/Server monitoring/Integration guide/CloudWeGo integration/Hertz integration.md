---
title: "Hertz integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_Hertz"
---

Hertz is a Golang microservice HTTP framework that delivers high usability, high performance, and high scalability.

<span id="c5e6c875"></span>
# Integration via OpenTelemetry

<span id="eda0720b"></span>
## Step 1: Initialize Hertz

Hertz integrates the OpenTelemetry SDK via middleware, natively supporting the generation and reporting of traces and metrics.

Currently, Hertz does not provide default integration for log data reporting. However, you can use community\-contributed logging libraries. A code sample for otelLogger is provided in the server\-side integration section.

<span id="70c84d66"></span>
### Server\-side integration:

```Go
package main

import (
    "context"
    "log/slog"
    "time"

    "github.com/cloudwego/hertz/pkg/app"
    "github.com/cloudwego/hertz/pkg/app/server"
    "github.com/cloudwego/hertz/pkg/protocol/consts"
    "github.com/hertz-contrib/obs-opentelemetry/provider"
    hertztracing "github.com/hertz-contrib/obs-opentelemetry/tracing"
    "go.opentelemetry.io/contrib/bridges/otelslog"
    "go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc"
    "go.opentelemetry.io/otel/log/global"
    sdklog "go.opentelemetry.io/otel/sdk/log"
)

var otelLogger *slog.Logger

func main() {
    // 1. Initialize the otel metrics/traces provider.
    ctx := context.Background()
    p := provider.NewOpenTelemetryProvider(
        provider.WithInsecure(),
    )
    defer p.Shutdown(ctx)

    // 2. Initialize the hertz tracer middleware.
    tracer, cfg := hertztracing.NewServerTracer()
    h := server.Default(tracer)
    h.Use(hertztracing.ServerMiddleware(cfg))

    // 3. Initialize the otel log provider.
    lp := initLog(ctx)
    defer lp.Shutdown(ctx)

    h.GET("/ping", func(c context.Context, ctx *app.RequestContext) {
        // 4. Use otelLogger to record logs.
        otelLogger.InfoContext(c, "/ping called", "time", time.Now().Unix())
        ctx.JSON(consts.StatusOK, time.Now().Unix())
    })

    h.Spin()
}

func initLog(ctx context.Context) *sdklog.LoggerProvider {
    logExporter, err := otlploggrpc.New(ctx, otlploggrpc.WithInsecure())
    if err != nil {
        panic("failed to initialize exporter")
    }

    lp := sdklog.NewLoggerProvider(
        sdklog.WithProcessor(
            sdklog.NewSimpleProcessor(logExporter),
        ),
    )

    global.SetLoggerProvider(lp)

    // init otelLogger, then use it directly anywhere in your app to record your log, and the
    // log content will be sent to apmplus backend.
    otelLogger = otelslog.NewLogger("slog")
    return lp
}
```


<span id="8c949022"></span>
### Client\-side integration:

```Go
package main

import (
    "context"
    "fmt"
    "time"

    "github.com/cloudwego/hertz/pkg/app/client"
    "github.com/cloudwego/hertz/pkg/common/hlog"
    "github.com/hertz-contrib/obs-opentelemetry/provider"
    hertztracing "github.com/hertz-contrib/obs-opentelemetry/tracing"
)

func main() {
    // 1. Initialize the otel metrics/traces provider.
    p := provider.NewOpenTelemetryProvider(
        provider.WithInsecure(),
    )
    defer p.Shutdown(context.Background())

    // 2. Initialize the hertz tracer middleware.
    c, _ := client.NewClient()
    c.Use(hertztracing.ClientMiddleware())

    for {
        ctx := context.Background()
        _, b, err := c.Get(ctx, nil, "http://0.0.0.0:8888/ping?foo=bar")
        if err != nil {
            hlog.CtxErrorf(ctx, err.Error())
        }

        fmt.Println("request sent return:", string(b))

        <-time.After(time.Second * 10)
    }
}
```


<span id="KPSwroYv"></span>
## Step 2: Report data

<span id="AVYfueUY"></span>
### Method 1: Report directly to Server\-side Monitoring


1. Obtain authentication information

2. Set environment variables and start the Kitex application.



|Variable name |Description |
|---|---|
|OTEL_SERVICE_NAME |Set the service name. |
|OTEL_EXPORTER_OTLP_ENDPOINT |Set the destination address of data reporting. For details, see "Destination addresses of reporting". |
|OTEL_EXPORTER_OTLP_HEADERS |Authentication information in the following format: OTEL_EXPORTER_OTLP_HEADERS=X\-ByteAPM\-AppKey=\*\*\*\*\*\*\* |


Destination addresses of reporting:


|Network type |Region |Destination address of reporting |
|---|---|---|
|Public network |Beijing |https://apmplus\-cn\-beijing.volces.com:4317 |
||China (Shanghai) |https://apmplus\-cn\-shanghai.volces.com:4317 |
|Private network |Beijing |http://apmplus\-cn\-beijing.ivolces.com:4317 |
||China (Shanghai) |http://apmplus\-cn\-shanghai.ivolces.com:4317 |


<span id="tWgdEnvq"></span>
### Method 2: Forward data via the OTel Collector

APMPlusOpenTelemetryCollector is a data collector developed by APMPlus based on OpenTelemetryCollector. You can install the OpenTelemetry Collector in your cluster to forward data.


1. Install the VKE add\-on: APMPlusOpenTelemetryCollector.

* Select the cluster where the application will be deployed.

* Click Addons \> Monitoring and install apmplus\-opentelemetry\-collector.

2. Set environment variables and start the Kitex application.



|Variable name |Description |
|---|---|
|OTEL_SERVICE_NAME |Set the service name. |
|OTEL_EXPORTER_OTLP_ENDPOINT |The address to which data will be reported. Set it to the address of the collector within the cluster: <br><br> http://apmplus\-opentelemetry\-gateway\-service\-grpc.apmplus\-opentelemetry\-operator:4317 |
