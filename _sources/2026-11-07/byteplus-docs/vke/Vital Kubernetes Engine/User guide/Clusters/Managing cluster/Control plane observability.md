---
title: "Control plane observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Control_plane_observability"
---

Control plane observability allows you to view the status of a cluster's control plane and troubleshoot abnormal requests using preset monitoring dashboards and audit logs. This topic describes how to view monitoring data for cluster resources and the control plane services, and how to use K8s Audit Insights to locate abnormal requests.

<span id="FneT4z6T"></span>
## Cluster resource and control plane service monitoring

<span id="AblPZE7L"></span>
### Background

Control plane service monitoring covers common abnormal scenarios related to the operating status of the cluster control plane and provides core dashboards for various types of key control plane resources and components. This helps you quickly understand the operating status and overall health of the control plane. The main monitored objects and content are shown in the following table.


|Monitoring |Major monitored content |
|---|---|
|API Server load and errors |Provides metrics such as request QPS (total volume and read/write distribution), rate\-limited (429) request rate, and 4xx and 5xx error request rates. This information helps you assess the current request load on the API Server, identify the main request types, and quickly detect client configuration errors (4xx) or internal server errors (5xx). Rate\-limiting metrics can also help locate the sources of high\-frequency requests and prevent API Server overload, which affects the entire cluster. |
|Control plane component resource usage |Provides real\-time CPU and memory usage data for control plane components, such as the API Server and Scheduler. This information helps you identify resource bottlenecks in advance. For example, when request volume surges or the node scale grows, you can determine whether to adjust control plane resource specifications to prevent slow cluster responses or entire unavailability due to insufficient resources. |
|ETCD storage size |Provides the total storage used by the ETCD database, as well as the distribution of the number of various Kubernetes resource objects by type. This information helps you assess cluster growth trends. When storage grows rapidly, you can identify which types of resources, such as ConfigMaps, Secrets, and custom resources, are accumulating in large numbers and clean them up in time to prevent ETCD storage overflow from causing cluster stability risks. |
|Scheduling throughput |Provides the number of scheduling attempts made by the scheduler per unit time, broken down by scheduling result (successful, failed, and unschedulable). This information helps you determine whether the cluster's scheduling capability meets business requirements. When the number of failed or unschedulable cases continues to rise, you can quickly identify whether the cause is insufficient resources, conflicts in node taint or affinity configurations, or abnormal processing by the scheduler itself, thereby reducing troubleshooting time. |
|Webhook health |Provides the call volume, request latency (P90), and number of rejected requests for admission webhooks. A webhook is a critical part of the cluster resource creation workflow. Excessive latency or a rising rejection rate can directly block Pod creation and resource changes. These metrics help you promptly detect webhook performance degradation or configuration errors and quickly determine whether the webhook service needs to be scaled out or the rule configuration needs to be fixed. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more control plane metrics and monitoring dashboards, see <a href="https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability?lang=en">Control plane service observability</a>.</div>


<span id="Ej1UOTJY"></span>
### Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* Control plane service observability has been enabled, and metric collection for control plane components such as the API Server, Scheduler, and etcd has been enabled. For details, see [Control plane service observability](https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability?lang=en).


<span id="Y6gFkAh8"></span>
### Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the name of the target cluster to go to the management page of this cluster.

