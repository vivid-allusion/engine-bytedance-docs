---
title: "Configuring and viewing persistent events"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events"
---

Integrated with [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS), VKE provides the event persistence feature, which can be used to collect cluster events through the event\-collector add\-on and send event alert notifications. This topic describes how to configure and view cluster events.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A **log project** and a **log topic** have been created in TLS. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* The event\-collector add\-on has been installed, and the **log project** and **log topic** have been configured. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.ZXZlbnQtY29sbGVjdG9yLee7hOS7tg==).


<span id="M3qYd5iU"></span>
## Limit

When collecting events from a VKE cluster, the event\-collector add\-on does not collect events generated in the following scenarios:


* Historical events before add\-on startup: Cluster events generated before the event\-collector add\-on starts will not be collected retroactively.

* Events generated during add\-on configuration changes: When the following configuration changes are made to the event\-collector add\-on, events generated during the change process will not be collected:

   * Modifying the log project or log topic associated with the add\-on.

   * Enabling or disabling pod scheduling based on taints, or the label selection feature, which triggers add\-on restart or rescheduling.

* Events generated during add\-on listening interruptions: If cluster event listening by the event\-collector add\-on is interrupted, the listening needs to be retriggered. Cluster events generated during the interruption period cannot be collected.


<span id=".5p-l55yL5LqL5Lu2"></span>
## Event query


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the target cluster for which you want to view events.

4. In the left navigation bar of the cluster management page, click **Event management**.

5. Click the **Event query** tab. Enter the search keywords, select the search time range, and then click **Search** to view cluster events.


<span id="1wJaxCRj"></span>
## Pod events

<span id="SIJ13Pos"></span>
### Configuring index fields

To view pod events, make sure that the following index fields are configured in the **log topic**. For configuration methods, see [Configuring indexes](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2).


|Index field |Type |**Field description** |
|---|---|---|
|involvedObject_kind |String |The Kubernetes resource type of the event, such as `Pod`, `Deployment`, `Job`, and `ConfigMap`. |
|type |String |The event level, such as `Normal` and `Warning`. |
|source_component |String |The event source, such as `kubelet`. |
|reason |String |The event type, such as `Started`, `Pulling`, and `Created`. |
|source_host |String |The event source host, such as `192.168.1.100`. |
|message |String |The details of the event. |
|metadata_name |String |The pod name, such as `nginx-deployment-5dc***`. |
|metadata_namespace |String |The namespace where the pod is located, such as `default` and `kube-system`. |


<span id="jisETzKx"></span>
### Viewing pod events

Click the **Pod event** tab. The system automatically generates charts to record pod events based on log indexes. You can use the filter criteria in the charts to view events for the specified pod.

The following table describes the parameters and filter criteria in the chart.


|No. |Parameters |Description |
|---|---|---|
|1 |PodNamspace |Select the namespace where the target pod is located, such as `default` and `kube-system`. |
||PodName |Select the target pod. |
||Log level |Select the event log level, such as `Normal` and `Warning`. |
|2 |Query time |Specify the time period for event queries. You can specify absolute time or relative time, and view historical records. |
||Refresh method |Configure the chart refresh method. The chart is manually refreshed by default. You can enable auto refresh and specify the auto refresh interval. |
