---
title: "Java application integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Java_application_integration"
---

Java applications have different integration Methods in different scenarios. This article describes detailed integration Actions for Java applications in various scenarios. After integration, you can automatically collect trace information, automatically generate metric, as well as perform trace search, log search, and other features.

<span id="421b1f78"></span>
## Integration via OpenTelemetry (recommended)

OpenTelemetry is an observability project under CNCF, designed to provide standardized solutions in the observability field. It addresses the standardization of data models, collection, processing, and export of observability data, and offers services independent of third\-party vendors.

If your application has already integrated the OpenTelemetry SDK, the APMPlus server side can receive data reported by OpenTelemetry. After integrating with APMPlus, you will gain capabilities such as RED metric generation, multidimensional trace search, single trace search, topology generation, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To isolate production and test data, see <a href="https://docs.byteplus.com/en/docs/apmplus/Isolate_production_and_test_data">Isolate production and test data</a>.</div>


<span id="b90ec799"></span>
### Limits


* There are certain limits when converting OpenTelemetry Metrics to Prometheus Metrics:

   * As with [open source](https://opentelemetry.io/docs/reference/specification/compatibility/prometheus_and_openmetrics/#dropped-data-points), [ExponentialHistogram](https://opentelemetry.io/docs/reference/specification/metrics/data-model/#exponentialhistogram) is not supported.

   * Data with aggregation method set to delta is not supported. Do not modify the default aggregation configuration on the SDK side. Ensure that the aggregation method on the SDK side is cumulative.

* Each workspace has its own data reporting credentials. To manage and isolate data using workspaces, ensure that the `apmplus-opentelemetry-collector` component has been upgraded to version v3.1.0 or above.


<span id="68a86b17"></span>
### Data reporting

<span id="5de05da1"></span>
#### Method 1: Report directly to the ApmPlus server side

Observable data is reported directly to the ApmPlus server side, supporting data reporting via grpc, http/protobuf, and other Methods.

<span id="290be053"></span>
#### Method 2: Otel Collector forwarding

APMPlusOpenTelemetryCollector is a data collector developed by APMPlus based on OpenTelemetryCollector. You can install the Opentelemetry Collector in the cluster for data forwarding. There are two installation Methods:


* Install the apmplus\-opentelemetry\-collector component via the VKE cluster component center using the graphical installation interface. In addition, it is recommended to install the apmplus\-server\-agent component at the same time to enable metric data collection at the host and process levels.

* Manually install using the script provided on the service integration page.


<span id="6b266739"></span>
### Data Integration

<span id="0e173ae9"></span>
#### Method 1: SDK integration

To report data using manual instrumentation with the community\-provided Opentelemetry Java SDK, refer to the community's [java demo](https://github.com/open-telemetry/opentelemetry-java-examples?tab=readme-ov-file#java-opentelemetry-examples). After building the Java project, specify the backend for data reporting and authentication parameters in the start command:


* To report data directly to the ApmPlus server side:

   ```Shell
   java -jar myapp.jar \
   -Dotel.exporter.otlp.endpoint=<Apmplus_endpoint> \
   -Dotel.service.name=myapp \
   -Dotel.exporter.otlp.protocol=<protocol> \
   -Dotel.exporter.otlp.headers=X-ByteAPM-AppKey=<app_key>
   ```
   

* To report data to Collector, otel.exporter.otlp.headers does not need to be specified.

   ```Shell
   java -jar myapp.jar \
   -Dotel.exporter.otlp.endpoint=<collector_endpoint> \
   -Dotel.service.name=myapp \
   -Dotel.exporter.otlp.protocol=<protocol>
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><service_name\> Enter the application service name.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enter the server side address for your environment.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><app_key\> Enter the app_key provided by the service access console. The app_key for each workspace is different. To obtain it, see: <a href="https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication">How to obtain the authentication information AppKey for performance monitoring?</a>.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enter the protocol used for data reporting. grpc and http/protobuf are supported.   </div>
   

<span id="56f4c1a7"></span>
#### Method 2: Probe integration

The Opentelemetry javaagent uses JVM bytecode enhancement technology to enable collection and automatic reporting of otel data for various popular [Java frameworks](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md). There are two specific usage methods:


1. Manual download of Javaagent

   The service access page provides the latest download method for Javaagent. Modify the start command when starting the application to inject the Javaagent:

   * To report data directly to the ApmPlus server side:

      ```Shell
      java -javaagent:/path/to/opentelemetry-javaagent.jar \
      -Dotel.exporter.otlp.endpoint=<Apmplus_endpoint> \
      -Dotel.service.name=myapp \
      -Dotel.exporter.otlp.protocol=<protocol> \
      -Dotel.exporter.otlp.headers=X-ByteAPM-AppKey=<app_key> \
      -jar myapp.jar
      ```
      

   * To report data to Collector, otel.exporter.otlp.headers does not need to be specified.

      ```Shell
      java -javaagent:/path/to/opentelemetry-javaagent.jar \
      -Dotel.exporter.otlp.endpoint=<collector_endpoint> \
      -Dotel.service.name=myapp \
      -Dotel.exporter.otlp.protocol=<protocol> \
      -jar myapp.jar
      ```
      

2. Automatic injection via Opentelemetry Operator

   In k8s scenarios, Operator\-based automatic injection of Javaagent into business POD containers is provided. You need to deploy the apmplus\-opentelemetry\-collector component in the cluster component center in advance.

   After deployment, modify the business workload (currently supports deployment and statefulset) to add the `instrumentation.apmplus.volcengine.com/inject-java` and `instrumentation.apmplus.volcengine.com/workspace` annotations.

   Method 1: Manual modification example:


```YAML
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
        instrumentation.apmplus.volcengine.com/inject-java: 'true' # Turn on APMPlus observation injection
        instrumentation.apmplus.volcengine.com/workspace: default  Specify the workspace for the service
    spec:
      containers:
      - name: simple-java
        image: java_demo_simple
        imagePullPolicy: Always
        env:
        - name: CONTAINER_RUNTIME
          value: "k8s"
```


Method 2: vke blank screen modification example, update the workload

After modification, restart the business POD.

<span id=".6YCa6L-HSmFlZ2Vy5o6l5YWl"></span>
## Integration via Jaeger

Jaeger is an open\-source distributed tracing system developed by Uber.

For existing systems already integrated with Jaeger, Jaeger trace data can be reported to APMPlus to achieve comprehensive trace monitoring capabilities.

After integrating with APMPlus, you will gain capabilities such as RED metric generation, multidimensional trace search, single trace search, topology generation, and more.

<span id=".SmFlZ2VyQWdlbnTmjqXlhaU="></span>
### JaegerAgent integration

The SDK reports data to the Agent, and the Agent reports data to the APMPlus server side.


1. Configure the application and enable data collection.

   Refer to the Jaeger documentation to send trace data to the Agent via UDP.

2. Configure the Agent and modify the reporting endpoint.

   1. Modify the jaeger\-agent start parameters. The configuration is as follows:

      ```bash
      ./jaeger-agent --reporter.grpc.host-port=apmplus-{region}.ivolces.com:4317 \ 
      --reporter.grpc.tls.enabled=false \ 
      --agent.tags=app_key={appkey}
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For the complete configuration command, view it in the Access Center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the Access Center?</a>.      </div>
      

3. Restart the application.


<span id=".U0RL55u05o6l5LiK5oql"></span>
### SDK direct reporting

The SDK performs data collection and reports directly to the APMPlus server side.


1. Configure the application and turn on data collection.

   * The following is sample code for configuring the reporter via the public network:

      ```Java
      io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration(); 
      sender.withEndpoint("https://apmplus-{region}.volces.com/server_collect/third_party/jaeger/v2/{appkey}/api/trace")
      ```
      

   * Sample code for configuring the reporter via the private network is as follows:

      ```Java
      io.jaegertracing.Configuration.SenderConfiguration sender = new io.jaegertracing.Configuration.SenderConfiguration(); 
      sender.withEndpoint("http://apmplus-{region}.ivolces.com/server_collect/third_party/jaeger/v2/{appkey}/api/trace")
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For the complete configuration command, view it in the Access Center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the Access Center?</a>.      </div>
      

2. Restart the application.


<span id=".6YCa6L-HWmlwa2lu5o6l5YWl"></span>
## Integration via Zipkin

Zipkin is an open\-source distributed tracing system from Twitter. Zipkin helps you collect trace data.

For systems that have already integrated Zipkin, existing trace data can be reported to APMPlus to achieve comprehensive full\-link monitoring capability.

After integrating with APMPlus, you will gain RED method generation, multidimensional trace search, single trace search, topology map generation, and many other APMPlus capabilities.

<span id="WBCTbdLC"></span>
### SDK direct reporting

The SDK performs data collection and reports directly to the APMPlus server side.


1. Configure the application and turn on data reporting.

   * The following is an example for obtaining the zipkin reporting endpoint via the public network.

      ```Bash
      https://apmplus-{region}.volces.com/server_collect/third_party/zipkin/v2/{appkey}/api/v2/spans
      ```
      

   * The following is an example for obtaining the zipkin reporting endpoint via the private network.

      ```Plain Text
      http://apmplus-{region}.ivolces.com/server_collect/third_party/zipkin/v2/{appkey}/api/v2/spans
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For the complete configuration command, view it in the Access Center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the Access Center?</a>.      </div>
      

2. Integrate the service and configure the reporting endpoint. For specifics, see [zipkin sample code](https://github.com/openzipkin/brave).

3. Restart the application.


<span id=".6YCa6L-HU2t5V2Fsa2luZ-aOpeWFpQ=="></span>
## Integration via SkyWalking

SkyWalking Agent performs data collection and reports directly to the APMPlus server side. Currently, integration of SkyWalking Trace, Meter, Log, JVM, and CLR data is supported.

<span id="6VAlKv5o"></span>
### SDK direct reporting


1. Configure the application and turn on data reporting.

   1. Configure the SkyWalking grpc reporting endpoint, set the authentication user identifier, and specify the service name. For specifics, see [SkyWalking Documentation](https://skywalking.apache.org/docs/skywalking-java/latest/readme/).

   2. Run the following command to start the service and SkyWalking Agent.

      ```sql
      java -javaagent:path/to/skywalking-agent.jar
          -Dskywalking.collector.backend_service=apmplus-{region}.ivolces.com:4317
          -Dskywalking.agent.authentication={appkey}
          -Dskywalking.agent.service_name={YOUR_SERVICE_NAME}
          -jar YOUR_SERVICE.jar
      ```
      

2. Restart the application.

3. Verify data reporting.

   * After trace integration, you can view the topology map, Trace Analysis, service details, and other data.

   * After meter integration, you can view data points among custom metrics.

   * After log integration, you can view logs.

   * After JVM and CLR integration, you can view metrics such as "skywalking_jvm_\*" and "skywalking_clr_\*" among custom metrics.
