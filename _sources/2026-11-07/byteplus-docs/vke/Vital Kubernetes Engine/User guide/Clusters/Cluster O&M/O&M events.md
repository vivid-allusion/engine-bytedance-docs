---
title: "O&M events"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/OM-events"
---

When potential anomalies exist on the container cluster platform, they may affect cluster stability, security, and availability, potentially causing the cluster to lose management control or disrupt workload scheduling. The O&M events feature uses a systematic, periodic inspection mechanism to actively scan for and discover such risks, and centrally displays detailed information about affected resources. This topic guides you on how to view and resolve such events via standard procedures, preventing risks from escalating into serious production incidents.

<span id="h5gNaMrF"></span>
## Background

<span id="mI4V788T"></span>
### Feature overview

Cluster O&M events are critical events that are proactively detected, generated, and pushed by VKE. They may affect user cluster stability, security, availability, or lifecycle management. This feature provides a centralized entry point for viewing cluster status, identifying risks, and handling events. In daily operations, when these resources show potential issues, such as an APIServer certificate nearing expiration, the system detects them through periodic inspections and generates corresponding O&M events. You can grasp event details at a glance, including event severity, occurrence time, and the specific resource scope affected.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The system proactively performs inspections and generates alerts in advance. Inspection intervals and lead times vary by event. For details, see <a href="https://docs.byteplus.com/en/docs/90/99467#gckTTrAK">Supported events</a>.</div>


Cluster O&M events are more than alerts. Depending on the event type, they provide clear remediation guidance or one\-click self\-service handling paths so that you can shift from reactive troubleshooting to proactive prevention. This helps you identify and resolve risks in time, reduce MTTR, and improve business availability and continuity.

<span id="mlZEKHyh"></span>
### Event levels

The system defines different event levels based on the impact on the cluster. This helps you quickly assess how urgent an event is.


|**Level** ||**Definition and business impact** |
|---|---|---|
|Critical |Urgent |Service is interrupted or about to be interrupted. This severely impacts the core business. |
|High |High |The service is experiencing performance degradation or functional impairment. There is a potential risk of business interruption. |
|Medium |Medium |This is a non\-critical issue or a potential risk that does not directly affect online services. |
|Low |Low |This is an informational or advisory notification. It is intended for routine observation and optimization. |


<span id="gckTTrAK"></span>
### Event status

Cluster O&M events go through different statuses during handling. See the table below.


|Event status |Status description |Business impact |
|---|---|---|
|Open |The system has detected an anomaly or potential risk in the cluster (e.g., an APIServer certificate is about to expire). Further attention is required. |The current cluster environment has a specific potential risk. If not resolved promptly, this may lead to loss of cluster control, business scheduling interruptions, or other potential security risks. |
|Recovered |The cluster anomaly or potential risk has been successfully resolved. No further attention is required. |The current cluster environment has cleared the risk alert associated with this event. No further remedies are required. You can archive such events as historical records for routine stability reviews and O&M audits. |


<span id="qoiXm6q0"></span>
### Supported events

Currently supported cluster O&M events are shown in the table below.


|**Event name** |**Severity level** |**Event description** |Advance alert time |Handling method |
|---|---|---|---|---|
|APIServer certificate is about to expire<br><br> |High |The control plane TLS certificate is about to expire or has already expired, which may cause API unavailability. |60 days |Upgrade cluster patch version and complete certificate rotation. For details, see [[Announcements] Patch version upgrade for VKE clusters](https://docs.byteplus.com/en/docs/vke/Patch-version-upgrade-for-VKE-clusters). |


<span id="uBjIiADZ"></span>
## Prerequisites

To subscribe to events via Cloud Monitor, complete the following configurations in advance.


* Cloud Monitor service has been activated. If not, log in to the [Cloud Monitor console](https://console.byteplus.com/observe/cloud-monitor). Follow the console wizard to activate the service.

* Alert contacts and contact groups have been created. For details, see [Creating contacts](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-contact-and-an-alarm-contact-group) and [Creating contact groups](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact).

* An alert callback URL has been created. For details, see [Creating callback address](https://docs.byteplus.com/en/docs/cloudmonitor/Managing-callback-address#414fd7c7).


<span id="ixKj8ITR"></span>
## Procedure

<span id="LxB3fYOK"></span>
### Step 1: View events


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, select **O&M events**. In the O&M events list, view the existing events in the cluster.

   You can filter events by occurrence time. Predefined options include last hour, last 3 hours, last 12 hours, last 24 hours, and more. You can also set a custom time range.


<span id="QzEkwBXl"></span>
### Step 2: (Optional) Subscribe to events

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you do not use Cloud Monitor for event subscription, you can still view and handle O&M events in the console. However, you will not receive active pushes via email, SMS, or phone.</div>


You can use Cloud Monitor to subscribe to cluster O&M Events. This gives you real\-time event pushes and alerts. Procedure:


1. Log in to the [Cloud Monitor console ](https://console.byteplus.com/observe/cloud-monitor/overview).

2. In the left navigation pane, select **Event Center \> Event rule**.

3. On the **Event rule** page, click **Create event rule** to start configuration.   

   * For **Resource type**, select **VKE**.

   * For **Event name**, select a cluster O&M event, e.g., APIServer certificate is about to expire.

4. Configure how to deliver events. Supported methods include email, phone, and SMS. For more details, see [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).


<span id="xDkgVviY"></span>
### Step 3: Handle events

After you view or receive cluster O&M events, you can use the console or OpenAPI to complete event handling.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Different event types may cause control plane changes or brief fluctuations during handling. We recommend performing the operation during off\-peak hours and assessing the impact in advance. If the cluster is in a critical business window, confirm the maintenance time with the business team first.</div>


* <div data-tips="true" data-tips-type="warning">Handling methods vary by event. Always refer to the console for accurate guidance.</div>


* <div data-tips="true" data-tips-type="warning">You can handle events via the console or OpenAPI. For example, to handle the event that an APIServer certificate is about to expire, you can upgrade the cluster patch version via the console or OpenAPI. This will rotate the certificate.</div>


1. In the O&M events list, find the event you need to handle.

2. Click **Resolve** in the **Actions** column. Follow the system prompts to complete the handling.

3. When the **Event status** changes to **Recovered**, the handling is complete. The system records the resolution time for traceability and audit.
