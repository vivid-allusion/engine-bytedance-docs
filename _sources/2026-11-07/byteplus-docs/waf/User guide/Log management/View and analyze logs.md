---
title: "View and analyze logs"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/docs-view-log-details"
---

The new log management function supports the collection of web attack and access log data for the protection resources already added on WAF, and provides retrieval analysis, monitoring alarms, data visualization, and other functions based on Log Service, helping you quickly understand the status of web request services and protection effects for timely handling of anomalies.

<span id="03ec25bf"></span>
## Constraints and limitations


* The WAF allocates log capacity based on the purchased log service specifications. If the amount of logs corresponding to the set log storage duration exceeds the purchased log capacity, logs will only be collected within the purchased log capacity. If some log data cannot be stored for the expected duration due to exceeding the log capacity or expiration, you can upgrade or renew as needed to ensure the log data is stored for the expected duration.

* When the WAF log service is activated, a WAF service associated role will be automatically created. This role has permissions for creating/recycling WAF log projects and collecting logs. During the usage of WAF log service, please do not delete this authorization; otherwise, it will affect the collection of logs and instance recycling operations.


<span id="8f90a8a6"></span>
## Requirements


* The WAF log service functional module has been purchased.

* The traffic of the domain needing protection has been directed to the WAF cluster.


<span id="84691483"></span>
## View log projects and topics


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the instance region in the top bar.

3. Select **Log Management** from the left navigation to enter the log management page.

4. Hover over the details next to Log Management to view log items and log topic information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After purchasing the log service, WAF will automatically create:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Associated role ServiceRoleForWaf, which has WAF log collection permissions.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Exclusive log items and log topics.   </div>
   

   
   |**Resource type** |**Description** |
   |---|---|
   |Log item |The log items automatically created by WAF are the basic units of resource management, and WAF log items do not support deletion. The naming convention for WAF's dedicated log items is: waf\-project\-<account_id\>\-. Clicking the log item name will redirect to the log service console to view project information. |
   |Log topic |A dedicated log topic is created by default under the WAF log project, and the log topic is the basic unit for log management. For example, log collection, storage, and query analysis, etc. The WAF log topic does not support writing other types of data besides WAF logs through APIs, SDKs, etc., and deletion is not supported. The WAF dedicated log project is fixedly named: waf\-log. Clicking the log topic name will redirect to the log service console to view relevant information. |
   


<span id="e9ad695f"></span>
## Quickly filter logs

Supports quickly filtering logs by domain name, path, source IP, WAF status code, risk level, rule ID, attack type, and execution action. The quick filter conditions will be used for log retrieval analysis, where you can view the number and trends of logs in the query results, and view log details under the original log page.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Log Management** to enter the log management page.

4. Perform domain filtering or other quick filtering.

   
   |Filter parameter |Description |
   |---|---|
   |Domain name. |The range of domain names to be retrieved for analysis defaults to all domain names, supporting switching to a single precise domain name. |
   |Path |Requires an exact path for retrieval and analysis; wildcards are not supported. |
   |Source IP |A single source IP address that needs to be retrieved and analyzed; multiple IP addresses or IP segments are not supported. |
   |WAF status code |Filter based on the status codes returned by WAF, supporting single or multiple selections.<br><br><br>* 0: Not triggered protection rule.<br><br>* 200: Allowed.<br><br>* 403: Blocked. |
   |Risk Level |Determine the risk situation of the attack, classified as high risk, medium risk, and low risk, supporting single or multiple selections. |
   |Rule ID |ID of the triggered protection rule, only supports configuring a single exact rule ID. |
   |Attack type |The triggered protection function module supports single selection or multiple selections. |
   |Action |For requests that trigger protective rules, actual disposal actions are supported for single or multiple selections. |
   

5. Click **Query**.

   You can view the number and trends of logs in the query results, and view log details on the raw log page.


<span id="caccbf9d"></span>
## Retrieve and analyze logs


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **Log Management** to enter the log management page.

