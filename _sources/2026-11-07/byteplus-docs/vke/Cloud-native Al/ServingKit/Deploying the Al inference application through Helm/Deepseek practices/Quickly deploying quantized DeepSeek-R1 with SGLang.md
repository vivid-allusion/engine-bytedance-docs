---
title: "Quickly deploying  quantized DeepSeek-R1 with SGLang"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploy_the_DeepSeek-R1_Quantitative_version_based_on_SGLang"
---

This topic introduces how to quickly deploy a quantized DeepSeek\-R1 model inference service based on SGLang using Vital Kubernetes Engine (VKE).

<span id="82ReG2Ex"></span>
## Solution introduction

This solution, combined with multiple acceleration technologies of the BytePlus, provides methods for quickly deploying the DeepSeek\-R1\-W4AFP8 Large Language Model (LLM) in the Kubernetes clusters.

**DeepSeek\-R1 model**: released by Chinese AI startup DeepSeek, the R1 model is an inference model trained based on DeepSeek\-V3\-Base, excelling in mathematics, code, and natural language reasoning, gaining wide attention for its open source, algorithm innovation, and cost\-effectiveness.

<span id="MzAQTQDo"></span>
### Deployment information


* Model: DeepSeek\-R1\-W4AFP8

* Inference engine: SGlang

* Recommended specification: ecs.hpcpni3ln.45xlarge \* 1 unit


<span id="maFlmxTs"></span>
### Supported capabilities


* Parallel policies: TP+EP

* Data precision: W4AFP8

* Observability: Vital Managed Service for Prometheus (VMP) and Application Performance Management Plus (APMPlus).

* Access: API Gateway (APIG)


<span id="ncGf9hOL"></span>
## Notes


* In this example, many add\-ons are used, which are dependent on each other and have complex configurations. To achieve the expected results, you must perform operations according to the guidance in this article.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of BytePlus. Contact the account manager of BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The Deepseek model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id="xkwB56Uo"></span>
## Prerequisites

<span id="2xeC1C8S"></span>
### Creating an HPC cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>region and availability zone</strong> where the high\-performance compute cluster is located need to be consistent with <strong>those</strong> of the VKE nodes.</div>


<span id="Vjweb9k3"></span>
### Creating a VKE cluster

The following parameters need to be configured as described in the table when creating a cluster by using VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).


|Configuration item |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select version v1.28 or later. |
|Network model |Select **VPC\-CNI**. |
|**Node pool configuration** ||
|Managed node pool |**Enable** managed node pool. |
|Availability zone |Same availability zone as the **High\-Performance Compute Cluster**. |
|Instance type |Select `ecs.hpcpni3ln`, the GPU Accelerated specification. Ensure you already obtained permission for trial of the beta version. |
|High Performance Computing Cluster |Select the HPC cluster you created. |
|Number of nodes |1 node. |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory has subsequent dependencies. Therefore, the directory cannot be modified or specified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure the data that needs long\-term storage has been <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backed up</a> properly in case of computer crashes or disk damage which causes data loss.   </div><br>    |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
|apig\-controller |(Required) API Gateway controller provides the AI Gateway capability of cloud\-native, which can complete the intelligent load balancing of the inference traffic according to different policies. |
|csi\-ebs |(Required) It enables VKE clusters to use the standard CSI implementation for Elastic Block Storage (EBS). |
|prometheus\-agent |(Required) Vital Managed Service for Prometheus (VMP) monitoring add\-on collects the metrics data of the Kubernetes cluster to VMP. |
|apmplus\-opentelemetry\-collector |(Required) Collect OpenTelemetry data and Prometheus metrics, and send them to APMPlus. |
|apmplus\-server\-agent |(Required) Send in parallel the collection service and host monitoring data to APMPlus. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) The event\-driven autoscaler based on Kubernetes. It performs auto scaling for reference services based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id="Cz8ap3v0"></span>
## Procedure

<span id="WEdAwu81"></span>
### Step 1: Deploy deepseek\-r1\-w4afp8\-sglang

The VKE provides the DeepSeek\-R1\-W4AFP8 model application based on the SGLang framework, and you can quickly deploy this application model through **Application template**.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find **deepseek\-r1\-w4afp8\-sglang** and click **Deploy**.

3. On the **Deploy application** page, configure the service parameters of **deepseek\-r1\-w4afp8\-sglang**.

   
   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of deepseek\-r1\-w4afp8\-sglang. We recommend you to select the latest version. |
   |Parameter configuration |The configuration method for deepseek\-r1\-w4afp8\-sglang. Click the Edit icon to view the configuration description of various parameters in the `values.yaml` file or edit the YAML file.  |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Customize and select the namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |
   

4. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace, and find the deployed application deepseek\-r1\-w4afp8\-sglang. Click the application name and enter the details page to view the basic information, the workloads, services, and other resources created in association with this application.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The services whose names are in the format of <code><application name>-api-svc</code> indicate those services that work as the external access points of their applications, and therefore are supposed to be used during routing configuration and model verification.   </div>
   

