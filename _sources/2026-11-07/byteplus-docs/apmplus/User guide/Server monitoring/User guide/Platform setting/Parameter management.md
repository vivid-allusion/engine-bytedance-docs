---
title: "Parameter management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/parameter_management"
---

Server\-side Monitoring provides workspace\-level configuration parameters, including error thresholds, sampling rates, and data encryption. You can configure parameters as needed for your business scenarios. This topic describes the configuration details and application scope of these parameters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Some parameters support custom settings. In such cases, workspace\-level parameter settings have lower priority than custom settings. For example, if sampling rules are configured both in Parameter management and for a specific service, the custom sampling rules configured for the service take effect.</div>


<span id="upyPGfnd"></span>
## Procedure


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, select **Platform Setting \> Workspace Management** to access the workspace management page.

3. Find the workspace in the workspace list and click **Parameter management** in the Actions column on the right side of the list. Configure parameters as required for your business scenario, such as system, probe, storage, and performance profiling settings.


<span id="j39hRaFG"></span>
## System settings

Currently, error threshold settings are supported. To define error threshold ranges for Satisfied, Normal, and Poor levels, click **Modify settings**, drag the slider as needed, and click **Save**.

This parameter primarily affects data statistics in the service topology.

<span id="2w6l1hjq"></span>
## Probe settings

<span id="7Q2IRnhl"></span>
### Slow database query settings

Define the threshold for slow queries. The recommended threshold is 500ms. To modify the threshold, click **Modify setting**, configure a threshold as needed, and click **Save**.

This parameter primarily affects slow query statistics, for example, the proportion of slow queries in middleware monitoring.

<span id="AL38cEGX"></span>
### Sampling settings

Configure parameters for custom sampling rules. To do so, click **Modify settings**, configure sampling parameters (such as Fixed Sampling and Wrong slow sampling) as needed, and click **Save**. At least one sampling method must be configured. The specific activation logic is as follows:


* If only "Fixed Sampling" is configured, both the APMPlus probe and the apmplus\-opentelemetry\-collector probe take effect.

* If only "Wrong slow sampling" is configured, the APMPlus probe does not take effect, whereas the apmplus\-opentelemetry\-collector probe takes effect.

* If both "Fixed Sampling" and "Wrong slow sampling" are configured, only the fixed\-sampling configuration applies to the APMPlus probe. Both sampling methods apply to the apmplus\-opentelemetry\-collector probe, which executes them in sequence.



|Sampling method |Description |
|---|---|
|Fixed sampling |Trace data sampling is performed based on the custom sampling rate. A value of 0% means all trace data is discarded and not reported. A value of 100% means all trace data is reported without sampling. |
|Wrong slow sampling |Data is reported based on the custom lower threshold of trace duration and error sampling rules. All trace data matching the error and slow sampling rules will be reported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The duration for error and slow sampling is based on the total trace duration, not the span duration. When configuring numeric values, specify a duration range for an entire trace.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If "Wrong slow sampling" is enabled, enable at least one of the following options: lower trace duration threshold and error sampling.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If both are configured, trace data that satisfies ‌either condition‌ will be reported.</div><br> |


This parameter primarily affects sampling, for example, the source of samples in trace analysis.

<span id="8bkBzaM2"></span>
### Interface settings

To configure interface\-related settings, click **Modify settings** and set parameters including Path Convergence, List of RPC service interfaces, Invalid Interface Call Filtering, and HTTP Status Code Allowlist. After completing the configuration, click **Save**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying Path Convergence or List of RPC service interfaces settings will prevent historical data from being filtered by the new Resource values. Proceed with caution.</div>



* **Path normalization**

   If this option is enabled, HTTP service interface names are generated according to default URL normalization rules. This process aggregates relative paths by replacing numeric IDs with wildcards "?" while preserving meaningful path information.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This applies only to HTTP services invoked as servers.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The maximum length defaults to 24 characters and can be modified per account. To modify the maximum length, contact technical support.   </div>
   

   The default URL normalization rules and examples are as follows:

   * If the path section of the URL does not contain any digits, the original string is retained. For example, `/api/health-check` remains `/api/health-check` after path normalization.

   * If the path section of the URL contains digits and the length of segments containing these digits is 2 or 3 characters, the version segments starting with v or V are retained, and the segments containing digits other than version numbers are replaced entirely with the wildcard "?". For example, `/v1/items/123` will be `/v1/items/?` after path normalization.

   * If the path section of the URL contains digits and the segments containing digits are from 4 to the maximum length, the digit\-containing segments are replaced with the wildcard "?". For example, `/api/users/name-456/details` will be `/api/users/?/details` after path normalization.

   * If the path section of the URL contains digits and the length exceeds the maximum length, the digit\-containing segments are replaced with the wildcard "?". For example, `/api/very-long-resource-name-1234567890` will be `/api/?` after path normalization.