3. In the left navigation pane, select **Overview**. On the **Overview** page, select the **Control plane observability** tab to view the cluster control plane service monitoring dashboard.

   The detailed chart descriptions for the control plane service monitoring dashboard are shown in the following table.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For the method of obtaining the PromQL statements that correspond to the charts, see <a href="https://docs.byteplus.com/en/docs/vke/Using_dashboard">Using dashboards</a>.   </div>
   

   
   |Chart name |Unit |Chart description |
   |---|---|---|
   |APIServer request QPS |req/s |The total number of requests, read requests, and write requests received per second by the API Server, reflecting the access load on the cluster API.<br><br><br>* Under normal circumstances, request QPS fluctuates steadily within the business baseline range.<br><br>* If request QPS continues to surge, it may indicate a spike in business requests or abnormal client retries. If request QPS suddenly drops, it may indicate abnormal client access or a service issue. |
   |APIServer limited viewership of (429) requests |req/s |The instantaneous rate at which the API Server returns status code 429 (rate limiting), calculated based on the last two samples in the past minute. This information reflects the rate at which requests are being rate\-limited.<br><br><br>* Under normal circumstances, the number of rate\-limited requests should be 0 or should increase only occasionally.<br><br>* If the number of rate\-limited requests remains above 0 or increases significantly, it indicates that the request rate has exceeded the current rate\-limiting threshold. Troubleshoot the sources of high\-frequency requests and the traffic control configuration. |
   |CPU Usage of Control Plane Components |% |The current CPU usage of control plane components, reflecting the compute resource load on the control plane components.<br><br><br>* Under normal circumstances, CPU usage fluctuates steadily within the business baseline range and does not remain close to 100% for an extended period.<br><br>* If CPU usage remains high or surges, it may indicate an increase in control plane requests or greater processing pressure on components. |
   |APIServer 4XX request |req/s |Shows the per\-second rate of requests for which the API Server returned 4xx status codes (client errors), sampled over the past minute. This metric reflects cases where client requests did not complete successfully and may be caused by factors such as authentication or authorization issues, missing resources, resource conflicts, parameter validation failures, or rate limiting.<br><br><br>* Under normal circumstances, the volume of 4xx requests should remain at a low level, and occasional fluctuations are normal.<br><br>* If 4xx requests continue to increase, it usually indicates that some clients have configuration errors or abnormal permissions. You are advised to use the HTTP 4xx query scenario in K8s Audit Insights to identify the sources of frequent errors and investigate the request content. |
   |APIServer 5XX request |req/s |The per\-second rate of API Server requests returning 5xx status codes (server\-side errors), sampled over the past 1 minute. This information reflects cases where the API Server or its backend dependencies failed to process requests successfully.<br><br><br>* Under normal circumstances, the number of 5xx requests should be close to 0. Occasional, extremely low\-frequency occurrences are reasonable.<br><br>* If the number of 5xx requests persists or suddenly increases, the API Server may have internal errors. We recommend using the HTTP 5XX query scenario in K8s Audit Insights to identify the sources of requests triggering server\-side errors and to check the resource usage of control plane components. |
   |Control plane components memory usage |% |The current memory usage of each control plane component, reflecting the control plane's memory resource consumption.<br><br><br>* Under normal circumstances, the memory usage of each component should remain stable without significant fluctuations.<br><br>* If memory usage continues to rise or approaches the upper limit, it may indicate that control plane components are processing a large number of requests or that there is a risk of a memory leak. Assess this together with request volume metrics and consider whether resource specifications need to be adjusted. |
   |Scheduling throughput (Pods/s) |req/s |Shows the number of scheduling attempts per second made by the Scheduler, categorized by scheduling result, reflecting Pod scheduling throughput and result distribution.<br><br><br>* Under normal circumstances, successful scheduling throughput varies with the number of Pods created, while failed or unschedulable attempts remain low.<br><br>* If failed or unschedulable attempts continue to increase, it may indicate insufficient cluster resources, scheduling constraint conflicts, or abnormal scheduler behavior. |
   |Resources object size |Bytes |Shows the total storage used by different resource objects in the cluster's etcd database, reflecting the overall storage size of resource objects in the cluster.<br><br><br>* Under normal circumstances, etcd storage usage should correspond to the number and size of resource objects in the cluster, with a stable growth trend.<br><br>* If storage usage continues to grow rapidly, it may indicate that cluster resources are not being cleaned up, or that the data volume of a certain object type is expanding abnormally. Cross\-reference the resource object count chart to identify the source of growth and clean up unnecessary resources promptly. |
   |number of resource objects |\- |Shows the number of objects for different resource types in the cluster and the top 50 resource types by object count, reflecting the distribution of resource object scale.<br><br><br>* Under normal circumstances, the number of each type of resource object aligns with the business scale, and the change trend remains stable.<br><br>* If the number of a certain type of resource object grows rapidly or significantly exceeds expectations, it may indicate that resources are not being cleaned up in time or that the controller is repeatedly creating resources. |
   |Webhook request |req/s |The number of requests per second sent by the API Server to the admission webhook. This information reflects the invocation load on the admission webhook.<br><br><br>* Under normal conditions, the request count changes steadily with resource creation and update operations.<br><br>* If the request count continues to surge, it may indicate a spike in resource change operations or frequent client retries. |
   |Webhook latency |Milliseconds |Shows the P90 value of admission webhook request latency over the past minute, reflecting the processing time for most admission requests.<br><br><br>* Under normal circumstances, P90 latency remains stable within the business baseline range.<br><br>* If P90 latency continues to rise, it may indicate that the webhook service is responding more slowly, the network is abnormal, or processing pressure is increasing. |
   |Webhook reject request |req/s |The number of requests per second rejected by the admission webhook on the API Server, broken down by error type. This information reflects admission validation failures.<br><br><br>* Under normal circumstances, the number of rejected requests should be 0, or only a small number of expected rejections exist.<br><br>* If the number of rejected requests continues to increase, it indicates that resource requests are failing admission validation. Troubleshoot the webhook configuration, policies, or service status based on the error type. |
   


