---
title: "Python application integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_Python_applications"
---

Python applications have different integration methods in various scenarios. This document describes the detailed actions for integrating Python applications with OpenTelemetry. After integration, you can automatically collect trace information, automatically generate metrics, and use features such as trace search and log search.

<span id=".6YCa6L-HT3BlblRlbGVtZXRyeeaOpeWFpQ=="></span>
## Integrate via OpenTelemetry

OpenTelemetry is an observability project under CNCF, designed to provide standardized solutions in the observability domain. It addresses standardization issues for data models, collection, processing, and export of observability data, and offers services independent of third\-party vendors.

If your application has already integrated the OpenTelemetry SDK, the APM server side can receive data reported by OpenTelemetry. After integrating with APM, you will gain capabilities such as RED metric generation, multidimensional trace search, single trace search, topology generation, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To isolate production and test data, see: <a href="https://docs.byteplus.com/en/docs/apmplus/Isolate_production_and_test_data">Isolate production and test data</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
### Limits


* APMPlus uses Prometheus as the storage for OpenTelemetry metrics and supports querying metrics with promql. For specific applications, see [custom dashboard](https://docs.byteplus.com/en/docs/apmplus/Custom_dashboard) and [alert management](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).

* There are certain limitations when converting OpenTelemetry metrics to Prometheus metrics:

   * As with [open source](https://opentelemetry.io/docs/reference/specification/compatibility/prometheus_and_openmetrics/#dropped-data-points), [ExponentialHistogram](https://opentelemetry.io/docs/reference/specification/metrics/data-model/#exponentialhistogram) is not supported.

   * Data with aggregation method delta is not supported. Do not modify the default aggregation configuration on the SDK side. Ensure that the aggregation method for SDK side data is cumulative.

* Each workspace has its own data reporting credentials. To manage and isolate data using a workspace, ensure that the `apmplus-opentelemetry-collector` component has been upgraded to version v3.1.0 or above.


<span id="YaTsrUYf"></span>
### Considerations


* Caution for gevent applications


To use gevent coroutines, you need to set the environment variable `GEVENT_ENABLE=true`. For example, if your program uses the following coroutine, you need the environment variable `GEVENT_ENABLE=true`.

```Python
from gevent import monkey
monkey.patch_all()
```



* Caution for Django applications


If your application uses the Django framework, pay attention to the following before integration:


   * To automatically integrate via OpenTelemetry in a K8s environment, ensure that the Python version is 3.8 or above;

   * It is recommended to deploy the service using uWSGI. For deployment methods, see [Host Django applications with uWSGI](https://docs.djangoproject.com/en/5.0/howto/deployment/wsgi/uwsgi/). Starting directly with the Python command may result in reporting failures.

   * The introduction of OpenTelemetry may cause Django applications to stop using the default configuration file, requiring you to re\-specify the configuration file via environment variables:


```Bash
export DJANGO_SETTINGS_MODULE=mysite.settings
```



You can add this setting to the project's startup script, or add environment variables through a YAML file:


```Bash
env: 
- name: DJANGO_SETTINGS_MODULE
  value: mysite.settings
```


<span id=".6Ieq5Yqo5o6l5YWl"></span>
### Automatic integration

APM OpenTelemetry Collector is a data collector developed by APM based on OpenTelemetry Collector, compliant with the Apache 2.0 license. It supports the collection of OpenTelemetry Monitoring data, as well as the collection of Prometheus metrics, application Monitoring data, and Kubernetes resource metrics.


1. Install APM OpenTelemetry Collector.

   Install the apmplus\-opentelemetry\-collector component via the VKE cluster component center. Go to the VKE cluster interface, select **Component Management \-\> Monitoring**, and click Install in the upper right corner of the apmplus\-opentelemetry\-collector component under `...` to complete the deployment and management of the Apmplus OpenTelemetry Collector.

2. Add the `instrumentation.apmplus.volcengine.com/inject-python` and `instrumentation.apmplus.volcengine.com/workspace` annotations to the Kubernetes Deployment configuration of the service. The following is a code example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: python-flask-demo
     labels:
       app: python-flask-demo
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: python-flask-demo
     template:
       metadata:
         labels:
           app: python-flask-demo
         annotations:
           instrumentation.apmplus.volcengine.com/inject-python: 'true' # Enable APMPlus observation injection
           instrumentation.apmplus.volcengine.com/workspace: default  # Specify the workspace to which the service belongs
       spec:
         containers:
           - name: python-flask-demo
             image: python-flask:latest
             imagePullPolicy: Always
             env:
               - name: CONTAINER_RUNTIME
                 value: "k8s"
   
   ```
   

3. Restart the application.


<span id="bqWaqUEy"></span>
### Opentelemetry SDK integration

To report data by manually instrumenting with the community\-provided Opentelemetry Python SDK, refer to the community's [integration documentation](https://opentelemetry.io/docs/languages/python/) and [python demo](https://opentelemetry.io/docs/demo/services/recommendation/) to complete the Python project setup.

<span id="Eo4uzmLi"></span>
#### Complete instrumentation and reporting using opentelemetry\-instrument

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For related information in the official Opentelemetry documentation, refer to: <a href="https://opentelemetry.io/docs/languages/python/getting-started/">getting\-started</a>.</div>



1. Install the dependency packages.


```YAML
pip install opentelemetry-distro opentelemetry-exporter-otlp
opentelemetry-bootstrap -a install
```


The opentelemetry\-distro package installs the API, SDK, as well as the opentelemetry\-bootstrap and opentelemetry\-instrument tools.


2. Specify the data reporting backend and authentication parameters in the startup command.



|Parameters |Descriptions |
|---|---|
|<your\-service_name\> |Application service name. |
|<apmplus_endpoint\> |The server address for the corresponding environment. You can go to apmplus_endpoint/collector_endpoint Access Center to view and obtain it. For details, see: [How to use the Access Center?](https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center). |
|<collector_endpoint\> ||
|<app_key\> |The app_key provided by the service access console. For the method to obtain it, see: [How to obtain the authentication information AppKey for application performance monitor?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication). |



* To report data directly to the ApmPlus backend, see the following example:


```Python
opentelemetry-instrument \
    --service_name <your-service-name> \
    --exporter_otlp_endpoint=<apmplus_endpoint> \
    --exporter_otlp_protocol=<protocol> \
    --exporter_otlp_headers=X-ByteAPM-AppKey=<app_key> \
    --python myapp.py
```



* To report data to the Collector, there is no need to specify exporter_otlp_headers. See the following example:


```Python
opentelemetry-instrument \
    --service_name <your-service-name> \
    --exporter_otlp_endpoint=<collector_endpoint> \
    --exporter_otlp_protocol=<protocol> \
    --python myapp.py
```



* You can also configure these parameters via environment variables, as shown below:


```Python
OTEL_SERVICE_NAME=your-service-name \
OTEL_EXPORTER_OTLP_ENDPOINT=<apmplus_endpoint>/<collector_endpoint>
OTEL_EXPORTER_OTLP_PROTOCOL=<protocol>
OTEL_EXPORTER_OTLP_HEADERS=X-ByteAPM-AppKey=<app_key>
opentelemetry-instrument \
    python myapp.py
```


<span id="mPM2DyRw"></span>
#### Manual instrumentation using opentelemetry\-sdk


1. Download the API and SDK packages.


```Python
pip install opentelemetry-api
pip install opentelemetry-sdk
pip install opentelemetry-exporter-otlp
```



2. In the code, create [TracerProvider](https://opentelemetry.io/docs/concepts/signals/traces/#tracer-provider), [MeterProvider](https://opentelemetry.io/docs/specs/otel/metrics/api/#meterprovider), and [LoggerProvider](https://opentelemetry.io/docs/specs/otel/logs/api/#loggerprovider) and use them to report data.


For related information in the official Opentelemetry documentation, refer to [Instrumentation](https://opentelemetry.io/docs/languages/python/instrumentation/). The demo in the official documentation prints metrics and traces to the console. To report data to the collector, in addition to using the grpc/http exporter, you also need to set the endpoint, headers, and other information.

It is recommended to use the collector endpoint as the reporting address. See the demo example below:


* TraceProvider example:


```Python
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import (
    BatchSpanProcessor,
    ConsoleSpanExporter,
)
from opentelemetry.sdk.resources import Resource
from opentelemetry.exporter.otlp.proto.grpc.trace_exporter import OTLPSpanExporter

# Set endpoint. It is recommended to directly use collector endpoint
# endpoint = "apmplus-opentelemetry-gateway-service-grpc.apmplus-opentelemetry-operator:4317"

# Set the reporting address as apmplus endpoint, use when APM OpenTelemetry Collector component cannot be installed. If accessed via public network, use apmplus-cn-beijing.volces.com:4317.
endpoint = "apmplus-cn-beijing.ivolces.com:4317"

# Set apmplus appkey. Only required when the reporting address is Apmplus endpoint.
headers = {
   "x-byteapm-appkey": "<app_key>",
}

# Set resource, such as service_name
resource_attributes = {
    "service.name": "your-service-name",
}
resource = Resource.create(resource_attributes)

exporter = OTLPSpanExporter(endpoint=endpoint, insecure=True, headers=headers) 

provider = TracerProvider(resource=resource)
processor = BatchSpanProcessor(exporter)
provider.add_span_processor(processor)

# Sets the global default tracer provider
trace.set_tracer_provider(provider)

# Creates a tracer from the global tracer provider
tracer = trace.get_tracer("my.tracer.name")
```



* MeterProvider example:


```Python

from opentelemetry import metrics
from opentelemetry.sdk.metrics import MeterProvider
from opentelemetry.sdk.metrics.export import (
    ConsoleMetricExporter,
    PeriodicExportingMetricReader,
)
from opentelemetry.sdk.resources import Resource
from opentelemetry.exporter.otlp.proto.grpc.metric_exporter import OTLPMetricExporter
    
# Set endpoint. It is recommended to directly use collector endpoint
# endpoint = "apmplus-opentelemetry-gateway-service-grpc.apmplus-opentelemetry-operator:4317"

# Set the reporting address as apmplus endpoint, use when APM OpenTelemetry Collector component cannot be installed. If accessed via public network, use apmplus-cn-beijing.volces.com:4317.
endpoint = "apmplus-cn-beijing.ivolces.com:4317"
# Set apmplus appkey. Only required when the reporting address is Apmplus endpoint
headers = {
   "x-byteapm-appkey": "<app_key>",
}

# Set resource, such as service_name
resource_attributes = {
    "service.name": "your-service-name",
}
resource = Resource.create(resource_attributes)

exporter = OTLPMetricExporter(endpoint=endpoint, headers=headers)
metric_reader = PeriodicExportingMetricReader(exporter)
provider = MeterProvider(metric_readers=[metric_reader], resource=resource)

# Sets the global default meter provider
metrics.set_meter_provider(provider)

# Creates a meter from the global meter provider
meter = metrics.get_meter("my.meter.name")
```



* LoggerProvider example:


For log reporting, in addition to initializing LoggerProvider, it is recommended to use opentelemetry LoggingInstrumentor to instrument the logging library, thereby associating logs and traces.


1. Install LoggingInstrumentor


```Python
pip install opentelemetry-instrumentation-logging
```



2. Initialize LoggerProvider and add LoggingInstrumentor


```Python
import logging

from opentelemetry._logs import get_logger, set_logger_provider
from opentelemetry.exporter.otlp.proto.grpc._log_exporter import OTLPLogExporter
from opentelemetry.sdk._logs import LoggerProvider, LoggingHandler
from opentelemetry.sdk._logs.export import BatchLogRecordProcessor
from opentelemetry.sdk.resources import Resource
from opentelemetry.instrumentation.logging import LoggingInstrumentor

# Set endpoint. It is recommended to directly use collector endpoint
# endpoint = "apmplus-opentelemetry-gateway-service-grpc.apmplus-opentelemetry-operator:4317"

# Set the reporting address as apmplus endpoint, use when APM OpenTelemetry Collector component cannot be installed. If accessed via public network, use apmplus-cn-beijing.volces.com:4317.
endpoint = "apmplus-cn-beijing.ivolces.com:4317"
# Set apmplus appkey. Only required when the reporting address is Apmplus endpoint
headers = {
   "x-byteapm-appkey": "<app_key>",
}

# Set resource, such as service_name
resource_attributes = {
    "service.name": "your-service-name",
}
resource = Resource.create(resource_attributes)

exporter = OTLPLogExporter(endpoint=endpoint, insecure=True, headers=headers)
provider = LoggerProvider(resource=resource)
processor = BatchLogRecordProcessor(exporter)
provider.add_log_record_processor(processor)

# Sets the global default logger provider
set_logger_provider(provider)

# Attach OTLP handler to root logger
handler = LoggingHandler(level=logging.INFO, logger_provider=provider)
logging.basicConfig(handlers=[handler], level=logging.INFO)
# instrument logging
LoggingInstrumentor().instrument(set_logging_format=True)

# log
logging.info("This is an OpenTelemetry log record!")
```


&nbsp;

<span id="ZgwoxRPa"></span>
### Frameworks supported for automatic injection


|<div style="text-align: center"><br>Supported Packages</div><br> |<div style="text-align: center"><br>Version</div><br> |
|---|---|
|<div style="text-align: center"><br>openai</div><br> |<div style="text-align: center"><br>\>= 0.27.0</div><br> |
|<div style="text-align: center"><br>langchain</div><br> |<div style="text-align: center"><br> \>= 0.0.346</div><br> |
|<div style="text-align: center"><br>mcp</div><br> |<div style="text-align: center"><br>\>=1.6.0, <=1.8.0</div><br> |
|<div style="text-align: center"><br>aio_pika</div><br> |<div style="text-align: center"><br>\>= 7.2.0, < 10.0.0</div><br> |
|<div style="text-align: center"><br>aiohttp</div><br> |<div style="text-align: center"><br>~= 3.0</div><br> |
|<div style="text-align: center"><br>aiopg</div><br> |<div style="text-align: center"><br>\>= 0.13.0, < 2.0.0</div><br> |
|<div style="text-align: center"><br>asgiref</div><br> |<div style="text-align: center"><br>~= 3.0</div><br> |
|<div style="text-align: center"><br>asyncio</div><br> |<div style="text-align: center"><br>all</div><br> |
|<div style="text-align: center"><br>asyncpg</div><br> |<div style="text-align: center"><br>\>= 0.12.0</div><br> |
|<div style="text-align: center"><br>aws_lambda</div><br> |<div style="text-align: center"><br>all</div><br> |
|<div style="text-align: center"><br>boto</div><br> |<div style="text-align: center"><br>~=2.0</div><br> |
|<div style="text-align: center"><br>boto3</div><br> |<div style="text-align: center"><br>~= 1.0</div><br> |
|<div style="text-align: center"><br>botocore</div><br> |<div style="text-align: center"><br> ~= 1.0</div><br> |
|<div style="text-align: center"><br>cassandra\-driver</div><br> |<div style="text-align: center"><br>~= 3.25</div><br> |
|<div style="text-align: center"><br>scylla\-driver</div><br> |<div style="text-align: center"><br>~= 3.25</div><br> |
|<div style="text-align: center"><br>celery</div><br> |<div style="text-align: center"><br> \>= 4.0, < 6.0</div><br> |
|<div style="text-align: center"><br>click</div><br> |<div style="text-align: center"><br>\>= 8.1.3, < 9.0.0</div><br> |
|<div style="text-align: center"><br>confluent\-kafka</div><br> |<div style="text-align: center"><br>\>= 1.8.2, <= 2.4.0</div><br> |
|<div style="text-align: center"><br>dbapi</div><br> |<div style="text-align: center"><br>all</div><br> |
|<div style="text-align: center"><br>django</div><br> |<div style="text-align: center"><br>\>= 1.10</div><br> |
|<div style="text-align: center"><br>elasticsearch</div><br> |<div style="text-align: center"><br>\>= 6.0</div><br> |
|<div style="text-align: center"><br>falcon</div><br> |<div style="text-align: center"><br>\>= 1.4.1, < 4.0.0</div><br> |
|<div style="text-align: center"><br>fastapi</div><br> |<div style="text-align: center"><br>~= 0.58</div><br> |
|<div style="text-align: center"><br>flask</div><br> |<div style="text-align: center"><br>\>= 1.0</div><br> |
|<div style="text-align: center"><br>grpcio</div><br> |<div style="text-align: center"><br> \>= 1.42.0</div><br> |
|<div style="text-align: center"><br>httpx</div><br> |<div style="text-align: center"><br>\>= 0.18.0</div><br> |
|<div style="text-align: center"><br>jinja2</div><br> |<div style="text-align: center"><br>\>= 2.7, < 4.0</div><br> |
|<div style="text-align: center"><br>kafka\-python</div><br> |<div style="text-align: center"><br> \>= 2.0, < 3.0</div><br> |
|<div style="text-align: center"><br>kafka\-python\-ng</div><br> |<div style="text-align: center"><br>\>= 2.0, < 3.0</div><br> |
|<div style="text-align: center"><br>logging</div><br> |<div style="text-align: center"><br>all</div><br> |
|<div style="text-align: center"><br>mysql\-connector\-python</div><br> |<div style="text-align: center"><br>\>= 8.0, < 10.0</div><br> |
|<div style="text-align: center"><br>mysqlclient</div><br> |<div style="text-align: center"><br>< 3</div><br> |
|<div style="text-align: center"><br>pika</div><br> |<div style="text-align: center"><br>\>= 0.12.0</div><br> |
|<div style="text-align: center"><br>psycopg</div><br> |<div style="text-align: center"><br>\>= 3.1.0</div><br> |
|<div style="text-align: center"><br>psycopg2</div><br> |<div style="text-align: center"><br>\>= 2.7.3.1</div><br> |
|<div style="text-align: center"><br>pymemcache</div><br> |<div style="text-align: center"><br>\>= 1.3.5, < 5</div><br> |
|<div style="text-align: center"><br>pymongo</div><br> |<div style="text-align: center"><br>\>= 3.1, < 5.0</div><br> |
|<div style="text-align: center"><br>PyMySQL</div><br> |<div style="text-align: center"><br> < 2</div><br> |
|<div style="text-align: center"><br>pyramid</div><br> |<div style="text-align: center"><br>\>= 1.7</div><br> |
|<div style="text-align: center"><br>redis</div><br> |<div style="text-align: center"><br>\>= 2.6</div><br> |
|<div style="text-align: center"><br>remoulade</div><br> |<div style="text-align: center"><br>\>= 0.50</div><br> |
|<div style="text-align: center"><br>requests</div><br> |<div style="text-align: center"><br> ~= 2.0</div><br> |
|<div style="text-align: center"><br>sqlalchemy</div><br> |<div style="text-align: center"><br> \>= 1.0.0, < 2.1.0</div><br> |
|<div style="text-align: center"><br>sqlite3</div><br> |<div style="text-align: center"><br>all</div><br> |
|<div style="text-align: center"><br>starlette</div><br> |<div style="text-align: center"><br>~= 0.13.0</div><br> |
|<div style="text-align: center"><br>psutil</div><br> |<div style="text-align: center"><br>\>= 5</div><br> |
|<div style="text-align: center"><br>threading</div><br> |<div style="text-align: center"><br>all</div><br> |
|<div style="text-align: center"><br>tornado</div><br> |<div style="text-align: center"><br>\>= 5.1.1</div><br> |
|<div style="text-align: center"><br>tortoise\-orm</div><br> |<div style="text-align: center"><br>\>= 0.17.0</div><br> |
|<div style="text-align: center"><br>urllib</div><br> |<div style="text-align: center"><br>all</div><br> |
|<div style="text-align: center"><br>urllib3</div><br> |<div style="text-align: center"><br>\>= 1.0.0, < 3.0.0</div><br> |
|<div style="text-align: center"><br>wsgi</div><br> |<div style="text-align: center"><br>all</div><br> |


<span id="MeBftQLn"></span>
## Python log integration and considerations

Log collection for Python applications relies on OpenTelemetry. Once the entire process of integrating OpenTelemetry into Python applications is completed, log information can be automatically collected and reported.

<span id="un6F43mx"></span>
### Operating principle

OpenTelemetry Python logs are implemented by instrumenting the logging library. By enhancing log information and adding the corresponding reporting handler, logs are reported to the APMPlus backend and associated with Trace and Span information. Therefore, only logs printed through the logging library can be collected and sent to APMPlus. Logs generated by other methods, such as the console, cannot be collected.

The complete process for a log in a Python application, from its creation to being sent via OpenTelemetry and reported to the APMPlus backend, is as follows:

<span id="qzrBxEFL"></span>
### Considerations

When collecting logs from Python applications, note the following considerations.

<span id="B59dvNjq"></span>
#### Log level configuration

The Python logging library has a log level configuration, which defaults to `WARNING`. If a log's level is lower than the configured level, the log will not be printed, nor will it be reported to the APMPlus server side. Therefore, to collect logs such as INFO and DEBUG, the log level must be manually set using `logging.basicConfig`. Example code is as follows:

```Python
import logging
logging.basicConfig(level=logging.INFO)
```


<span id="iaaQU8O9"></span>
#### Propagate parameter configuration

Typically, logging is not used directly for log recording; instead, `logging.getLogger(name)` is used to create a logger, and logs are recorded through the logger. OpenTelemetry logging is instrumented based on the root logger. Therefore, when logs are recorded using a logger and `propagate = False` ** **  is set, logs recorded by the logger will not propagate to the root logger and cannot be collected or reported by OpenTelemetry.

Each logger instance created via `logging.getLogger(name)` has a propagate property, which defaults to True. The operating principle is as follows.


* **propagate = True (default)** : After a logger processes a log, it checks the propagate flag. If it is True, the log record will continue to be passed up to the parent logger. This process continues until the root logger.

* **propagate = False**: After a logger processes a log, propagation will stop. The parent logger and higher\-level ancestor loggers will be completely unaware of the existence of this log.


<span id="tV9rrnJC"></span>
##### Asynchronous log recording

Log recording needs to associate logs with the request trace to which they belong. Therefore, in OpenTelemetry LoggingInstrumentor, log information is enhanced by obtaining the context information at the time of log printing and storing it in the log information. However, when an asynchronous method is used to record logs in actual business scenarios, context information may be lost. In this case, logs cannot be associated with a Trace, resulting in the TraceId information being displayed as empty on the APMPlus log page.

<span id="0NLENOHN"></span>
### Troubleshooting

When log collection does not yield any log data, after ruling out the situations mentioned in the Note section, you can troubleshoot the issue by proactively adding the corresponding logs. Example:


* After setting logging basicConfig and before printing logs, add the following code to print the handler and level information of the logging library.


```Python
print(f"logging handlers: {logging.root.handlers}")
print(f"logging level: {logging.root.level}")
```


At this point, if LoggingInstrumentor is enabled, the logging.root.handlers in the output information will include the following handler.

```Python
 <LoggingHandler (NOTSET)>
```



* If you use logger to print logs, you can use the following code to print logs.


```Python
print(f"logger propagate: {your_logger.propagate}")
print(f"logger level: {your_logger.level}")
```


At this point, if LoggingInstrumentor is enabled, the logging.root.handlers in the output information will include the following handler.

```Python
 <LoggingHandler (NOTSET)>
```
