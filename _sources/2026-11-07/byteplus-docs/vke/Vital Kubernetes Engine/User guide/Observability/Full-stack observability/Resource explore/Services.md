---
title: "Services"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Service-monitoring"
---

Service resource retrieval provides the monitoring information of Service resources in clusters, including the resource list and resource details. This topic describes how to view the Service list and details.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* Full\-stack observability has been enabled. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).


<span id=".6LWE5rqQ5YiX6KGo"></span>
## Resource list


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Resource explorer**.


<span id=".5p-l55yL6LWE5rqQ5YiX6KGo"></span>
### Viewing the resource list

In the **Resource type** panel, select **Service** to view the Service list. The list displays basic information about services, including the service name, type, namespace, cluster IP, internal endpoint, external endpoint, pod, label, error rate, response time P90, average response time, and QPS.

In the service list, you can click the service name to go to its details page and view its details.

<span id=".6LWE5rqQ562b6YCJ"></span>
### Filtering resources

You can filter services by namespace, type, and service in the service list.


1. Select the information to be retrieved from the **Namespace**, **Type**, and **Service** drop\-down lists.

2. Click **Add label/annotation** to configure the labels or annotations for the Service.

   
   |Parameter |Description |
   |---|---|
   |Type |Select Label or Annotation to filter services. |
   |Name |Enter the name of the label or annotation in string format. |
   |Operator |Configure the operator. Valid values:<br><br><br>* **Include**: Indicates that the label contains the specified value.<br><br>* **Not equal to**: Indicates that the label does not contain the specified value. |
   |Value |Specify the value of the label or the annotation in string format. You can enter multiple values by pressing the spacebar. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add multiple labels or annotations for retrieval.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Multiple values are in the <strong>AND</strong> relationship, which means the service must contain all values.   </div>
   

3. Click **Search** to retrieve the service.


<span id=".6LWE5rqQ6IGa5ZCI"></span>
### Aggregating resources

You can aggregate services by **Namespace** and **Type** in the Service list. After aggregation, Services are displayed by aggregation dimension.


1. Select the target aggregation dimension from the **Aggregation dimension** drop\-down list.

2. Click **Search** to aggregate services.


<span id=".6LWE5rqQ6K-m5oOF"></span>
## Resource details

In the service list, click the name of the target service to go to its details page. You can view service details, including the basic information, performance overview, application monitoring, and YAML.

<span id=".5Z-656GA5L-h5oGv"></span>
### Basic information

In the **Basic information** section, view the basic information about the service, such as the running time, label, annotation, and pod list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the <strong>Pod list</strong> section, you can click the name of the target pod to go to the pod details page and view pod details.</div>


<span id=".5bqU55So5oCn6IO955uR5o6n"></span>
### Application monitoring

On the Application monitoring tab, you can view the application performance overview, the observability dashboard on the server side, and the span list of the service. You can also configure the query time range.

<span id=".5pyN5Yqh5oCn6IO9"></span>
#### Performance

Click **Application monitoring** \> **Performance** to view the performance dashboards and span list of the service.  


* **Service performance dashboard**: Includes service QPS, service P90 response latency, service error rate, number of service errors, service QPS grouped by upstream workload (top 5), and other information.

* **Span list**: Displays the information about the spans when the service functions as a server, such as the status, time, status code, side, client, server, URL, and response latency. You can filter the span list based on the call result, status code, span side, and response latency.

   Click **Details** in the **Action** column of the target span to view its details.


<span id=".5L2c5Li65pyN5Yqh56uv"></span>
#### As server end

Click **Application monitoring** \> **As server end** to view the upstream list, call topology, monitoring dashboard, and span list when the service functions as a server. You can also configure the query time range.  


* **Upstreams**: Displays the upstream interface list and monitoring information, including QPS, P90 latency, and number of errors. Click an interface in the list to view its monitoring information.

* **Call topology**: Displays the call topologies between the service and upstream instances.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can perform the following operations in the call topology chart:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click the icon of the service or the upstream instance to select different objects and view their monitoring information.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Move the pointer over the specified icon to view the monitoring information of the instance, such as the error rate and the QPS.   </div>
   

* **Monitoring information**: You can view call information for the service and upstream services, such as the QPS, P90 response latency, error rate, number of errors, and QPS grouped by pod.

* **Span list**: Displays the information about the spans when the pod functions as a server, such as the status, time, status code, side, client, server, URL, and response latency. You can filter the span list based on the call result, status code, span side, and response latency.


<span id=".eWFtbC3kv6Hmga8="></span>
### YAML information

Click the **YAML** tab to view the YAML file content of the Service.
