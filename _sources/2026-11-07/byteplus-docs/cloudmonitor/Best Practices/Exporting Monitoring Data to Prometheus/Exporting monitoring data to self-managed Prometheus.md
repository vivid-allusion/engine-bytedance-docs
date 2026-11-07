---
title: "Exporting monitoring data to self-managed Prometheus"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Export_monitoring_data_to_self-managed_Prometheus"
---

If you have a complete on\-premises enterprise management system, you can use the monitoring data export tool Exporter provided by Cloud Monitor to export cloud data to your on\-premises system in real time for centralized monitoring, and continuously write the data to Prometheus.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature is in public beta and is temporarily available for free. To use this feature, enable pay\-as\-you\-go first and then contact your account manager.</div>


<span id="OhDWhdFo"></span>
## Background

You can export monitoring data to self\-managed Prometheus by using two methods: Scrape and Remote Write, which have significant differences in architecture, data flow, and applicable scenarios.


|**Comparison dimension** |**Scrape** |**Remote Write** |
|---|---|---|
|Data flow |Pull mode. In this mode, the Prometheus server actively initiates metric requests to the monitoring target. |Push mode. In this mode, the collection client actively pushes metric data to the remote Prometheus server. |
|Suitable cluster scale |Suitable for small to medium clusters with a small number of nodes |Suitable for medium to large or ultra\-large clusters with a large number of nodes |
|Typical application scenario |* Non\-isolated internal network environments with the same network segment<br><br>* Monitoring of physical servers and long\-running business services<br><br>* Scenarios with minimal architecture and no scale\-out requirements<br><br>* Scenarios that require fast local query and real\-time alerting |* Cross\-data center, cross\-network segment, and multi\-cloud isolated network environments<br><br>* Large\-scale Kubernetes container clusters<br><br>* Short\-lived containers and temporary task monitoring<br><br>* Scenarios requiring centralized aggregation of monitoring data from multiple regions |


<span id="Z1JnlE0R"></span>
## Prerequisites

You have obtained the AK and SK with the `CloudMonitorReadOnlyAccess` permission on Cloud Monitor. They are used when the Exporter is running. 

<span id="gnXdQAgK"></span>
## Limits


* The Exporter can only be used to export data of the Gauge type.

* Exporter v1.4.0 and later can export data by using Remote Write.

* The Exporter obtains monitoring data by calling the `GetMetricData` API, which uses the API quota. If the quota is exceeded, metric retrieval will be restricted.

* If you need to retrieve a large number of metrics and objects, rate limits may cause data retrieval failures. We recommend that you distribute requests evenly based on the time dimension.


<span id="NrTGlqxE"></span>
## Procedure

The Exporter retrieves Cloud Monitor metric data by using APIs and exports metrics by using the Prometheus protocol. You can configure Prometheus collection tasks for data collection.


<Tabs>
<Tab zoneid="uW9MlP8Q" title="Method 1: Export data via Remote Write">
<TabTitle>Method 1: Export data via Remote Write</TabTitle>

<span id="3zlyYVz8"></span>
### Step 1: Enable the Remote Write feature


1. Open the out\-of\-order writing window.

   ```YAML
   storage:
     tsdb:
       out_of_order_time_window: 10m
   ```
   

2. Enable the Remote Write feature of Prometheus.

   ```YAML
    # Add the --web.enable-remote-write-receiver parameter to Prometheus startup parameters.
   ./prometheus --web.enable-remote-write-receiver
   ```
   


<span id="265eti1f"></span>
### Step 2: Install the Exporter


<Tabs>
<Tab zoneid="OWMjYkiC3s" title="Install Exporter on Kubernetes">
<TabTitle>Install Exporter on Kubernetes</TabTitle>

1. Add parameters in a Kubernetes cluster.


```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: cloud-monitor-exporter-conf
data:
  conf.yaml: |
    Credentials:
      AccessKey: "********"
      SecretKey: "********"
    Region: "cn-beijing"
    ServiceName: cloudmonitor
    Host: cloudmonitor.cn-beijing.byteplusapi.com.cn
    MaxRetries: 3
    BatchInstanceCount: 50
    DataQueueSize: 100
    DataConcurrency: 10
    MetaFreshIntervalSeconds: 60
    DataFreshIntervalSeconds: 60
    Limiter:
      LimitQPSGetMetricData: 9
      LimitQPSMonitorObjectList: 9
    BehaviorWhenPullTimeout: SkipMissExecute
    StatisticsType: "LAST"
    Products:
      - Namespace: "VCM_Kafka"
      - Namespace: "VCM_ECS"
    RemoteWrites:
     - Name: "my-prometheus"
       EndPoint: "https://prometheus.example.com/api/v1/write"
       Username: "admin"
       Password: "${PROMETHEUS_PASSWORD}"
       MaxWaitTime: "10s"
       HTTPWriteConcurrency: 16
       RetryCount: 3
       GlobalLabel:
         cluster: "production"
         region: "beijing"
       Scope:
         - self-metric
         - cloud-monitor
```



