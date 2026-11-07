---
title: "Quickly deploying DeepSeek-R1 (full version) with SGLang"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_full-version_DeepSeek-R1_on_SGLang"
---

The following content introduces how to quickly deploy a model inference service with the full\-version DeepSeek\-R1 based on SGLang by using Vital Kubernetes Engine (VKE).

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

This solution provides a quick method of deploying DeepSeek\-R1 LLM in a Kubernetes cluster that integrates a series of acceleration technologies that come with the BytePlus:


* **DeepSeek\-R1 model**: released by Chinese AI startup DeepSeek, the R1 model is an inference model trained based on DeepSeek\-V3\-Base, excelling in mathematics, code, and natural language reasoning, gaining wide attention for its open source, algorithm innovation, and cost\-effectiveness.

* **GDKV model acceleration**: a fast model loading solution achieved through the Remote Direct Memory Access (RDMA) and GPU Direct RDMA (GDR) technologies provided by BytePlus.


Advantages of the solution:


* **Rapid model loading**: Multiple acceleration technologies are used to reduce the loading time of the DeepSeek\-R1 model to 13 seconds, with a loading speed increased by more than 40 times.

* **Cache pooling**: breaks through the single\-machine memory wall limit by integrating idle memory and disks of GPU clusters to build a distributed cache pool.


<span id=".6YOo572y5L-h5oGv"></span>
### Deployment information


* Model: DeepSeek\-R1\-671B

* Inference engine: SGLang

* Instance specification: ecs.hpcpni3ln.45xlarge instance\* 2


<span id=".5pSv5oyB6IO95Yqb"></span>
### Capabilities


* Precision: FP8

* Model acceleration: GDKV

* Monitoring: Vital Managed Service for Prometheus (VMP) and Application Performance Management Plus (APMPlus)

* Access: API Gateway (APIG)


<span id=".5L2_55So6K-05piO"></span>
## Notes


* To ensure successful deployment, which involves a bunch of add\-ons dependent on each other and a variety of configurations, you need to exactly follow the instructions in this document.

* To avoid violation of the VKE [limit](https://docs.byteplus.com/en/docs/vke/Limits), we recommend that you proceed based on this solution (or on the resources mentioned in the documents). If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The DeepSeek model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

<span id=".5Yib5bu66auY5oCn6IO96K6h566X6ZuG576k"></span>
### Create a High\-Performance Compute Cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>region and availability zone</strong> where the high\-performance compute cluster is located need to be consistent with the <strong>region and availability zone</strong> of the VKE nodes.</div>


<span id=".5Yib5bu6LXZrZS3pm4bnvqQ="></span>
### Creating a VKE cluster

The following parameters need to be configured as described in the table when creating a cluster by using the VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).


|Configuration item |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select version v1.28 or later. |
|Network model |Select **VPC\-CNI**. |
|**Node pool configuration** ||
|Managed node pool |**Enable** Managed node pool. |
|Availability zone |Same availability zone as the **High\-Performance Compute Cluster**. |
|Instance type |Select `ecs.hpcpni3ln`, the GPU Accelerated specification. Ensure you already obtained permission for trial of the beta version. |
|High Performance Computing Cluster |Select the HPC cluster you created. |
|Number of nodes |2 nodes. |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory has subsequent dependencies. Therefore, the directory cannot be modified or specified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure the data that needs long\-term storage has been <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backed up</a> properly in case of computer crashes or disk damage which causes data loss.   </div><br>    |
|Node labels |When you deploy the DeepSeek model by using VKE, you need to specify the RDMA usage mode by using node labels.<br><br>Set the label key to `vke.node.rdma.mode` and the label value to `shared`. |
|Kubelet configs |The non\-uniform memory access (NUMA) affinity policy for RDMA devices needs to be configured by using custom parameters with the Kubelet when deploying DeepSeek model in the VKE.<br><br>Select the parameter `topology-manager-policy` and its value `best-effort`. |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
|rdma\-device\-plugin |(Required) The add\-on manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. |
|apig\-controller |(Required) API Gateway controller provides the AI Gateway capability of cloud\-native, which can complete the intelligent load balancing of the inference traffic according to different policies. |
|csi\-ebs |(Required) It allows VKE clusters to use the standard Container Storage Interface (CSI) of TOS. |
|prometheus\-agent |(Required) Vital Managed Service for Prometheus (VMP) monitoring add\-on collects the monitoring metrics data of the Kubernetes cluster to VMP. |
|apmplus\-opentelemetry\-collector |(Required) Collect OpenTelemetry data and Prometheus metrics, and send them to Application Performance Management Plus (APMPlus). |
|apmplus\-server\-agent |(Required) Send the collection service and host monitoring data to APMPlus in parallel. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) The event\-driven autoscaler based on Kubernetes completes the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LqM77ya6YOo572yLWxlYWRlcndvcmtlcnNldA=="></span>
### Step1: Deploy LeaderWorkerSet

In this topic, LeaderWorkerSet (LWS) is used to orchestrate the inference workloads across multiple nodes (for example, DeepSeek R1 needs to be deployed across two nodes). LWS allows you to specify a group of pods as objects to be replicated.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Application template**. Scroll to the bottom of the page, click **More application templates**.

3. Find **leader\-worker\-set**, move the pointer over it, and then click **Deploy**.

4. On the **Deploy application** page, configure the parameters for **leader\-worker\-set**.

   
   |Configuration item |Descriptio |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the latest Chart version of **leader\-worker\-set**. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster type |Keep the default value as **Managed version**. |
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |
   

5. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Find  leader\-worker\-set application by specifying target project, cluster, and namespace, and then click it to view detailed information of the application.


