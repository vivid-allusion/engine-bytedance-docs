---
title: "Data transformation"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Data_conversion"
---

Custom dashboards offer data transformation capabilities. You can sort, merge, reorganize, or perform other operations on queried data to facilitate chart visualization. This topic describes how to use the data transformation feature.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can configure multiple transformation rules. Each rule processes the output of the previous rule.</div>


<span id="2onADW1o"></span>
## Add field from calculation

Based on the values of existing fields in the current row, new fields are generated through calculation. This is commonly used for scenarios such as metric derivation, unit conversion, and data normalization.

This data transformation method provides multiple modes, including Binary operation, Unary operation, Reduce row, Row index, Cumulative functions, and Window functions. Select an appropriate mode based on your specific scenario.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The "Replace all fields" toggle is off by default. You can turn it on as needed.</div>



* <div data-tips="true" data-tips-type="default">Off: All fields of the original data are retained, and the newly generated calculation field is appended only to the end of the data. This applies to scenarios where you need to keep both the original and derived metrics for comparison and traceability.</div>


* <div data-tips="true" data-tips-type="default">On: All original business fields are removed. Only essential index fields, such as time and primary keys, and the newly generated calculation field are retained. The original value or dimension fields no longer appear in the result. This applies to scenarios where you focus only on the final calculation result and need to streamline the data source to prevent redundant fields from interfering with chart rendering or table display.</div>



<span id="85S0PMsq"></span>
## Reduce

This data transformation method uses functions such as max, min, mean, or last to reduce all rows or data points to a single value. This commonly applies to scenarios such as global total statistics, global extreme value extraction, and single metric summary. This data transformation method supports two modes: Series to rows and Reduce fields. Select an appropriate mode based on your specific scenario.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The "Convert tag to field" toggle is off by default. You can turn it on as needed.</div>



* <div data-tips="true" data-tips-type="default">Off: After reduction, only the series identifier and the aggregated numerical result are output. The dimension labels of the original time series (for example, agent_id, instance, and tool_name) are not split into separate columns. They are embedded in the series name as a concatenated string. This applies to scenarios where you only need to display simple aggregation results and do not need to further filter, sort, or join by dimensions.</div>


* <div data-tips="true" data-tips-type="default">On: After reduction, each dimension label of the original time series is split into a separate column field, and the aggregated value column is retained. The labels change from series metadata into structured table fields. This applies to scenarios where you need to perform subsequent data processing based on dimensions, or where the table needs to explicitly display separate dimension columns.</div>



<span id="oiw4Bujc"></span>
## Merge

When multiple query statements are configured, the system defaults to displaying different query configurations as individual tables in the panel. You can toggle between tables using the drop\-down list at the bottom of the panel. By configuring data merging, you can merge the results of multiple queries.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To enable data merging, simply click "Add conversion". No further settings are needed. When only one query statement is configured, data merging does not take effect by default.</div>


The merging logic is as follows: If the common fields of two data rows are equal, the rows are merged into a single row. Otherwise, they remain as separate rows. The missing fields will be set to null. Example:


* **Query A**



|**Time** |**Job** |**Value A** |
|---|---|---|
|2024\-01\-01 11:34:20 |node |10 |
|2024\-01\-01 11:44:20 |postgre |2 |



* **Query B**



|**Time** |**Job** |**Value B** |
|---|---|---|
|2024\-01\-01 11:34:20 |node |15 |
|2024\-01\-01 11:44:20 |postgre |5 |



* **Merged result**



|**Time** |**Job** |**Value A** |**Value B** |
|---|---|---|---|
|2024\-01\-01 11:34:20 |node |10 |15 |
|2024\-01\-01 11:44:20 |postgre |2 |5 |


<span id="JtcgdWZO"></span>
## Sort by

You can use the field sorting capability to define the row order of a table. You can select which column's data to use as the sorting basis and enable descending order.

