---
title: "Quickly deploying Qwen3-235B-A22B-FP8 with SGLang"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_Qwen3-235B-A22B-FP8_based_on_SGLang"
---

This topic mainly describes how to quickly deploy the Qwen3\-235B\-A22B\-FP8 large language model (LLM) based on SGLang by using Vital Kubernetes Engine (VKE).

<span id="uUgjNoqY"></span>
## Solution introduction

The solution integrates multiple acceleration technologies of BytePlus to quickly deploy the Qwen3\-235B\-A22B\-FP8 LLM in a Kubernetes cluster.


* **Qwen3**: the latest Qwen LLM launched by Alibaba Cloud, which features six dense models and two Mixture\-of\-Experts (MoE) models. With 0.6 billion to 235 billion parameters, Qwen3 can meet diverse business requirements.


<span id="SXXXPhlF"></span>
### Deployment information


* Model: Qwen3\-235B\-A22B\-FP8

* Inference engine: SGLang

* Instance specification: ecs.hpcpni3ln.45xlarge instance \* 1


<span id="njaLQspn"></span>
### Supported features


* Parallel policy: TP

* Precision: FP8

* Monitoring: Vital Managed Service for Prometheus (VMP) and Application Performance Management Plus (APMPlus)

* Access: API Gateway (APIG)


<span id="tp6qAFfV"></span>
## Notes


* To ensure successful deployment, which involves multiple interdependent add\-ons and various configurations, you need to precisely follow the instructions in this document.

* The recommended instance specification described in the **Deployment information** section does not include Remote Direct Memory Access (RDMA) network interface card (NIC), which indicates that GDKV is not supported. Do not edit the `*values.yaml*` file of the application template to enable GDKV.

* To avoid violation of the Vital Kubernetes Engine [limit](https://docs.byteplus.com/en/docs/vke/Limits), we recommend that you proceed based on this solution (or on the resources mentioned in the documents). If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The Qwen model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id="E5oe4lGB"></span>
## 

<span id="ZnxoJ39p"></span>
## Prerequisites

<span id="OcaOUgh0"></span>
### Creating a VKE cluster

The following parameters need to be configured as described in the table when creating a cluster by using the VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). You can also use the managed cluster template for heterogeneous computing to quickly create a VKE cluster for this scenario.


|Configuration item |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select version v1.28 or later. |
|Pod networking model |Select **VPC\-CNI**. |
|**Node pool configuration** ||
|Managed node pool |Enable Managed node pool. |
|Instance type |Select the applied `ecs.hpcpni3ln` instance family of the GPU Accelerated type in beta. |
|Number of nodes |1 node. |
|Data volume |You need to configure two **ESSD** data volumes. Select **1024 GiB** and select the default value **PL0** as the performance level for the two data volumes. In addition, specify `/data01` as the mount directory for one of the **ESSD** data volumes.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The <code>data01</code> directory will be used as a dependency later and therefore cannot be modified.</div><br> |
|**add\-on configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
|apig\-controller |(Required) The APIG controller, which provides cloud\-native AI gateway capabilities to achieve intelligent load balancing of inference traffic based on different policies. |
|csi\-ebs |(Required) It enables VKE clusters to use the standard CSI implementation for Elastic Block Storage (EBS). |
|prometheus\-agent |(Required) Vital Managed Service for Prometheus (VMP) monitoring add\-on collects the monitoring metrics data of the Kubernetes cluster to VMP. |
|apmplus\-opentelemetry\-collector |(Required) Collect OpenTelemetry data and Prometheus metrics, and send them to APMPlus. |
|apmplus\-server\-agent |(Required) Send the collection service and host monitoring data to APMPlus in parallel. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) The event\-driven autoscaler based on Kubernetes completes the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id="NgJlvvqi"></span>
## Procedure

<span id="VYDfuqBv"></span>
### Step 1: Deploy Qwen3\-235B\-A22B\-FP8

VKE provides the Qwen3\-235B\-A22B\-FP8 model application based on the SGLang framework. The application can be quickly deployed through the **Application template** page of the VKE console.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find **qwen3\-235b\-a22b\-fp8\-sglang**, and click **Deploy**.

3. On the **Deploy application** page, specify the parameters of **qwen3\-235b\-a22b\-fp8\-sglang**.

   
   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of qwen3\-235b\-a22b\-fp8\-sglang. We recommend that you select the latest version. |
   |Parameter configuration |The configuration method of qwen3\-235b\-a22b\-fp8\-sglang. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created as described in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |
   

4. Click **Confirm** to start.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace, and click the name of the deployed qwen3\-235b\-a22b\-fp8\-sglang application to go to the details page. On the details page, view the basic information about the application and the created workloads, services, and other resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The services whose names are in the format of <code><application name>-api-svc</code> indicate those services that work as the external access points of their applications, and therefore are supposed to be used during routing configuration and model verification.   </div>
   

