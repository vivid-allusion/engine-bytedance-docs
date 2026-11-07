---
title: "Creating cloud service event rules"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_cloud_service_event_rules"
---

To monitor the status of a cloud service event, create an event rule for the cloud service. When an event matching the rule occurs, the system will send an alert notification using the specified method, allowing recipients to quickly identify cloud service resources with anomalies. This topic describes how to create a cloud service event rule.

<span id="O4lvdVk4"></span>
## Prerequisites

You have selected an appropriate notification method and created a matching notification policy. They are used to specify the contacts who receive notification messages, notification templates, and other information. For more details, see [Creating notification policies](https://docs.byteplus.com/en/docs/Observability_Platform/Creating_notification_policies).

<span id="kVKlBGUA"></span>
## Limits

Up to 1,000 event rules can be created within an account.

<span id="bUSMHrGz"></span>
## Procedure


<Tabs>
<Tab zoneid="a2bwc689nu" title="Method 1: Create an event rule">
<TabTitle>Method 1: Create an event rule</TabTitle>

Create a cloud service event rule from scratch via the console. Configure key information such as the resource type, severity level, and event detail matching in order. This method applies to on\-demand customization or scenarios with a small number of event rules.


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the "Alert Configuration" page.

3. In the left "Alert settings" section, select **Cloud Service Event**, click **Create Event Rule**, and configure the relevant parameters for the cloud service event rule based on your actual needs.

   
   |Parameter |Description |
   |---|---|
   |Name |Specify a name as a unique identifier for the cloud service event rule. Duplicate names are not allowed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using certain characters in the name may cause alert SMS delivery failures. </div><br> |
   |Resource type |Specify the cloud service to be monitored. |
   |Event name |After you select **Resource type**, names of events supported by the cloud product are displayed on the page. You can select one or more events from the drop\-down list. |
   |Level |Specify the severity level of the event. Valid values: **Critical**, **Warning**, **Notice**. |
   |Project selection |After you select one or more resource types, you can select **All projects** or **Part of the project**. You can manage resources in batches by project.  |
   |Match by event details |Click **Add** to enable more granular event matching based on the fields in the `data` item of the cloud product event details. For example, you can implement event matching based on the instance status or instance ID of a cloud product. For example, if you set `data.WithGPUDevice` to `false`, events with the field `"WithGPUDevice": false` will be matched.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Event details vary by cloud product. For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events">Querying events</a>.</div><br> |
   |Notify policy |Select an appropriate notification policy based on actual circumstances. A notification policy defines the recipients, delivery channels, and content display format for alert notifications when alerts of different levels are triggered or recovered. |
   





</Tab>
<Tab zoneid="KeyRwIWgvl" title="Method 2: Import/export event rules via JSON">
<TabTitle>Method 2: Import/export event rules via JSON</TabTitle>

Export cloud service event rules from another account as a JSON file, and then import them into the cloud service event rules in the current account. This applies to batch copying of event rules across accounts.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The import and export features enable quick synchronization of alert configurations across accounts, regions, projects, or workspaces for efficient reuse. The synchronization granularity for cloud service event rules is at the account level.</div>



1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, click **Alert Center \> Alert Configuration** to go to the "Alert Configuration" page.

3. In the alert configuration section on the left, select **Cloud Service Event** and click the **Event Rule** tab.

4. In the upper\-right corner, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c35cb0c323edd4d26fc0ea35f521975b.png) </span>icon and select an operation to perform it. Use the import and export features to import cloud service event rules from another account into the cloud service event rules in the current account.

   
   |Actions |Description |
   |---|---|
   |Export the selected Cloud Service Event rules |Export the selected rules from the cloud service event rule list to a local JSON file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only items on the current page can be selected. Cross‑page selection is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Do not arbitrarily modify the structure of the JSON file, because it may cause import failures. If you lack professional expertise, we recommend not directly editing the JSON file.</div><br> |
   |Export all Cloud Service Event rules matching search criteria |Export all cloud service event rules that match the current filter criteria to a local JSON file. The export is not affected by pagination. You can filter data by rule name, rule status, and other information. |
   |Import a JSON file to generate cloud product event rules |Use a JSON file to import cloud service event rules from another account into the current cloud service event rules. During the import, you can specify a name suffix to avoid duplicate names.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only rules of the same type can be imported. For example, you can export cloud service event rules from Account A and import them into the cloud service event rules within Account B. However, cloud service event rules cannot be imported into VMP alert rules.</div><br><br><br> |
   





</Tab>
</Tabs>


&nbsp;
