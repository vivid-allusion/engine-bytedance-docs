---
title: "Quickly deploying Qwen3-32B-FP8 with SGLang"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quick_deployment_of_Qwen3-32B-FP8_based_on_SGlang"
---

The following content introduces how to quickly deploy a Qwen3\-32B\-FP8 LLM based on SGLang using Vital Kubernetes Engine (VKE).

<span id="JLIWsYJe"></span>
## Solution introduction

This solution provides a quick method of deploying Qwen3\-32B\-FP8 LLM in a Kubernetes cluster that integrates a series of acceleration technologies that come with the BytePlus:

**Qwen3**: the latest Qwen model launched by Alibaba Cloud, which includes 2 Mixture of Experts (MoE) models and 6 Dense models, with a parameter count ranging from 0.6B to 235B to meet diverse needs.

Advantages of the solution:


* **Cache pooling**: build a distributed cache pool by gathering the idle memory and disk of GPU clusters, overcoming the limitation of single\-machine memory size.


<span id="65oKEbQz"></span>
### Deployment information


* Model: Qwen3\-32B\-FP8

* Inference engine: SGlang

* Instance specification: ecs.pni3l.11xlarge instance \* 1


<span id="F2K6qxYl"></span>
### Capabilities


* Precision: FP8

* Monitoring: Vital Managed Service for Prometheus (VMP) and Application Performance Management Plus (APMPlus)

* Access: API Gateway (APIG)


<span id="NLwTWdFk"></span>
## Notes


* To ensure successful deployment, which involves multiple interdependent add\-ons and various configurations, you need to precisely follow the instructions in this document.

* The recommended instance specification described in the **Deployment information** section does not include Remote Direct Memory Access (RDMA) network interface card (NIC), which indicates that GDKV is not supported. Do not edit the `*value.yaml*` file of the application template to enable GDKV.

* To avoid violation of the Vital Kubernetes Engine [limit](https://docs.byteplus.com/en/docs/vke/Limits), we recommend that you proceed based on this solution (or on the resources mentioned in the documents). If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |ecs.pni3l instance family of the GPU Accelerated type |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The GPU Accelerated instances, which provide computing power. The model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.pni3l.11xlarge`. |
   


<span id="bV0WH9Tv"></span>
## Prerequisites

<span id="kvNtACvk"></span>
### Creating a VKE cluster

The following parameters need to be configured as described in the table when creating a cluster by using the VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). You can also use the managed cluster template for heterogeneous computing to quickly create a VKE cluster for this scenario.


|Configuration item |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select version v1.28 or later. |
|Pod networking model |Select **VPC\-CNI**. |
|**Node pool configuration** ||
|Managed node pool |**Enable** Managed node pool. |
|Instance type |Select the applied `ecs.pni3l` instance family of the GPU Accelerated type in beta. |
|Number of nodes |1 node. |
|data volume |You need to configure two **ESSD** data volumes. Select **1024 GiB** and set the performance level to the default value PL0 for the two data volumes. In addition, specify `/data01` as the mount directory for one of the **ESSD** data volumes.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The <code>data01</code> directory will be used as a dependency later and therefore cannot be modified.</div><br> |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
|apig\-controller |(Required) The API Gateway controller provides cloud\-native AI gateway capabilities and enables intelligent load balancing for inference traffic based on different policies. |
|csi\-ebs |(Required) It enables VKE clusters to use the standard CSI implementation for Elastic Block Storage (EBS). |
|prometheus\-agent |(Required) Vital Managed Service for Prometheus (VMP) monitoring add\-on collects the monitoring metrics data of the Kubernetes cluster to VMP. |
|apmplus\-opentelemetry\-collector |(Required) Collects OpenTelemetry data and Prometheus metrics, and sends them to APMPlus. |
|apmplus\-server\-agent |(Required) Collects service and host monitoring data and sends it to APMPlus. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) The event\-driven autoscaler based on Kubernetes completes the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU workloads, such as system add\-ons, using Vital Container Instance (VCI), which eliminates the need for O&M and does not consume the computing resources of GPU nodes. |


<span id="6DtgycWE"></span>
## Procedure

<span id="fXBt6QkY"></span>
### Step 1: Deploy Qwen3\-32B\-FP8

The VKE allows Qwen3\-32B\-FP8 model\-based applications to run on the SGLang framework, which can be quickly realized by using the **application template**.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Application center \> Application template**.

2. On the **Application template** page, find **qwen3\-32b\-fp8\-sglang** and click **Deploy**.

3. Configure **qwen3\-32b\-fp8\-sglang** parameters on the **Deploy application** page.

   
   |Configuration item |Description |
   |---|---|
   |**application template** ||
   |Application template |Select the latest Chart version of qwen3\-32b\-fp8\-sglang. |
   |Parameter configuration |The configuration method of qwen3\-32b\-fp8\-sglang. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting the agreement.  |
   

4. Click **Confirm** to start.

   The applications that are already deployed can be found on the **Helm** page. Find qwen3\-32b\-fp8\-sglang application by specifying the target project, cluster, and namespace, then click it to view detailed information about the application.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The services whose names are in the format of <code><application name>-api-svc</code> indicate those services that work as the external access points of their applications, and therefore are supposed to be used during routing configuration and model verification.   </div>
   

5. View the load status of qwen3\-32b\-fp8\-sglang applications on the **Deployment** page of the VKE cluster.

   1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Cluster** and click the cluster name.

   2. In the left navigation bar, select **Workload** \> **Deployment**, then enter the name qwen3\-32b\-fp8\-sglang in the search box to find it and view its status.