<span id=".5q2l6aqk5LiJ77ya6YOo572yLWRlZXBzZWVrLXIxLXNnbGFuZw=="></span>
### Step 2: Deploy deepseek\-r1\-sglang

VKE allows DeepSeek\-R1 model based applications to run with PD (Prefill\-Decode) disaggregation on the SGLang framework, which can be quickly realized by using the **Application template**.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find **deepseek\-r1\-sglang** and click **Deploy**.

3. On the **Deploy application** page, configure the parameters for **deepseek\-r1\-sglang**.

   
   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the latest Chart version of  deepseek\-r1\-sglang. |
   |Parameter configuration |Select the configuration method for  deepseek\-r1\-sglang. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it. |
   

4. Click **Confirm ** to deploy the application.

   The applications that are already deployed can be found on the **Helm** page. Find deepseek\-r1\-sglang application by specifying target project, cluster, and namespace, then click it to view detailed information of the application.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The service names that match the pattern <code><application name>-api-svc</code> indicate those services will be working as the external access points of their applications, and therefore are supposed to be used when configuring routing and verifying model deployment.   </div>
   

5. View the load status of deepseek\-r1\-sglang applications on the **Deployment** page of the VKE cluster.

   1. On the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Cluster**, and find the target cluster and click the cluster name.

   2. In the left navigation bar, select **Workload** \> **StatefulSet**, then enter the name deepseek\-r1\-sglang in the search box to find it and view its status.


<span id=".5q2l6aqk5Zub77ya6YWN572u6Lev55Sx"></span>
### Step 3: Configure Ingress

Configure model routing through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that are required in cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace in which the deepseek\-r1\-sglang application template is deployed. It is used to associate the service that is supposed to be exposed for its application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you are using the API Gateway to expose the model service in the clusters, we recommend you to configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the Classic Load Balancer (CLB) instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong> When some GPU instances malfunction, common practice is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If timeout is needed, you can configure it on the <a href="https://console.byteplus.com/veapig">API Gateway console</a>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: Monitoring alert and log feature are not turned on by default for the API Gateway instances created in the VKE console. If needed, we recommend that you enable logging and monitoring/alerting for the instance in the APIG console.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This can help you to detect the unexpected anomalies in the whole system chain from the gateway entry level. For example: Unhealthy back end and back\-end crashes will cause the APIG to return <code>503</code> error code and specific errors.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Round Robin**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select the service that is named in the pattern `<application name>-api-svc` and is associated with the application created based on deepseek\-r1\-sglang template, and then set the port number to **8080**. |
   

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: Click **Consumer management** in the left navigation bar and click **Create consumers**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level** and configure the instance, Service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in step 1.

      4. Other options can remain as default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP.

   * **Backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * In the production environment, configure the access domain name of Ingress among the domain name providers, and ensure the A record of the Ingress access domain name has been configured with the public IP address or private IP address of Ingress.


<span id=".5q2l6aqk5LqU77ya5byA5ZCv6KeC5rWL6YWN572u"></span>
### Step 4: Enable observability

Basic observability provides the monitoring metrics for AI resources and inference service. Deep observability provides full\-link performance monitoring service for inference application.

<span id=".5Z-656GA6KeC5rWL"></span>
#### Basic observability


1. In the left navigation bar of the page for a specific cluster, select **Overview** under the gray title **Cloud native observability**, then click **Enable** on the page to start monitoring. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitoring dashboard** in the left navigation bar and search for `sglang` to open dashboard as shown below:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png) </span>

   * You can also use Grafana to build a custom monitoring dashboard for SGLang\-based applications. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the above Grafana and select to import the following dashboard JSON file:

         <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8a819899c3bab3f2b507a0d738b02aa.json" name="SGLang Dashboard-1747206543364.json">SGLang Dashboard-1747206543364.json</Attachment>
         

      2. The effect after import is shown in the figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png) </span>


<span id=".5rex5bqm6KeC5rWL"></span>
#### Deep observability


1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation bar, click **Server\-side monitoring**.

2. Search for `sglang` and click the service name in the results to open the monitoring dashboard page.

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
          "model": "/data/models/DeepSeek-R1",
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

   From the Trace analysis tab of the SGLang application, you can retrieve link information based on different conditions. Click the ID of the target trace to go to the details page of the trace. View the trace information in the list.


<span id=".5qih5Z6L6aqM6K-B"></span>
## Model verification

<span id=".5pa55byP5LiA77ya6YCa6L-HLXNlcnZpY2Ut5pa55byP6K6_6Zeu"></span>
### Method 1: Access through Service

The service, created along with the deployment of deepseek\-r1\-sglang application, has a name matching the pattern `<application name>-api-svc`. You can use the endpoint address (port 8080) corresponding to that service name to perform tests in this method. The endpoint can be called as you do with OpenAI APIs.

The sample code is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>******</code> in <code>http://******</code> with the endpoint of your <code><application name>-api-svc</code> Service.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> specifies the text you input to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "/data/models/DeepSeek-R1",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```


Alternatively, you can directly log in to the pod to perform API calls. To do that, you can go to the **Helm application details page** of deepseek\-r1\-sglang application, click the associated StatefulSet in the section **Workload**, and then in the new page, click **Console** in the top\-right corner to open the console where commands can be executed.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_efc34d5222444ba3342ca7f8c442307c.png) </span>

<span id=".5pa55byP5LqM77ya6YCa6L-HLWFwaWct5pa55byP6K6_6Zeu"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the <code>example.com</code> in <code>http://example.com</code> with the domain name of the back\-end services obtained in <strong>Step 3</strong><strong>: Configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 3</strong><strong>: Configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "/data/models/DeepSeek-R1-W4AFP8",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
