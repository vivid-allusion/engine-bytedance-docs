---
title: "Metric production"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Tag_cardinality_limit"
---

Server\-side Monitoring dynamically generates high\-value metrics by aggregating raw data from designated application clusters according to metric generation rules. This resolves difficulties in capturing and quantifying sporadic system errors and the inability to track experience data over time in specific business scenarios. Additionally, you can quickly integrate generated metric data into custom dashboards for visualization or configure alert rules to enable real\-time detection of anomalies in seconds, eliminating monitoring blind spots at the source. This topic describes how to generate metrics from raw data.

<span id="jF7SR4PY"></span>
## Prerequisites

The latest `apmplus-opentelemetry-collector` version has been installed in the cluster and can collect data normally. For details about the add\-on, see [Installing the add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on) and [Upgrading the add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="HIn1oSTw"></span>
## Limits


* The metric production feature is effective only for data collected by the `apmplus-opentelemetry-collector` add\-on.

* Currently, metrics can be produced from logs and trace data.


<span id="A1QTa2Zt"></span>
## Procedure


<Tabs>
<Tab zoneid="jnSNROhhnD" title="Produce metrics from log data">
<TabTitle>Produce metrics from log data</TabTitle>

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, click **Metric Production** to go to the metric production management page.

3. Click **Create production metrics**. Refer to the following instructions to configure parameters. Then, click **Confirm**.

* **Basic information**: Configure basic information and raw data sources for metric generation. For example, you can choose to generate metrics from log data reported through the SDK.



|Parameter |Description |
|---|---|
|Rule name |Provide a custom rule name. |
|Application cluster |The cluster sources of raw data used for metric generation. By default, all clusters are selected.<br><br><br>* To select all clusters, check **Select all**. All clusters where the apmplus\-opentelemetry\-collector add\-on is currently or subsequently installed will apply the metric generation rule.<br><br>* To specify a target cluster, select the target clusters. You can select multiple ones. The metric production rule applies only to the selected clusters. |
|Data source |The raw data source for metric generation. In this scenario, select **Log**. |
|Data range |The data scope for producing metrics. Currently, **SDK report** is supported. For example, in clusters where the apmplus\-opentelemetry\-collector add\-on is installed, use log data reported through the SDK for metric generation. |
|Filter criteria |Filter raw data used for metric generation based on the configured SDK filtering rules. For example, you can filter for logs by log content, service name, and log level.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can configure multiple filtering rules. Multiple rules apply "AND" logic, meaning only data that meets all filtering rules will be retained.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A single filtering rule supports only the "Include" or "Exclude" operator.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A single rule can have multiple values, which apply ‌"OR" logic.</div><br> |



* **Data processing**: Process the raw data that matches the basic information settings to extract fields suitable for metric generation.



|Parameter |Description |
|---|---|
|Field extraction |Click **Add field** to configure field extraction rules and field\-related information. This configuration controls how raw data is processed as metric production\-compliant fields. |
|Extraction rule |The rule for extracting raw data. The rule adopts a triple form. Among them, N represents the left boundary position, L represents the left boundary marker, R represents the right boundary marker, and the content between the left and right boundaries is the extraction result.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Extracting Chinese content is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">N starts counting from 0, meaning 0 represents the first, 1 represents the second, and so on.</div><br><br><br><br> **[Reference example]** : Assume the original log content is `INFO 2025-01-02 03:04:05 ETC station=X-station lsn=A00001 cost=10s`.<br><br><br>* When the extraction rule is `(0, "", " ")`, it means extracting the content from the beginning to the next space. The extraction result is `INFO`.<br><br>* When the extraction rule is `(0, " ", " ")`, it means extracting the content from the first space to the next space. The extraction result is `2025-01-02`.<br><br>* When the extraction rule is `(2, " ", " ")`, it means extracting the content from the second space to the next space. The extraction result is `ETC`.<br><br>* When the extraction rule is `(0, "station=", " ")`, it means extracting the content from the first station= to the next space. The extraction result is `X-station`.<br><br>* When the extraction rule is `(0, "lsn=", " ")`, it means extracting the content from the first lsn= to the next space. The extraction result is `A00001`.<br><br>* When the extraction rule is `(0, "cost=", "")`, it means extracting the content from the first cost= to the end. The extraction result is `10s`. |
|Field preview |The system fills in a data sample based on the data range and automatically highlights the field content to be extracted according to the extraction rule, providing a result preview.<br><br><br>* Click **Retrieve the sample** to obtain a new data sample.<br><br>* Click **Edit preview sample** to provide custom sample data.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Extracting Chinese content is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We recommend filling in 5 data entries to preview extraction results.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Preview samples can only be obtained when log data has already been submitted to Server\-side Monitoring. Otherwise, the sample content will be empty.</div><br> |
|Field name |Provide a custom name for the extracted field. Field names cannot be duplicate within the same configuration. |
|Allowlist |‌Configure an allowlist filter for field extraction. This configuration is not enabled by default. When enabled, it filters extracted fields based on the configured allowlist. If the extracted data value range is too broad, it retains allowlist\-matched values to narrow the processing scope. |
|Value translation |Configure translation rules for field values. By default, this feature is not enabled. If this feature is enabled, extracted field values will be translated or mapped according to the configured rules, with the translated field value type being String.<br><br>To enable field value translation, you need to configure the following parameters:<br><br><br>* **Value type**: Add translation rules for numeric or string values as needed. You can add multiple translation rules that use different types.<br><br>* **Default value**: The default value to use when no translation rule is matched. If the default value is empty, values that do not match any translation rule will not be translated. If the default value is not empty, the default value will be used to fill in values that do not match any of the above translation rules.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once field value translation is enabled, the field value will be replaced with the translated value. In this case, if this field is used for data filtering, the filter condition should use the translated value rather than the originally reported value.</div><br> |



* **Data filtering**: Filter the processed data to further select data that meets metric generation criteria. Currently, allowlist and blocklist filtering are provided.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Filtering rules within the same list apply "OR" logic.</div>


* <div data-tips="true" data-tips-type="default">Filtering rules across different lists apply "AND" logic.</div>




|Parameter |Description |
|---|---|
|Allowlist |List of permitted data entries. Matching data will be retained. You can configure allowlist rules based on key\-value or keyword filtering. |
|Blocklist |List of blocked data. Data that meets the blocklist criteria will be discarded. Blocklist rules can be configured by filtering with key\-value pairs or keywords. |



* **Metric definition**: Define the metric generation rule by using the metric type, basic information, tags, and aggregation cycle, enabling standardized aggregation statistics and dimension splitting of source data.



|Parameter |Description |
|---|---|
|Metric type |The type of generated metrics. Currently, only the **Simple metric** type is supported. |
|Metric definition |Basic metric information and additional information, for example, metric name, unit, source, and aggregation method.<br><br><br>* **Metric name**: Provide a custom metric name. Metrics generated from logs will, by default, start with `log_metric_ `.<br><br>* **Aggregation method**: Select a metric data aggregation method as needed. Currently supported methods include COUNT, AVG, SUM, MIN, MAX, PCT50, PCT75, and PCT90.<br><br>* **Filter criteria**: Filter metrics by metric name. Multiple filtering rules apply "AND" logic.<br><br>* **Source field**: Aggregation methods other than COUNT require specifying the metric source field to record the source of the metric.<br><br>* **Unit**: Select the metric unit as needed. |
|Tag field |‌Metric aggregation dimension. Exercise caution when using mutable tag fields.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Pay attention to the following information when configuring tag fields:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Do not configure duplicate tag keys. Otherwise, data accuracy cannot be guaranteed.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Minimize tags. We recommend including only business\-critical information.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Tag keys must be enumerable. Otherwise, reporting tags will cause a cardinality explosion. For example, avoid configuring ever\-growing attributes (such as IDs) as tag fields.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend against using UUIDs or URLs with parameters.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Avoid using timestamps or metrics. Otherwise, the system will record timestamps for each series.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Metrics have dimension limits. Excessive TagKV combinations can cause a dimension explosion, and excess data will be discarded.</div><br> |
|Aggregation interval |Select the metric aggregation cycle based on actual requirements. |





</Tab>
<Tab zoneid="OQw5ZbgILM" title="Produce metrics from trace data">
<TabTitle>Produce metrics from trace data</TabTitle>

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, click **Metric Production** to go to the metric production management page.

3. Click **Create production metrics**. Refer to the following instructions to configure parameters. Then, click **Confirm**.

* **Basic information**: Configure basic information and raw data sources for metric generation. For example, you can choose to generate metrics from trace and span data.



|Parameter |Description |
|---|---|
|Rule name |Provide a custom rule name. |
|Application cluster |The cluster sources of raw data used for metric generation. By default, all clusters are selected.<br><br><br>* To select all clusters, check **Select all**. All clusters where the apmplus\-opentelemetry\-collector add\-on is currently or subsequently installed will apply the metric generation rule.<br><br>* To specify a target cluster, select the target clusters. You can select multiple ones. The metric production rule applies only to the selected clusters. |
|Data source |The raw data source for metric generation. In this scenario, select **Trace**. |
|Data range |The data scope for producing metrics. Currently, **Trace Span Data** is supported. |
|Filter criteria |Filter raw data for metric generation using configured span filtering rules. For example, you can filter raw data by span type, service name, interface name, span operation name, status code, downstream service name, downstream service type, downstream interface name, and whether it is an AI application.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can configure multiple filtering rules. Multiple rules apply "AND" logic, meaning only data that meets all filtering rules will be retained.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A single filtering rule supports only the "Include" or "Exclude" operator.</div><br><br><br>* <div data-tips="true" data-tips-type="default">A single rule can have multiple values, which apply ‌"OR" logic.</div><br> |



* **Data processing**: Process the raw data that matches the basic information settings to extract fields suitable for metric generation.



|Parameter |Description |
|---|---|
|Field extraction |Click **Add field** to configure field extraction rules and field\-related information. This configuration controls how raw data is processed as metric production\-compliant fields. |
|Sample preview |The system fills in a data sample based on the data range and automatically highlights the field content to be extracted according to the extraction rule, providing a result preview.<br><br><br>* Click **View trace** to jump to the trace analysis page, where you can view the original trace data.<br><br>* Click **Retrieve the sample** to obtain a new data sample.<br><br>* Click **Edit sample** to provide a custom sample.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can obtain preview samples only when trace data has been reported to Server\-side Monitoring. Otherwise, the sample content will be empty.</div><br> |
|Extraction rule |Rules for extracting raw data. Complete and partial extractions are supported. Partial extraction uses a regular expression, which can be configured by using two methods:<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For partial extraction, only one value can be extracted from the original field value using a regular expression. Extracting multiple values simultaneously is not currently supported.</div><br><br><br><br>* Enter a custom regular expression pattern.<br><br>* Select the part to extract in the sample preview region to have a regular expression pattern generated automatically. |
|Field name |Provide a custom name for the extracted field. Field names cannot be duplicate within the same configuration. |
|Allowlist |‌Configure an allowlist filter for field extraction. This configuration is not enabled by default. When enabled, it filters extracted fields based on the configured allowlist. If the extracted data value range is too broad, it retains allowlist\-matched values to narrow the processing scope. |
|Value translation |Configure translation rules for field values. By default, this feature is not enabled. If this feature is enabled, extracted field values will be translated or mapped according to the configured rules, with the translated field value type being String.<br><br>To enable field value translation, you need to configure the following parameters:<br><br><br>* **Value type**: Add translation rules for numeric or string values as needed. You can add multiple translation rules that use different types.<br><br>* **Default value**: The default value to use when no translation rule is matched. If the default value is empty, values that do not match any translation rule will not be translated. If the default value is not empty, the default value will be used to fill in values that do not match any of the above translation rules.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once field value translation is enabled, the field value will be replaced with the translated value. In this case, if this field is used for data filtering, the filter condition should use the translated value rather than the originally reported value.</div><br> |



* **Data filtering**: Filter the processed data to further select data that meets metric generation criteria. Currently, allowlist and blocklist filtering are provided.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Filtering rules within the same list apply "OR" logic.</div>


* <div data-tips="true" data-tips-type="default">Filtering rules across different lists apply "AND" logic.</div>




|Parameter |Description |
|---|---|
|Allowlist |List of permitted data entries. Matching data will be retained. You can configure allowlist rules based on key\-value filtering. |
|Blocklist |List of blocked data. Data that meets the blocklist criteria will be discarded. You can configure blocklist rules based on key\-value filtering. |



* **Metric definition**: Define the metric generation rule by using the metric type, basic information, tags, and aggregation cycle, enabling standardized aggregation statistics and dimension splitting of source data.





</Tab>
</Tabs>


<span id="IovDr05A"></span>
## What to do next

<span id="3ZHm8AHZ"></span>
### View metric trends

After the metric production rule is successfully delivered and metrics are generated normally, go to the details page of the metric production rule and click the **indicator trend** tab to preview the trends of the generated metrics.


* If metrics are generated based on logs, click **Log analysis** to go to the log query page for more details.

* If metrics are generated based on traces, click **Trace analysis** to go to the trace analysis page for more details.


<span id="LYBqPnou"></span>
### Configure custom dashboards

Go to the custom dashboard to create an observability dashboard based on the generated metrics. For more information about custom dashboards, see [Getting started quickly with custom dashboards](https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards).

<span id="we6q0fbv"></span>
### Configuring alerts

Go to the Alert Task to configure alerts based on generated metrics. For more information about alert tasks, see [Creating alert tasks](https://docs.byteplus.com/en/docs/apmplus/Alert_tasks).

<span id="D4wjUgy6"></span>
### Manage metric rules

You can perform the following management operations on the created metric production rules.


|Actions |Description |
|---|---|
|Deliver metric rule |After you create or edit a metric production rule, the rule delivery is automatically triggered. Once delivery is successful, metrics will be produced according to this rule.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The delivery status of indicator rules follows asynchronous update logic, with updates occurring at most every 5 minutes.</div><br> |
|Enable/Disable |Enable or disable a metric production rule. After you enable a rule, metrics will be generated based on this rule. Disabling a rule halts metric generation. |
|Edit |Edit the target metric production rule. After you complete the edit, the rule is re\-delivered, and metrics are produced based on the new rule. |
|Copy |Copy the target metric production rule to create a new rule quickly. |
|Delete |Delete metric production rules that are no longer needed. After deletion, metrics will no longer be produced, but previously generated metrics remain unaffected. |