<span id="IJfq0ZmX"></span>
### Step 2: Configure routing

Configure routing for the model through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that is required in cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |**Configuration item** |**Description** |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace in which the qwen3\-32b\-fp8\-sglang application template is deployed. It is used to associate the service that is supposed to be exposed for its application. |
   |**Ingress configuration** ||
   |Ingress type |Select **cloud\-native API Gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you are using APIG to expose the model service in the clusters, we recommend that you configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the CLB instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance in the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Circuit breaking: </strong> When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If you have timeout demand, the VKE supports that you configure timeout in the <a href="https://console.byteplus.com/veapig">API Gateway console</a>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Observability</strong>: By default, the alerting, monitoring, and logging capabilities are disabled for APIG instances that are created via the VKE console. If needed, we recommend that you enable the logging, monitoring, and alerting capabilities of the instances in the <a href="https://console.byteplus.com/veapig">API Gateway console</a>.</div><br><br><br>      * <div data-tips="true" data-tips-type="default"><strong>Instance monitoring</strong>: This feature can help you to timely detect the unexpected phenomena in the chains of the whole system at the entry gateway level. For example: When the back end is unhealthy or crashes, the API Gateway will report 503 error code and specific errors.</div><br><br><br>      * <div data-tips="true" data-tips-type="default"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listening configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select the service that was named in the pattern `<application name>-api-svc` and associated with the application created based on qwen3\-32b\-fp8\-sglang template, and then set the port number to **8080**. |
   

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: In the left navigation bar, click **Consumer Management**. On the page that appears, click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: in the left navigation bar, select **Plugin Center \> Key Auth** and click **Create Plugin** on the page.

      1. **Effect level**: select the **Routing level** and configure the instance, Service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select the **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that the API Key will be included in the Authorization header of requests.

      3. **Consumer**: Select the consumer created in Step 1.

      4. Other options can remain as the default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP addresses.

   * **backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution.

   * To test in the production environment, you need to register the Ingress domain name with your DNS provider and add public or private IPs correspondingly.


<span id="TccaSQBQ"></span>
### Step 3: Enable observability configuration

Basic observability provides the metrics for AI resources and inference services. Deep observability provides end\-to\-end performance monitoring services for inference applications.

<span id="DbT06odt"></span>
#### Basic observability


1. In the left navigation bar of the cluster management page, click **Cloud native observability** \> **Overview**. On the page that appears, click **Enable ** to enable cloud native observability and VKE observability. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitoring dashboard** in the left navigation bar and search for SGLang to open the dashboard as shown below:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png) </span>

   * You can also use Grafana to build a custom monitoring dashboard for SGlang\-based applications. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the above Grafana and select to import the following dashboard JSON file:

         <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_21c0b851c442e6eb2b5cd86062e751d4.json" name="SGLang Dashboard-1747206543364.json">SGLang Dashboard-1747206543364.json</Attachment>
         

      2. The effect after import is shown in the figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png) </span>


<span id="Jw01gxG7"></span>
#### Deep observability


1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation bar, click **Server\-side Monitoring**.

2. Search for SGlang and click the service name in the results to open the monitoring dashboard page.

3. View metrics.

   * LLM metrics

      On tabs such as ** Service Overview**, **LLM Performance**, and **Token Usage**, you can view the core metrics of the LLM service, including the number of LLM calls, token usage, response latency, TTFT, TPOT, QPS, and request error rate.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">TTFT and TPOT are effective only when LLMs are called with streaming\-enabled requests.      </div>
      

      The example of a streaming call is as follows:

      ```Bash
      curl localhost:8080/v1/chat/completions \
        -H "Content-Type: application/json" \
        -d '{
          "model": "Qwen3-32B-FP8",
          "messages": [
            {
              "role": "user",
              "content": "hello"
            }
          ],
          "stream": true,
          "stream_options": {
            "include_usage": true,
            "continuous_usage_stats": true
          }
        }'
      ```
      

   * Runtime metrics

      On the **Runtime monitoring** tab, you can view runtime\-related metrics, including CPU time, CPU usage, Memory usage, Number of GC objects, Number of threads, and Number of context switches.

4. View link analysis.

   On the Trace analysis page of the SGLang\-based applications, you can search for trace information based on different conditions. Click the ID of the target trace to go to the details page of the trace. View trace information in the list.


<span id="SLZtLexl"></span>
## Model verification

<span id="x9nEylt8"></span>
### Method 1: Access via Service

The service, created along with the deployment of qwen3\-32b\-fp8\-sglang application, has a name matching the pattern `<application name>-api-svc`. You can use the endpoint address (port 8080) corresponding to that service name to implement a test in this method. The endpoint is OpenAPI\-compatible.

The sample code is as follows.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Replace <code>******</code> in the <code>http://******</code> with the endpoint of your <code><application name>-api-svc</code> service.</div>


* <div data-tips="true" data-tips-type="default">The parameter content is what you want to type to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "/data/models/Qwen3-32B-FP8",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```


Alternatively, you can directly log in to the pod to perform API calls. To do that, you can go to the **Helm application details** page of the qwen3\-32b\-fp8\-sglang application, click the associated deployment in the **Workload ** section, and then click **Console** in the upper\-right corner of the new page to open the console where commands can be executed.

<span id="Ssiv58rU"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Replace the <code>example.com</code> in <code>http://example.com</code> with the domain name of the back\-end services obtained in <strong>step 2: configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="default">Replace<code> eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>S</strong><strong>tep 2: Configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="default">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "/data/models/Qwen3-32B-FP8",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