2. Configure the YAML file based on your business requirement and then install Exporter in your Kubernetes cluster.


```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cloud-monitor-exporter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cloud-monitor-exporter
  template:
    metadata:
      labels:
        app: cloud-monitor-exporter
      annotations:
        prometheus.io/scrape: "true"
        prometheus.io/port: "9898"
    spec:
      containers:
      - name: cloud-monitor-exporter
        image: cloud-monitor-cn-beijing.cr.volces.com/cm/cloud-monitor-exporter:v1.2.0
        args:
          - "--config=/conf/conf.yaml"
          - "--port=9898"
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 9898
        volumeMounts:
          - name: conf
            mountPath: /conf
      volumes:
        - name: conf
          configMap:
            name: cloud-monitor-exporter-conf
```



</Tab>
<Tab zoneid="qX9OSQwOSH" title="Install Exporter on Docker">
<TabTitle>Install Exporter on Docker</TabTitle>

1. Create the `config.yaml` file and modify it based on your business requirements.


```YAML
Credentials:
  AccessKey: "********"
  SecretKey: "********"
Region: "cn-beijing"
ServiceName: cloudmonitor
Host: cloudmonitor.cn-beijing.byteplusapi.com.cn
MaxRetries: 3
BatchInstanceCount: 50
DataQueueSize: 100
DataConcurrency: 10
MetaFreshIntervalSeconds: 60
DataFreshIntervalSeconds: 60
Limiter:
  LimitQPSGetMetricData: 9
  LimitQPSMonitorObjectList: 9
BehaviorWhenPullTimeout: SkipMissExecute
StatisticsType: "LAST"
Products:
  - Namespace: "VCM_Kafka"
  - Namespace: "VCM_ECS"
RemoteWrites:
 - Name: "my-prometheus"
   EndPoint: "https://prometheus.example.com/api/v1/write"
   Username: "admin"
   Password: "${PROMETHEUS_PASSWORD}"
   MaxWaitTime: "10s"
   HTTPWriteConcurrency: 16
   RetryCount: 3
   GlobalLabel:
     cluster: "production"
     region: "beijing"
   Scope:
     - self-metric
     - cloud-monitor
```



2. In the directory where the configuration file is located, run the following command to start the Docker image.


```Bash
docker run -itd -p 9898:9898 -v $(pwd)/config.yaml:/conf/conf.yaml cloud-monitor-cn-beijing.cr.volces.com/cm/cloud-monitor-exporter:v1.2.0 --config /conf/conf.yaml --port=9898
```





</Tab>
<Tab zoneid="mCxYUOpJ5S" title="Install Exporter on the virtual machine">
<TabTitle>Install Exporter on the virtual machine</TabTitle>

1. Download the binary artifact, extract it, and access the artifact directory. For the latest binary artifact, see [Exporter change log](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_update_log).

2. In the artifact directory, create the `config.yaml` file and modify it based on your business requirements.


```YAML
Credentials:
  AccessKey: "********"
  SecretKey: "********"
Region: "cn-beijing"
ServiceName: cloudmonitor
Host: cloudmonitor.cn-beijing.byteplusapi.com.cn
MaxRetries: 3
BatchInstanceCount: 50
DataQueueSize: 100
DataConcurrency: 10
MetaFreshIntervalSeconds: 60
DataFreshIntervalSeconds: 60
Limiter:
  LimitQPSGetMetricData: 9
  LimitQPSMonitorObjectList: 9
BehaviorWhenPullTimeout: SkipMissExecute
StatisticsType: "LAST"
Products:
  - Namespace: "VCM_Kafka"
  - Namespace: "VCM_ECS"
RemoteWrites:
 - Name: "my-prometheus"
   EndPoint: "https://prometheus.example.com/api/v1/write"
   Username: "admin"
   Password: "${PROMETHEUS_PASSWORD}"
   MaxWaitTime: "10s"
   HTTPWriteConcurrency: 16
   RetryCount: 3
   GlobalLabel:
     cluster: "production"
     region: "beijing"
   Scope:
     - self-metric
     - cloud-monitor
```