5. In the **Deployment** page of the VKE clusters, view the load status corresponding to the deepseek\-r1\-w4afp8\-sglang application.

   1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Cluster**. ** ** Find the target cluster and click the cluster name.

   2. Select **Workload** \> **Deployment** on the management page of the target cluster, and then search for the name of the deepseek\-r1\-w4afp8\-sglang application to view the relevant load status.


<span id="YF1yzLid"></span>
### Step 2: Configure routing

Configure model routing through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that are required in cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace of the deepseek\-r1\-w4afp8\-sglang application template. This is associated with the services exposed by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you are using the API Gateway to expose the model service in the clusters, we recommend that you configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the CLB instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance in the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong> When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If timeout is needed, you can configure it on the <a href="https://console.byteplus.com/veapig">API Gateway console</a>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: By default, the alerting, monitoring, and logging capabilities are disabled for APIG instances that are created via the VKE console. If needed, we recommend that you enable the logging, monitoring, and alerting capabilities of the instances in the <a href="https://console.byteplus.com/veapig">APIG console</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This can help you to detect the anomalies in the whole system chain from the gateway entry level. For example: Unhealthy back end and back\-end crashes will cause the APIG to return <code>503</code> error code and specific errors.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the ** Load balancing algorithm** to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |After deploying the deepseek\-r1\-w4afp8\-sglang application template, associate it with the service whose name is in the format of  `<application name>-api-svc`, and set the port number to **8080**. |
   

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: Select **Consumer management** on the left navigation bar and click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level** and configure the instance, service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: Select the consumer created in Step 1.

      4. Other options can remain as default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP.

   * **Backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * In a production environment, configure an access domain name for the Ingress at the domain name provider, and make sure that the public or private IP address of the Ingress is configured in the A record of the Ingress access domain name.


<span id="dKeoHq0l"></span>
### Step 3: Enable observability configuration

Basic observability provides the metrics for AI resources and inference services. Deep observability provides end\-to\-end performance monitoring services for inference applications.

<span id="ogSEWXzS"></span>
#### Basic observability


1. In the left navigation bar of the page for a specific cluster, select **Overview** under the gray title **Cloud native observability**, then click **Enable** on the page to start monitoring. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitoring dashboard** in the left navigation bar and search for `SGlang` to open the dashboard as shown below:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png) </span>

   * You can also build a Grafana on your own and establish the monitoring dashboard of sglang. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the above Grafana and select Import the JSON file of the following dashboard:

         <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8a819899c3bab3f2b507a0d738b02aa.json" name="SGLang Dashboard-1747206543364.json">SGLang Dashboard-1747206543364.json</Attachment>
         

      2. The effect after import is shown in the figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png) </span>


<span id="GdfwvAFb"></span>
#### Deep observability


1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation bar, click **Server\-side monitoring**.

2. Search for `SGlang` and click the service name in the results to open the monitoring dashboard page.

3. View metrics.

   * LLM metrics

      On tabs such as ** Service Overview**, **LLM performance**, and **Token usage**, you can view the core metrics of the LLM service, including number of LLM calls, token usage, response latency, TTFT, TPOT, QPS, and request error rate.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">TTFT and TPOT are effective only when LLMs are called with streaming\-enabled requests.      </div>
      

      The example of streaming call is as follows:

      ```Bash
      curl localhost:8080/v1/chat/completions \
        -H "Content-Type: application/json" \
        -d '{
          "model": "DeepSeek-R1-W4AFP8",
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

      On the **Runtime monitoring** tab, you can view runtime\-related metrics, including CPU time, CPU usage, memory usage, number of GC objects, thread count, and context switch count.

4. View link analysis.

   From the Trace analysis tab of the SGLang application, you can retrieve the link information according to different conditions. Click the ID of the target trace to go to the details page of the trace. View the trace information in the list.


<span id="PcC6kNO5"></span>
## Model verification

<span id="NV7LnIpW"></span>
### Method 1: Access through Service

After deploying the deepseek\-r1\-w4afp8\-sglang application template, associate it with the services whose names are in the format of `<application name>-api-svc`, which provides an HTTP API endpoint (port 8080).

The sample code is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>******</code> in <code>http://******</code> with the endpoint of your <code><application name>-api-svc</code> Service.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "DeepSeek-R1-W4AFP8",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```


You can, in the **Workload** area of the **Helm application details page** corresponding to the deepseek\-r1\-w4afp8\-sglang application, click to associate with the workload created. Then the page will redirect to the **Deployment** page. Click **Console ** in the upper\-right corner of the page, and log in to the Pod of the application, to execute API invocations.

<span id="4ATqqSmQ"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>example.com</code> in the <code>http://example.com</code> with the Ingress backend service access domain name obtained in <strong>Step 2: Configure routing</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 2: Configure routing</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> specifies the text you input to chat with LLMs.</div>



```Bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "DeepSeek-R1-W4AFP8",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
