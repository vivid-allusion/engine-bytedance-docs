---
title: "Quickly deploying quantized DeepSeek-R1 with TensorRT-LLM"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploy_the_quantized_version_of_DeepSeek-R1_based_on_TensorRT-LLM"
---

This topic describes how to use Vital Kubernetes Engine (VKE) to quickly deploy an inference service for the quantized DeepSeek\-R1 model based on TensorRT\-LLM.

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

This solution allows you to quickly deploy a large language model (LLM) of DeepSeek\-R1 in a Kubernetes cluster.


* **DeepSeek\-R1 model**: Released by the Chinese AI startup DeepSeek, DeepSeek\-R1 is an inference model trained on DeepSeek\-V3\-Base. It excels at mathematics, coding, and natural language reasoning, and has attracted widespread attention for its open\-source availability, algorithmic innovation, and cost\-effectiveness.

* **TensorRT\-LLM**: This is a high\-performance deep learning inference optimization library launched by NVIDIA. It is focused on enhancing the inference speed and efficiency of LLMs on NVIDIA GPUs.


<span id=".6YOo572y5L-h5oGv"></span>
### Deployment information


* Model: DeepSeek\-R1\-W4AFP8

* Inference engine: TensorRT\-LLM

* Instance specification: ecs.hpcpni3ln.45xlarge \* 1


<span id=".5pSv5oyB6IO95Yqb"></span>
### Support capabilities


* Parallel strategy: TP and EP

* Quantization technology: W4A8

* Precision: FP8

* Access: API Gateway (APIG)


<span id=".5L2_55So6K-05piO"></span>
## Notes


* In this example, many add\-ons are used, which are dependent on each other and have complex configurations. To achieve the expected results, you must perform operations according to the guidance in this article.

* To achieve the expected results and stay within the usage limits of VKE, follow the procedure in this article or use the recommended resources described here. If you need to use a different solution, contact your BytePlus account manager.

* Do not use mGPU on GPU resources.

* The complete deployment workflow depends on certain beta features from BytePlus. Contact your Volcengine account manager to request trial access to the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln HPC\-optimized instance |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. Because the DeepSeek model has a large number of parameters, it requires a GPU instance with a large amount of graphics memory, e.g., ecs.hpcpni3ln.45xlarge. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

<span id=".5Yib5bu66auY5oCn6IO96K6h566X6ZuG576k"></span>
### Creating an HPC cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>region and availability zone</strong> where the high\-performance compute cluster is located needs to be consistent with the <strong>region and availability zone</strong> of the VKE nodes.</div>


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
|Number of nodes |1 node. |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory has subsequent dependencies. Therefore, the directory cannot be modified or specified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the physical host fails or the local disk is damaged, data loss may occur. Do not store data that must be retained long\-term on the local disk, and make sure backups are in place.    </div><br>    |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows the use of management add\-ons for GPUs in containers. |
|rdma\-device\-plugin |(Required) The add\-on manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. |
|apig\-controller |(Required) API Gateway controller provides the AI Gateway capability of cloud\-native, which can complete the intelligent load balancing of the inference traffic according to different policies. |
|csi\-ebs |(Required) It enables VKE clusters to use the standard CSI implementation for Elastic Block Storage (EBS).. |
|prometheus\-agent |(Required) Vital Managed Service for Prometheus (VMP) monitoring add\-on collects metrics data from the Kubernetes cluster to VMP. |
|apmplus\-opentelemetry\-collector |(Not supported yet) Collect OpenTelemetry data and Prometheus metrics, and send them to APMPlus. |
|apmplus\-server\-agent |(Not supported yet) It collects and sends monitoring data of services and hosts to APMPlus. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) An event\-driven autoscaler for Kubernetes that enables autoscaling of inference services based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YOo572yLWRlZXBzZWVrLXIxLXc0YWZwOC10ZW5zb3JydC1sbG0="></span>
### Step 1: Deploy deepseek\-r1\-w4afp8\-tensorrt\-llm

This solution provides a w4a8\-quantized DeepSeek\-R1 model application based on the TensorRT\-LLM framework. You can quickly deploy it by using a VKE application template.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Application template**. Scroll to the bottom of the page, click **More application templates**.

3. Find **deepseek\-r1\-w4afp8\-tensorrt\-llm**, and click **Deploy**.

