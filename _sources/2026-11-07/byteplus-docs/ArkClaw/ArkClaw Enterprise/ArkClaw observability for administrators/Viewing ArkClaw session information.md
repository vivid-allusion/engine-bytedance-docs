---
title: "Viewing ArkClaw session information"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_sessions"
---

The platform provides a session management page that enables administrators to quickly locate problems by tracing complete ArkClaw interactions within a specified time range. This topic describes how to view and export ArkClaw session information.

<span id="EGX7cQ9k"></span>
## Prerequisites


* The administrator has completed basic settings (such as enterprise system permissions and callback configuration) and has activated ArkClaw Enterprise. For details, see [Getting started with space activation](https://docs.byteplus.com/en/docs/ArkClaw/Getting_Started).

* Enterprise employees have provisioned ArkClaw instances and started conversations with ArkClaw to process tasks. For details, see the [ArkClaw guide for employees](https://docs.byteplus.com/en/docs/ArkClaw/Employee_use_of_ArkClaw_new_version).

* (Optional) To view complete input and output information, ensure the observability data masking feature is disabled for the ArkClaw instances. For more details, see [Observability data masking](https://docs.byteplus.com/en/docs/ArkClaw/Masking_observability_data).


<span id="hEaZFovZ"></span>
## View session information


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select **O&M \> Observability**.

3. Select the data source for the observability dashboard and data analytics. The Claw instance page displays the observability dashboards and data analysis related to employee Claw instances. The enterprise service agent page displays the observability dashboards and data analysis related to enterprise service agents.

4. Click the **Session management** tab. Select a time range to view all sessions in the selected range and their basic information.

   You can filter sessions by ArkClaw instance ID, session ID, user ID, duration, and other criteria. The session list provides basic session information, such as session ID, duration, total token count, input token count, output token count, trace count, user ID, and start time.

5. To view details of a session, find the session in the session list and click its session ID or the **Details** button in the Actions column. Session details include the start time, input, and output details for each trace, as well as the total token count, trace count, trace ID, user ID, model name, and other items.

6. Click **Trace ID** in the session details to open the trace details page, where you can view the complete request trace, trace logs, trace diagnosis results, as well as LLM\-related data and metrics. For a more detailed description, see [Viewing ArkClaw traces](https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_traces).


<span id="cha9tmEw"></span>
## Export session information

Session management provides data export capabilities, supporting the export of session list data as well as the detailed trace of a target session.


* Go to the Sessions page, select the sessions to export, and click the **Export** button in the upper\-right corner to export the basic session information to a CSV file.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can export up to 100 items per export.   </div>
   

* On the Sessions page, click the target session ID to go to the session details page. Click the **Export** button in the upper\-right corner of the page to export the detailed trace related to the current session to a CSV file.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can export up to 1,000 trace records per export.   </div>
