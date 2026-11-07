---
title: "Quickly deploying DeepSeek-V3/R1 (full version) with xLLM (PD disaggregation)"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_full-version_model_DeepSeek-V3_R1_based_on_xLLM_PD_disaggregation"
---

This topic mainly describes how to quickly deploy a model inference service with the DeepSeek\-R1 or DeepSeek\-V3 full version based on xLLM by using Vital Kubernetes Engine (VKE).

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

This solution achieves the prefill\-decode (PD) disaggregation deployment of the DeepSeek\-R1 or DeepSeek\-V3 large language model (LLM) in Kubernetes clusters.


* **DeepSeek\-V3 model**: Released by the Chinese AI startup DeepSeek, the DeepSeek\-V3 model is a general LLM with 671 billion parameters and 37 billion activated parameters, featuring a mixture of experts (MoE) architecture. Pre\-trained on 14.8 trillion tokens, the DeepSeek\-V3 model provides services such as information retrieval, data analysis, and natural language processing, which apply to various application scenarios such as customer service, educational tutoring, and content creation.

* **DeepSeek\-R1 model**: Released by Chinese AI startup DeepSeek, the R1 model is an inference model trained based on DeepSeek\-V3\-Base. It excels in mathematics, code, and natural language reasoning and has gained wide attention for its open source, algorithm innovation, and cost\-effectiveness.

* **xLLM engine**: As an efficient inference framework independently developed byModelArkModelArk, the xLLM engine provides PD disaggregation, elastic scaling, and other features, outperforming other open source frameworks.

* **PD disaggregation technology**: The technology divides the inference process into two phases, which are deployed in different hardware resources to optimize performance:

   * Prefill: A compute\-intensive phase.

   * Decode: A memory\-intensive phase.


Advantages of the solution


* **Improved resource utilization**: The prefill phase is separated from the decode phase, and resources are allocated to different phases.

* **Increased throughput**: New requests are being processed in the Prefill phase while the old ones are being handled in the Decode phase.

* **Reduced latency**: The wait time of concurrent requests is reduced and the overall efficiency is improved.


<span id=".6YOo572y5L-h5oGv"></span>
### Deployment information


* Model: DeepSeek\-V3\-671B and DeepSeek\-R1\-671B

* Inference engine: xLLM

* Instance specification: ecs.hpcpni3ln.45xlarge

   * Prefill: ecs.hpcpni3ln.45xlarge instance\* 1

   * Decode: ecs.hpcpni3ln.45xlarge instance\* 1


<span id=".5pSv5oyB6IO95Yqb"></span>
### Supported capabilities


* Parallel strategy: PD disaggregation, Data Parallelism (DP), Tensor Parallelism (TP), and Expert Parallelism (EP).

* Observability: Vital Managed Service for Prometheus (VMP)

* Access: API Gateway (APIG)


<span id="gEpYd1FE"></span>
### Performance evaluation

The following table shows the performance differences between the open source scenario and the solution provided in this topic.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The delivered performance is related to machine specifications, distribution configuration, and network bandwidth. The actual test result shall prevail.</div>



