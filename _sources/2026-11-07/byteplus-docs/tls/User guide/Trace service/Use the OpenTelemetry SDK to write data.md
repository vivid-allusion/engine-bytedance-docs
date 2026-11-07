---
title: "Use the OpenTelemetry SDK to write data"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_the_opentelemetry_sdk_to_write_data"
---

Torch Log Service (TLS) allows you to use the OpenTelemetry SDK to directly write trace data to TLS. This topic uses the TLS SDK for Go as an example to describe how a Golang application integrates with the trace feature. The integration method is applicable to business systems that use end\-to\-end tracing for the first time.

<span id="前提条件"></span>
## Before you begin


* Configure the Golang development environment. For more information, visit the [Go official website](https://golang.org/doc/install/source) to download and install the Go environment.

* Make sure that the Go version is 1.19 or later. To view the current Go version, run `go version`.


<span id="背景信息"></span>
## Background

In microservice and distributed architectures or systems, multiple services interact with each other. In these architectures or systems, you can use end\-to\-end tracing to analyze service call chains and monitor architecture performance. Trace offers distributed tracing capabilities based on the [OpenTelemetry](https://opentelemetry.io/docs/what-is-opentelemetry/) protocol. By referring to this topic, you can deploy the trace feature in your business system, enable trace events on data sources, and collect and send log data to BytePlus TLS.

<span id="操作步骤"></span>
## Procedure

<span id="_1-创建-trace-实例"></span>
## Step 1: Create a trace instance

In the TLS console, create a trace instance to collect, send, and manage trace data specific to your business system. After the trace instance is created, TLS creates a topic to store the trace data. For more information, refer to [Create a trace instance](https://docs.byteplus.com/docs/tls/create_a_trace_instance).

<span id="_2-添加相关依赖"></span>
## Step 2: Add dependencies

In your local Go project, run the following commands to add dependencies:

```Shell
# Add the OpenTelemetry protocol dependency.
go get go.opentelemetry.io/otel
go get go.opentelemetry.io/otel/trace
go get go.opentelemetry.io/otel/bridge/opentracing

# Add the OpenTelemetry exporter dependency. The exporter is used to send trace data to TLS.
go get go.opentelemetry.io/otel/exporters/otlp/otlptrace

# Add the HTTP exporter dependency if the TLS HTTP port is configured.
go get go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracehttp

# Add the gRPC exporter dependency if the TLS gRPC port is configured.
go get go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracegrpc
```


<span id="_3-初始化-provider"></span>
## Step 3: Initialize the Provider

After you add the dependencies, execute code to initialize an OpenTelemetry Provider. Also, specify a data transmission protocol so that OpenTelemetry can transfer data from your application to the trace instance. In the trace constructor, use the protocol parameter to specify a protocol.

When you initialize the Provider, configure TLS endpoint and authentication parameters. For more information on the parameters, refer to [Parameter description](https://docs.byteplus.com/docs/tls/use_the_opentelemetry_sdk_to_write_data#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E). Use one of the following methods to configure authentication parameters:


* Configure authentication parameters in the headers of a gRPC or HTTPS request.

* Configure authentication parameters in the Resource field of the OpenTelemetry protocol.


<span id="http-协议初始化示例"></span>
### Initialization sample code for HTTP

When you use HTTP to integrate with the trace feature, refer to the following sample code to initialize an OpenTelemetry Provider. TLS supports two methods of configuring authentication parameters. Refer to the sample code for integration. For more information on the parameters, refer to [Parameter description](https://docs.byteplus.com/docs/tls/use_the_opentelemetry_sdk_to_write_data#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E).


* Configure authentication parameters in the Resource field of the OpenTelemetry protocol:

   ```Go
   import (
       "context"
   
       "go.opentelemetry.io/otel/attribute"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracehttp"
       "go.opentelemetry.io/otel/sdk/resource"
       "go.opentelemetry.io/otel/sdk/trace"
       semconv "go.opentelemetry.io/otel/semconv/v1.10.0"
   )
   
   // During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the HTTP OpenTelemetry protocol. In addition, add TracerProvider with authentication information to the body of trace data.
   func InitTlsOtelTracerWithHttpResource(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
       traceTopicKey := attribute.Key("tls.otel.tracetopic")
       akKey := attribute.Key("tls.otel.ak")
       skKey := attribute.Key("tls.otel.sk")
       regionKey := attribute.Key("tls.otel.region")
   
       opts := []otlptracehttp.Option{otlptracehttp.WithEndpoint(endPoint + ":4318")} // The endpoint protocol is HTTP. For more information, refer to Parameter description.
       exporter, _ := otlptrace.New(
          context.Background(),
          otlptracehttp.NewClient(opts...),
       )
   
       tp := trace.NewTracerProvider(
          trace.WithBatcher(exporter),
          trace.WithResource(resource.NewWithAttributes(
             semconv.SchemaURL,
             semconv.ServiceNameKey.String("your_service_name"),
             // Add the authentication parameters required by TLS to the OpenTelemetry request body. For more information, refer to Parameter description.
             traceTopicKey.String(topicId),
             akKey.String(ak),
             skKey.String(sk),
             regionKey.String(region),
          )),
       )
       return tp
   }
   ```
   

* Configure authentication parameters in the HTTPS request headers:

   ```Go
   import (
       "context"
   
       "go.opentelemetry.io/otel/attribute"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracehttp"
       "go.opentelemetry.io/otel/sdk/resource"
       "go.opentelemetry.io/otel/sdk/trace"
       semconv "go.opentelemetry.io/otel/semconv/v1.10.0"
   )
   
   // During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the HTTP OpenTelemetry protocol. In addition, add TracerProvider with authentication information to the HTTP request headers.
   func InitTlsOtelTracerWithHttpHeader(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
       // Add the authentication fields required by TLS to the HTTP request headers. For more information, refer to Parameter description.
       opts := []otlptracehttp.Option{otlptracehttp.WithEndpoint(endPoint + ":4318"), // For more information on the endpoint, refer to Parameter description.
          otlptracehttp.WithHeaders(map[string]string{"x-tls-otel-tracetopic": topicId, "x-tls-otel-ak": ak, "x-tls-otel-sk": sk, "x-tls-otel-region": region})}
       exporter, _ := otlptrace.New(
          context.Background(),
          otlptracehttp.NewClient(opts...),
       )
   
       tp := trace.NewTracerProvider(
          trace.WithBatcher(exporter),
          trace.WithResource(resource.NewWithAttributes(
             semconv.SchemaURL,
             semconv.ServiceNameKey.String("your_service_name"),
          )),
       )
       return tp
   }
   ```
   


<span id="grpc-协议初始化示例"></span>
### Initialization sample code for gRPC

When you use gRPC to integrate with the trace feature, refer to the following sample code to initialize an OpenTelemetry Provider. TLS supports two methods of configuring authentication parameters. Refer to the sample code for integration. For more information on the parameters, refer to [Parameter description](https://docs.byteplus.com/docs/tls/use_the_opentelemetry_sdk_to_write_data#%E5%8F%82%E6%95%B0%E8%AF%B4%E6%98%8E).


* Configure authentication parameters in the Resource field of the OpenTelemetry protocol:

   ```Go
   import (
       "context"
   
       "go.opentelemetry.io/otel/attribute"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracegrpc"
       "go.opentelemetry.io/otel/sdk/resource"
       "go.opentelemetry.io/otel/sdk/trace"
       semconv "go.opentelemetry.io/otel/semconv/v1.10.0"
       "google.golang.org/grpc/credentials/insecure"
   )
   
   // During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the gRPC OpenTelemetry protocol. In addition, add TracerProvider with authentication information to the body of trace data.
   func InitTlsOtelTracerWithGrpcResource(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
       exporter, _ := otlptrace.New(
          context.Background(), otlptracegrpc.NewClient(otlptracegrpc.WithTLSCredentials(insecure.NewCredentials()), otlptracegrpc.WithEndpoint(endPoint+":4317")), // The endpoint protocol is gRPC. For more information, refer to Parameter description.
       )
       traceTopicKey := attribute.Key("tls.otel.tracetopic")
       akKey := attribute.Key("tls.otel.ak")
       skKey := attribute.Key("tls.otel.sk")
       regionKey := attribute.Key("tls.otel.region")
       tp := trace.NewTracerProvider(
          trace.WithBatcher(exporter),
          trace.WithResource(resource.NewWithAttributes(
             semconv.SchemaURL,
             semconv.ServiceNameKey.String("your_service_name"),
             // Add the authentication parameters required by TLS to the OpenTelemetry request body. For more information, refer to Parameter description.
             traceTopicKey.String(topicId),
             akKey.String(ak),
             skKey.String(sk),
             regionKey.String(region),
          )),
       )
       return tp
   }
   ```
   

* Configure authentication parameters in the gRPC request headers:

   ```Go
   import (
       "context"
   
       "go.opentelemetry.io/otel/attribute"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace"
       "go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracegrpc"
       "go.opentelemetry.io/otel/sdk/resource"
       "go.opentelemetry.io/otel/sdk/trace"
       semconv "go.opentelemetry.io/otel/semconv/v1.10.0"
       "google.golang.org/grpc/credentials/insecure"
   )
   
   // During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the gRPC OpenTelemetry protocol. Also, add authentication information to the gRPC request headers when configuring the TracerProvider.
   func InitTlsOtelTracerWithGrpcHeader(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
       // Add the authentication parameters required by TLS to the gRPC request headers. For more information, refer to Parameter description.
       exporter, _ := otlptrace.New(
          context.Background(),
          // Use otlptracegrpc.WithTLSCredentials(insecure.NewCredentials()) to access trace data over the TLS protocol.
          otlptracegrpc.NewClient(otlptracegrpc.WithTLSCredentials(insecure.NewCredentials()), otlptracegrpc.WithEndpoint(endPoint+":4317"), // The endpoint protocol is gRPC. For more information, refer to Parameter description.
             otlptracegrpc.WithHeaders(map[string]string{"x-tls-otel-tracetopic": topicId, "x-tls-otel-ak": ak, "x-tls-otel-sk": sk, "x-tls-otel-region": region})),
       )
       tp := trace.NewTracerProvider(
          trace.WithBatcher(exporter),
          trace.WithResource(resource.NewWithAttributes(
             semconv.SchemaURL,
             semconv.ServiceNameKey.String("your_service_name"),
          )),
       )
       return tp
   }
   ```
   


<span id="参数说明"></span>
### Parameter description

When you initialize the Provider, configure endpoint and authentication parameters in the initialization code. The following section describes the parameters.


* Endpoint parameters

   The endpoint is the URL used to access TLS. It consists of a TLS endpoint and port number. The port number varies depending on the protocol type. The endpoint format is `${tls_endpoint}:PORT_NUMBER`, where `${tls_endpoint}` is the TLS endpoint. For more information, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint).

   * For HTTPS, the endpoint format is `${tls_endpoint}:4318`, such as `tls-ap-southeast-1.ibytepluses.com:4318`.

   * For gRPC, the endpoint format is `${tls_endpoint}:4317`, such as `tls-ap-southeast-1.bytepluses.com:4317`.

      To secure data transmission, enable TLS if you use gRPC.

* Authentication parameters: When you initialize a Provider, configure authentication parameters in the gRPC or HTTPS request headers, or in the Resource field of the OpenTelemetry protocol. The following table describes the parameters in different configuration methods.

   
   |Header Key |Resource Key |Example |Description |
   |---|---|---|---|
   |x\-tls\-otel\-tracetopic |tls.otel.tracetopic |39f0bce1\-e37e\-4dc5\-ab06\-801d310b\*\*\*\* |The ID of the topic that stores the trace data for the trace instance. For more information, refer to [Create a trace instance](https://docs.byteplus.com/docs/tls/create_a_trace_instance). |
   |x\-tls\-otel\-ak |tls.otel.ak |AKKTNTA1OTlmOWQ1NTM5DNk5OIWwZGNmMTg0ZWUxNmU\*\*\*\* |The AccessKey ID of a BytePlus account or an IAM user. On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
   |x\-tls\-otel\-sk |tls.otel.sk |T0RPLS5EUTFZV1JrTmpAKE5EaGCVRGsxTjJVMk5UTTBNV1UzKODJME1U\*\*\*\* |The AccessKey secret of a BytePlus account or an IAM user. On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
   |x\-tls\-otel\-region |tls.otel.region |ap\-southeast\-1 |The ID of the Region where the trace instance resides. View the Region ID in [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   


<span id="_4-使用-tlsoteltracer-发送-trace-数据"></span>
## Step 4: Send trace data using tlsOtelTracer

Send trace data to BytePlus TLS using tlsOtelTracer by referring to the following sample code. For more information, refer to [OpenTelemetry official documentation](https://opentelemetry.io/docs/instrumentation/go/manual/).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you use OpenTelemetry to collect and send trace data, make sure that the data is accurate and complete. To ensure data reliability, we recommend that you verify data and handle errors in your application.</div>


* <div data-tips="true" data-tips-type="tip">Alternatively, enable trace events and use the Config class of OpenTelemetry to configure an event processing procedure on data sources to automatically send trace data to TLS. For more information, refer to <a href="https://opentelemetry.io/docs/instrumentation/go/libraries/">OpenTelemetry official documentation</a>.</div>



```Go
package main

import (
    "context"
    "fmt"
    "math/rand"
    "strconv"
    "time"

    "github.com/google/uuid"
    "github.com/opentracing/opentracing-go"
    "github.com/opentracing/opentracing-go/ext"
    "go.opentelemetry.io/otel/attribute"
    otbridge "go.opentelemetry.io/otel/bridge/opentracing"
    "go.opentelemetry.io/otel/exporters/otlp/otlptrace"
    "go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracegrpc"
    "go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracehttp"
    "go.opentelemetry.io/otel/sdk/resource"
    "go.opentelemetry.io/otel/sdk/trace"
    semconv "go.opentelemetry.io/otel/semconv/v1.10.0"
    "google.golang.org/grpc/credentials/insecure"
)

func main() {
    SendTrace(1000)
    time.Sleep(time.Minute)
}

func SendTrace(traceCnt int) {
    endPoint := "tls-ap-southeast-1.bytepluses.com" // For other Regions, replace the endpoint with the actual one. Type a private endpoint if you use a virtual private cloud (VPC).
    topicId := "${topicId}"
    ak := "${AK}"
    sk := "${SK}"
    region := "cn-shanghai" // Replace the Region with the actual one.
    // Select a method to initialize the TracerProvider.
    httpHeaderProvider := InitTlsOtelTracerWithHttpHeader(endPoint, topicId, ak, sk, region)
    // httpResourceProvider := InitTlsOtelTracerWithHttpResource(endPoint, topicId, ak, sk, region)
    // grpcHeaderProvider := InitTlsOtelTracerWithGrpcHeader(endPoint, topicId, ak, sk, region)
    // grpcResourceProvider := InitTlsOtelTracerWithGrpcResource(endPoint, topicId, ak, sk, region)

    tracer, _ := otbridge.NewTracerPair(httpHeaderProvider.Tracer("my_trace"))
    ctx := context.TODO()
    for i := 0; i < traceCnt; i++ {
       sendTrace(ctx, tracer)
    }
}

func sendTrace(ctx context.Context, tracer *otbridge.BridgeTracer) {
    var OperationName []string
    OperationName = append(OperationName, "Operation_1", "Operation_2", "Operation_3", "Operation_4", "Operation_5")
    i := 0
    var last_span opentracing.Span
    var span opentracing.Span
    for {
       uid, _ := uuid.NewUUID()
       index := strconv.Itoa(i)
       if i == 0 {
          span = spanInit(true, ctx, "test.span."+index, tracer, nil)
       } else {
          span = spanInit(false, ctx, "test.span"+index, tracer, last_span.Context())
       }
       ext.SpanKindRPCClient.Set(span)
       ext.PeerService.Set(span, "tls-test-service")
       // // // #nosec
       span.LogKV(
          "event", "soft error",
          "type", "cache timeout",
          "waited.millis", 1500)
       span.SetTag("uuid", uid.String())
       span.SetTag("host", "")
       span.SetBaggageItem("BaggageItem", "TLS test")
       span.SetOperationName(OperationName[rand.Intn(4)])
       span.FinishWithOptions(opentracing.FinishOptions{FinishTime: time.Now()})
       last_span = span
       fmt.Println("successful", i)
       i++
       if i > 100 {
          break
       }
    }
}

func spanInit(isRoot bool, context context.Context, span_name string, otTracer *otbridge.BridgeTracer, childOfSpanContext opentracing.SpanContext) opentracing.Span {
    var span opentracing.Span
    if isRoot {
       span, _ = opentracing.StartSpanFromContext(context, span_name+".root.span")
    } else {
       span = otTracer.StartSpan("TLS test", opentracing.ChildOf(childOfSpanContext))
    }
    return span
}

// During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the HTTP OpenTelemetry protocol. In addition, add TracerProvider with authentication information to the HTTP request headers.
func InitTlsOtelTracerWithHttpHeader(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
    // Add the authentication fields required by TLS to the HTTP request headers. For more information, refer to Parameter description.
    opts := []otlptracehttp.Option{otlptracehttp.WithEndpoint(endPoint + ":4318"), // For more information on the endpoint, refer to Parameter description.
       otlptracehttp.WithHeaders(map[string]string{"x-tls-otel-tracetopic": topicId, "x-tls-otel-ak": ak, "x-tls-otel-sk": sk, "x-tls-otel-region": region})}
    exporter, _ := otlptrace.New(
       context.Background(),
       otlptracehttp.NewClient(opts...),
    )

    tp := trace.NewTracerProvider(
       trace.WithBatcher(exporter),
       trace.WithResource(resource.NewWithAttributes(
          semconv.SchemaURL,
          semconv.ServiceNameKey.String("your_service_name"),
       )),
    )
    return tp
}

// During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the HTTP OpenTelemetry protocol. In addition, add TracerProvider with authentication information to the body of trace data.
func InitTlsOtelTracerWithHttpResource(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
    traceTopicKey := attribute.Key("tls.otel.tracetopic")
    akKey := attribute.Key("tls.otel.ak")
    skKey := attribute.Key("tls.otel.sk")
    regionKey := attribute.Key("tls.otel.region")

    opts := []otlptracehttp.Option{otlptracehttp.WithEndpoint(endPoint + ":4318")} // The endpoint protocol is HTTP. For more information, refer to Parameter description.
    exporter, _ := otlptrace.New(
       context.Background(),
       otlptracehttp.NewClient(opts...),
    )

    tp := trace.NewTracerProvider(
       trace.WithBatcher(exporter),
       trace.WithResource(resource.NewWithAttributes(
          semconv.SchemaURL,
          semconv.ServiceNameKey.String("your_service_name"),
          // Add the authentication parameters required by TLS to the OpenTelemetry request body. For more information, refer to Parameter description.
          traceTopicKey.String(topicId),
          akKey.String(ak),
          skKey.String(sk),
          regionKey.String(region),
       )),
    )
    return tp
}

// During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the gRPC OpenTelemetry protocol. Also, add authentication information to the gRPC request headers when configuring the TracerProvider.
func InitTlsOtelTracerWithGrpcHeader(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
    // Add the authentication parameters required by TLS to the gRPC request headers. For more information, refer to Parameter description.
    exporter, _ := otlptrace.New(
       context.Background(),
       // Use otlptracegrpc.WithTLSCredentials(insecure.NewCredentials()) to access trace data over the TLS protocol.
       otlptracegrpc.NewClient(otlptracegrpc.WithTLSCredentials(insecure.NewCredentials()), otlptracegrpc.WithEndpoint(endPoint+":4317"), // The endpoint protocol is gRPC. For more information, refer to Parameter description.
          otlptracegrpc.WithHeaders(map[string]string{"x-tls-otel-tracetopic": topicId, "x-tls-otel-ak": ak, "x-tls-otel-sk": sk, "x-tls-otel-region": region})),
    )
    tp := trace.NewTracerProvider(
       trace.WithBatcher(exporter),
       trace.WithResource(resource.NewWithAttributes(
          semconv.SchemaURL,
          semconv.ServiceNameKey.String("your_service_name"),
       )),
    )
    return tp
}

// During the initialization, when setting the endPoint parameter, pass in the TLS endpoint and the port using the gRPC OpenTelemetry protocol. In addition, add TracerProvider with authentication information to the body of trace data.
func InitTlsOtelTracerWithGrpcResource(endPoint string, topicId string, ak string, sk string, region string) *trace.TracerProvider {
    exporter, _ := otlptrace.New(
       context.Background(), otlptracegrpc.NewClient(otlptracegrpc.WithTLSCredentials(insecure.NewCredentials()), otlptracegrpc.WithEndpoint(endPoint+":4317")), // The endpoint protocol is gRPC. For more information, refer to Parameter description.
    )
    traceTopicKey := attribute.Key("tls.otel.tracetopic")
    akKey := attribute.Key("tls.otel.ak")
    skKey := attribute.Key("tls.otel.sk")
    regionKey := attribute.Key("tls.otel.region")
    tp := trace.NewTracerProvider(
       trace.WithBatcher(exporter),
       trace.WithResource(resource.NewWithAttributes(
          semconv.SchemaURL,
          semconv.ServiceNameKey.String("your_service_name"),
          // Add the authentication parameters required by TLS to the OpenTelemetry request body. For more information, refer to Parameter description.
          traceTopicKey.String(topicId),
          akKey.String(ak),
          skKey.String(sk),
          regionKey.String(region),
       )),
    )
    return tp
}
```


<span id="验证接入结果"></span>
## Verifying the integration result

After trace data is integrated, you can use the query and analysis feature of TLS to view the collected trace data. If the trace data you uploaded can be queried from the corresponding topic of the trace instance, the trace data is integrated as expected. For more information on how to query trace data, refer to [Query logs](https://docs.byteplus.com/docs/tls/Query-logs-2).

For example, use the following SQL syntax to query trace data by trace ID.

```SQL
* ｜ select * where TraceID = '877247fa95024d2f3a1234216010****'
```