<span id="kZFGdmR7"></span>
## Rename fields by regex

You can match existing field names by using [regular expressions](https://tc39.es/ecma262/#sec-regexp-regular-expression-objects) to replace, extract, and rename fields in bulk. This method is suitable for standardizing field names in bulk. This commonly applies to scenarios such as unifying field naming conventions across data sources, trimming redundant prefixes or suffixes, and standardizing fields across multiple instances in bulk.

For example, if the match rule is set to `^metrics_(.+)` and the replacement template is set to `$1`, the `metrics_` prefix is removed from the field name. For example, if the original field name is` metrics_cpu_usage`, the field name becomes` cpu_usage `after this rule is applied.

<span id="ZXkwmxxQ"></span>
## Filter data by query

Filter data by the selected query condition to display only matching results. This is suitable for scenarios such as quickly locating target data or narrowing the scope of results. If no query conditions are selected, all data is displayed by default.

<span id="AKccjA6T"></span>
## Filter data by values

Filter data rows by field values. You can keep or exclude rows that match the specified conditions. This is useful for visualizations focused on a specific data range. Click  **+ Add condition** to add a filter rule. The logical relationship between multiple rules is determined by the **Condition combination** settings.

<span id="t7JAlCIx"></span>
## Group by

You can group data by specified dimension fields and then perform aggregate calculations on each group, such as sum, mean, percentile, maximum, and minimum. The output contains one row for each group. This commonly applies to scenarios such as breaking down metrics by multiple dimensions, aggregating by time granularity, and hierarchical statistics.

<span id="dEjAygRv"></span>
## Grouping to matrix

This transformation uses three specified dimensions to reorganize flat, row\-based raw metric data into a two\-dimensional matrix pivot table, enabling cross\-comparison across two dimensions.

One field is used as the column dimension, one as the row dimension, and one as the display value within the cells. After transformation, the originally row‑expanded data is converted into a table format better suited for horizontal comparison and cross‑analysis. This is suitable for two‑dimensional categorical display scenarios.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Grouping to matrix takes effect when only a single frame exists.</div>


The following example uses "Pod instance" as the row dimension, "Protocol type" as the column dimension, and "Received traffic KB/s" as the cell value. It displays how the original flat data is restructured after the grouping\-to\-matrix transformation.

Original flat data:


|**Pod instance (row dimension)**  |**Protocol type (column dimension)**  |**Received traffic (KB/s) (cell value)**  |
|---|---|---|
|o11y\-agent\-01 |grpc |31.2 |
|o11y\-agent\-01 |http |0.3 |
|o11y\-agent\-02 |grpc |30.8 |
|o11y\-agent\-02 |http |0.1 |


Data after the grouping\-to\-matrix transformation:


|**Pod instance\Protocol** |**grpc** |**http** |
|---|---|---|
|o11y\-agent\-01 |31.2 |0.3 |
|o11y\-agent\-02 |30.8 |0.1 |


<span id="zPMZ7MLd"></span>
## Organize fields

You can rename columns, rearrange column order, and hide columns in a table by using the field reorganization feature. For example, you can hide the Time column, rename "cluster" to "Cluster", and adjust the column order by dragging the target columns.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The field reorganization feature only takes effect on a single data frame. Consider performing a data merge first if needed.</div>


<span id="BvyBzJLI"></span>
## Series to rows

This data transformation method merges multiple series into a single series and appends a column of metric names to each value. This commonly applies to scenarios such as unified visualization of multiple metrics, standardizing multi\-series data formats, and normalizing multi\-dimensional time series data.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Series to rows does not take effect when only a single frame exists.</div>


<span id="JzNvvvun"></span>
## Limit the number of rows

Limit the number of data rows displayed. This is suitable for previewing data, querying data in a paginated form, or reducing the amount of data loaded at a time. When a limit is configured, the system returns results according to the specified row count. When no row limit is set, 10 rows of data are displayed by default.
