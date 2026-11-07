---
title: "Integrating log monitoring with Go applications"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_log_monitoring_into_a_Go_application"
---

APMPlus supports log monitoring and provides the following capabilities on collected logs: log list, log search, and single\-trace log query. This topic describes how to integrate APMPlus log monitoring with your Go applications by using OpenTelemetry.

<span id="3vVDrKRX"></span>
## Prerequisites

You have obtained service\-related configuration information, such as service name, appkey, and endpoint.


|Variable |Description |
|---|---|
| *{apmplus_endpoint}*  |The Server\-side Monitoring endpoint. This configuration varies with the reporting method. Configure this field based on your reporting method.<br><br><br>* **Reporting to Otel Collector**: (Recommended) Forwarding is performed by the Otel Collector. If the apmplus\-opentelemetry\-collector version is greater than or equal to 2.0.0, use `http://apmplus-opentelemetry-gateway-service-grpc.apmplus-opentelemetry-operator:4317`. If the version is lower than 2.0.0, use `http://apmplus-opentelemetry-gateway-service-grpc.kube-system:4317`.<br><br>* **Reporting to Server\-side Monitoring**: In the integration center, obtain the public or private access *endpoint* for the region of the service. |
|{apmplus_appkey} |The Server\-side Monitoring authentication information. This information is required for reporting to Server\-side Monitoring.<br><br><br>* **Reporting to Otel Collector**: appkey is not required. You need to delete the appkey\-related configuration.<br><br>* **Reporting to Server\-side Monitoring**: appkey must be configured. For instructions on obtaining an appkey, see [How do I obtain the AppKey for authentication in Server-side Monitoring?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication) |
| *{service_name}*  |Service name. You can obtain it from the service list. |


<span id="AqMqYOrZ"></span>
## Procedure