3. In the artifact directory, run the following command to start the Exporter.


```YAML
./exporter --config config.yaml --port=9898
```





</Tab>
</Tabs>



</Tab>
<Tab zoneid="FSYCGUHtOj" title="Method 2: Export data via Scrape">
<TabTitle>Method 2: Export data via Scrape</TabTitle>

<span id="kXhKAvIg"></span>
### Step 1: Install the Exporter


<Tabs>
<Tab zoneid="xB9Wr0nCdT" title="Install Exporter on Kubernetes">
<TabTitle>Install Exporter on Kubernetes</TabTitle>

1. Add parameters in a Kubernetes cluster.


```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: cloud-monitor-exporter-conf
data:
  conf.yaml: |
    Credentials:
      AccessKey: "********"
      SecretKey: "********"
    Region: "cn-beijing"
    ServiceName: cloudmonitor
    Host: cloudmonitor.cn-beijing.byteplusapi.com.cn
    MaxRetries: 3
    BatchInstanceCount: 50
    DataQueueSize: 100
    DataConcurrency: 10
    MetaFreshIntervalSeconds: 60
    DataFreshIntervalSeconds: 60
    Limiter:
      LimitQPSGetMetricData: 9
      LimitQPSMonitorObjectList: 9
    BehaviorWhenPullTimeout: SkipMissExecute
    StatisticsType: "LAST"
    Products:
      - Namespace: "VCM_Kafka"
      - Namespace: "VCM_ECS"
```



2. Configure the YAML file based on your business requirement and then install Exporter in your Kubernetes cluster.


```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cloud-monitor-exporter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cloud-monitor-exporter
  template:
    metadata:
      labels:
        app: cloud-monitor-exporter
      annotations:
        prometheus.io/scrape: "true"
        prometheus.io/port: "9898"
    spec:
      containers:
      - name: cloud-monitor-exporter
        image: cloud-monitor-cn-beijing.cr.volces.com/cm/cloud-monitor-exporter:v1.2.0
        args:
          - "--config=/conf/conf.yaml"
          - "--port=9898"
        resources:
          limits:
            memory: "128Mi"
            cpu: "500m"
        ports:
        - containerPort: 9898
        volumeMounts:
          - name: conf
            mountPath: /conf
      volumes:
        - name: conf
          configMap:
            name: cloud-monitor-exporter-conf
```



</Tab>
<Tab zoneid="c7hwYfNcI5" title="Install Exporter on Docker">
<TabTitle>Install Exporter on Docker</TabTitle>

1. Create the `config.yaml` file and modify it based on your business requirements.


```YAML
Credentials:
  AccessKey: "********"
  SecretKey: "********"
Region: "cn-beijing"
ServiceName: cloudmonitor
Host: cloudmonitor.cn-beijing.byteplusapi.com.cn
MaxRetries: 3
BatchInstanceCount: 50
DataQueueSize: 100
DataConcurrency: 10
MetaFreshIntervalSeconds: 60
DataFreshIntervalSeconds: 60
Limiter:
  LimitQPSGetMetricData: 9
  LimitQPSMonitorObjectList: 9
BehaviorWhenPullTimeout: SkipMissExecute
StatisticsType: "LAST"
Products:
  - Namespace: "VCM_Kafka"
  - Namespace: "VCM_ECS"
```



2. In the directory where the configuration file is located, run the following command to start the Docker image.


```Bash
docker run -itd -p 9898:9898 -v $(pwd)/config.yaml:/conf/conf.yaml cloud-monitor-cn-beijing.cr.volces.com/cm/cloud-monitor-exporter:v1.2.0 --config /conf/conf.yaml --port=9898
```





</Tab>
<Tab zoneid="T9jsCEbAjU" title="Install Exporter on the virtual machine">
<TabTitle>Install Exporter on the virtual machine</TabTitle>

1. Download the binary artifact, extract it, and access the artifact directory. For the latest binary artifact, see [Exporter change log](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_update_log).

2. In the artifact directory, create the `config.yaml` file and modify it based on your business requirements.


