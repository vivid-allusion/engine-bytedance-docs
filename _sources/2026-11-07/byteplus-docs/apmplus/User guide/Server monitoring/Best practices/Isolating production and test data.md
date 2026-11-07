---
title: "Isolating production and test data"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Isolate_production_and_test_data"
---

If you use a root account to manage both production and test data, you can follow the steps below to isolate them, making it easier to distinguish monitoring metric changes between production and test data.

<span id="adb383d2"></span>
## Considerations


* Only services integrated via OpenTelemetry support isolating production and test data.

* Only services using automatic data collection methods support isolating production and test data.


<span id="b3d35adc"></span>
## Integrate services via OpenTelemetry

OpenTelemetry is a CNCF observability project that aims to provide a standard solution. It addresses the standardization of data models, collection, processing, and export, offering vendor\-agnostic services.

If your application has already integrated the OpenTelemetry SDK, the APMPlus server can receive data reported via OpenTelemetry. After integrating with APMPlus, you will gain capabilities such as RED metric generation, multi\-dimensional trace search, single trace search, and topology generation.

<span id="bf0fe71c"></span>
### Limits


* APMPlus uses Prometheus as the storage backend for OpenTelemetry metrics and supports PromQL queries. For specific applications, see [Custom dashboards](https://docs.byteplus.com/en/docs/apmplus/Custom_dashboard) and [Alert management](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).

* There are certain limitations when converting OpenTelemetry metrics to Prometheus metrics:

   * Same as [open source](https://opentelemetry.io/docs/reference/specification/compatibility/prometheus_and_openmetrics/#dropped-data-points), [ExponentialHistogram](https://opentelemetry.io/docs/reference/specification/metrics/data-model/#exponentialhistogram) is not supported.

   * Data with delta aggregation is not supported. Do not modify the default aggregation configuration on the SDK side. Ensure that the aggregation method on the SDK side is set to cumulative.


<span id="b2e05062"></span>
### Distinguish by annotation


1. Log in to the VKE console, go to the **Addons** page, and ensure that the `apmplus-opentelemetry-collector` add\-on has been upgraded to version 2.0.2 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on), [Add-on update log](https://docs.byteplus.com/en/docs/apmplus/apmplus-opentelemetry-collector_component_release_notes).

2. Add the specified annotation to the service's Kubernetes deployment configuration to distinguish data by annotation.



|Annotation |Description |
|---|---|
|instrumentation.apmplus.volcengine.com/inject\-java |It is used to determine whether to enable automatic javaagent injection.<br><br><br>* true: enabled.<br><br>* false: disabled. |
|apmplus.volcengine.com/env |Inject user\-defined environment information. When querying the service list on the APMPlus platform later, you can switch based on the user\-specified env. |
|apmplus.volcengine.com/service.name |It is used to specify the service name of the current service. When manually configuring, we recommend including env characteristics. The system requires that service names be unique and does not allow the same service name to be associated with different envs. |



Sample code:

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: simple-java
     labels:
       app: simple-java
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: simple-java
     template:
       metadata:
         labels:
           app: simple-java
         annotations:
           instrumentation.apmplus.volcengine.com/inject-java: 'true'
           apmplus.volcengine.com/env: 'test'
           apmplus.volcengine.com/service.name: 'simple-java-test'
       spec:
         containers:
         - name: simple-java
           image: java_demo_simple
           imagePullPolicy: Always
           env:
           - name: CONTAINER_RUNTIME
             value: "k8s"
   ```
   

3. Restart the application.


<span id="ea10fbe3"></span>
### Verify data

<span id="0a7e0282"></span>
### View service list


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Select an available region.

3. In the service list, select env to check whether the integrated services can be found under the selected envs.


<span id="880aad4d"></span>
### View service topology


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Select an available region.

3. In the upper\-left corner, select **Service monitoring** \> **Service topology**.

4. On the "Service topology" page, select env to check whether the topology under the selected env is correct.
