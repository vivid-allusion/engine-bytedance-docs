---
title: "Deployments"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deployment-monitoring"
---

Deployment resource retrieval provides the monitoring information of Deployment resources in clusters, including the resource list and resource details. This topic describes how to view the Deployment list and details.

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

In the **Resource type** panel, select **Deployment** to view the Deployment list. The list displays the basic information and metrics of Deployments.

You can perform the following operations in the Deployment list:


* Click the name of the target Deployment to go to the Deployment details page and view the details.

* Click the number in the **Pods** column to go to the Pod page and view the information about all pods for the Deployment.

* In the upper\-right corner of the list, click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9412a7c0776ecd53386822a7f20fea53.png) </span>icon to switch the metric protocol in the list, including: HTTP(S), DNS, and gRPC \- Unary.


<span id=".6LWE5rqQ562b6YCJ"></span>
### Filtering resources

You can filter Deployments by namespace, status, service, and workload name in the Deployment list.


1. Select the information to be retrieved from the **Namespace**, **Status**, **Service**, and **Deployment** drop\-down lists.

2. Click **Add label/annotation** to configure the labels or annotations for the Deployment.

   
   |Parameters |Description |
   |---|---|
   |Type |Select Label or Annotation to filter Deployments. |
   |Name |Enter the name of the label or annotation in string format. |
   |Operator |Configure the operator. Valid values:<br><br><br>* **Include**: Indicates that the label and annotation contain the specified value.<br><br>* **Not equal to**: Indicates that the label and annotation do not contain the specified value. |
   |Value |Specify the value of the label or the annotation in string format. You can enter multiple values by pressing the spacebar. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add multiple labels or annotations for retrieval.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Multiple values are in an <strong>AND</strong> relationship, which means the Deployment must contain all values.   </div>
   

3. Click **Search** to retrieve the Deployment.


<span id=".6LWE5rqQ6IGa5ZCI"></span>
### Aggregating resources

You can aggregate Deployments by **Namespace**, **Service**, and **Status** in the Deployment list. After aggregation, Deployments are displayed by aggregation dimension.


1. Select the target aggregation dimension from the **Aggregation dimension** drop\-down list.

2. Click **Search** to aggregate Deployments.


<span id=".6LWE5rqQ6K-m5oOF"></span>
## Resource details

In the Deployment list, click the name of the target Deployment to go to its details page. You can view details of the Deployment, including basic information, basic resource observability, application performance observability, network performance observability, and YAML.

<span id=".5Z-656GA5L-h5oGv"></span>
### Basic information

In the **Basic information** section, view the basic information about the Deployment, such as the number of ready pods, number of updated pods, number of available pods, running time, labels, annotations, and pods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the <strong>Pods</strong> section, you can click the name of the target pod to go to the pod details page and view pod details.</div>


<span id=".5Z-656GA6LWE5rqQ6KeC5rWL"></span>
### Basic observability

Click the **Basic observability** tab to view the basic resource information of the Deployment. You can specify the query time range. The information includes CPU information, memory information, storage information, network information, and other information.

<span id=".5bqU55So5oCn6IO955uR5o6n"></span>
### Application monitoring

On the Application monitoring tab, you can view the application performance information of the Deployment and specify the query time range.  


* The application performance can be monitored for different protocols such as HTTP(S), DNS, and gRPC \- Unary.

* Service performance overview, server\-side or client\-side observability dashboards, and span list are supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The monitoring information slightly varies based on different application protocols. This topic provides an example of how to view the monitoring information of the HTTP(S) protocol. For other protocols, the information displayed in the console shall prevail.</div>


<span id=".5pyN5Yqh5oCn6IO9"></span>
#### Performance

Click the **Application monitoring** tab and click a specific protocol. Click **Performance** to view the service performance dashboard and span list for the Deployment.  


* **Service performance dashboard**: Includes service QPS, service QPS grouped by upstream workload (top 5), number of service errors, service error rate, number of service errors grouped by upstream workload (top 5), number of service errors grouped by status code, service P90 response latency, and service P90 response latency grouped by upstream workload (top 5).

* **Span list**: Displays the information about the spans under this protocol, such as the status, time, status code, side, client, server, URL, and response latency. You can filter the span list based on the call result, status code, span side, and response latency.

   Click **Details** in the **Action** column of the target span to view its details.


<span id=".5L2c5Li65pyN5Yqh56uv"></span>
#### As server end

Click the **Application monitoring** tab and click a specific protocol. Click **As server end** to view the upstream list, call topology, monitoring dashboard, and span list when the Deployment functions as a server. You can also specify the query time range.  


* **Upstreams**: Displays the upstream interface list and monitoring information of the Deployment, including QPS, P90 latency, and number of errors. Click an interface in the list to view its monitoring information.

* **Call topology**: Displays the call topologies between the Deployment and upstream instances.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the call topology chart, you can perform the following operations:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click the icon of the workload or the upstream instance to select different objects and view their monitoring information.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Move the pointer over the specified icon to view the monitoring information of the instance, such as the error rate and the QPS.   </div>
   

* **Monitoring information**: You can view call information for the Deployment and upstream services, such as the QPS, P90 response latency, error rate, number of errors, and QPS grouped by pod.

* **Span list**: Displays the information about the spans when the Deployment functions as a server, such as the status, time, status code, side, client, server, URL, and response latency. You can filter the span list based on the call result, status code, span side, and response latency.


<span id=".5L2c5Li65a6i5oi356uv"></span>
#### As client end

Click the **Application monitoring** tab and click a specific protocol. Click **As client end** to view the downstream list, call topology, monitoring dashboard, and span list when the Deployment functions as a client. You can also specify the query time range.  


* **Downstreams**: Displays the downstream interface list and monitoring information of the Deployment, including QPS, P90 latency, and number of errors. Click an interface in the list to view the monitoring information of the interface.

* **Call topology**: Displays the call topologies between the Deployment and upstream instances.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the call topology chart, you can perform the following operations:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click the icon of the workload or the downstream instance to select different objects and view their monitoring information.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Move the pointer over the specified icon to view the monitoring information of the instance, such as the error rate and QPS.   </div>
   

* **Monitoring information**: You can view call information for the Deployment and downstream services, such as the QPS, P90 response latency, error rate, number of errors, and QPS grouped by pod.

* **Span list**: Displays the information about the spans when the Deployment functions as a server, such as the status, time, status code, side, client, server, URL, and response latency. You can filter the span list based on the call result, status code, span side, and response latency.


<span id=".572R57uc5oCn6IO955uR5o6n"></span>
### Network monitoring

On the Network monitoring tab, you can view the network performance information of the Deployment and specify the query time range.

<span id=".5L2c5Li65pyN5Yqh56uv"></span>
#### As server end

Click the **Network monitoring** tab and click **As server end** to view the network monitoring dashboards for the Deployment when it functions as a server, such as dashboards for TCP network traffic, network packet loss, number of TCP connections, number of TCP retransmissions, and TCP connection latency.

<span id=".5L2c5Li65a6i5oi356uv"></span>
#### As client end

Click the **Network monitoring** tab and click **From client side** to view the network monitoring dashboards for the Deployment when it functions as a client, such as dashboards for TCP network traffic, network packet loss, number of TCP connections, number of TCP retransmissions, and TCP connection latency.

<span id=".eWFtbC3kv6Hmga8="></span>
### YAML

Click the **YAML** tab to view the YAML file content of the Deployment.