```YAML
Credentials:
  AccessKey: "********"
  SecretKey: "********"
Region: "cn-beijing"
ServiceName: cloudmonitor
Host: cloudmonitor.cn-beijing.byteplusapi.com.cn
MaxRetries: 3
BatchInstanceCount: 50
DataQueueSize: 100
DataConcurrency: 10
MetaFreshIntervalSeconds: 60
DataFreshIntervalSeconds: 60
Limiter:
  LimitQPSGetMetricData: 9
  LimitQPSMonitorObjectList: 9
BehaviorWhenPullTimeout: SkipMissExecute
StatisticsType: "LAST"
Products:
  - Namespace: "VCM_Kafka"
  - Namespace: "VCM_ECS"
```



3. In the artifact directory, run the following command to start the Exporter.


```YAML
./exporter --config config.yaml --port=9898
```





</Tab>
</Tabs>





</Tab>
</Tabs>


<span id="crqswZyO"></span>
## Verifying results

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2be1e7bf65a4717ad3a185ce0fac5da~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Descriptions |
|---|---|
|Metric name |The name of the metric exported by the Exporter is `metricName_subNamespace_namespace`.<br><br>In the example, MetricName is `AggregatedMemUtil`, SubNamespace is `aggregated_server`, and Namespace is `VCM_Redis`. In this case, the actual exported metric name is `AggregatedMemUtil_aggregated_server_VCM_Redis`. |
|Metric value |The value is a float. If you want to display the value in two decimal places, you need to manually handle it. |
|Timestamp |The time returned by the `GetMetricData` action. Time of the current product metric = Time returned by GetMetricData \- DelaySeconds.<br><br>For example, when you call the `GetMetricData` API to query metric data at 10:00:00, if you set `DelaySeconds` to 300 seconds (5 minutes), the data for 10:00:00 will be queried at 10:05:00. |


<span id="4PKIVBoO"></span>
## More information

<span id="qrBsldxu"></span>
### Startup parameters

```Bash
  -config string
        # The configuration file path. Default value: "/conf/config.yaml".
  -enable-self-metrics
        # Whether to enable self-monitoring metrics. Valid values: true and false. Default value: true.
  -host string
        # The EndPoint that the Exporter listens on. Default value: "0.0.0.0".
  -log-level string
        # The log level. Valid values:
        # - panic
        # - fatal
        # - error
        # - warn/warning
        # - info
        # - debug
        # - trace
        # Case-insensitive. Default value: "info".
  -port int
        # The port that the Exporter listens on. Default value: 9898.
```


<span id="ZQ7OGSVJ"></span>
### Global settings

The Exporter provides custom configurations, which not only apply to basic scenarios that require simple configurations but also to various extreme scenarios.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The service access address <code>Host</code> varies based on different regions. The cn\-beijing region is used in this example. During actual operations, replace <code>Host</code> in the following code with the actual address. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Service_address">Service addresses</a>.</div>


* <div data-tips="true" data-tips-type="warning">Some cloud products are available in all regions without region restrictions. In this case, the <code>Host</code> will automatically select the endpoint for a region from the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Service_address">service addresses</a> based on the nearest location to the request origin environment, and the <code>Region</code> in the request header must be set to the <code>RegionId</code> of that selected region.</div>


* <div data-tips="true" data-tips-type="warning">For the value of subnamespace, see the SubNamespace column in the metric documentation for each cloud product. For details, see <a href="https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric">Cloud Monitor metric queries</a>.</div>


* <div data-tips="true" data-tips-type="warning">For the value of metricname, see the MetricName column in the metric documentation for each cloud product. For details, see <a href="https://console.byteplus.com/cloud_monitor/metricDoc?tabKey=metric">Cloud Monitor metric queries</a>.</div>



