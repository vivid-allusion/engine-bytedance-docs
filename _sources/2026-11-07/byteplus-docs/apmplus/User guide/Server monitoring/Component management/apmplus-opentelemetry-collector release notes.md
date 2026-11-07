---
title: "apmplus-opentelemetry-collector release notes"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/apmplus-opentelemetry-collector_component_release_notes"
---

The apmplus\-opentelemetry\-collector component automates the deployment and management of the OpenTelemetry collector. It supports automatic agent injection for Java, Python, and other applications, enabling the collection, processing, and export of logs, traces, and metric data using the OpenTelemetry protocol. This topic provides the release notes for the apmplus\-opentelemetry\-collector.

<span id="FXAaPIzq"></span>
## July 2026


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.2.1 |Cluster version ≥ v1.24\-0 |Maintained |* The collector health probe is optimized for detection reliability. The timeout is reduced from 10 seconds to 3 seconds.<br><br>* The installation and readiness check process is optimized by switching to an asynchronous, non\-blocking mode. This resolves Helm operation timeouts on the VKE control plane and installation failures caused by slow cluster synchronization, improving the installation success rate.<br><br>* EndpointSlice RBAC permissions are added. The collector endpoint discovery mechanism is switched to EndpointSlice. |None |
|v3.2.0 |Cluster version ≥ v1.24\-0 |Maintained |* Profile collection is supported. You can enable continuous profiling in the console based on your requirements.<br><br>* Pod injection for higher Kubernetes versions is supported. ||


<span id="Ud4P79Jg"></span>
## June 2026


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.1.1 |Cluster version ≥ v1.24\-0 |Maintained |* The component uninstallation process is optimized. Before uninstallation, the component checks for CRDs.<br><br>* The component self\-monitoring capability is enhanced to facilitate troubleshooting.<br><br>* The `cluster_id` label will be uniformly added to user\-reported observability data for easier data management. |None |


<span id="2YZjPhvu"></span>
## May 2026


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.1.0 |Cluster version ≥ v1.24\-0 |Maintained |Add the workspace feature. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. |None |


<span id="Uf0Ukr2h"></span>
## March 2026


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.0.3 |Cluster version ≥ v1.24\-0 |Maintained |* The component kernel version is upgraded to `o11yagent_cloud@v1.4.2`.<br><br>* Custom spans can be converted to metrics.<br><br>* gzip compression is enabled for Otel gRPC Input.<br><br>* lz4 compression is enabled for metrics reporting by default.<br><br>* Java Agent is upgraded to v1.2.0. The url label is added to the database connection pool metrics. |None |


<span id="yknLdcto"></span>
## January 2026


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v3.0.2 |Cluster version ≥ v1.24\-0 |Maintained |* The component kernel version is upgraded to `o11yagent_cloud@v1.4.0`.<br><br>* Custom logs can be converted to metrics.<br><br>* Span sampling is supported. Sampling rules and rates can be delivered via the Sever\-side Monitoring platform. Probabilistic sampling and slow/error sampling are supported.<br><br>* You can modify data labels and filter labels via rules delivered by the Server\-side Monitoring platform.<br><br>* `SpanToMetrics R.E.D` statistics are added.<br><br>* HPA is supported, with the default set to n and n+2 nodes.<br><br>* The instrumentation image tags have been upgraded. Java Agent is upgraded to v1.1.0. Python Agent is upgraded to v1.1.15. NodeJs Agent is upgraded to v1.0.0. |None |


<span id="KeWekUZf"></span>
## June 2025


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v2.0.3 |Cluster version ≥ v1.24\-0 |Maintained |* The Python auto\-injection base image is upgraded to v1.1.5.<br><br>* The NodeJS auto\-injection base image is upgraded to v1.0.0.<br><br>* The Java auto\-injection base image is upgraded to v2.7.1.<br><br>   * Connection pool monitoring is supported: Jedis [\>=4.0.0] or lettuce [\>=5.0.0]<br><br>   * Thread pool monitoring is supported: Dubbo [\>=2.7], okhttp3 [\>=3.0], or tomcat [\>=7.0.4]<br><br>* The collector has been upgraded:<br><br>   * Span baggage entries can be converted to attributes.<br><br>   * The grpc keepalive attribute is added to address long\-term uneven load distribution for persistent gRPC connections.<br><br>   * The VKE authentication add\-on is upgraded. |None |


<span id="b1b65f82"></span>
## March 2025


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v2.0.2 |Cluster version ≥ v1.24\-0 |Maintained |* The Javaagent base image has been modified to reduce Javaagent image size.<br><br>* The Python auto\-injection base image is upgraded to v1.1.0.<br><br>* The annotations can be added to Operator:<br><br>   * apmplus.volcengine.com/env: Injects the env attribute.<br><br>   * apmplus.volcengine.com/service.name: Injects the service name. The annotation has lower priority than the OTEL_SERVICE_NAME environment variable.<br><br>* The \-\-enable\-multi\-instrumentation startup parameter for Operator has been added to support automatic injection for multiple containers.<br><br>* The spanmetricsconnector processor is added to the Collector to support custom rules for converting span data into metrics.<br><br>* The chart feature is updated to support security orchestration\-specific nodeAffinity and tolerations. |None |


<span id="b1b65f82"></span>
## December 2024


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v2.0.1 |Cluster version ≥ v1.24\-0 |Maintained |* The automatic injection of the service.name attribute by the Operator has been optimized. |None |


<span id="054639e0"></span>
## September 2024


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v2.0.0 |Cluster version ≥ v1.24\-0 |EOM |* RBAC permissions are adjusted.<br><br>* Exporting to TLS over OLTP is supported. |None |


<span id="a746d1d8"></span>
## June 2024


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.1.3 |Cluster version ≥ v1.20\-0 |EOM |*  Automatic authentication for BytePlus VKE is supported.<br><br>* Automatic injection for Java and Python is supported.<br><br>* The following capabilities are supported: Collection, processing, and export of logs, traces, and metrics based on the OTLP protocol. |None |
