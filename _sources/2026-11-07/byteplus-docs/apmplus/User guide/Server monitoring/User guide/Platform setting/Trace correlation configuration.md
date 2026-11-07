---
title: "Trace correlation configuration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Trace_correlation_configuration"
---

Trace correlation configuration maps Span fields to logs in TLS. After the configuration is complete, you can go directly from the Span details page to the search and analysis page of the corresponding log topic without manually switching pages or entering query conditions. This helps you quickly identify the root cause when troubleshooting trace exceptions. This topic describes how to configure correlations between traces and logs.

<span id="Vd9VxM0S"></span>
## Prerequisites


* The current account already has accessible log projects and log topics in the same region, and the target business logs have been written to the topic. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* The current account has permissions to view Trace data, manage correlation rules, and search the target log topic. For details, see [Workspace-level IAM permission control](https://docs.byteplus.com/en/docs/apmplus/Workspace-level_IAM_permission_control) and [Querying and analyzing logs](https://docs.byteplus.com/en/docs/tls/getting_started_query_and_analyze_logs).

* The target Span contains a field that can be used for correlation, and the field value can be matched against the log content. For example, both the Span and the log record the Trace ID or order ID.

* Make sure that the workspace of Server\-side Monitoring and the target log project are located in the same region.


<span id="bEQOvnlx"></span>
## Limits

Trace correlation configuration only provides page redirection and does not create log topics or collect logs.

<span id="TTlGaQQR"></span>
## Procedure


<Tabs>
<Tab zoneid="sBH2r7QXKf" title="Method 1: Configure on the Trace correlation configuration page">
<TabTitle>Method 1: Configure on the Trace correlation configuration page</TabTitle>

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, click **Platform Setting** \> **Trace Association Configuration**.

3. Click **New rule**. Specify the following parameters, and then click **Save**.

   
   |**Parameters**<br><br>**Parameters** |**Description**<br><br>**Description** |**Legend**<br><br>**Legend** |
   |---|---|---|
   |Effective scope |Set the Span scope to which the rule applies.<br><br><br>* All services: The rule applies to all Spans associated with the current account in the current region.<br><br>* Specify a workspace: The rule applies to all Spans under the selected workspace. You can select multiple workspaces.<br><br>* Specify a service: The rule applies to the Spans of the selected service under the specified workspace. You can select multiple services. | |
   |Effective field |Specify the Span field that triggers the correlation entry.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The View associated logs option is displayed only if the field exists in the current Span. If the Span does not contain the field, the entry will not be visible.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When <strong>Effective field</strong> is set to <strong>trace_id</strong>, use the <strong>Log</strong> tab or the Trace ID field value to go to the search and analysis page of the corresponding log topic. For other fields, the <strong>Log</strong> tab does not provide a link to the log topic page.</div><br> ||
   |Event name |The display name of the correlation entry on the Span details page. Click the correlation entry to go to the search and analysis page for the target log topic. ||
   |Event type |Set the target product for redirection. Select **TLS** when associating logs. ||
   |Region |The region where the target log project is located.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The workspace of Server\-side Monitoring and the target log project must be located in the same region.</div><br> ||
   |Log project |Select the target log project.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The list only displays projects that the current account has permissions to access. If the target project is not found, check the account permissions.</div><br> ||
   |Log topic |Select the target log topic. The following two methods are supported:<br><br><br>* Custom: Select an existing log topic from the drop\-down list.<br><br>* Regex matching: Enter a regular expression, and the system matches all log topics in the selected log project that match the expression. ||
   |Search query |Set the query statement that the system automatically enters after redirecting you to the target log search page. You can use template variables in the following format: `${{field_name}}`. When you click the link, the system automatically retrieves the actual value from the current Span and replaces the placeholder.<br><br>For example, if the search statement is set to `trace_id:${{trace_id}} and ${{tags.apmplus.third_party_sdk}}`, it will be automatically replaced with the actual value of the current Span, `trace_id:abc123ef and custom_sdk` after redirection. ||
   |Time range |Set the default log time range for queries after you are redirected to the log page. | |
   |Open method |When this feature is enabled, the log search and analysis page will open in a new browser tab. When this feature is disabled, you will be redirected from the current page. ||
   |Status |The activation status of the rule. This feature is enabled by default. If it is disabled, the rule will no longer trigger the correlation entry. ||
   





</Tab>
<Tab zoneid="mkGnXMvpVP" title="Method 2: Configure on the Trace details page">
<TabTitle>Method 2: Configure on the Trace details page</TabTitle>

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, click **Server\-side Monitoring** \> **Service Monitoring** \> **Trace Analysis**.

3. After you filter data as needed, click the name of the target Span to go to the Span details page.

4. Click **Association configuration** to go to the **Service association configuration** page.

5. Click **Add field**. Specify parameters and then click **Save**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For parameter configuration descriptions, see <strong>Method 1: Configure on the Trace correlation configuration page</strong>.</div>


* <div data-tips="true" data-tips-type="default">To create a rule that applies to multiple workspaces or services, click <strong>Manage all rules</strong> to go to the global configuration page.</div>



</Tab>
</Tabs>


<span id="QosLipDT"></span>
## Validate results


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. In the left navigation pane, click **Server\-side Monitoring** \> **Service Monitoring** \> **Trace Analysis**.

3. Click the Trace ID of the target Span. On the **Basic information** or **Property** tab, confirm that the current Span contains the field specified as the effective field in the rule.

4. Click the link on the effective field value and then click **View associated logs** to go to the search and analysis page of the corresponding log topic. After you are redirected to the page, the system automatically fills in the preset search statement and time range. Run the search to view the corresponding logs. For details, see [Querying and analyzing logs](https://docs.byteplus.com/en/docs/tls/getting_started_query_and_analyze_logs).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When <strong>Effective field</strong> is set to <strong>trace_id</strong>, use the <strong>Log</strong> tab or the Trace ID field value to go to the corresponding log topic. For other fields, the <strong>Log</strong> tab does not provide a link to the log topic page.   </div>
