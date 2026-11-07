---
title: "View and analyze logs"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/View_and_analyze_logs"
---

The logging feature supports collecting access log data for protected resources that have been added to the LLM Application Firewall, and provides search, analysis, monitoring, alerting, and data visualization capabilities based on Log Service. These functions help you quickly understand the status and effectiveness of protection for LLM workloads, so that you can handle anomalies in a timely manner.

<span id="03ec25bf"></span>
## Precautions

When enabling the log service, a service\-linked role is automatically created. This role has permissions for creating and recycling log projects, as well as collecting logs. Do not delete this service\-linked role, as doing so will affect log collection, instance recycling, and other operations.

<span id="8f90a8a6"></span>
## Prerequisites


* The log service feature is enabled when creating an instance. For related operations, refer to [Create an LLM Application Firewall instance](https://docs.byteplus.com/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance).

* You have completed asset integration. For further steps, refer to [Introduction to assets integration](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_assets_integration).


<span id="84691483"></span>
## View log project and topic


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region to which the instance belongs.

3. Select **Log details** from the left navigation.

4. Hover over the details icon next to Log Management to view information about the log project and log topic.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/339cf68baf824ba3b056cca351355d95) </span>

   
   |**Resource types** |Description |
   |---|---|
   |Log project |* The log project, automatically created by the LLM Application Firewall, is a fundamental resource management unit. These log projects cannot be deleted.<br><br>* Click the log project name to navigate to the log service console and view project information. |
   |Log topic |* By default, a dedicated log topic is created under the LLM Application Firewall log project. The log topic is the basic unit for log management (e.g., log collection, storage, query analysis). You cannot write data to log topics (via API, SDK, or other methods) unless it is LLM Application Firewall log data. Log topics also cannot be deleted.<br><br>* Click the log topic name to navigate to the log service console and view relevant information. |
   


<span id="caccbf9d"></span>
## Retrieve and analyze logs


1. Log in to the [LLM Application Firewall console](https://console.volcengine.com/omni-shield/llm-shield/).

2. Select the instance's region from the top bar.

3. Select **Log details** from the left navigation.

4. Enter your query in the search box.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5ddf441405574a8cb48b9be1a534764d) </span>

   * To filter logs that meet specific criteria using search conditions, refer to the related documents of Log Service. 

   * To perform log statistical analysis using SQL statements, refer to the analysis feature of Log Service.

   * For detailed information about log fields, see [Log field descriptions](https://docs.byteplus.com/docs/LLM-Application-Firewall/Log_field).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When multiple search queries are separated by spaces, this indicates "or" logic, which is equivalent to <code>OR</code>. For example, <code>warning error</code> is equivalent to <code>warning OR error</code>, which means logs containing the keyword <code>warning</code> or <code>error</code> will be matched.   </div>
   

5. Click **Search**.

   The chart of query results will be displayed below.

6. (Optional) Set the time range and auto\-refresh for the query chart.

   * Time range: By default, displays query results within the past 3 days and supports customizing relative and absolute time ranges.

   * Auto refresh: Auto refresh is disabled by default. Once auto refresh is enabled, you can set the refresh frequency.


<span id="825032cc"></span>
## Query and analysis results explanation

<span id="d091989a"></span>
### Original log

You can view the results of the log query in the original log tab, and switch to the view mode as needed. By default, all retrieved log information is displayed in the original view.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bd8c2870c1584172b70de289e87710ca) </span>


* Instructions for the original log page

   
   |Icon number |Functionality |Note |
   |---|---|---|
   | **①**  |**Show all fields** |Once enabled, all fields in the query results are displayed. |
   | **②**  |**Switch log view** |* Log content fields are displayed together in this view, where you can set content to wrap by field, flatten JSON\-like fields, and use a compact layout.<br><br>* Table: Logs are displayed in a table format, with different fields shown in separate columns. |
   | **③**  |**Adjust original log views** |The original view supports adjusting its appearance.<br><br><br>* Line break: When enabled, the fields of the log content will be displayed on separate lines.<br><br>* Filtering and preset fields: When enabled, some preset fields will not be displayed. The specific fields affected are indicated in the UI.<br><br>* Compact layout: When enabled, log time and content are displayed together instead of in separate columns.<br><br>* More configurations:<br><br>   * Filter empty fields<br><br>   * Navigate between pages using the paginator<br><br>   * Force parsing of JSON fields |
   | **④**  |**Search fields** |Enter the field name to search for the corresponding field. |
   | **⑤**  |**Set display fields** |Select the target field from the hidden fields list and click the icon indicated by ⑤ to add the field to the visible fields list. The log content view on the right will display the content of the selected field. |
   | **⑥**  |**Adjust the display order of fields** |Hold down the icon indicated by ⑥ with the mouse, then drag the fields up or down to adjust their display order. |
   ||**View field distribution percentages** |Click the icon labeled ⑥ to view the top five most frequent values in the query results for this field. Click **View field distribution in the chart** to go to the chart analysis page and view information about the query values for this field. |
   

* The label to the left of a field name indicates its data type.

   * `d`: A field of `double` type, which is a floating\-point data type.

   * `l`: `long` type, an integer\-type field.

   * `j`: `json` type, suitable for fields formatted as JSON objects.

   * `t`: `text` type, suitable for string fields.


<span id="6e049b6d"></span>
### Chart analysis

On the chart analysis tab, select the appropriate chart to view the analysis results. Results can be displayed as a table, line chart, bar chart, pie chart, or single value visualization. For more information about chart descriptions and configuration, refer to the analysis feature of Log Service.

&nbsp;