4. On the **Deploy application** page, configure the service parameters of **deepseek\-r1\-w4afp8\-tensorrt\-llm**.

   
   |Configuration item |Descriptions |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of deepseek\-r1\-w4afp8\-tensorrt\-llm. We recommend that you select the latest version. |
   |Parameter configuration |The configuration methods for deepseek\-r1\-w4afp8\-tensorrt\-llm. Click the Edit icon to view the configuration description of various parameters in the values.yaml file or edit the YAML file. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting the agreement.  |
   

5. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select target project, cluster, and namespaces, find the applications already deployed based on the template deepseek\-r1\-w4afp8\-tensorrt\-llm, and click application name. Enter details page to view the basic information of the application, workloads, services, and other resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The service named in the format <code><application name>-deepseek-r1-w4afp8-tensorrt-llm-httpsvc</code> is the Service exposed by the application. You will need to reference this Service in later steps, such as route configuration and model verification.   </div>
   

6. On the **StatefulSet** page in the VKE cluster, view the load status of the application deepseek\-r1\-w4afp8\-tensorrt\-llm.

   1. On the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Cluster**, and find the target cluster and click the cluster name.

   2. On the management page of the target cluster, click **Workload** \> **StatefulSet. T**hen, search for the name of the application deepseek\-r1\-w4afp8\-tensorrt\-llm to view the load status.


<span id=".5q2l6aqk5LqM77ya6YWN572u6Lev55Sx"></span>
### Step 2: Configure routing

Configure model routing through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that are required in cloud\-native applications.


5. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select and deploy the namespace of the application template deepseek\-r1\-w4afp8\-tensorrt\-llm, which is used to associate the application services that are exposed externally. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you are using the API Gateway to expose the model service in the clusters, we recommend that you configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong> and two availability zones to achieve high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the Classic Load Balancer (CLB) instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong> When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If timeout is needed, you can configure it on the <a href="https://console.byteplus.com/veapig">API Gateway console</a>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: Monitoring alert and log features are not turned on by default for the API Gateway instances created in the VKE console. If needed, we recommend you to turn on the log and monitoring alarm capabilities of the instances in the <a href="https://console.byteplus.com/veapig">APIG console</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This can help you to detect the unexpected anomalies in the whole system chain from the gateway entry level. For example: Unhealthy back end and back\-end crashes will cause the APIG to return <code>503</code> error code and specific errors.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend setting the Load Balancing Algorithm parameter to Round Robin. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select a service with the format name of `<application name>-deepseek-r1-w4afp8-tensorrt-llm-httpsvc` that is created when you deploy the deepseek\-r1\-w4afp8\-tensorrt\-llm application template and set the port number to **80**. |
   

2. (Optional) Configure API Gateway authentication and authorization.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: Select **Consumer management** on the left navigation bar and click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer to go to the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level**: and configure the instance, service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in step 1.

      4. Other options can remain as default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP addresses.

   * **Backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution.

   * In the production environment, configure the access domain name of Ingress among the domain name providers, and ensure the A record of the Ingress access domain name has configured the public IP address or private IP address of Ingress.


<span id=".5qih5Z6L6aqM6K-B"></span>
## Model verification

<span id=".5pa55byP5LiA77ya6YCa6L-HLXNlcnZpY2Ut5pa55byP6K6_6Zeu"></span>
### Method 1: Access through Service

After deploying the application template deepseek\-r1\-w4afp8\-tensorrt\-llm, associate the service created with `<application name>-deepseek-r1-w4afp8-tensorrt-llm-httpsvc`. The service provides an HTTP API endpoint (port 80). The endpoint can be called as you do with OpenAI APIs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>******</code> in <code>http://******</code> with the service endpoint associated and created when you are deploying the deepseek\-r1\-w4afp8\-tensorrt\-llm application.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "/data/models/DeepSeek-R1-W4AFP8",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```


You can click the name of the Deployment in the **Deployment** area on the **Helm application details page** of the application, and redirect to the **Deployment** page, and click the console in the upper\-right corner. Log in to the Pod of the application to implement API calls.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee1dbaedf124a0dbc1ed28c8b6905a29.png) </span>

<span id=".5pa55byP5LqM77ya6YCa6L-HLWFwaWct5pa55byP6K6_6Zeu"></span>
### Method 2: Access through the APIG method

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>example.com</code> in the <code>http://example.com</code> with the Ingress backend service access domain name obtained in <strong>Step Two: Configure routing</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 2: Configure routing</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "/data/models/DeepSeek-R1-W4AFP8",    "messages": [      {"role": "system", "content": "You are a helpful assistant."},      {"role": "user", "content": "Who won the world series in 2020?"}        ]    }'
```