* **List of RPC service interfaces**

   The source of assignment for RPC service\-related interface names. The default option is the method level. You can select the method level or the service method level as needed.

   * **Method level**: The Resource field is assigned by rpc.method.

   * **Service method level**: The Resource field is assigned by rpc.service and rpc.method.

   This parameter primarily affects the interface names of RPC services in interface monitoring.

* **Invalid interface call filtering**

   Mark interfaces for which you do not need to record observability data as inactive. After this setting takes effect, inactive interfaces will no longer report trace data, and the corresponding metric statistics will exclude data from these interfaces, including spans and metric statistics.

   * Data impact: All metrics and spans corresponding to these interfaces are ignored.

   * Functional impact: All metrics for the corresponding interfaces on pages such as service overview, interface monitoring, upstream calls, downstream calls, as well as the span count and related metric alerts on the trace analysis page.



&nbsp;

* **HTTP status code allowlist**

   By default, status codes greater than or equal to 400 are classified as erroneous calls. To exclude specific status codes from being treated as errors, configure an HTTP status code allowlist based on actual needs. Once configured, allowlisted HTTP status codes are treated as successful in RED metrics and error statistics.

   * Data impact: Error count metrics and span status for HTTP servers/clients.

   * Functional impact: Service overview, trace analysis, span status, and more.


&nbsp;

<span id="SPjk4LiJ"></span>
### Data reporting

Data reporting settings include settings for reporting of metrics, logs, and traces. This option is enabled by default. You can disable or enable it as needed.

&nbsp;

<span id="Pp6mAx7e"></span>
### Log configuration management

The global switch for TLS access. It is enabled by default. You can disable or enable it as needed.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Disabling TLS will simultaneously delete historical log data and the log topic. Deleted data cannot be recovered. Proceed with caution.</div>


<span id="ydKjXmaC"></span>
## Storage settings

Data encryption settings are currently supported. To configure data encryption, click **Modify settings**, select an appropriate encryption method for your scenario, and then click **Save**.

This parameter primarily affects Server\-side Monitoring trace data stored in TLS. It supports two encryption methods: Service Key (SSE\-TLS) and ‌User Key (SSE\-KMS). Detailed descriptions are as follows:

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Select one data encryption method that suits your actual scenario. Once the encryption method is selected, you cannot change it, but you can enable or disable it. Proceed with caution. </div>


* <div data-tips="true" data-tips-type="danger">If the master key is deleted or disabled, customer\-managed keys will become invalid, causing read/write failures for trace data stored in TLS by Server\-side Monitoring. Therefore, make sure that the keys are available and enabled.</div>




|Encryption method |Description |
|---|---|
|Service Key (SSE\-TLS) |The default encryption method provided by TLS. This method requires no additional configuration and enables a transparent encryption experience. It is suitable for scenarios that require rapid deployment of data encryption without self\-managed keys (managed by the service provider) and long\-term key stability.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This encryption method is free of charge.</div><br> |
|User Key (SSE\-KMS) |Keys generated using Key Management Service (KMS). KMS provides secure key storage, generation, encryption, and rotation. This solution offers full lifecycle control and proactive management. It is suitable for self\-managed key scenarios that require security compliance, periodic permission audits, and reduced leakage risks.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">KMS activation is free. However, using KMS for server\-side encryption incurs API call fees, and creating a KMS key incurs key hosting fees. KMS charges these fees. </div><br><br><br>* <div data-tips="true" data-tips-type="default">To use this encryption method, create a customer master key in advance and obtain the key ID.</div><br> |


<span id="LbtakEJu"></span>
## Performance profiling

After you enable **Continuous CPU profiling**, you can collect CPU performance metrics for specified services and pods and create profiling tasks in **Infrastructure Monitoring**. For related operations, see [Performance profiling](https://docs.byteplus.com/en/docs/apmplus/Performance_profiling?TagIDs=2,237&lang=en&type=preview).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before enabling this toggle, ensure that the apmplus\-opentelemetry\-collector add\-on in the VKE cluster where the target service resides has been upgraded to V3.2.0 and that the DaemonSet deployment has been enabled. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on?lang=en">Upgrading the add\-on</a> and <a href="https://docs.byteplus.com/en/docs/vke/apmplus-opentelemetry-collector-add-on?lang=en">apmplus\-opentelemetry\-collector</a>.</div>


* <div data-tips="true" data-tips-type="warning">Continuous CPU profiling incurs additional resource overhead. Enable it as needed.</div>


* <div data-tips="true" data-tips-type="warning">After this toggle is disabled, the system stops collecting CPU profiling data, and no new profiling tasks can be created.</div>



&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
