---
title: "Chart settings"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Chart_settings"
---

Custom dashboards provide a wide range of chart types including time series charts, metric cards, tables, pie charts, and bar gauge charts. They support chart configurations such as styles, decimal precision, and units to meet usage demands in various scenarios. This topic describes chart types and relevant chart configurations.

<span id="y9Jdj0FH"></span>
## Time series graph

A time series graph displays data trends over time (X\-axis: time, Y\-axis: metric value). It is mainly used to present the "pattern of metric fluctuations over time" and is suitable for identifying trend exceptions. Applicable scenarios cover metric trend analysis and exception investigation, identifying periodic patterns, and reviewing points that triggered alerts.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Tooltip |The tooltip\-related configurations, that is, the temporary data window displayed when the mouse hovers over the chart.<br><br><br>* **Tooltip mode:**  The default mode is "all". You can select **single** to display the series closest to the pointer or select **hide** to hide the tooltip.<br><br>* **Tooltip sorting**: Takes effect only when "Tooltip mode" is set to "All". "Ascending" is selected by default. If you select "No sorting", tooltip items are arranged in the order of attributes returned by the data source. |
||Legend |The legend\-related configuration.<br><br><br>* **Legend mode**: "List" is selected by default. If you select "**Hide**", the legend will not be displayed. If you select "**Table**", the legend will be displayed in table format.<br><br>* **Legend position**: Controls where the legend is placed. You can select "Bottom" or "Right" as needed.<br><br>* **Show calculated values in legend**: This parameter is available when "Legend mode" is set to "Table". Multiple calculation methods are available **.**  The following calculation methods are currently supported:<br><br>   * **Last\*** : Extracts the last valid value that is neither null nor zero in the data series. Use this method to obtain the final valid status and eliminate interference from null and zero values.<br><br>   * **Last**: Extracts the raw value of the last record in the data series, which may include null and zero values. Use this method to strictly restore the last piece of original data.<br><br>   * **First\*** : Extracts the first valid value that is neither null nor zero in the data series. Use this method to capture the initial valid status and filter out invalid null and zero values.<br><br>   * **First**: Extracts the raw value of the first record in the data series, which may include null and zero values. Use this method to strictly restore the first piece of original data.<br><br>   * **Min**: Takes the minimum value among all non\-null values within the specified range. Use this method to collect the lower limit of the data, which reflects the lowest level of the metric.<br><br>   * **Max**: Takes the maximum value among all non\-null values within the specified range. Use this method to collect the upper limit of the data, which reflects the highest level of the metric.<br><br>   * **Mean**: Calculates the average of all non\-null values within the specified range. Use this method to measure the average level of metrics and reflect the average state of overall operation.<br><br>   * **Total**: Sums all non\-null values within a specified range. Use this method to calculate the total amount of data, which reflects the overall aggregated scale.<br><br>   * **Count**: Counts the number of non\-null data records within the specified range. Use this method to calculate the amount of valid data and assess data coverage.<br><br>   * **All Zeros**: Checks if all values within a specified range are zero. Use this method to verify whether there are no valid values and to identify all\-zero scenarios.<br><br>   * **All Nulls**: Checks if all records within a specified range are null. Use this method to verify if data is completely missing and to identify no\-data scenarios. |
||Chart style |Configure custom styles for the time series chart as needed. Available configuration items include "Line width", "Fill opacity", "Gradient mode", and "Connection method". |
||Standard configuration |Configure the decimal place, unit, data upper limit, and color scheme of data as needed. |
||Data link |Customize the data link configuration based on the actual scenario. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Threshold settings |Add threshold points as needed. Thresholds are displayed as dashed lines on the y\-axis. |
|Overrides |Override configuration |Configure override settings for different fields by fieldName. Display names and color schemes can be overridden. |


<span id="132iSomk"></span>
## Bar chart

