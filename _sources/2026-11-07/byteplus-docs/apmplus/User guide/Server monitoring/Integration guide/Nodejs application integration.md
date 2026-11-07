---
title: "Nodejs application integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_a_Nodejs_application"
---

Nodejs applications have different integration methods depending on the scenario. This article describes the detailed steps for integrating Nodejs applications with OpenTelemetry. After integration, you can automatically collect trace information, automatically generate metrics, and use features such as trace search, log search, and more.

<span id=".6YCa6L-HT3BlblRlbGVtZXRyeeaOpeWFpQ=="></span>
## Integrate via OpenTelemetry

OpenTelemetry is an observability project under CNCF that aims to provide standardized solutions in the observability domain. It addresses the standardization of data models, collection, processing, and export of observability data, and offers services independent of third\-party vendors.

If your application has already integrated the OpenTelemetry SDK, the APMPlus server side can receive data reported by OpenTelemetry. After integrating with APMPlus, you will gain capabilities such as RED metric generation, multidimensional trace search, single trace search, topology generation, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To isolate production and test data, see <a href="https://docs.byteplus.com/en/docs/apmplus/Isolate_production_and_test_data">Isolate production and test data</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
### Limits


* APMPlus uses Prometheus as the storage for OpenTelemetry metrics and supports querying metrics using PromQL. For specific applications, see [custom dashboard](https://docs.byteplus.com/en/docs/apmplus/Custom_dashboard) and [alert management](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).

* There are certain restrictions when converting OpenTelemetry metrics to Prometheus metrics:

   * As with [open source](https://opentelemetry.io/docs/reference/specification/compatibility/prometheus_and_openmetrics/#dropped-data-points), [ExponentialHistogram](https://opentelemetry.io/docs/reference/specification/metrics/data-model/#exponentialhistogram) is not supported.

   * Data with the aggregation method set to delta is not supported. Do not modify the default aggregation configuration on the SDK side. Ensure that the aggregation method for SDK\-side data is cumulative.

* Each workspace has its own data reporting credentials. To manage and isolate data using workspaces, ensure that the `apmplus-opentelemetry-collector` component has been upgraded to version v3.1.0 or above.


<span id=".6Ieq5Yqo5o6l5YWl"></span>
### Automatic integration

APMPlus OpenTelemetry Collector is a data collector developed by APMPlus based on OpenTelemetry Collector. It complies with the Apache 2.0 license, supports the collection of OpenTelemetry monitoring data, and also supports the collection of Prometheus metrics, application monitoring data, and K8s resource metrics.


1. Install APM OpenTelemetry Collector.

   Use the VKE cluster component center to perform blank screen installation of the apmplus\-opentelemetry\-collector component. Go to the VKE cluster interface, select **Component Management \-\> Monitoring**, and click the Install button in the upper right corner of the apmplus\-opentelemetry\-collector component under `...` to complete the deployment and management of Apmplus OpenTelemetry Collector.

2. Add the `instrumentation.apmplus.volcengine.com/inject-nodejs` and `instrumentation.apmplus.volcengine.com/workspace` annotations to the k8s deployment configuration of the service.

   The VKE blank screen configuration is shown below:

   The code example is as follows:

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: node-demo
     labels:
       app: node-demo
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: node-demo
     template:
       metadata:
         labels:
           app: node-demo
         annotations:
           instrumentation.apmplus.volcengine.com/inject-nodejs: 'true' # Turn on APMPlus observation injection
           instrumentation.apmplus.volcengine.com/workspace: default  # Specify the workspace to which the service belongs
       spec:
         containers:
           - name: node-demo
             image: node-demo:latest
             imagePullPolicy: Always
             env:
               - name: CONTAINER_RUNTIME
                 value: "k8s"
   ```
   

3. Restart the application.

&nbsp;


<span id="neO5nOXm"></span>
### OpenTelemetry SDK integration

Use the automatic instrumentation method provided by the community Opentelemetry Node.js SDK to report data. For details, see the community\-provided [integration documentation](https://opentelemetry.io/docs/languages/js/).

<span id="4FmJHuGR"></span>
#### Report data using Opentelemetry automatic instrumentation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For related information in the official Opentelemetry Node.js documentation, see: <a href="https://opentelemetry.io/docs/languages/js/getting-started/nodejs/">getting\-started</a>.</div>



1. Install dependencies.


```Bash
npm install --save @opentelemetry/api
npm install --save @opentelemetry/auto-instrumentations-node
```



2. Set environment variables and load the instrumentation script using the NODE_OPTIONS and \-\-require mechanisms.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The app_key for each workspace is different. To obtain it, see: <a href="https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication">How to obtain the AppKey for application performance monitor authentication information?</a>.</div>


```Bash
# Enter your-app-key as the App key displayed in the APMPlus platform access center. Enter your-service-name as the desired service name.
# Adjust OTEL_EXPORTER_OTLP_ENDPOINT according to the access region.
# If accessed via the public network, use http://apmplus-cn-beijing.volces.com:4317 for OTEL_EXPORTER_OTLP_ENDPOINT.
export OTEL_TRACES_EXPORTER="otlp"
export OTEL_METRICS_EXPORTER="otlp"
export OTEL_LOGS_EXPORTER="otlp"
export OTEL_EXPORTER_OTLP_PROTOCOL="grpc"
export OTEL_EXPORTER_OTLP_ENDPOINT="http://apmplus-cn-beijing.ivolces.com:4317" 
export OTEL_EXPORTER_OTLP_HEADERS=X-ByteAPM-AppKey="your-app-key"
export OTEL_SERVICE_NAME="your-service-name"
export OTEL_NODE_RESOURCE_DETECTORS="env,host,os"
export OTEL_PROPAGATORS="tracecontext,baggage"
export OTEL_METRIC_EXPORT_INTERVAL=30000 
export NODE_OPTIONS="--require @opentelemetry/auto-instrumentations-node/register"
node app.js
```
