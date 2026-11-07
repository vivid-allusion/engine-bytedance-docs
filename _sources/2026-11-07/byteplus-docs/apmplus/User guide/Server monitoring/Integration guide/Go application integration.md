---
title: "Go application integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_Go_applications"
---

Go applications have different integration methods for different scenarios. This document describes detailed integration actions for Go applications in various scenarios. After integration, you can automatically collect trace information, automatically generate metric data, and use features such as trace search, log search, and more.

<span id="6b81f40b"></span>
## Integration via OpenTelemetry (recommended)

OpenTelemetry is an observability project under CNCF, designed to provide standardized solutions in the observability field. It addresses the standardization of data models, collection, processing, and export of observability data, and offers services independent of third\-party vendors.

To integrate with the OpenTelemetry SDK, the APMPlus server side can receive data reported by OpenTelemetry. After integrating with APMPlus, you will gain capabilities such as RED method generation, multidimensional trace search, single trace search, topology generation, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To isolate production and test data, see <a href="https://docs.byteplus.com/en/docs/apmplus/Isolate_production_and_test_data">Isolate production and test data</a>.</div>


<span id="5784f89b"></span>
### Limits


* There are certain limits when converting OpenTelemetry metrics to Prometheus metrics:

   * As with [open source](https://opentelemetry.io/docs/reference/specification/compatibility/prometheus_and_openmetrics/#dropped-data-points), [ExponentialHistogram](https://opentelemetry.io/docs/reference/specification/metrics/data-model/#exponentialhistogram) is not supported.

   * Data with the aggregation method set to delta is not supported. Do not modify the default aggregation configuration on the SDK side. Ensure that the aggregation method on the SDK side is set to cumulative.

* Each workspace has independent data reporting credentials. To manage and isolate data using workspaces, ensure that the `apmplus-opentelemetry-collector` component has been upgraded to version v3.1.0 or above.


<span id="e5675db8"></span>
### Data reporting

<span id="6f253b70"></span>
#### Method 1: Report directly to the ApmPlus server side

Observability data can be reported directly to the ApmPlus server side, supporting users to report data via grpc, http/protobuf, and other methods.

<span id="6dc21260"></span>
#### Method 2: Otel Collector forwarding [recommended]

APMPlusOpenTelemetryCollector is a data collector developed by APMPlus based on OpenTelemetryCollector. You can install the Opentelemetry Collector in the cluster for data forwarding. There are two installation methods:


* Install the apmplus\-opentelemetry\-collector component via the VKE cluster component center using the blank screen installation method (a direct installation process provided by the platform). In addition, it is recommended to install the apmplus\-server\-agent component at the same time to enable metric data collection at the host and process levels.

* Manually install using the script provided on the service integration page.


<span id="0343ccda"></span>
### Data Integration

To integrate Opentelemetry with Go services, you typically need to introduce the [Opentelemetry SDK](https://github.com/open-telemetry/opentelemetry-go) or [third-party enhancement libraries](https://github.com/open-telemetry/opentelemetry-go-contrib) in your application. For details, see the [opentelemetry Go open source documentation](https://opentelemetry.io/docs/instrumentation/go/).

After completing code compilation, set otel\-related properties via environment variables before starting:


* To send data directly to the ApmPlus server side:

   ```Shell
   export OTEL_GO_X_RESOURCE=true
   export OTEL_EXPORTER_OTLP_PROTOCOL=<protocol>
   export OTEL_EXPORTER_OTLP_ENDPOINT=<apmplus_endpoint>
   export OTEL_SERVICE_NAME=<service_name>
   export OTEL_EXPORTER_OTLP_HEADERS="X-ByteAPM-AppKey=<app_key>"
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><protocol\> It is recommended to use grpc</div>


<div data-tips="true" data-tips-type="tip"><apmplus_endpoint\> The address varies depending on region (Shanghai, Beijing, and so on) and network type (public network, private network). For details, see the ApmPlus service access page to obtain the specific endpoint.</div>


<div data-tips="true" data-tips-type="tip"><app_key\> Enter the app_key provided by the service access console. The app_key for each workspace is different. For the method to obtain it, see: <a href="https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication">How to obtain authentication information AppKey for application performance monitoring?</a>.</div>



* To send data to Collector

   * Method 1: Inject via environment variables

   ```Shell
   export OTEL_GO_X_RESOURCE=true
   export OTEL_EXPORTER_OTLP_PROTOCOL=<protocol>
   export OTEL_EXPORTER_OTLP_ENDPOINT=<collector_endpoint>
   export OTEL_SERVICE_NAME=<service_name>
   export OTEL_RESOURCE_ATTRIBUTES=apmplus.workspace=<workspace_name>
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><protocol\> It is recommended to use grpc.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><service_name\> Enter the application service name.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><collector_endpoint\> According to the installed apmplus\-opentelemetry\-collector version: if \>= 2.0.0, use http://apmplus\-opentelemetry\-gateway\-service\-grpc.apmplus\-opentelemetry\-operator:4317; if lower than this version, use http://apmplus\-opentelemetry\-gateway\-service\-grpc.kube\-system:4317.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><workspace_name\> Specify the name of the workspace to which the service belongs.   </div>
   

   * Method 2: In the VKE scenario, manually add `instrumentation.apmplus.volcengine.com/inject-sdk` and `instrumentation.apmplus.volcengine.com/workspace` annotations in the Yaml.

      ```YAML
      apiVersion: apps/v1
      kind: Deployment
      metadata:
        name: simple-go
        labels:
          app: simple-go
      spec:
        replicas: 1
        selector:
          matchLabels:
            app: simple-go
        template:
          metadata:
            labels:
              app: simple-go
            annotations:
              instrumentation.apmplus.volcengine.com/inject-sdk: 'true' # Turn on APMPlus observation injection
              instrumentation.apmplus.volcengine.com/workspace: default  # Specify the workspace to which the service belongs
          spec:
            containers:
            - name: simple-go
              image: java_demo_simple
              imagePullPolicy: Always
              env:
              - name: CONTAINER_RUNTIME
                value: "k8s"
      ```
      

   * Method 3: Modify the workload in the VKE blank screen. See the example below. After modification, restart the business POD.


To monitor Go runtime metrics, perform the following actions:


1. Import the [runtime Instrument](https://github.com/open-telemetry/opentelemetry-go-contrib/tree/main/instrumentation/runtime) library (version must be \>= `v0.53.0`), and manually initialize it in the business code. For details, see: [example](https://pkg.go.dev/go.opentelemetry.io/contrib/instrumentation/runtime#example-package)


```Go
package main

import (
        "context"
        "log"
        "time"

        "go.opentelemetry.io/contrib/instrumentation/runtime"
        "go.opentelemetry.io/otel"
        "go.opentelemetry.io/otel/sdk/metric"
)

func main() {
        // This reader is used as a stand-in for a reader that will actually export
        // data. See https://pkg.go.dev/go.opentelemetry.io/otel/exporters for
        // exporters that can be used as or with readers.
        reader := metric.NewManualReader(
                // Add the runtime producer to get histograms from the Go runtime.
                metric.WithProducer(runtime.NewProducer()),
        )
        provider := metric.NewMeterProvider(metric.WithReader(reader))
        defer func() {
                err := provider.Shutdown(context.Background())
                if err != nil {
                        log.Fatal(err)
                }
        }()
        otel.SetMeterProvider(provider)

        // Initialize runtime metric collection
        err := runtime.Start(runtime.WithMinimumReadMemStatsInterval(time.Second))
        if err != nil {
                log.Fatal(err)
        }
}
```



2. When starting the application, set environment variables to disable deprecated runtime metrics.


```Shell
export OTEL_GO_X_DEPRECATED_RUNTIME_METRICS=false
```


<span id=".6YCa6L-HSmFlZ2Vy5o6l5YWl"></span>
## Integration via Jaeger

Jaeger is an open\-source distributed tracing system developed by Uber.

For existing systems already integrated with Jaeger, Jaeger trace data can be reported to APMPlus to achieve comprehensive full trace monitoring capabilities.

After integrating with APMPlus, you will gain capabilities such as RED metric generation, multidimensional trace search, single trace search, topology generation, and more.

<span id=".SmFlZ2VyIEFnZW505o6l5YWl"></span>
### Jaeger Agent integration

The SDK reports data to the Agent, and the Agent reports data to the ApmPlus server side.


1. Configure the application to turn on data collection.

   Refer to the Jaeger documentation to send trace data to the Agent via UDP.

2. Configure the Agent and modify the reporting endpoint.

   1. Modify the jaeger\-agent start parameters. Example configuration is as follows:

      ```bash
      ./jaeger-agent --reporter.grpc.host-port=apmplus-{region}.ivolces.com:4317 \ 
      --reporter.grpc.tls.enabled=false \ 
      --agent.tags=app_key={appkey}
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For the complete configuration command, see the access center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the access center?</a>.      </div>
      

3. Restart the application.


<span id=".U0RL55u05o6l5LiK5oql"></span>
### SDK direct reporting

The SDK collects data and reports directly to the ApmPlus server side.


1. Configure the application to turn on data collection and reporting.

   * The following is sample code for configuring the reporter via the public network:

      ```Go
      sender := jaeger_transport.NewHTTPTransport("https://apmplus-{region}.volces.com/server_collect/third_party/jaeger/v2/{appkey}/api/traces") 
      reporter := jaeger.NewRemoteReporter(sender)
      ```
      

   * The following is sample code for configuring the reporter via the private network:

      ```go
      sender := jaeger_transport.NewHTTPTransport("http://apmplus-{region}.ivolces.com/server_collect/third_party/jaeger/v2/{appkey}/api/traces") 
      reporter := jaeger.NewRemoteReporter(sender)
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For the complete configuration command, please go to the access center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the access center?</a>.      </div>
      

2. Restart the application.


<span id=".6YCa6L-HWmlwa2lu5o6l5YWl"></span>
## Integrate via Zipkin

Zipkin is an open\-source distributed tracing system developed by Twitter. Zipkin helps you collect trace data.

For systems that have already integrated Zipkin, existing trace data can be reported to APMPlus to achieve comprehensive end\-to\-end monitoring capabilities.

After integrating with APMPlus, you will gain capabilities such as RED metric generation, multidimensional trace search, single trace search, topology map generation, and other APMPlus capabilities.

<span id="EoynKG1m"></span>
### SDK direct reporting

The SDK collects data and reports directly to the APMPlus server side.


1. Configure the application and turn on data reporting.

   * Obtain the zipkin reporting endpoint via the public network.

      ```Bash
      https://apmplus-{region}.volces.com/server_collect/third_party/zipkin/v2/{appkey}/api/v2/spans
      ```
      

   * Obtain the zipkin reporting endpoint via the private network.

      ```Plain Text
      http://apmplus-{region}.ivolces.com/server_collect/third_party/zipkin/v2/{appkey}/api/v2/spans
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For the complete configuration command, please go to the access center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the access center?</a>.      </div>
      

   2. Integrate the service and configure the reporting endpoint. For details, see [zipkin-go sample code](https://github.com/openzipkin/zipkin-go).

2. Restart the application.


<span id=".6YCa6L-HU2t5V2Fsa2luZ-aOpeWFpQ=="></span>
## Integrate via SkyWalking

The SkyWalking Agent collects data and reports directly to the APMPlus server side. Currently, integration is supported for SkyWalking Trace, Meter, Log, JVM, and CLR data.

<span id="5nuDqDFl"></span>
### SDK direct reporting


1. Obtain the SkyWalking grpc reporting endpoint.

   ```sql
   skywalking.collector.backend_service=apmplus-{region}.ivolces.com:4317
   ```
   

2. Obtain the authentication user identifier.

   ```sql
   skywalking.agent.authentication={appkey}
   ```
   

3. Configure the application and turn on data reporting. For details, see [SkyWalking Documentation](https://skywalking.apache.org/docs/).

4. Restart the application.

5. Verify data reporting.

   * After trace integration, you can view the topology map, Trace Analysis, service details, and other data.

   * After meter integration, you can view data points in custom metrics.

   * After log integration, you can view the logs.

   * After JVM and CLR integration, you can view metrics such as "skywalking_jvm_\*" and "skywalking_clr_\*" in custom metrics.
