---
title: "Reporting self-managed gateway usage data"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Reporting_self-managed_gateway_usage_data"
---

By reporting self\-managed gateway data to Server\-side Monitoring, you can collect usage metrics for token input, output, and cache calls and visualize metrics based on the platform's observability capabilities to reflect actual business usage and access trends and intuitively monitor resource consumption. This topic describes how to report usage data from a self\-managed gateway to Server\-side Monitoring.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic provides standard definitions for usage data reporting in self\-managed gateway scenarios. For additional metric reporting requirements, refer to this specification for supplementary configurations.</div>


<span id="FJCKvQQg"></span>
## Background information

ArkClaw Enterprise allows you to bind self\-managed gateways and expose your model pools to employees. However, data of self\-managed gateways currently falls outside the observability scope. To display token usage, you need to report token usage data of self\-managed gateways to Server\-side Monitoring. After data is reported, you can view data details in the preset dashboard in Server\-side Monitoring or the usage analysis dashboard in ArkClaw Enterprise.

<span id="ZGUalUgf"></span>
### Metric description

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Counters are monotonically increasing synchronous metrics. They can be exported by using the SDK in cumulative or incremental mode. However, business applications must always allow calls to the add method only for the current increment. Calling add for the cumulative total or passing negative values is not allowed.</div>



|**Metric name** |**Type** |**Unit** |**Description** |
|---|---|---|---|
|custom_gateway_token_used |Counter |1 (number) |Token consumption of the self\-managed gateway. |


<span id="jCWyiry7"></span>
### Label fields


|**Label** |Required |**Sample value** |**Description** |
|---|---|---|---|
|apmplus_business_carrier |Yes |arkclaw_enterprise |Set this field to `arkclaw_enterprise`. This information needs to be included in the resource attributes. |
|service |Yes |claw_instance_xxx |ID of the Claw instance. This information needs to be included in the resource attributes. |
|claw_space_id |Yes |space_xxx |The workspace to which the Claw instance belongs. |
|token_type |Yes |input<br><br> |Token type. Enumeration values include:<br><br><br>* input: Input token consumption.<br><br>* output: Output token consumption.<br><br>* cache_read: Cached token consumption. |
|model |Yes |doubao\-pro\-32k |Model name. |
|provider |Yes |ark |Model provider.<br><br> |
|from |Yes |gateway\-prod\-bj |Data source. We recommend specifying the name or unique and stable ID of the self\-managed gateway. Dynamic addresses are not allowed. |
|user_name |Yes |zhangsan |Username. This is a user metadata field.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">User metadata fields such as username, email, and department can be obtained by calling the <a href="https://docs.byteplus.com/en/docs/87732/2516784?lang=en">ListUsers</a> API.</div><br> |
|user_email<br><br> |Yes |zhangsan@example.com |Email address of the user. This is a user metadata field. |
|user_department<br><br> |Yes |gateway\-prod\-bj |Department of the user. This is a user metadata field. |


<span id="Izy268Rm"></span>
## Prerequisites

The following key information is required for reporting usage data from self\-managed gateways.


