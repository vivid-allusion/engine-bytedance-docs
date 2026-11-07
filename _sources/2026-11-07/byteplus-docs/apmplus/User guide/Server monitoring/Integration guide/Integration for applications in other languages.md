---
title: "Integration for applications in other languages"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integration_of_applications_in_other_languages"
---

This article describes how to integrate applications developed in languages other than Java, Go, or Python with APMPlus using open\-source products.

<span id=".6YCa6L-HT3BlblRlbGVtZXRyeeaOpeWFpQ=="></span>
## Integrate via OpenTelemetry

OpenTelemetry is an observability project under CNCF, designed to provide standardized solutions in the observability domain. It addresses standardization issues for data models, collection, processing, export, and more for observability data, and offers services independent of third\-party vendors. After integrating with APMPlus, you will gain multiple APMPlus capabilities, including RED method generation, multidimensional trace search, single trace search, topology generation, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To isolate production and test data, see <a href="https://docs.byteplus.com/en/docs/apmplus/Isolate_production_and_test_data">Isolate production and test data</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
### Limits


* APMPlus uses Prometheus as the storage for OpenTelemetry metrics and supports querying metrics with PromQL. For specific use cases, see [custom dashboard](https://docs.byteplus.com/en/docs/apmplus/Custom_dashboard) and [alert management](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).

* There are certain limitations when converting OpenTelemetry metrics to Prometheus metrics:

   * As with the open\-source version, [ExponentialHistogram](https://opentelemetry.io/docs/reference/specification/metrics/data-model/#exponentialhistogram) is not supported.

   * Data with the aggregation method set to delta is not supported. Do not modify the default aggregation configuration on the SDK side. Ensure that the aggregation method for SDK\-side data is cumulative.

* Each workspace has independent data reporting credentials. To use a workspace for data management and data isolation, ensure that the `apmplus-opentelemetry-collector` component has been upgraded to version v3.1.0 or above.


<span id=".Q29sbGVjdG9y6YeH6ZuG"></span>
### Collector data collection

The SDK reports data to the Collector, and the Collector collects data and reports it to the APM server side.


1. Configure the application and turn on data reporting.

   1. Download OpenTelemetryJavaAgent.

      ```shell
      wget https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/latest/download/opentelemetry-javaagent.jar
      ```
      

   2. Modify the application start parameters, setting javaagent and otel.service.name. Example:

      ```java
      java -javaagent:<path/to/opentelemetry-javaagent.jar> \
           -Dotel.exporter.otlp.endpoint=<your-ot-collector-endpoint> \
           -Dotel.exporter.otlp.protocol=<your-ot-collector-protocol> \ 
           -Dotel.service.name=java-opentelemetry-otlp-instrumentation \
           -jar myapp.jar
      ```
      

2. Configure the collector and modify the reporting endpoint.

   Go to the integration center, select **Other \> OpenTelemetry \> Collector**, and obtain the following configuration. Identify your service region and network access method. The appkey is the user's unique identifier.

   ```YAML
   exporters:
     otlp:
       endpoint: apmplus-{region}.volces.com:4317
       compression: gzip
       headers:
           X-ByteAPM-AppKey: {appkey}
       tls:
           insecure: true
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Refer to the integration center for the complete configuration command. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the integration center?</a>.   </div>
   

3. Restart the application.


<span id=".U0RL6YeH6ZuG"></span>
### SDK data collection

The SDK collects data and reports it directly to the APM server side.


1. Configure the application and turn on data reporting.

   1. Download OpenTelemetryJavaAgent.

      ```shell
      wget https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/latest/download/opentelemetry-javaagent.jar
      ```
      

   2. Modify the application start parameters, setting javaagent and otel.service.name. Example:

      ```java
      java -javaagent:<path/to/opentelemetry-javaagent.jar> \
           -Dotel.exporter.otlp.endpoint=apmplus-grpc.volces.com:443 \
           -Dotel.exporter.otlp.headers=X-ByteAPM-AppKey={appkey} \
           -Dotel.exporter.otlp.protocol=grpc \ 
           -Dotel.service.name=java-opentelemetry-otlp-instrumentation \
           -jar myapp.jar
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Refer to the integration center for the complete configuration command. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the integration center?</a>.      </div>
      

2. Restart the application.


<span id=".6YCa6L-HUHJvbWV0aGV1c-aOpeWFpQ=="></span>
## Integrate via Prometheus

Prometheus is an open\-source Monitoring and alert system originally developed by SoundCloud. It is now an independent open\-source project and was added to CNCF in 2016, becoming CNCF's second project.

You can use Prometheus to meet custom instrumentation requirements. APMPlus has been customized based on OpenTelemetry's PrometheusReceiver, with data collectors for both K8s and Host Deployment. By installing the APMPlus data collector, you can collect PrometheusSDK instrumentation data and store it in APMPlus, which supports subsequent dashboard and alert needs.

<span id=".5a655Zmo6YOo572y"></span>
### Container Deployment

If your application is deployed on a Kubernetes cluster, see the following steps to install the APM data collector and connect to the APM server side.


1. Install APMPlus OpenTelemetryCollector.

   Go to the access center, select **Other \> Prometheus \> Container Deployment**, and obtain the following configuration. You need to distinguish your region and network access method. The appkey is the user's unique identifier.

   ```PowerShell
   kubectl apply -f "https://apmplus.volcbiz.com/server_warehouse/generate_assets/download/apmplus-opentelemetry-k8s/apmplus-opentelemetry-operator-v0.0.17.yaml?appkey={appkey}&promReplicas=1"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To view the complete installation command, go to the access center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the access center?</a>.   </div>
   

2. Configure the application and turn on data instrumentation.

3. In the K8S scenario, service discovery is supported via pod annotation.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   ...
   spec:
     ...
     template:
       metadata:
         annotations:
           prometheus.io/path: /metrics # your path
           prometheus.io/port: "30002"  # your port
           prometheus.io/scrape: "true"   
   ```
   

4. Restart the application.


<span id=".5Li75py66YOo572y"></span>
### Host Deployment

If your application is deployed on a virtual machine or physical machine, see the following steps to install the APMPlus data collector and connect to the APMPlus server side.


1. Install APMPlus OpenTelemetryCollector.

   Go to the access center, select **Other \> Prometheus \> Host Deployment**, and obtain the following configuration. You need to distinguish your region. The appkey is the user's unique identifier.

   * For installation via public network, sample code is as follows:

   ```PowerShell
   bash -c "$(curl -L 'https://apmplus-dl-{region}.volces.com/server_warehouse/generate_assets/download/apmplus-opentelemetry-ecs/install-otel_0.0.9.sh?appkey={appkey}&network=public')"
   ```
   

   * 若 installation via private network, sample code is as follows:

   ```PowerShell
   bash -c "$(curl -L 'http://apmplus-dl-{region}.ivolces.com/server_warehouse/generate_assets/download/apmplus-opentelemetry-ecs/install-otel_0.0.9.sh?appkey={appkey}&network=private')"
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To view the complete installation command, go to the access center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the access center?</a>.   </div>
   

2. Configure the application and turn on data instrumentation.

3. In the ECS scenario, service discovery is supported via file. The configuration file address is `/usr/local/apmplus-opentelemetry-collector/targets.json`.

   ```json
   [
     {
       "targets": [
         "localhost:8888"
       ]
     }
   ]
   ```
   

4. Restart the application.


<span id=".6YCa6L-HSmFlZ2Vy5o6l5YWl"></span>
## Access via Jaeger

Jaeger is an open\-source distributed tracing system developed by Uber.

For existing systems that have integrated Jaeger, you can report trace data from applications configured through Jaeger to APMPlus, enabling comprehensive end\-to\-end Monitoring capabilities. After integrating with APMPlus, you will gain RED metric generation, multidimensional trace search, single trace search, topology generation, and other APMPlus features.

<span id=".SmFlZ2VyQWdlbnTmjqXlhaU="></span>
### JaegerAgent integration

The SDK reports data to the Agent, and the Agent reports data to the APMPlus server.


1. Configure the application and enable data collection.

   Send trace data to the Agent via UDP. For details, see [jaeger Documentation](https://www.jaegertracing.io/docs/1.39/).

2. Configure the Agent and modify the reporting endpoint.

   1. Modify the jaeger\-agent startup parameters. The configuration example is as follows:

      ```bash
      ./jaeger-agent --reporter.grpc.host-port=apmplus-grpc.volces.com:443  \
          --reporter.grpc.tls.enabled=true \
          --agent.tags=app_key={appkey}
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For the complete configuration command, go to the integration center. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center">How to use the integration center?</a>.      </div>
      

3. Restart the application.


<span id="qCkavc8e"></span>
### SDK direct reporting

The SDK collects data and reports directly to the APMPlus server.


1. Configure the application and enable data collection.

   1. Obtain the Jaeger HTTP Thrift reporting endpoint.

      ```PowerShell
      https://apmplus-{region}.volces.com/server_collect/third_party/jaeger/v2/{appkey}/api/trace
      ```
      

2. Restart the application.


<span id=".6YCa6L-HWmlwa2lu5o6l5YWl"></span>
## Zipkin integration

Zipkin is an open\-source distributed tracing system developed by Twitter. Zipkin helps users collect trace data.

For existing systems that have integrated Zipkin, you can report trace data from applications configured through Zipkin to APMPlus, enabling comprehensive end\-to\-end Monitoring capabilities. After integrating with APMPlus, you will gain RED metric generation, multidimensional trace search, single trace search, topology generation, and other APMPlus features.

<span id="jz9yOHVu"></span>
### SDK direct reporting

The SDK collects data and reports directly to the APMPlus server.


1. Configure the application and enable data reporting.

   1. Obtain the Zipkin reporting endpoint.

      ```Plain
      https://apmplus-{region}.volces.com/server_collect/third_party/zipkin/v2/{appkey}/api/v2/spans
      ```
      

   2. Integrate the service and configure the reporting endpoint. For details, see [zipkin sample code](https://zipkin.io/pages/tracers_instrumentation.html).

2. Restart the application.


<span id=".6YCa6L-HU2t5V2Fsa2luZ-aOpeWFpQ=="></span>
## SkyWalking integration

The SkyWalking Agent collects data and reports directly to the APMPlus server. Currently, SkyWalking Trace, Meter, Log, JVM, and CLR data ingestion are supported.

<span id="Ac2cvQFB"></span>
### SDK direct reporting


1. Obtain the SkyWalking gRPC reporting endpoint.

   ```sql
   skywalking.collector.backend_service=apmplus-{region}.ivolces.com:4317
   ```
   

2. Obtain the authentication user identifier.

   ```sql
   skywalking.agent.authentication={appkey}
   ```
   

3. Configure the application and enable data reporting. For details, see [SkyWalking Documentation](https://skywalking.apache.org/docs/).

4. Restart the application.

5. Verify data reporting.

   * After trace integration, you can view the topology map, trace analysis, service details, and other data.

   * After meter integration, you can view custom metrics.

   * After log integration, you can view logs.

   * After integrating JVM and CLR, you can view metrics such as "skywalking_jvm_\*" and "skywalking_clr_\*" in custom metrics.