```YAML
 # User authentication information
Credentials: <Credentials>

 # Specify the domain name for the Exporter to make API requests.
[ Host: <String> | default = "cloudmonitor.cn-beijing.byteplusapi.com.cn" ]

 # Optional. Whether to disable the SSL connection. Default value: false, which indicates that https requests are used. [Exporter version >= v1.0.21]
[ DisableSSL: <true|false> | default = false ]

 # Obtain data for the specified Region.
[ Region: <String> | default = "cn-beijing"]

 # The number of retries for API 5xx status codes and rate limiting.
[ MaxRetries: <Integer> | default = 3, range = [1, 3] ]

 # The maximum number of instances for each metric pull request.
[ BatchInstanceCount: <Integer> | default = 50, range = [1, 50] ]

 # The queue size for the internal request body.
[ DataQueueSize: <Integer> | default = 100, range = [1, +] ]

 # The number of threads for pulling data.
[ DataConcurrency: <Integer> | default = 10, range = [1, +] ]

 # Refresh interval for metadata pulling
[ MetaFreshIntervalSeconds: <Seconds> | default = 60, range = [30, +] ]

 # The interval at which metric data is pulled.
[ DataFreshIntervalSeconds: <Seconds> | default = 60, range = [30, +] ]

 # The request limiting configuration.
[ Limiter: <Limiter> ]

 #
 # Round timeout: The scenario where metric pull time exceeds the configured DataFreshIntervalSeconds.
 #
 # This configuration describes how the Exporter handles data pulling for the current and next rounds after a round timeout occurs.
 #
 # - SkipMissExecute: After the current pull is complete, skip rounds that are not executed and directly perform the latest pull.
 # - ContinueMissExecute: After the current pull is complete, continue executing rounds that are not executed.
 # - StopAndBackFilling: Stop the current pull, directly start the next pull, place the current unfinished pull requests in the offline queue,
 # and then write them to Prometheus by using the Remote Write method.
[ BehaviorWhenPullTimeout: <String> | default = "" ]

 # The backfill configuration takes effect only if BehaviorWhenPullTimeout = StopAndBackFilling.
[ OfflinePullConfig: <OfflinePullConfig> ]

 #Optional. Pull N data points and then perform calculations such as max, min, avg, and last. The LAST calculation is used by default, which returns the latest value. You can set the value only to one of MAX, MIN, AVG, LAST, FIRST, COUNT, and SUM, and the value is case-insensitive.
StatisticsType: <String>

 #Optional. The product data latency. Query end time of the Exporter = Current time - QueryDelaySeconds.
QueryDelaySeconds: <Seconds | [0, +]>

 #Optional. The query time range for product data. Default value: 2 minutes. Query start time = Query end time - QueryRangeSeconds.
QueryRangeSeconds: <Seconds | [0, +]>

 #Optional. The query period of time. Minimum value: 30 seconds.
QueryPeriodSeconds: <Seconds | [0, +]>

 #Optional. The additional static labels for the Product. The labels will be merged with the global ExtraLabels and deduplicated. The key is the label name, and the value is the label value.
[ StaticLabels: <String>:<String> ]

 #Optional. Whether to use new metrics to record instance metadata. Default value: false, which directly appends the metadata to the original metrics.
MetaLabelWithNewMetric: <true|false>

 #Optional. The metric name for metadata. This parameter takes effect only if MetaLabelWithNewMetric is set to true. Default value: volc_resource_info.
MetaLabelWithNewMetricName: <String>

 #Optional. Additional labels for the product. The labels will be merged with the global ExtraLabels and deduplicated.
ExtraLabels: <StringArray>

 #Optional. Regular expression rules for filtering additional product metadata tags. Use golang regular expressions and follow the RE2 specifications to match tag names. The tag_ prefix is added to the tags by default.
ExtraLabelsWithTagNameRegex:  <StringArray>

 #Optional. The list of projects for which the metrics are to be exported. You can configure up to 20 projects. The configuration applies to all Products, with lower priority than the ProjectNames configuration of Products.
ProjectNames: <StringArray>

 #Optional. Prometheus Remote Write mode configuration.
[ RemoteWrites: <RemoteWrite[]> ]

 #Required. The list of products for which the metrics are to be exported. If you do not declare the product list, the Exporter will not export metrics.
Products: <ProductConfig ...>

 #Optional. Metric collection configuration
Metrics: 
  <Namespace>: 
     <SubNamespace>: <MetricConfig ...>
```


<span id="YAFTNdti"></span>
#### Credentials configuration description

```YAML
 # The AK used for user authentication.
AccessKey: <String>

 # The SK used for user authentication.
SecretKey: <String>
```


<span id="fu5XywK9"></span>
#### Limiter configuration description

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Adaptive rate limiting for LimitQPSGetMetricData takes effect only if BehaviorWhenPullTimeout is set to SkipMissExecute or ContinueMissExecute.</div>


```YAML
 # The QPS for calling the Cloud Monitor metric API. This parameter is required only if BehaviorWhenPullTimeout is set to StopAndBackFilling. If you do not specify this parameter, adaptive rate limiting is used by default, which will distribute a large number of requests in a certain time period to different time points within the refresh cycle for processing.
[ LimitQPSGetMetricData: <Integer> | default = ]

 # Optional. The QPS for obtaining Cloud Monitor metric metadata. If you do not specify this parameter, adaptive rate limiting is used by default, which will distribute a large number of requests in a certain time period to different time points within the refresh cycle for processing.
[ LimitQPSMonitorObjectList: <Integer> | default = ]
```