A bar chart is a chart that compares data values by category dimensions (the horizontal axis represents categories, and the vertical axis represents metric values). It is mainly used to display the comparative differences of metric values across various categories and supports quick identification of magnitude gaps among data values. It is commonly applied to scenarios including multi\-category data comparison, TopN metric ranking, and difference analysis between different groups.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Tooltip |The tooltip\-related configurations, that is, the temporary data window displayed when the mouse hovers over the chart.<br><br><br>* **Tooltip mode:**  The default mode is "all". You can select **single** to display the series closest to the pointer or select **hide** to hide the tooltip.<br><br>* **Tooltip sorting**: Takes effect only when "Tooltip mode" is set to "All". "Ascending" is selected by default. If you select "No sorting", tooltip items are arranged in the order of attributes returned by the data source. |
||Chart style |Configure custom styles for the time series chart as needed. Available configuration items include stacking, orientation, and the X\-axis.<br><br><br>* **Stacking**: Controls whether multiple data series are displayed in a stacked manner. When enabled, the values of each series are stacked in order. When disabled, the values of each series are plotted separately.<br><br>* **Direction**: Controls the drawing direction of the time series chart. Available options include Automatic, Vertical, and Horizontal.<br><br>* **X\-axis**: Controls the data type displayed on the horizontal axis. |
||Legend |The legend\-related configurations.<br><br><br>* **Legend mode**: "List" is selected by default. If you select "**Hide**", the legend will not be displayed. If you select "**Table**", the legend will be displayed in table format. You can configure "**Show calculated values in legend**". Currently supported calculation methods include Last\*, Last, First\*, First, Min, Max, Mean, Total, Count, All Zeros, and All Nulls.<br><br>* **Legend position**: Controls where the legend is placed. You can select "Bottom" or "Right" as needed. |
||Standard configuration |‌Configure the number of decimal places, unit, and color scheme for data as needed. |


<span id="P4i89gAt"></span>
## Stat

Stat is a concise display component of a single value or key indicator, usually presented in the form of value + unit + status indicator. It focuses on whether the current value is normal, making it ideal for quickly capturing the instant state of a core metric. Applicable scenarios cover monitoring core health metrics, tracking key thresholds, and displaying summary metrics.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Stat style |The metric card style can be adjusted via graphic mode.<br><br><br>* **Graphical mode**: "**Display chart**" is selected by default. If you select "**Value only**", only data values are displayed.<br><br>* **Show change rate**: The change rate switch, which is turned off by default. When the switch is turned on, the change rate between the first non\-null value and the last non\-null value will be displayed. Additionally, when the switch is turned on, you can configure the change rate prefix as needed.<br><br>* **Text alignment**: The text alignment method. "Align center" and "Align left" are available.<br><br>* **Font size**: The font size for displayed text. "auto" is selected by default. You can adjust it as needed. |
||Data value settings |Customize the calculation method of data values. Currently supported calculation methods include Last\*, Last, First\*, First, Min, Max, Mean, Total, Count, All Zeros, and All Nulls. |
||Standard configuration |Configure the number of decimal places and the unit for the data based on your actual requirements. |
||Data link |Customize the data link configuration based on the actual scenario. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Threshold settings |Add threshold points as needed. Thresholds are indicated by the color of the data value. |
|Overrides |Override configuration |Configure override settings for different fields by fieldName. Decimal precision, units and thresholds can be overridden, which is highly practical for metric card and table scenarios. |


<span id="4bHw8ikm"></span>
## Table

Table is a list\-style display component for multi\-field structured data. It supports sorting, filtering, and highlighting by field, making it suitable for presenting detailed data with dimensional attributes. It is typically used for detailed comparison of multidimensional metrics, log or event detail queries, key node analysis in distributed tracing, and batch object status monitoring.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Cell Options |Customize cell style configurations.  <br><br><br>* **Cell type**: "Auto" is selected by default. You can set text coloring or background coloring based on actual scenarios.<br><br>* **Column Width**: "Auto" is selected by default. You can customize the table column width based on actual scenarios. |
||Standard configuration |Configure the number of decimal places and the unit for the data based on your actual requirements. |
||Data link |Customize the data link configuration based on the actual scenario. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Threshold settings |Add threshold points as needed. Thresholds are indicated by the background color of the cell. |
|Overrides |Override configuration |Configure override settings for different fields by fieldName. Display names, decimal precision, units, column widths, and thresholds can be overridden. |


<span id="qWKrAYGg"></span>
## Pie chart

A pie chart displays the proportional relationship of parts to the whole based on proportions (the whole is 100%, and each sector represents the proportion of each category). It is mainly used to present the composition ratio of each category within the whole. It is suitable for comparing the weight of different parts and is commonly used for overall structure analysis, category proportion comparison, and component breakdown.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Pie chart style |Select the pie chart style as needed. Options: pie chart and donut chart. |
||Data value settings |Customize the calculation method of data values. Currently supported calculation methods include Last\*, Last, First\*, First, Min, Max, Mean, Total, Count, All Zeros, and All Nulls. |
||Standard configuration |‌Configure the number of decimal places, unit, and color scheme for data as needed. |
|Overrides |Override configuration |Configure override settings for different fields by fieldName. Decimal precision and units can be overridden. |