|Key information |Sample value |Description |
|---|---|---|
|ArkClaw SpaceID |csi\-yehw6ow1kwa5g0\*\*\*\* |ID of the ArkClaw space. You can get it directly from the ArkClaw Enterprise console. For more information, see [Space information](https://docs.byteplus.com/en/docs/ArkClaw/Space_information).<br><br>You can use this information to query details about ArkClaw instances, users, and spaces in batches. For example, you can use the [ListClawInstances](https://docs.byteplus.com/en/docs/87732/2466959?lang=en) API to obtain Claw instance IDs. |
|APMPlus AppKey |378c\*\*\*\*\*\*c45589\*\*\*\*\*\*c08d\*\*\*\*\*\* |When testing data reporting from a self\-managed gateway, we recommend creating a dedicated workspace for verifying data writes and accuracy. This prevents subsequent test data from being mixed with production data, thereby compromising dashboard quality.<br><br>For information about creating a workspace and getting an AppKey, see [Managing workspaces](https://docs.byteplus.com/en/docs/apmplus/Workspace_management?lang=en). |
|||To report data from a self\-managed gateway directly to the production environment, refer to the following steps to obtain the AppKey for the Claw space.<br><br><br>1. Call the [GetClawSpace](https://docs.byteplus.com/en/docs/87732/2532487?lang=en) API to obtain the ApmID for the Claw space.<br><br>2. On the Server\-side Monitoring workspace management page, find the workspace with the same name as the ApmID.<br><br>3. Obtain the AppKey for this workspace. Each workspace corresponds to one AppKey. For information about obtaining the AppKey, see [Workspace management](https://docs.byteplus.com/en/docs/apmplus/Workspace_management?lang=en). |
|APMPlus endpoint |apmplus\-cn\-beijing.volces.com:4317 |The target endpoint of metric reporting. For information about getting the endpoint, see [Getting APMPlus endpoints](https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center?lang=en#59K0hBuu).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For reporting data directly to Server\-side Monitoring via a domain name, ensure the header includes <code>"X-ByteAPM-AppKey": ${app_key}</code>.</div><br> |


<span id="Sdoy4F5R"></span>
## Procedure

Data reporting uses the OpenTelemetry protocol. For integration details, see [metrics API](https://opentelemetry.io/docs/specs/otel/metrics/api/) or the Server\-side Monitoring [integration documentation](https://docs.byteplus.com/en/docs/apmplus/Integrate_Python_applications?lang=en#mPM2DyRw). The following illustrates the development process using Python as an example:


1. Run the following code to install dependencies.

   ```Plain Text
   pip install opentelemetry-api
   pip install opentelemetry-sdk
   pip install opentelemetry-exporter-otlp
   ```
   

2. Create a [MeterProvider](https://opentelemetry.io/docs/specs/otel/metrics/api/#meterprovider) in the code.

   The demo in the [OpenTelemetry official documentation](https://opentelemetry.io/docs/languages/python/instrumentation/) prints metrics to the console. However, for reporting to Server\-side Monitoring, in addition to replacing grpc/http exporter information, you need to configure information such as the endpoint and headers. The following is a creation example:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>init_metrics()</code> must be called once during the process startup stage. In multi\-worker deployment, each process initializing its own Provider instance is normal behavior. However, calling <code>metrics.set_meter_provider()</code> repeatedly within the same process is prohibited.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>service.instance.id</code> must be set to a unique identifier of the current instance. We recommend using a UUID or the pod name. Otherwise, data queries may behave unexpectedly.   </div>
   

   ```Python
   import uuid
   
   from opentelemetry import metrics
   from opentelemetry.sdk.metrics import MeterProvider
   from opentelemetry.sdk.metrics.export import (
       ConsoleMetricExporter,
       PeriodicExportingMetricReader,
   )
   from opentelemetry.sdk.resources import Resource
   from opentelemetry.exporter.otlp.proto.grpc.metric_exporter import OTLPMetricExporter
   
   def init_metrics():
       # Sets the target reporting address to the APMPlus endpoint.
       endpoint = "apmplus-cn-beijing.volces.com:4317"  # Endpoint. For information about how to get it, see the instructions in Prerequisites.
       headers = {
          "x-byteapm-appkey": "<app_key>",   # The AppKey of the Claw space or test workspace. For information about how to get it, see the instructions in Prerequisites.
       }
       # Sets the resource attributes.
       resource_attributes = {
           "service_name": "<claw_instance_id>", # Use claw_instance_id to populate this field. This information will be populated into the service label during data writing.
           "apmplus_business_carrier": "arkclaw_enterprise",  # Identifies ArkClaw Enterprise data.
           "service.instance.id": str(uuid.uuid4()),   # When the process starts, a random UUID will be generated to identify this process instance.
       }
       resource = Resource.create(resource_attributes)
       exporter = OTLPMetricExporter(endpoint=endpoint, headers=headers)
       metric_reader = PeriodicExportingMetricReader(exporter)
       provider = MeterProvider(metric_readers=[metric_reader], resource=resource)
       # Sets the global default meter provider
       metrics.set_meter_provider(provider)
       
       # Creates a meter from the global meter provider
       meter = metrics.get_meter(
           "arkclaw.custom_gateway", version="1.0.0"
       )
       token_used_metrics = meter.create_counter(
           name="custom_gateway_token_used",
           unit="1",
           description="Token usage reported by an ArkClaw custom gateway",
       )
       return provider, token_used_metrics
   ```
   

3. Perform metric instrumentation.

   After obtaining valid usage data returned by the model provider in the code, call `record_token_usage()` to perform metric instrumentation. Example:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Metric instrumentation should function as bypass logic and must not impact the main tracing.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Counter attributes can be used for aggregation and filtering in preset dashboards.   </div>
   

   ```Python
   def record_token_usage(
       token_used_metrics,
       *,
       token_type: str,
       token_count: int,
       claw_space_id: str,
       claw_instance_id: str,
       model: str,
       provider: str,
       gateway_id: str,
       user_name: str | None = None,
       user_email: str | None = None,
       user_department: str | None = None,
   ) -> None:
   
       # Set metric labels.
       attributes = {
           "claw_space_id": claw_space_id,
           "token_type": token_type,
           "service": claw_instance_id,
           "model": _required_string("model", model),
           "provider": _required_string("provider", provider).lower(),
           "from": _required_string("gateway_id", gateway_id),
       }
   
       # Attributes from the user dimension. You can add other dimensions as needed.
       optional_attributes = {
           "user_name": user_name,
           "user_email": user_email.lower() if user_email else None,
           "user_department": user_department,
       }
       attributes.update(
           {
               key: str(value).strip()
               for key, value in optional_attributes.items()
               if value is not None and str(value).strip()
           }
       )
   
       # Pass in the increment for this call, not the historical cumulative value.
       token_used_metrics.add(token_count, attributes=attributes)
   ```
   

4. Flush and shut down the provider.

   Data writing is an asynchronous aggregation operation. For testing convenience, you may immediately ‌flush data after writing to prevent loss from test service termination. Additionally, to ensure zero data loss, the gateway service must flush and shut down the metric provider before restarting/shutdown for a graceful restart or shutdown.

   ```Python
   # Test or short tasks: Wait for the current metric to be exported for immediate verification.
   metric_provider.force_flush(timeout_millis=10000)
   
   # Graceful service shutdown: Make a call once in the ASGI/WSGI/Kubernetes shutdown hook.
   metric_provider.shutdown(timeout_millis=10000)
   ```
   


<span id="iTzty7UH"></span>
## Result verification

After the self\-managed gateway's usage data is successfully reported, you can view the data details in the dashboard.


* If data is reported to a test workspace, you can search for the **Token usage from custom gateway** dashboard on the "Built\-in dashboard" tab of Observability Platform to view data details visually. For details, see [Preset dashboards](https://docs.byteplus.com/en/docs/Observability_Platform/Preset_dashboards).

* If data is reported directly to the production environment, you can go to the **Usage** dashboard in ArkClaw Enterprise to view data details visually. For detailed instructions, see [Viewing ArkClaw usage analysis](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_usage_data).