<span id="HasNrOKA"></span>
#### OfflinePullConfig configuration description

```YAML
 # The proportion of request QPS for backfill threads to total request QPS.
[ RequestQPSRatio: <Float> | default = 0.3, range = [0.1, 0.9] ]
  
 # The concurrency for backfilling data. If you set it to 0, it will be set to the value of Config.DataConcurrency.
[ Concurrency: <Integer> | default = 0, range = [0, +] ]
  
 # The request queue size for backfilling data. If you set it to 0, it will be set to the value of Config.DataQueueSize.
[ DataQueueSize: <Integer> | default = 0, range = [0, +] ]

 # The maximum validity period. Requests exceeding this period will be discarded.
 #
 # Each metric data pull carries a time range. The result of the data pull is within the requested time range. If the estimated metric pull time is later than the time that is calculated by the following formula:
 # Current time - MaxAllowedOfflineDelayTime, the request will be discarded.
 # MaxAllowedOfflineDelayTime must be less than the out-of-order writing time range configured in Prometheus. Otherwise, write
 # failures will occur. Out-of-order writing in Prometheus requires a later version of Prometheus.
 #
 # Prometheus OTLP:
 # https://prometheus.io/docs/prometheus/latest/querying/api/#otlp-receiver
 #
 # Prometheus provides the out-of-order writing capability, which needs to be configured and enabled. In addition, you need to trust the timestamp of metrics exported by the Exporter.
 # > --------- prometheus.yml ---------------
 # > scrape_config:
 # >   honor_timestamps: true
 # >
 # > storage:
 # >   tsdb:
 # >     out_of_order_time_window: <Duration>
 # > --------- prometheus.yml ---------------
[ PromOutOfOrderTimeWindow: <Duration> | default = ? ]
  
 # The Remote Write address of Prometheus.
 #
 # The Exporter performs data backfill by using Remote Write. If the Prometheus Remote Write address is left empty,
 # data cannot be backfilled to Prometheus.
 #
 # The method of enabling backfill in Prometheus:
 # The method of enabling WriteAPI EndPoint in prometheus:
 # > ------- Prometheus start command -------
 # > prometheus \
 # >   --web.enable-remote-write-receiver \
 # >   --config.file={FilePATH} \
 # >   {Other parameters}
 # > ----------------------------------------
PromWriteAddress: <String>

[ PromBasicAuth: <PromBasicAuth>]
```


<span id="F8aLDPfx"></span>
#### PromBasicAuth configuration description

```YAML
 # Prometheus basic authentication information

 # Prometheus web basic auth username.
Username: <String>

 # Prometheus web basic auth password.
Password: <String>
```


<span id="Rgr6IIuq"></span>
#### ProductConfig configuration description

```YAML
 #Required. The product namespace.
Namespace: <String>

 #Optional. Only collect the metrics of instances under the specified project. If this parameter is left empty, the global ProjectName is used.
 #Restriction: ProjectName and ProjectNames cannot both be specified.
ProjectName: <String>

 #Optional. Only collect the metrics of instances under the specified multiple projects. If this parameter is left empty, the global ProjectNames is used.
 #Restriction: ProjectName and ProjectNames cannot both be specified.
ProjectNames: <StringArray>

 #Optional. Additional labels for the product. The labels will be merged with the global ExtraLabels and deduplicated.
ExtraLabels: <StringArray>

 #Optional. Regular expression rules for filtering additional product metadata tags. Use golang regular expressions and follow the RE2 specifications to match tag names. The tag_ prefix is added to the tags by default.
ExtraLabelsWithTagNameRegex:  <StringArray>

 #Optional. Optional product Dimension. For details, see the Dimension field of each cloud product on the Cloud Monitor metric queries page. Note: Dimensions without (optional) labels are exported by default and do not require additional configuration.
ExtraDimensions:  <StringArray>

 #Optional. Pull N data points and then perform calculations such as max, min, avg, and last. The FIRST calculation is used by default, which returns the earliest value. You can set the value only to one of MAX, MIN, AVG, LAST, FIRST, COUNT, and SUM, and the value is case-insensitive.
StatisticsType: <String>

 #Optional. The product data latency. Query end time of the Exporter = Current time - QueryDelaySeconds.
QueryDelaySeconds: <Seconds | [0, +]>

 #Optional. The query time range for product data. Default value: 2 minutes. Query start time = Query end time - QueryRangeSeconds.
QueryRangeSeconds: <Seconds | [0, +]>

 # Optional. The query period of time.
QueryPeriodSeconds: <Seconds | [0, +]>

 #Optional. The sub-namespaces for which the metrics are to be collected. By default, the metrics of all sub-namespaces are exported.
OnlyIncludeSubNamespaces:
  [ - <SubNamespace> ]

 #Optional. The sub-namespaces for which the metrics are not to be collected. By default, all metrics are exported.
ExcludeSubNamespaces:
  [ - <SubNamespace> ]

 #Optional. The metrics to be collected. key = sub-namespace. By default, all metrics are exported.
OnlyIncludeMetrics:
  [- <SubNamespace>: '[' <MetricName> [, ...] ']' ]

 #Optional. The metrics not to be collected. key = sub-namespace. By default, all metrics are exported.
ExcludeMetrics: <SubNamespace: StringArray...>
  [- <SubNamespace>: '[' <MetricName> [, ...] ']' ]

 #Optional. The instance IDs for which the metrics are to be collected. By default, the metrics of all instances are exported.
OnlyIncludeInstances: <StringArray>

 #Optional. The instance IDs for which the metrics are not to be collected. By default, the metrics of all instances are exported.
ExcludeInstances: <StringArray>

 #Optional. The cloud product metadata fields, which are used to filter instances.
InstanceMatchers:
 [- <InstanceMatcher> ]
```



