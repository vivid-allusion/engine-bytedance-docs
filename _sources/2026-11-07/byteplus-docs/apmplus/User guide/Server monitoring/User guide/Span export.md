---
title: "Span export"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Span_export"
---

Server\-side Monitoring supports span export for AI\-related applications and lets you export span information for further analysis. This topic describes how to export span data.

<span id="jHPTrGmu"></span>
## Prerequisites


* AI\-related applications have been integrated with Server\-side Monitoring and are reporting observability data normally. For more details, see [Overview of AI scenario monitoring](https://docs.byteplus.com/en/docs/Observability_Platform/Overview_of_AI_application_monitoring).

* (Optional) To export data to CozeLoop evaluation sets, ensure a workspace is created. For more details, see [Creating and managing workspaces](https://loop.coze.cn/open/docs/guides/manage_teams).


<span id="KM8QAWln"></span>
## Limits


* The span export feature is only available for AI\-related applications, such as VeADK and AI agents.

* This method supports exporting only historical data. To export new data, see [Exporting trace data online](https://docs.byteplus.com/en/docs/Observability_Platform/Data_backflow).


<span id="OUMOxE3X"></span>
## Procedure


<Tabs>
<Tab zoneid="Tw26rGhmzC" title="Method 1: Export data to a CozeLoop evaluation set">
<TabTitle>Method 1: Export data to a CozeLoop evaluation set</TabTitle>

<span id="qrHgq2uK"></span>
### Step 1: Add a personal access token


1. Log in to the [CozeLoop console](https://loop.coze.cn/console/) and select **Authorization** in the left navigation pane.

2. At the top of the page, switch to the **Personal access token** tab and click **Add** in the upper\-right corner.

3. Configure the relevant parameters for the personal access token. Then, click **Confirm** and save the token in a secure and accessible location.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The token is displayed only once. Save this token in a secure and accessible location. Do not share it with others, and do not expose it in a browser or other client code.</div>



|Parameter |Description |
|---|---|
|Name |Provide a custom name for the personal access token. |
|Expiration time |Configure the validity period of the personal access token.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Select the expiration time carefully. Once the personal access token is generated, its expiration time cannot be modified.</div><br> |
|Permissions |Configure the permissions for operations allowed by the current token and the level to which these permissions apply. If you select the workspace level scope, the permissions apply only within workspaces you own. If you select the account level, the permissions apply within your personal account.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The minimum permissions required to export data to a CozeLoop evaluation set include all permissions in the CozeLoop category and listWorkspace in team space management.</div><br> |
|Accessible workspace |Select the workspaces that can be accessed.<br><br><br>* **Specified workspace**: Only the selected workspaces can be accessed. You can select multiple workspaces.<br><br>* **All workspaces**: All workspaces, including newly created workspaces in the future, are allowed to be accessed.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Transferring the ownership of a workspace will invalidate all existing personal access tokens requested for this workspace. Exercise caution when transferring workspace ownership.</div><br> |


<span id="NH2g7vui"></span>
### Step 2: Export span data to a CozeLoop evaluation set


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Click the **Click to go to service list** link to access the service management page.

3. Select **Service Monitoring \> Trace Analysis** in the left navigation pane to go to the Trace Analysis page. On the page, enable **AI Application Trace Analysis**.

4. Filter for data as needed, select the target spans in the span list, and click **Span export**.

5. Configure the relevant parameters for the span export as needed and click **Preview** to view the export result. Click **Confirm** to export the target span data.



|Parameter |Description |
|---|---|
|Export destination |The destination of the span data export. For this scenario, select **CozeLoop** to export span data to a CozeLoop evaluation set. |
|CozeLoop Token |Your personal access token in CozeLoop. The token is used to push trace data to the evaluation sets of the corresponding CozeLoop workspace. Use the personal access token created in Step 1 or any other available personal access token.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure that your token includes only the necessary permissions. Avoid granting excessive permissions to reduce security risks.</div><br> |
|Workspace |Select the target CozeLoop workspace. |
|Target evaluation set |Select an existing evaluation set in CozeLoop, or create a new evaluation set. When adding a new evaluation set, you need to customize the name of the target evaluation set.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also go to CozeLoop to create an evaluation set. For more details, see <a href="https://loop.coze.cn/open/docs/cozeloop/create-dataset">Managing evaluation sets</a>.</div><br> |
|Import method |Select a span data import method.<br><br><br>* **Append data**: Append imported data to the existing data.<br><br>* **Replace all**: Imported data will overwrite all existing data. To avoid data loss, select this method only if the existing data is no longer used. |
|Field mapping |The field mappings during data import. Sequentially select the trace span fields and the columns in the target evaluation set. |
|Sample Span |Sample span. The sample is for reference only. |





</Tab>
<Tab zoneid="haaF9GNpJC" title="Method 2: Export data to a local file">
<TabTitle>Method 2: Export data to a local file</TabTitle>

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Click the **Click to go to service list** link to access the service management page.

3. Select **Service Monitoring \> Trace Analysis** in the left navigation pane to go to the Trace Analysis page. On the page, enable **AI Application Trace Analysis**.

4. Filter for data as needed, select the target spans in the span list, and click **Span export**.

5. Configure the relevant parameters for the span export as needed and click **Preview** to view the export result. Click **Confirm** to export the target span data.



|Parameter |Description |
|---|---|
|Export destination |The destination of the span data export. For this scenario, select **Local file** to export the span data to a local CSV file. |
|Export format |The format for the span data export.<br><br><br>* **Select fields to export**: Manually select the span fields to export and configure their mappings.<br><br>* **Export Span details**: Export complete span data. |
|Field mapping |Field mappings during data import. You need to configure this parameter when selecting fields to export. Select the trace span fields and the target evaluation set columns to which the fields will be exported. |
|Sample Span |Sample span. The sample is for reference only. |





</Tab>
<Tab zoneid="bkO1e2I3Pu" title="Method 3: Export data to the agent evaluation platform">
<TabTitle>Method 3: Export data to the agent evaluation platform</TabTitle>

1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Click the **Click to go to service list** link to access the service management page.

3. Select **Service Monitoring \> Trace Analysis** in the left navigation pane to go to the Trace Analysis page. On the page, enable **AI Application Trace Analysis**.

4. Filter for data as needed, select the target spans in the span list, and click **Span export**.

5. Configure the relevant parameters for the span export as needed and click **Preview** to view the export result. Click **Confirm** to export the target span data.



|Parameter |Description |
|---|---|
|Export destination |The destination of the span data export. For this scenario, select **Agent evaluation** to export span data to an evaluation set on the agent evaluation platform. |
|Target evaluation set |Select an existing evaluation set on the agent evaluation platform, or add a new evaluation set. When adding a new evaluation set, you need to customize the name of the target evaluation set. |
|Import method |The method used to import span data to the agent evaluation platform. Currently, only appending data is supported. This indicates that data is appended to the existing data. |
|Field mapping |The field mapping relationships when data is imported to the agent evaluation platform. Sequentially select the trace span fields and the fields in the target evaluation set. |





</Tab>
</Tabs>


<span id="ZpFybTPE"></span>
## What to do next


* If you export data to a CozeLoop evaluation set, go to the [CozeLoop console](https://loop.coze.cn/console/) and view the imported span data on the details page of the target evaluation set.

* If you export data to a local file, go to local download management to view downloaded CSV files.

* If you export data to the agent evaluation platform, go to the [AgentKit console](https://console.byteplus.com/agentkit), click Evaluation Dataset in the pane, and view the imported span data on the details page of the target evaluation set.


&nbsp;