|**Category** |**open source** |**Optimized** |
|---|---|---|
|Inference engine |SGLang (open source edition) |xLLM (self\-developed by BytePlus) |
|Input/Output |3500/1500 |3500/1500 |
|TTFT (ms) |<=5000 |<=5000 |
|TPOT (ms) |<=50 |<=50 |
|Parallel strategy |TP |PD disaggregation, DP, TP, and EP. |
|Single\-GPU throughput (TPS) |167.4 |669 |


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* In this example, many add\-ons are used, which are dependent on each other and have complex configurations. To achieve the expected results, you must perform operations according to the guidance in this article.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you want to use a different solution, contact your BytePlus account manager for assistance.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |xLLM inference acceleration solution |[ModelArk](https://www.byteplus.com/en/product/modelark) |The core capability of this best practice needs to be used with an xLLM License. |
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The Deepseek model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

<span id=".5Yib5bu66auY5oCn6IO96K6h566X6ZuG576k"></span>
### Creating an HPC cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <strong>region and availability zone</strong> where the high\-performance compute cluster is located need to be consistent with <strong>those</strong> of the VKE nodes.</div>


<span id=".5Yib5bu6LXZrZS3pm4bnvqQ="></span>
### Creating a VKE cluster


1. The following parameters need to be configured as described in the table when creating a cluster by using VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   
   |Configuration item |Description |
   |---|---|
   |**Cluster configuration** ||
   |Kubernetes version |Select v1.28 or later. |
   |Network model |Select **VPC\-CNI**. |
   |**Node pool configuration** ||
   |Managed node pool |**Enable** managed node pool. |
   |Availability zone |Same availability zone as the **High\-Performance Compute Cluster**. |
   |Instance type |Select `ecs.hpcpni3ln`, the GPU Accelerated specification. Ensure you already obtained permission for trial of the beta version. |
   |High Performance Computing Cluster |Select the HPC cluster you created. |
   |Number of nodes |2 nodes. |
   |Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory is required by subsequent steps and must not be changed or customized.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the physical host fails or the local disk is damaged, data loss may occur. Do not store data that must be retained long\-term on the local disk, and make sure your data is backed up in case of physical host failures or local disk damage.   </div><br>    |
   |Node labels |When you deploy the DeepSeek model by using VKE, you need to specify the RDMA usage mode by using node labels.<br><br>Set the label key to `vke.node.rdma.mode` and the label value to `shared`. |
   |Kubelet configs |The non\-uniform memory access (NUMA) affinity policy for RDMA devices needs to be configured by using custom parameters with the Kubelet when deploying DeepSeek model in the VKE.<br><br>Select the parameter `topology-manager-policy` and parameter value `best-effort`. |
   |**Addon configuration** ||
   |nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
   |rdma\-device\-plugin |(Required) The add\-on manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. |
   |apig\-controller |(Required) The API Gateway controller provides cloud\-native AI gateway capabilities and enables intelligent load balancing for inference traffic based on different policies. |
   |csi\-ebs |(Required) It enables VKE clusters to use the standard CSI implementation for Elastic Block Storage (EBS). |
   |prometheus\-agent |(Required) Vital Managed Service for Prometheus (VMP) monitoring add\-on collects the monitoring metrics data of the Kubernetes cluster to VMP. |
   |apmplus\-opentelemetry\-collector |(Not supported yet) Collect OpenTelemetry data and Prometheus metrics, and send them to APMPlus. |
   |apmplus\-server\-agent |(Not supported yet) It collects and sends monitoring data of services and hosts to APMPlus. |
   |cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
   |keda |(Recommended) The event\-driven autoscaler based on Kubernetes completes the autoscaler tasks of the inference service based on complex metrics. |
   |vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |
   

2. After the VKE cluster and nodes are created, bind an elastic IP address (EIP) to each ECS instance corresponding to the nodes. For more details, refer to [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).

3. Locally run the following command to upload xLLM License to all GPU nodes used in this solution.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace the value of <code>[your_ip_address]</code> with the EIP of the GPU node.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>[your_ip_address]</code> can contain only one IP address. If multiple GPU nodes exist, run the command multiple times.   </div>
   

   ```bash
   scp license.lic  root@[your_ip_address]:/root/license.lic
   ```
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YOo572y5bqU55So"></span>
### Step 1: Deploy the application


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Application center \> Application template**.

3. On the **Application template** page, find **deepseek\-v3\-xllm\-pd** or **deepseek\-r1\-xllm\-pd** and click **Deploy**.

4. On the **Deploy application** page, specify the parameters of **deepseek\-v3\-xllm\-pd** or **deepseek\-r1\-xllm\-pd**.

   
   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of deepseek\-v3\-xllm\-pd or deepseek\-r1\-xllm\-pd. We recommend that you select the latest version. |
   |Parameter configuration |The configuration method of deepseek\-v3\-xllm\-pd or deepseek\-r1\-xllm\-pd. Click the edit icon to edit the `values.yaml` file, and update the YAML file based on the **YAML file parameter description** in the following table. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Customize and select the namespace under the target cluster. |
   |Protocol |Read and understand the agreement, and then select the checkbox to accept it.  |
   

   **YAML file parameters**

   
   |Configuration item |Description |Example |
   |---|---|---|
   |modelConfig.local.path |The local path of the ECS instance used to store the model file. If you want to use a local disk, the path needs to be consistent with the mount target configured in the node pool. |/data01/models |
   |prefillWorker.resources.limits.vke.volcengine.com/rdma |The number of RDMA network interface cards (RNICs) used by the prefill worker. It is recommended that you set the value based on the number of RNICs (4 or 8) corresponding to the model. |4 |
   |prefillWorker.resources.requests.vke.volcengine.com/rdma ||4 |
   |decodeWorker.resources.limits.vke.volcengine.com/rdma |The number of RNICs used by the decode worker. We recommend that you set the value based on the number of RNICs (4 or 8) corresponding to the model. |4 |
   |decodeWorker.resources.requests.vke.volcengine.com/rdma ||4 |
   

5. Click **Confirm** to start deployment.

   The deployed application will be displayed on the **Helm** page. Select the target project, cluster, and namespace and click the name of the deployed deepseek\-v3\-xllm\-pd or deepseek\-r1\-xllm\-pd application to go to the details page. On the details page, view the basic information about the application and the created workloads, services, and other resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code><application name>-<template name>-httpsvc</code> indicates the name of the service externally exposed by the application. You need to associate the service in the subsequent steps, such as Ingress configuration and model validation.   </div>
   

<span id=".5q2l6aqk5LqM77ya6YWN572u6Lev55Sx"></span>
### Step 2: Configure an Ingress

Configure model routing through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that are required in cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace where the deepseek\-v3\-xllm\-pd or deepseek\-r1\-xllm\-pd application template is deployed to associate the service exposed by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you are using the API Gateway to expose the model service in the clusters, we recommend you to configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the CLB instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong>When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If timeout is needed, you can configure it on the <a href="https://console.byteplus.com/veapig">API Gateway console</a>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: Monitoring alert and log feature are not turned on by default for the API Gateway instances created in the VKE console. If needed, we recommend that you enable the logging, monitoring, and alerting capabilities of the instances in the <a href="https://console.byteplus.com/veapig">APIG console</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This can help you to detect the unexpected anomalies in the whole system chain from the gateway entry level. For example: Unhealthy back end and back\-end crashes will cause the APIG to return <code>503</code> error code and specific errors.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select a service that is created when you deploy the deepseek\-v3\-xllm\-pd or deepseek\-r1\-xllm\-pd application template and set the port number to **80**. The name of the service is in the format of `<application name>-<template name>-httpsvc`. |
   

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: On the left navigation bar, select **Consumer management**, and click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level** and configure the instance, service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in step 1.

      4. Other options can remain as default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP addresses.

   * **Backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * In a production environment, configure an access domain name for the Ingress at the domain name provider, and make sure that the public or private IP address of the Ingress is configured in the A record of the Ingress access domain name.


<span id=".5q2l6aqk5LiJ77ya5byA5ZCv6KeC5rWL6YWN572u"></span>
### Step 3: Enable observability configuration


1. In the left navigation bar of the cluster management page, click **Cloud native observability** \> **Overview**. On the page that appears, click **Enable basic observability** to enable cloud native observability and VKE observability. For more configuration details, refer to [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After you enable cloud native observability, xLLM metrics will be collected into VMP, and you can view xLLM monitoring charts on the preset dashboards in the [VMP console](https://console.byteplus.com/prometheus).

   Search `xllm` to view xLLM dashboards, which are shown in the following figure.

3. (Optional) Use Grafana to view xLLM monitoring charts.

   If you want to use Grafana to view xLLM monitoring charts, you can deploy Grafana or import dashboards into your self\-built Grafana.

   1. For the method of installing the Grafana service, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

   2. Log in to Grafana and select dashboards to be imported.

      <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_67cf8d4f5256b13b24369baead851214.json" name="xllm_default_dashboard.json">xllm_default_dashboard.json</Attachment>
      

      The following figure shows the result after importing.


<span id=".5qih5Z6L6aqM6K-B"></span>
## Model validation

<span id=".5pa55byP5LiA77ya6YCa6L-HLXNlcnZpY2Ut5pa55byP6K6_6Zeu"></span>
### Method 1: Access the model by using the service

After you deploy the deepseek\-v3\-xllm\-pd or deepseek\-r1\-xllm\-pd application template, the created service whose name is in the format of `<application name>-<template name>-httpsvc` will provide an HTTP API endpoint (port 80). You can call the service endpoint by using an OpenAI\-compatible API.

The sample code is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the value of <code>localhost:80</code> with the endpoint of your <code><application name>-<template name>-httpsvc</code> service.</div>


* <div data-tips="true" data-tips-type="tip">Set the <code>content</code> parameter to your conversation content with the model.</div>



```bash
curl localhost:80/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "xllm",
    "messages": [
    {
        "role": "user",
        "content": "In the heart of Eldoria, an ancient land of boundless magic and mysterious creatures, lies the long-forgotten city of Aeloria. Once a beacon of knowledge and power, Aeloria was buried beneath the shifting sands of time, lost to the world for centuries. You are an intrepid explorer, known for your unparalleled curiosity and courage, who has stumbled upon an ancient map hinting at ests that Aeloria holds a secret so profound that it has the potential to reshape the very fabric of reality. Your journey will take you through treacherous deserts, enchanted forests, and across perilous mountain ranges. Your Task: Character Background: Develop a detailed background for your character. Describe their motivations for seeking out Aeloria, their skills and weaknesses, and any personal connections to the ancient city or its legends. Are they driven by a quest for knowledge, a search for lost familt clue is hidden."
    }
    ],
    "stream":false,
    "max_tokens": 30
  }'
```


In the **Workload** section of the **Helm details page** that corresponds to the deepseek\-v3\-xllm\-pd or deepseek\-r1\-xllm\-pd application, you can select a network\-reachable workload to go to the details page. In the upper\-right corner of the details page, click **Console** to log in to the pod that corresponds to the application to call the API.

<span id=".5pa55byP5LqM77ya6YCa6L-HLWFwaWct5pa55byP6K6_6Zeu"></span>
### Method 2: Access the model by using APIG

When enabling the authentication feature of the APIG, you need to add an authentication token to the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the value of <code>localhost:80</code> with the access domain name of the Ingress backend service obtained in <strong>Step 2</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace the value of <code>eyJhbGciOiJSUzI******</code> with the API key generated in <strong>Step 2</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is the conversation content you want to send to the model.</div>



```bash
curl localhost:80/v1/chat/completions -X POST \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "xllm",
    "messages": [
    {
        "role": "user",
        "content": "In the heart of Eldoria, an ancient land of boundless magic and mysterious creatures, lies the long-forgotten city of Aeloria. Once a beacon of knowledge and power, Aeloria was buried beneath the shifting sands of time, lost to the world for centuries. You are an intrepid explorer, known for your unparalleled curiosity and courage, who has stumbled upon an ancient map hinting at ests that Aeloria holds a secret so profound that it has the potential to reshape the very fabric of reality. Your journey will take you through treacherous deserts, enchanted forests, and across perilous mountain ranges. Your Task: Character Background: Develop a detailed background for your character. Describe their motivations for seeking out Aeloria, their skills and weaknesses, and any personal connections to the ancient city or its legends. Are they driven by a quest for knowledge, a search for lost familt clue is hidden."
    }
    ],
    "stream":false,
    "max_tokens": 30
  }'
```