OpenTelemetry supports the following logging frameworks. Select a framework that meets your requirements. See the [official OpenTelemetry documentation](https://opentelemetry.io/ecosystem/registry/?component=log-bridge&language=go) for details.


<Tabs>
<Tab zoneid="N5tdbegHDU" title="Use zap">
<TabTitle>Use zap</TabTitle>

1. Download dependencies.


```Go
go get go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc
go get go.opentelemetry.io/contrib/bridges/otelzap
go get go.uber.org/zap
```



2. Configure *LoggerProvider*.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For instructions on obtaining and configuring variable values, see the prerequisites.</div>


```Go
import (
    "context"
    "time"

    "go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc"
    "go.opentelemetry.io/otel/log/global"
    "go.opentelemetry.io/otel/sdk/log"
)

func InitOtlLog() *log.LoggerProvider {
    ctx := context.Background()
    // Report using the gRPC protocol.
    exporter, err := otlploggrpc.New(ctx,
       otlploggrpc.WithEndpoint("{{apmplus_endpoint}}"), // Specify the endpoint to report logs to.
       otlploggrpc.WithInsecure(),
       otlploggrpc.WithHeaders(map[string]string{"x-byteapm-appkey": "{{apmplus_appkey}}"}), // appkey (Server-side Monitoring authentication information). For reporting to the Otel Collector, delete this line, as this configuration item is not required. For reporting to Server-side Monitoring, an appkey is required.
       otlploggrpc.WithTimeout(10*time.Second),
    )
    if err != nil {
       panic(err)
    }

    hostname, _ := os.Hostname()
    loggerProvider := log.NewLoggerProvider(
       log.WithProcessor(log.NewBatchProcessor(exporter)),
       log.WithResource(resource.NewWithAttributes(
          semconv.SchemaURL,
          semconv.ServiceNameKey.String("{{service_name}}"), // The service name.
          semconv.HostNameKey.String(hostname)),
       ),
    )

    global.SetLoggerProvider(loggerProvider)
    // Properly handle the shutdown process to ensure no leaks.
    return loggerProvider
}

// Put it in the initialization path to ensure the following logic is executed.
loggerProvider := initOtlLog()
defer loggerProvider.Shutdown(context.Background())
```



3. Initialize zap and use it to print logs.


```Go
package zap_demo

import (
    "context"

    "go.opentelemetry.io/contrib/bridges/otelzap"
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/baggage"
    "go.opentelemetry.io/otel/log/global"
    "go.uber.org/zap"
)

var (
    tracer = otel.Tracer("otel-demo-tracer")
    // AddCaller ensures the file name and line number are printed.
    logger = zap.New(otelzap.NewCore("my/demo/pkg", otelzap.WithLoggerProvider(global.GetLoggerProvider())), zap.AddCaller())
)

// Call the Call method and print logs.
func Call(ctx context.Context) {
    // Generate a new span based on ctx.
    ctx, span := tracer.Start(ctx, "otelLogCall")
    defer span.End()

    ctx = context.WithValue(ctx, "key", "value")
    // Use ctx to report traceId and spanId. Additionally, the keys and values in Fields are also reported.
    logger.Info("this is zap info demo", zap.Any("context", ctx), zap.String("method", "zapCall"))
    logger.Info("this is zap info demo without context")
}
```



</Tab>
<Tab zoneid="v0CceuQ4A4" title="Use slog">
<TabTitle>Use slog</TabTitle>

1. Download dependencies.


```Go
go get go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc
go get go.opentelemetry.io/contrib/bridges/otellogrus
go get github.com/sirupsen/logrus
```



2. Configure *LoggerProvider*.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For instructions on obtaining and configuring variable values, see the prerequisites.</div>


```Go
import (
    "context"
    "time"

    "go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc"
    "go.opentelemetry.io/otel/log/global"
    "go.opentelemetry.io/otel/sdk/log"
)

func InitOtlLog() *log.LoggerProvider {
    ctx := context.Background()
    // Report using the gRPC protocol.
    exporter, err := otlploggrpc.New(ctx,
       otlploggrpc.WithEndpoint("{{apmplus_endpoint}}"), // Specify the endpoint to report logs to.
       otlploggrpc.WithInsecure(),
       otlploggrpc.WithHeaders(map[string]string{"x-byteapm-appkey": "{{apmplus_appkey}}"}), // appkey (Server-side Monitoring authentication information). For reporting to the Otel Collector, delete this line, as this configuration item is not required. For reporting to Server-side Monitoring, an appkey is required.
       otlploggrpc.WithTimeout(10*time.Second),
    )
    if err != nil {
       panic(err)
    }

    hostname, _ := os.Hostname()
    loggerProvider := log.NewLoggerProvider(
       log.WithProcessor(log.NewBatchProcessor(exporter)),
       log.WithResource(resource.NewWithAttributes(
          semconv.SchemaURL,
          semconv.ServiceNameKey.String("{{service_name}}"), // The service name must be specified.
          semconv.HostNameKey.String(hostname)),
       ),
    )

    global.SetLoggerProvider(loggerProvider)
    // Properly handle the shutdown process to ensure no leaks.
    return loggerProvider
}

// Put it in the initialization path to ensure the following logic is executed.
loggerProvider := initOtlLog()
defer loggerProvider.Shutdown(context.Background())
```



3. Initialize logrus and use logrus to print logs.


```Go
package logrus_demo

import (
    "context"

    "github.com/sirupsen/logrus"
    "go.opentelemetry.io/contrib/bridges/otellogrus"
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/baggage"
    "go.opentelemetry.io/otel/log/global"
)

var (
    tracer = otel.Tracer("otel-demo-tracer")
    logger = logrus.New()
)

func init() {
    // Create *otellogrus.Hook and use it in the application.
    hook := otellogrus.NewHook("my/demo/pkg", otellogrus.WithLoggerProvider(global.GetLoggerProvider()))
    logger.AddHook(hook)
    logger.SetReportCaller(true)
}

// Call the Call method and print logs.
func Call(ctx context.Context) {
    // Generate a new span based on ctx.
    ctx, span := tracer.Start(ctx, "otelLogCall")
    defer span.End()

    // Use ctx to report traceId and spanId. Additionally, the keys and values in Fields are also reported.
    logger.WithContext(ctx).WithFields(logrus.Fields{"user_id": 10010, "ip": "192.168.32.15"}).Info("this is logrus info demo with context")
    logger.Warn("this is logrus warn demo without context")
    logger.Error("this is logrus error demo without context")
}
```



</Tab>
<Tab zoneid="qkw9TYTN5K" title="Use slog">
<TabTitle>Use slog</TabTitle>

1. Download dependencies.


```Go
go get go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc
go get go.opentelemetry.io/contrib/bridges/otelslog
```



2. Configure *LoggerProvider*.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For instructions on obtaining and configuring variable values, see the prerequisites.</div>


```Go
import (
    "context"
    "time"

    "go.opentelemetry.io/otel/exporters/otlp/otlplog/otlploggrpc"
    "go.opentelemetry.io/otel/log/global"
    "go.opentelemetry.io/otel/sdk/log"
)

func InitOtlLog() *log.LoggerProvider {
    ctx := context.Background()
    // Report using the gRPC protocol.
    exporter, err := otlploggrpc.New(ctx,
       otlploggrpc.WithEndpoint("{{apmplus_endpoint}}"), // Specify the endpoint to report logs to.
       otlploggrpc.WithInsecure(),
       otlploggrpc.WithHeaders(map[string]string{"x-byteapm-appkey": "{{apmplus_appkey}}"}), // appkey (Server-side Monitoring authentication information). For reporting to the Otel Collector, delete this line, as this configuration item is not required. For reporting to Server-side Monitoring, an appkey is required.
       otlploggrpc.WithTimeout(10*time.Second),
    )
    if err != nil {
       panic(err)
    }

    hostname, _ := os.Hostname()
    loggerProvider := log.NewLoggerProvider(
       log.WithProcessor(log.NewBatchProcessor(exporter)),
       log.WithResource(resource.NewWithAttributes(
          semconv.SchemaURL,
          semconv.ServiceNameKey.String("{{service_name}}"), // The service name must be specified.
          semconv.HostNameKey.String(hostname)),
       ),
    )

    global.SetLoggerProvider(loggerProvider)
    // Properly handle the shutdown process to ensure no leaks.
    return loggerProvider
}

// Put it in the initialization path to ensure the following logic is executed.
loggerProvider := initOtlLog()
defer loggerProvider.Shutdown(context.Background())
```



3. Initialize slog and use slog to print logs.


```Go
package slog_demo

import (
    "context"

    "go.opentelemetry.io/contrib/bridges/otelslog"
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/baggage"
)

var (
    logger = otelslog.NewLogger("my/demo/pkg", otelslog.WithSource(true))
    tracer = otel.Tracer("otel-log-tracer")
)

func init() {

}
// Call the Call method and print logs.
func Call(ctx context.Context) {
    // Generate a new span based on ctx.
    ctx, span := tracer.Start(ctx, "otelLogCall")
    defer span.End()
    logger.Info("this is slog info demo without context")
    // When printing logs, include the context so that traceId and spanId are reported.
    logger.InfoContext(ctx, "this is slog info demo with context")
    logger.ErrorContext(ctx, "this is slog error demo with context")
    // When printing logs, include the context so that traceId and spanId are reported. In addition, the keys and values in attr are also reported to Attribute.
    logger.LogAttrs(ctx, slog.LevelInfo, "this is slog info logAttrs demo with context", slog.String("k1", "v1"))
}
```



</Tab>
</Tabs>


<span id="725amjF9"></span>
## What to do next

After you integrate your Go application with log monitoring, use the OpenTelemetry SDK to report printed logs to APMPlus. You can go to the Server\-side Monitoring page to query logs. Supported capabilities include log query and single\-trace log details. For details, see [Log monitoring](https://docs.byteplus.com/en/docs/apmplus/Log_monitoring).
