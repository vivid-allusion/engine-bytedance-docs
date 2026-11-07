---
title: "Querying and handling events"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Event-types"
---

After you create a cluster, the cluster is automatically integrated with Cloud Monitor, which reports cluster events. You can query or handle these events in the Cloud Monitor console.

<span id="J4dKc96w"></span>
## Querying events


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation bar, click **Event Center \> Cloud product event**.

3. On the **Cloud product event** page, you can view cloud service events for the specified time period.

4. To view details of an event, find the event in the event list and click **Details** in the **Actions** column. For a failure event, you can view the cause of the failure by checking the `data.detailreason` field.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For details, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-cloud-service-events">Viewing cloud service events</a>.   </div>
   

<span id="EEAkV8Jk"></span>
## Event alerts

You can use Cloud Monitor to configure event alert rules for VKE clusters. When an event matching the rule occurs, you can promptly receive an alert notification in a timely manner and quickly locate the problematic cluster or resource. Additionally, you can configure suppression policies for frequent but non\-severe events to filter out such noise, helping you better focus on truly important issues. For details, see [Event alerts for core resources](https://docs.byteplus.com/en/docs/vke/Event_alerts_for_core_resources?lang=en).