5. On the **Deployment** page of the VKE cluster, view the load status of the qwen3\-235b\-a22b\-fp8\-sglang application.

   1. On the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Cluster**, find the target cluster, and click the cluster name.

   2. In the left navigation bar, click **Workload** \> **Deployment**. Then, enter the application name qwen3\-235b\-a22b\-fp8\-sglang in the search box to view the status of the related workload.


<span id="DEfZBSIE"></span>
### Step 2: Configure Ingress

Configure routing for the model through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that is required in cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |**Configuration item** |**Description** |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace where the qwen3\-235b\-a22b\-fp8\-sglang application template is deployed to associate the service exposed by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **cloud\-native API Gateway**. |
   |APIG specification settings ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you are using APIG to expose the model service in the clusters, we recommend that you configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the Classic Load Balancer (CLB) instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Circuit breaking: </strong> When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If a timeout is required, you can configure a timeout in the <a href="https://console.byteplus.com/veapig">API Gateway console</a>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="default"><strong>Observability</strong>: The API Gateway instance created in the VKE console does not enable monitoring alarm and log feature in the default settings. If you need, we recommend that you enable the log feature and monitoring alarm capability of the corresponding instance in the <a href="https://console.byteplus.com/veapig">API Gateway console</a>.</div><br><br><br>      * <div data-tips="true" data-tips-type="default"><strong>Instance monitoring</strong>: This feature helps you detect the issues of the entire system link from the perspective of the Ingress in a timely manner. For example: When the back end is unhealthy or crashes, the API Gateway will report 503 error code and specific errors.</div><br><br><br>      * <div data-tips="true" data-tips-type="default"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select a service that is created when you deploy the qwen3\-235b\-a22b\-fp8\-sglang application template and set the port number to **8080**. The name of the service is in the format of `<application name>-api-svc`. |
   

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: Select **Consumer management** on the left navigation bar and click **Create consumers**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: in the left navigation bar, select **Plugin Center \> Key Auth** and click **Create Plugin** on the page.

      1. **Effect level**: select the **Routing level** and configure the instance, service, and route to which the add\-on belongs.

      2. **Authentication configuration**: select the **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that the API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in step 1.

      4. Other options can remain as the default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP addresses.

   * **backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * To test in the production environment, you need to register the Ingress domain name with your DNS provider and add public or private IPs correspondingly.


<span id="VvdZUbpP"></span>
### Step 3: Enable observability configuration

There are two observability levels, i.e., basic and full\-stack observability. The former one allows you to read the metrics of AI resources and inference services, and the latter offers full\-chain monitoring for inference applications.

<span id="mv4cXYxO"></span>
#### Basic observability


1. In the left navigation bar of the page for a specific cluster, select **Overview** under the gray title **Cloud native observability**, then click **Enable** on the page to start monitoring. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitor dashboard** in the left navigation bar and search for SGLang to open the dashboard as shown below:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png) </span>

   * You can also use Grafana to build a custom monitor dashboard for SGLang\-based applications. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the above Grafana and select to import the following dashboard JSON file:

         <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_21c0b851c442e6eb2b5cd86062e751d4.json" name="SGLang Dashboard-1747206543364.json">SGLang Dashboard-1747206543364.json</Attachment>
         

      2. The effect after import is shown in the figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png) </span>


<span id="KGmBrnie"></span>
#### Deep observability


1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation bar, click **Server\-side Monitoring**.

2. Search for SGLang and click the service name in the results to open the monitoring dashboard page.

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
          "model": "Qwen/Qwen3-235B-A22B-FP8",
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

      On the **Runtime Monitoring** tab, you can view runtime\-related metrics, including CPU time, CPU usage, memory usage, number of GC objects, number of threads, and number of context switches

4. View link analysis.

   From the Trace analysis tab of the SGLang application, you can retrieve the link information according to different conditions. Click a Trace ID you want to open the details page of the trace. View Trace information in the list.


<span id="PztqXyYX"></span>
## Model verification

<span id="vjl5OsM4"></span>
### Method 1: Access through Service

After you deploy the qwen3\-235b\-a22b\-fp8\-sglang application template, the created service, whose name is in the format of `<application name>-api-svc` will provide an HTTP API endpoint (port 8080). The endpoint can be called as you do with OpenAI APIs.

The sample code is as follows.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Replace <code>******</code> in <code>http://******</code> with your service endpoint <code><Application name>-api-svc</code>.</div>


* <div data-tips="true" data-tips-type="default">The parameter content is what you want to type to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen/Qwen3-235B-A22B-FP8",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```


In the **Workload** section of the **Helm details page** that corresponds to the qwen3\-235b\-a22b\-fp8\-sglang application, click the name of the created Deployment to go to the Deployment page. In the upper\-right corner of the details page, click **Console** to log in to the pod that corresponds to the application to call the API.

<span id="zrAyUbgP"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token to the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Replace the <code>example.com</code> in <code>http://example.com</code> with the domain name of the back\-end services obtained in<strong> </strong><strong>Step 2</strong><strong>: configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="default">Replace<code> eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 2</strong><strong>: configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="default">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "Qwen/Qwen3-235B-A22B-FP8",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