<span id="ixCL52Tu"></span>
## Audit log

<span id="xCXD5Ayp"></span>
### Background

After the audit feature is enabled for the cluster, the system uploads audit logs to [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS?lang=en) for storage and querying. To help you quickly locate abnormal API Server requests, the system provides the following preset query scenarios in the control plane observability feature, covering common API Server anomalies. This eliminates the need to manually write log query statements, allowing you to quickly diagnose and locate control plane issues.


|Preset events |Description |
|---|---|
|Top Clients by Request Volume |Shows a ranking of the clients that sent the most requests to the API Server within the specified time range. This information helps you quickly identify high\-frequency callers. When the API Server is under excessive load or rate limiting occurs, you can directly determine which component or application is generating the most requests, providing a clear target for subsequent rate limiting or optimization. |
|Slow Requests |Displays API Server requests sorted by duration in descending order, highlighting the requests with the longest processing time. This information helps you identify the operation types and call sources with abnormal latency. When users report slow responses to cluster operations, you can quickly determine which types of requests are slowing overall response and troubleshoot control plane performance bottlenecks. |
|HTTP 4XX |Statistics on the request sources that return the most 4xx status codes (client errors, such as 403 for insufficient permissions and 404 for resource not found). This information helps you quickly identify callers with configuration errors or permission issues. A continued accumulation of 4xx responses usually means that a component or user is calling APIs incorrectly. Fixing the issue in time can reduce the extra load that invalid requests place on the API Server. |
|Rate\-Limited Requests |Shows the client with the highest number of blocked requests due to exceeding the API Server rate limit (429). This information helps you determine which components or applications are putting request pressure on the control plane. Rate limiting affects not only the client itself but also consumes the request quota of other components. This scenario helps you precisely identify the source of the pressure and optimize traffic control or client requests. |
|HTTP 5XX |Statistics on the request sources and operation types that trigger the most 5xx status codes (server errors). This information helps you identify operation patterns that may cause control plane instability. A 5xx status code usually means that an error occurred during internal processing in the API Server. By locating high\-frequency triggering sources, you can quickly determine whether the issue is caused by a specific operation or by an overall control plane issue, shortening troubleshooting time. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more cluster audit events, you can go to TLS to query them in detail. For details, see <a href="https://docs.byteplus.com/en/docs/tls/Query-and-analysis-2?lang=en">Retrieval analysis</a>.</div>


<span id="zVbj9bAt"></span>
### Prerequisites

The cluster audit feature has been enabled. For details, see [Cluster audit](https://docs.byteplus.com/en/docs/vke/Cluster-auditing?lang=en).

<span id="oNisRoLi"></span>
### Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to go to its management page.

3. In the left navigation pane, select **Overview**. On the **Overview** page, select the **Control plane observability** tab to view the cluster's preset audit logs.
