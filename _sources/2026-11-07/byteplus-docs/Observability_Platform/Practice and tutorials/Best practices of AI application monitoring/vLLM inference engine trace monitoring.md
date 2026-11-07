---
title: "vLLM inference engine trace monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/vLLM_inference_engine_trace_monitoring"
---

Application Performance Management (APM) provides end\-to\-end tracing capabilities across multiple platforms. This topic describes how to instrument the vLLM inference engine with APM, and view the trace and metric data for vLLM\-related tracing.

<span id="bAJMD3fa"></span>
## Background

vLLM is an open\-source framework dedicated to‌ the inference and deployment of large language models (LLMs). It is designed to optimize and accelerate LLM usage, especially for efficient inference. vLLM processes an enormous volume of data, which makes collecting observability data for the framework highly challenging. Furthermore, effective observability of vLLM may require annotation of the collected data. APM can be seamlessly integrated with the vLLM inference engine to address these challenges: it ingests vLLM observability data, enables dialogue analysis, and delivers in\-depth insights into the LLM operations.

<span id="2mJfQ1xX"></span>
## Prerequisites


* The basic environment has been prepared, and information such as the service name has been obtained.

* APM has been activated. For detailed steps, refer to [Activating APM](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring).


<span id="DdMryOze"></span>
## Procedure

<span id="GjQzt4sN"></span>
### Step 1: Report observability data

You can report observability data to APM via `apmplus-opentelemetry-collector`, or directly report observability data to the APM backend based on your needs.


<Tabs>
<Tab zoneid="kfSgJQRR4H" title="Data reporting via Otel Collector">
<TabTitle>Data reporting via Otel Collector</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke), select **Cluster** in the left navigation bar. On the cluster list page, click the target cluster name to go to the cluster management page. 

2. On the **Monitoring** tab of the **Addons** page, install the `apmplus-opentelemetry-collector` add\-on. Additionally, to collect metric data at the host and process levels, we recommend that you install the `apmplus-server-agent` add\-on at the same time.

3. Configure the following environment variables in the environment to use `apmplus-opentelemetry-collector` to report observability data to APM.


```Bash
export OTEL_EXPORTER_OTLP_ENDPOINT="http://<apmplus-otel-collector>:4317"
export OTEL_EXPORTER_OTLP_INSECURE=true
export OTEL_SERVICE_NAME="<your-service-name>"
export OTEL_RESOURCE_ATTRIBUTES="apmplus.business_type=gen_ai"
```





</Tab>
<Tab zoneid="EEYQkpWaaK" title="Direct data reporting">
<TabTitle>Direct data reporting</TabTitle>

1. Log in to the [APM console](https://console.byteplus.com/observe/apmplus-server), and select the project and region in the top navigation bar. 

2. In the left navigation bar, select **Integration hub** and retrieve the AppKey and endpoint from the Java access information section.

3. Configure the following environment variables in the environment to directly report observability data to the APM backend without the need to use an agent.


```Bash
export OTEL_EXPORTER_OTLP_ENDPOINT="http://<apmplus-domain>:4317"
export OTEL_EXPORTER_OTLP_INSECURE=true
export OTEL_EXPORTER_OTLP_HEADERS="x-byteapm-appkey=<appkey>"
export OTEL_SERVICE_NAME="<your-service-name>"
export OTEL_RESOURCE_ATTRIBUTES="apmplus.business_type=gen_ai"
```





</Tab>
</Tabs>


<span id="S4NDbSLu"></span>
### Step 2: Instrument vLLM


1. Execute the following command in your environment to install vLLM.


```Bash
pip install vllm
```



2. Execute the following command in your environment to install the OpenTelemetry package.


```Bash
pip install \
  'opentelemetry-sdk' \
  'opentelemetry-api' \
  'opentelemetry-exporter-otlp' \
  'opentelemetry-semantic-conventions-ai' \
  'opentelemetry-distro' \
  'opentelemetry-instrumentation-fastapi'
  
opentelemetry-bootstrap -a install
```



3. Execute the following command in your environment to start vLLM.

* Sample command for the default configuration


```Bash
vllm serve /deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B --otlp-traces-endpoint="$OTEL_EXPORTER_OTLP_ENDPOINT"
```



* Sample command for optional configurations


Add the `collect-detailed-traces` parameter to the startup command to specify the module and collect detailed trace information, such as the `time_in_model_execute` and `time_in_model_forward` information.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This parameter involves potentially costly and blocking operations and may impact inference performance. We recommend that you use this parameter based on your needs.</div>


```Bash
vllm serve /deepseek-ai/DeepSeek-R1-Distill-Qwen-1.5B --otlp-traces-endpoint="$OTEL_EXPORTER_OTLP_ENDPOINT" --collect-detailed-traces=all

--collect-detailed-traces COLLECT_DETAILED_TRACES
# Valid choices are model,worker,all. It makes sense to set this only if ``--otlp-traces-endpoint`` is set. If set, it will collect detailed traces for the specified modules. This involves use of possibly costly and or blocking operations and hence might have a performance impact.
```


<span id="gwhvyTZm"></span>
### Step 3: View vLLM tracing data


1. Log in to the [APM console](https://console.byteplus.com/observe/apmplus-server), and select the project and region in the top navigation bar. 

2. In the left navigation bar, select **Service Monitoring \> Service List** to go to the service list page.

3. Filter the service associated with the target vLLM by service name, click the service name to access the service details page, and view the vLLM golden signals on the **Service overview** tab. Such golden signals include QPS, number of requests, error rate, number of errors, number of errors per second, and response latency.

4. On the **Trace analysis** tab, click the target trace ID to go to the details page of a single trace. View the vLLM instrumentation data in the list view.

5. (Optional) If the `collect-detailed-traces` parameter is added in Step 2, two additional attributes are added to the inference span.


&nbsp;

&nbsp;
