---
title: "Kitex integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_Kitex"
---

Kitex is an open\-source Go microservice RPC framework developed by ByteDance. This framework delivers **high performance and strong extensibility** and has been widely used internally at ByteDance.

<span id="b7a0590c"></span>
# Integration via OpenTelemetry

<span id="d9600344"></span>
## Step 1: Initialize Kitex

Kitex integrates the OpenTelemetry SDK via middleware, natively supporting the generation and reporting of traces and metrics to Server\-side Monitoring.

Currently, Kitex does not provide default integration for log data reporting. However, you can use community\-contributed logging libraries. A code sample for otelLogger is provided in the server\-side integration section.

The required hello.thrift source file for running the sample code, as well as the generated code, can be obtained from the [cloudwego/kitex-examples](https://github.com/cloudwego/kitex-examples/tree/main/hello) repository. The following section provides the core code for the OpenTelemetry observability integration.

<span id="xTjAR9GT"></span>
### Server\-side integration:

```Go
package main

import (
    "context"
    "log"
    "log/slog"

    api "github.com/cloudwego/kitex-examples/hello/kitex_gen/api/hello"
    "github.com/cloudwego/kitex/server"
    "github.com/kitex-contrib/obs-opentelemetry/provider"
    "github.com/kitex-contrib/obs-opentelemetry/tracing"
    "go.opentelemetry.io/contrib/bridges/otelslog"
    "go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc"
    "go.opentelemetry.io/otel/log/global"
    sdklog "go.opentelemetry.io/otel/sdk/log"
)

var otelLogger *slog.Logger

func main() {
    ctx := context.Background()
    // 1. Initialize the otel provider.
    p := provider.NewOpenTelemetryProvider(
        provider.WithInsecure(),
    )
    defer p.Shutdown(ctx)

    svr := api.NewServer(
        new(HelloImpl),
        // 2. Initialize tracing middleware.
        server.WithSuite(tracing.NewServerSuite()),
    )

    // 3. Initialize the otel log provider.
    lp := initLog(ctx)
    defer lp.Shutdown(ctx)

    // 4. Use a third-party logger to print logs. Logs will be automatically reported to the backend service.
    otelLogger.Info("init logger successfully")

    err := svr.Run()
    if err != nil {
        log.Println(err.Error())
    }
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


<span id="knombVGf"></span>
### Client\-side integration:

```Go
package main

import (
    "context"
    "log"
    "time"

    "github.com/cloudwego/kitex-examples/hello/kitex_gen/api"
    "github.com/cloudwego/kitex-examples/hello/kitex_gen/api/hello"
    "github.com/cloudwego/kitex/client"
    "github.com/kitex-contrib/obs-opentelemetry/provider"
    "github.com/kitex-contrib/obs-opentelemetry/tracing"
)

func main() {
    ctx := context.Background()
    // 1. Initialize the otel provider.
    p := provider.NewOpenTelemetryProvider(
        provider.WithInsecure(),
    )
    defer p.Shutdown(ctx)

    client, err := hello.NewClient(
        "hello",
        client.WithHostPorts("0.0.0.0:8888"),
     // 2. Initialize tracing middleware.
        client.WithSuite(tracing.NewClientSuite()),
    )
    if err != nil {
        log.Fatal(err)
    }
    for {
        req := &api.Request{Message: "my request"}
        resp, err := client.Echo(context.Background(), req)
        if err != nil {
            log.Fatal(err)
        }
        log.Println(resp)
        time.Sleep(time.Second * 10)
    }
}
```


<span id="YXkZF7jU"></span>
## Step 2: Report data

<span id="3d65c1a9"></span>
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


<span id="H8nuyxIJ"></span>
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


&nbsp;

&nbsp;