|Parameter |Configuration description |Configuration example |
|---|---|---|
|```YAML```<br>```InstanceMatchers:```<br>``` [- <InstanceMatcher> ]```<br> |Use metadata fields to filter cloud product instances. `<InstanceMatcher>` contains the following fields:<br><br><br>* `Field: <String>`: Cloud product metadata field, which varies based on different cloud products. For details, see [Supported cloud products](https://console.byteplus.com/cloud_monitor/exporter).<br><br>* `Type: <String>`: The matching relationship. Valid values:<br><br>   * `include`: Collect the metrics of instances with the specified Field value.<br><br>   * `exclude`: Exclude instances with the specified Field value.<br><br>   * `regex`: Collect the metrics of instances whose field value matches the regular expression list.<br><br>   * If you do not specify this parameter, the default value is `include`.<br><br>* `Values: <StringArray>`: The values of the cloud product metadata fields.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the specified metadata field does not exist, the system will ignore this filter configuration.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When you configure multiple filter conditions, the conditions are in an <strong>AND</strong> relationship. In this way, only cloud product instances that meet all conditions will be selected.</div><br> |Take ECS as an example. ECS supports exporting the following metadata fields: `AvailableZone` and `IP.Inside`.<br><br>The following sample code shows how to use the `IP.Inside` metadata field to export metrics of ECS instances with specified private addresses.<br><br>```YAML```<br>```InstanceMatchers:```<br>```  - Field: "IP.Inside"```<br>```    Type: "include"```<br>```    Values:```<br>```      - "192.168.1.10"```<br>```      - "192.168.1.20"```<br> |


<span id="GPA6ONKN"></span>
#### MetricConfig configuration description

```YAML
 #Required. The metric name.
MetricName: <String>

 #Optional. Optional metric Dimension, which has higher priority than the product-level (ProductConfig) ExtraDimensions. For details, see the Dimension field of each metric on the Cloud Monitor metric queries page. Note: Dimensions without (optional) labels are exported by default and do not require additional configuration.
ExtraDimensions:  <StringArray>

 #Optional. Pull N data points and then perform calculations such as max, min, avg, and last. The FIRST calculation is used by default, which returns the earliest value. You can set the value only to one of MAX, MIN, AVG, LAST, FIRST, COUNT, and SUM, and the value is case-insensitive.
StatisticsType: <String>

 #Optional. The product data latency. Query end time of the Exporter = Current time - QueryDelaySeconds.
QueryDelaySeconds: <Seconds | [0, +]>

 #Optional. The query time range for product data. Default value: 2 minutes. Query start time = Query end time - QueryRangeSeconds.
QueryRangeSeconds: <Seconds | [0, +]>

 #Optional. The query period of time. Minimum value: 30 seconds.
QueryPeriodSeconds: <Seconds | [0, +]>


```


<span id="kwlMEuPs"></span>
#### StatisticsType configuration description

By default, the Exporter periodically pulls metric data from the server. The data time range for each pull is 2 minutes (You can specify this period by specifying the QueryRangeSeconds parameter). The time range typically contains N data points, and the point with the earliest timestamp within that range is selected as the data point for the current collection round by default. In scenarios where some sparse data points or metric data glitches occur, you can apply a sampling method to N data points pulled from the last time range each time. You can choose to use the MAX, MIN, AVG, LAST, FIRST, COUNT, or SUM of these points as the sampling points for the current collection round. You can specify this parameter at the metric granularity.

<span id="gAWffFJt"></span>
#### Remote Write configurations

The Prometheus Remote Write mode configuration supports directly writing collected metrics to a time series database that supports the Remote Write protocol.

```YAML
 # RemoteWrite configuration array. You can configure multiple targets.
RemoteWrites:
  - # Required. The Prometheus Remote Write API endpoint.
    # Endpoint format: http://host:port/api/v1/write or https://host:port/api/v1/write.
    # Auto-completion. If no protocol prefix is specified, http:// is automatically added.
    EndPoint: <String>

    # Optional. The instance name. It is used for identification in logs and self-monitoring.
    # Default value: the value of EndPoint.
    [ Name: <String> ]

    # Optional. The HTTP basic authentication username.
    [ Username: <String> ]

    # Optional. The HTTP basic authentication password.
    [ Password: <String> ]

    # Optional. The periodic flush interval for aggregation blocks.
    # Default value: "10s". Minimum value: "1s".
    [ MaxWaitTime: <Duration> ]

    # Optional. The buffer queue size.
    # Default value: 10000. Minimum value: 1000.
    [ WriteBufferQueueSize: <Integer> ]

    # Optional. The maximum sample bytes to send per request.
    # Default value: 10000. Minimum value: 2000.
    [ MaxSampleBytesPreSend: <Integer> ]

    # Optional. The number of retries on write failures.
    # Default value: 3. Value range: [1, 10].
    [ RetryCount: <Integer> ]

    # Optional. The concurrency for Relabel/aggregation workers (CPU-intensive).
    # Default value: the number of CPU cores. Value range: [1, 2*CPU].
    [ RelabelWorkerConcurrency: <Integer> ]

    # Optional. The concurrency for HTTP writes (I/O-intensive).
    # Default value: the number of CPU cores. Value range: [1, 16*CPU].
    [ HTTPWriteConcurrency: <Integer> ]

    # Optional. The maximum number of sample points per aggregation block.
    # Default value: the value of WriteBufferQueueSize.
    [ MaxSamplesPerBlock: <Integer> ]

    # Optional. The capacity of the input-to-block channel.
    # Default value: 1000.
    [ ChannelCapacity: <Integer> ]

    # Optional. The tag rewriting rules.
    [ RelabelConfigs: <RelabelConfig[]> ]

    # Optional. The global tag. It is added to all metrics after being relabeled.
    [ GlobalLabel: <Map<String, String>> ]

    # Optional. The collection scope. It controls which types of data to write.
    # Default value: ["self-metric", "cloud-monitor"].
    # Valid values: "self-metric", "cloud-monitor", and "offline-pool".
    [ Scope: <StringArray> ]

    # Optional. The self-monitoring collection interval.
    # Default value: "10s".
    [ SelfMonitorCollectPeriod: <Duration> ]
```


<span id="ZxehEy0Y"></span>
### Health checks and readiness probes

The Exporter provides the `/ready` and `/health` endpoints for liveness and readiness checks.

<span id="XWa22vqY"></span>
#### Health checks

When you access the `/health` endpoint, the response `content-type: text/plain; charset=utf-8` will be returned:

The status code is always `200`.

```HTML
ok
```



1. After the Exporter starts, the `/health` endpoint begins to work and always returns `ok` until the Exporter stops running.

2. If an exception occurs, the `/health` endpoint may experience timeouts, no response, or other situations.


<span id="mJfhRG7H"></span>
#### Readiness endpoint

After the Exporter collects data for the first time, the `/ready` endpoint returns the response `content-type: text/plain; charset=utf-8`:

The status code is always `200`.

```HTML
ready
```



* If the Exporter has not completed its first data collection, the `/ready` endpoint returns `not ready`.

* If the `/health` endpoint does not return the expected result, the response from the `/ready` endpoint is unreliable.


<span id="rTcNq5R0"></span>
## Related document


* To export data to Grafana, export data from Cloud Monitor by using the Exporter first and then import the data into Grafana. For the method of deploying Grafana, see [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

* To view the update logs and troubleshooting solutions of the Exporter, see [Exporter troubleshooting solutions](https://docs.byteplus.com/en/docs/cloudmonitor/Exporter_exception_troubleshooting_solution).