<span id="kDyYOlZg"></span>
## Gauge

A gauge displays a single value within a specified range using a circular progress ring. This is suitable for displaying real\-time status, attainment rates, and resource usage.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Data value settings |Customize the data granularity, fields, and number of entries displayed in the gauge.<br><br><br>* Show: Specifies the data granularity displayed in the gauge.<br><br>   * Calculated value: Aggregates each time series using a custom calculation method and displays a single result value.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Currently supported calculation methods include Last\*, Last, First\*, First, Min, Max, Mean, Total, Count, All Zeros, and All Nulls.      </div><br>      <br><br>   * All values: Displays every raw data point within the time range. Each data point corresponds to one gauge card.<br><br>* Field: Specifies the field used for display. Once the field is configured, the system displays the data content of the selected field.<br><br>* Items per page: Takes effect only when **Show** is set to **All values**. Limits the maximum number of gauge cards displayed. Default value: 25. |
||Gauge |Customize the layout orientation, threshold label display, threshold marker display, and neutral point of the gauge.<br><br><br>* Orientation: Specifies how multiple gauge cards are arranged. Default value: **Auto**.<br><br>* Show threshold label: When this option is enabled, a value label is displayed for each threshold on the gauge scale.<br><br>* Show threshold marker: When this option is enabled, a tick mark is displayed on the gauge arc at the position of each threshold.<br><br>* Neutral point: When this parameter is left empty, the lower bound of the value range is used as the starting point of the arc. |
||Text Size |Customize the text size of the gauge title and data values. |
||Standard configuration |Customize the display name, decimal places, unit, minimum value, maximum value, no\-value display, and color scheme of the gauge. |
||Threshold settings |Add threshold points as needed. Thresholds are displayed as data values and gauge colors. |
|Overrides |Override configuration |Override configurations for individual fields by fieldName. Supported overrides include: display name, decimal places, unit, minimum value, maximum value, no\-value display, color scheme, thresholds, and neutral point. |


&nbsp;

<span id="mkWf9dXf"></span>
## Bar meter chart

A bar meter chart displays the magnitude of values based on categories (with the category on the x‑axis and the metric value on the y‑axis). It is mainly used to present value differences between different categories. It is intuitive for comparing values across categories. Common use cases include category value comparison, ranking display, and horizontal magnitude analysis.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Chart settings |Customize the chart display style.<br><br><br>* **Items per page**: The number of data items to display. If it is left blank, all data is displayed. For example, when this parameter is set to 3, the top 3 data items based on the current sort order are displayed.<br><br>* **Sort**: The sort order for data. The default is descending. Options: ascending, descending, and no sorting.<br><br>* **Navigation bar height**: Navigation bar display height. The default is 4px. You can configure this parameter as needed. |
||Data value settings |Customize the calculation method of data values. Currently supported calculation methods include Last\*, Last, First\*, First, Min, Max, Mean, Total, Count, All Zeros, and All Nulls. |
||Standard configuration |Configure the number of decimal places, the unit, and the upper limit for the data based on your actual requirements. If the upper limit is not set, the maximum value is used by default. |
||Data link |Customize the data link configuration based on the actual scenario. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Threshold settings |Add threshold points as needed. Thresholds are indicated by the color of the meter bar. |
|Overrides |Override configuration |Configure override settings for different fields by fieldName. Decimal precision, units, upper value limit, data links, and thresholds can be overridden. |


<span id="Yg8sdoui"></span>
## Text

The text component is used to display text content in Markdown format on dashboards. It supports rich text styles including custom layout, hyperlinks, and lists. It is mainly adopted to supplement dashboard background, metric definitions, operation guides, or key reminders, improving the readability and information integrity of dashboards. It is commonly applied to scenarios such as dashboard descriptions, explanations of metric definitions, scenario introductions, and important announcements.


|Type |Parameter |Description |
|---|---|---|
|All |Panel configuration |Customize the chart name, description, and panel link. For detailed description of link configuration, see [Link configuration](https://docs.byteplus.com/en/docs/Observability_Platform/Link_configuration). |
||Stat style |Stat style supports modification via graphics mode. The default option of graphics mode is **Display chart**. Choose the **value only** option to display the numerical value only. |
||Standard configuration |Configure the number of decimal places and the unit for the data based on your actual requirements. |
||Threshold settings |Add threshold points as needed. Thresholds are indicated by the color of the data value. |