4. Enter the corresponding statement in the retrieval analysis statement input box.

   * For how to filter logs that meet the conditions through retrieval criteria, please refer to the description of Log Service retrieval function.

   * To perform log statistical analysis through SQL statements, you can refer to the Log Service analysis function description.

   * For detailed explanations of log fields, please refer to [Log Field Description](https://docs.byteplus.com/en/docs/waf/Log_field_description).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When multiple search statements are separated by spaces, it indicates an "or" logic, which is equivalent to <code>OR</code>. For example, <code>warning error</code> is equivalent to <code>warning OR error</code>, indicating that the log contains keywords <code>warning</code> or <code>error</code>.   </div>
   

5. Click **Search Analysis.** 

   The query result chart will be displayed below.

6. (Optional) Set the time range for the query chart and automatic refresh.

   * Time Range: The default display shows query results from the past 3 days, supporting custom relative and absolute time.

   * Auto Refresh: Auto refresh is turned off by default. When enabled, you can set the auto refresh frequency.


<span id="b921e346"></span>
## Create scheduled SQL analysis tasks

The log service supports creating scheduled SQL tasks through the console to periodically search and analyze log topics and save the processed log data to the target log topic.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the region where the instance is located from the top bar.

3. Select **Log Management** from the left navigation to enter the log management page.

4. Click "Save as Scheduled SQL Analysis" in the top right corner of the raw log.

5. Configure the Scheduled SQL task <Parameter\>.

   
   |Configuration |Description |
   |---|---|
   |Task name |Task name for scheduled SQL analysis task. Must comply with the following rules:<br><br><br>* The length must be between 3 and 63 characters.<br><br>* Support lowercase letters, numbers, Chinese characters, and hyphens (\-).<br><br>* Must start and end with a lowercase letter, number, or Chinese character. |
   |Description |A simple <a i=1\>description</a\> of the scheduled SQL analysis task. Within 64 characters. |
   |Source log topic |The log topic where the raw logs for scheduled SQL analysis are located. |
   |Target log subject |After executing the scheduled SQL analysis task, the processed log data is stored in the log item and log topic.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is no suitable log topic, you can create one based on the page prompts.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the log topic is not configured for indexing, creating the scheduled SQL analysis task will fail.</div><br> |
   |Task status |Whether to start the scheduled SQL analysis task immediately. Defaults to the enabled state, which means the scheduled SQL analysis task will start immediately after task configuration is completed. If not enabled, after configuration is completed, the scheduled SQL analysis task will be in a paused state and needs to be started manually. |
   

6. Click **Next: SQL Analysis Rules Configuration.** 

7. Configure the parameters related to SQL analysis rules.


<span id="825032cc"></span>
## Query and Analysis Results Explanation

<span id="d091989a"></span>
### Raw Log

You can view the log results of the query under the raw log tab and view the visual effects as needed. By default, all log information found is displayed in the original view.


* Instructions related to the original log page.

   
   |Function |Description |
   |---|---|
   |**Switch log view** |* Original: The fields of log content are displayed in a concentrated manner, and settings can be made for content to wrap by field, tile JSON type fields, and compact layout.<br><br>* Table: Logs displayed in table style, with different fields shown in separate columns. |
   |**Filter out empty fields** |After enabled, fields with empty query results will be filtered out and not displayed in the log list. |
   |**Adjust original log view** |The original view supports adjusting display effects.<br><br><br>* Line break: When enabled, the fields of log content will be displayed on separate lines.<br><br>* Flatten JSON\-like fields: When enabled, JSON type fields will be displayed in a flattened style, meaning each of its subfields will be expanded and displayed.<br><br>* Compact layout: When enabled, the log time and content will be combined and displayed together, rather than in separate columns. |
   |**Search field** |Input field name, which can be used to retrieve the corresponding field. |
   |**Set display fields** |Select the target field from the hidden field list, click the icon, which will add the field to the display field list, and the log content view on the right will show the selected field content. |
   |**Adjust field display order** |Press and hold the icon to drag the field up or down, which can adjust the field display order. |
   |**View field distribution ratio** |Click the icon to view the top five values with the most query results for that field. Click **view field distribution in the chart** to go to the chart analysis page to see the data information of the query values for that field. |
   

* The label on the left side of the field name indicates the data type of the field.

   * `d`: `double` type, refers to fields of floating\-point data type.

   * `l`: `long` type, refers to fields of integer type.

   * `j`: `json` type, applicable to fields formatted as JSON objects.

   * `t`: `text` type, applicable to fields of string type.


<span id="6e049b6d"></span>
### Chart Analysis

You can view the analysis results by selecting the appropriate chart under the Chart Analysis tab. Supports display in table, line chart, bar chart, pie chart, and single value chart styles.
