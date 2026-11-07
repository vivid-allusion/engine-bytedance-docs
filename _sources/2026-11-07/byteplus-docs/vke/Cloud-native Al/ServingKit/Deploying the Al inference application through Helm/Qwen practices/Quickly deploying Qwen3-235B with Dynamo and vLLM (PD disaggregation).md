---
title: "Quickly deploying Qwen3-235B with Dynamo and vLLM (PD disaggregation)"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_Qwen3-235B_based_on_Dynamo_and_vLLM_PD_disaggregation"
---

This topic mainly describes how to quickly deploy the Qwen3\-235B model inference service (PD disaggregation) based on Dynamo and vLLM by using Vital Kubernetes Engine (VKE).

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

The solution integrates multiple acceleration technologies of BytePlus to quickly deploy the Qwen3\-235B\-A22B model in a Kubernetes cluster.


* **Qwen3**: the latest Qwen large language model (LLM) launched by Alibaba Cloud, which features six dense models and two Mixture\-of\-Experts (MoE) models. With 0.6 billion to 235 billion parameters, Qwen3 can meet diverse business requirements.

* **Dynamo**: NVIDIA Dynamo is an open\-source, low\-latency, modular inference framework for serving generative AI models in distributed environments.

* **GDKV model acceleration**: a fast model loading solution achieved through the Remote Direct Memory Access (RDMA) and GPU Direct RDMA (GDR) technologies provided by BytePlus.

* **PD disaggregation technology**: The technology divides the inference process into two phases, which are deployed in different hardware resources to optimize performance:

   * Prefill: A compute\-intensive phase.

   * Decode: A memory\-intensive phase.


<span id=".6YOo572y5L-h5oGv"></span>
### Deployment information


* Model: Qwen3\-235B\-A22B

* Inference engine: Dynamo and vLLM

* Instance specification: ecs.hpcpni3ln.45xlarge

   * Prefill: ecs.hpcpni3ln.45xlarge instance\* 1

   * Decode: ecs.hpcpni3ln.45xlarge instance\* 1


<span id=".5pSv5oyB6IO95Yqb"></span>
### Supported capabilities


* Parallel strategy: PD disaggregation

* Precision: FP8

* Model acceleration: GDKV

* Monitoring: Vital Managed Service for Prometheus (VMP) and Application Performance Management Plus (APMPlus)

* Access: API Gateway (APIG)


<span id="xCIzIrWX"></span>
### Performance evaluation

The following table shows the performance differences between the open source scenario and the solution provided in this topic.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The delivered performance is related to machine specifications, distribution configuration, and network bandwidth. The actual test result shall prevail.</div>



|**Category** |**Open source** |**Optimized** |
|---|---|---|
|Inference engine |vLLM (open source edition) |Dynamo and vLLM (BytePlus optimized version) |
|Input/Output |3500/1500 |3500/1500 |
|TTFT (ms) |<=5000 |<=5000 |
|TPOT (ms) |<=50 |<=50 |
|Parallel policy |TP |PD disaggregation and TP |
|Single card throughput (TPS) |897 |1595 |


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* To ensure successful deployment, which involves a bunch of add\-ons dependent on each other and a variety of configurations, you need to strictly follow the instructions in this document.

* To avoid violation of the VKE [limit](https://docs.byteplus.com/en/docs/vke/Limits), we recommend that you proceed based on this solution (or on the resources mentioned in the documents). If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The Qwen3\-235B model has a large number of parameters. Therefore, you need to apply for a GPU instance with large memory, such as `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id="lXCkcoJO"></span>
## 

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

<span id=".5Yib5bu66auY5oCn6IO96K6h566X6ZuG576k"></span>
### Creating an HPC cluster

The HPC cluster can achieve the logical isolation of high\-performance computing GPU instances (computing nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating High-Performance Compute Clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The<strong> region and availability zone</strong> where the high\-performance compute cluster is located need to be consistent with those of the VKE nodes.</div>


<span id=".5Yib5bu6LXZrZS3pm4bnvqQ="></span>
### Creating a VKE cluster

The following parameters need to be configured as described in the table when creating a cluster by using VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).


|Configuration item |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select v1.28 or later. |
|Network model |Select VPC\-CNI. |
|**Node pool configuration** ||
|Managed node pool |**Enable** Managed node pool. |
|Availability zone |Same availability zone as the **High\-Performance Compute Cluster**. |
|Instance type |Select `ecs.hpcpni3ln`, the GPU Accelerated specification. Ensure you already obtained permission for trial of the beta version. |
|High Performance Computing Cluster |Select the HPC cluster you created. |
|Number of nodes |2 nodes. |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory has subsequent dependencies. Therefore, the directory cannot be modified or specified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure the data that needs long\-term storage has been <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backed up</a> properly in case of computer crashes or disk damage which causes data loss.   </div><br>    |
|Node labels |When you deploy the model by using VKE, you need to specify the RDMA usage mode by using node labels.<br><br>The label key is set to: `vke.node.rdma.mode`, and the label value is set to: `shared`. |
|Kubelet configs |When you deploy the model by using VKE, you need to configure the non\-uniform memory access (NUMA) affinity policy of the RDMA device by specifying the parameters of Kubelet.<br><br>Select the parameter `topology-manager-policy` and its value `best-effort`. |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
|rdma\-device\-plugin |(Required) The add\-on manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. |
|apig\-controller |(Required) API Gateway controller provides the cloud\-native AI Gateway capability, which can complete the intelligent load balancing of the inference traffic according to different policies. |
|csi\-ebs |(Required) It allows VKE clusters to use the standard Container Storage Interface (CSI) of the TOS. |
|prometheus\-agent |(Required) Vital Managed Service for Prometheus (VMP) monitoring add\-on collects the metrics data of the Kubernetes cluster and send the data to VMP. |
|apmplus\-opentelemetry\-collector |(Required) Collect OpenTelemetry data and Prometheus metrics, and send them to APMPlus. |
|apmplus\-server\-agent |(Required) Send the collection service and host monitoring data in parallel to APMPlus. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) The event\-driven autoscaler based on Kubernetes. It bComplete the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LqM77ya56Gu6K6kLW5hdHMt5ZKMLWV0Y2Qt6ZyA6KaB55qE5a2Y5YKo57G7"></span>
### Step 1: Check the StorageClass required by NATS and ETCD

In the [VKE console](https://console.byteplus.com/vke), click **Storage** \> **StorageClass** in the left navigation bar of the management page for the target cluster. On the StorageClass page, check whether the StorageClass named **ebs\-ssd** exists, which is used for storage related to NATS and ETCD.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The StorageClass is automatically created after the csi\-ebs add\-on is installed in the cluster. If the StorageClass does not exist, install the csi\-ebs add\-on in the cluster first. For detailed operations, refer to <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on">Installing an add\-on</a>.</div>


<span id=".5q2l6aqk5LiJ77ya6YOo572yLXF3ZW4zLWR5bmFtby12bGxtLXBk"></span>
### Step 2: Deploy qwen3\-dynamo\-vllm\-pd

VKE provides the Qwen3\-235B\-A22B model application (PD disaggregation) based on the Dynamo and vLLM frameworks. The application can be quickly deployed through the **Application template** page of the VKE console.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find **qwen3\-dynamo\-vllm\-pd** and click **Deploy**.

3. On the **Deploy application** page, specify the parameters of **qwen3\-dynamo\-vllm\-pd**. Configure the parameters mentioned below as described. Other parameters can be configured according to the prompts on the page or by referring to the descriptions in [Application template](https://docs.byteplus.com/en/docs/vke/Application-templates).

   
   |Configuration item |Description |
   |---|---|
   |**application template** ||
   |Application template |Select the Chart version of qwen3\-dynamo\-vllm\-pd. We recommend that you select the latest version. |
   |Parameter configuration |The configuration method of qwen3\-dynamo\-vllm\-pd. Click the edit icon next to `values.yaml` to edit the YAML file of the current application. For the descriptions of some parameters, refer to the following table. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created as described in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |
   

   You can modify the configurations of the `values.yaml` file based on your business requirements. The following table describes some parameters. We recommend that you keep the default configurations.

   
   |Configuration item |Description |Sample value |
   |---|---|---|
   |modelConfig.local.path |The local path of the ECS instance used to store the model file, which must be the created data volumes. |/data01/models |
   |prefillWorker.replicas |Prefill the number of replicas to deploy on the node. |1 |
   |decodeWorker.replicas |Decode the number of replicas deployed on the node. |1 |
   |decodeWorker.router |Decode the Router algorithm of the node. |round\-robin |
   |etcd.persistence.storageClass |The StorageClass used by ETCD. |ebs\-ssd |
   |etcd.persistence.size |The storage capacity of ETCD. |10Gi |
   |nats.config.cluster.enabled |Does NATS use cluster configuration? |true |
   |nats.config.cluster.replicas |The number of replicas in a NATS cluster is larger than or equal to 3. |3 |
   |nats.config.jetstream.fileStore.pvc.storageClassName |The StorageClass used by NATS. |ebs\-ssd |
   |nats.config.jetstream.fileStore.pvc.size |The size of NATS storage. |10Gi |
   

5. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace, and click the name of the deployed qwen3\-dynamo\-vllm\-pd application to go to the details page. On the details page, view the basic information about the application and the created workloads, services, and other resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code><application name>-qwen3-dynamo-vllm-pd</code> indicates the name of the service externally exposed by the application. You need to associate the service in the subsequent steps, such as Ingress configuration and model validation.   </div>
   

6. View the status of pods that correspond to the qwen3\-dynamo\-vllm\-pd application on the **Pod** page of the VKE cluster.

   1. On the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Cluster**, find the target cluster, and click the cluster name.

   2. In the left navigation bar of the target cluster management page, click **Workload** \> **Pod**. Then, enter the application name qwen3\-dynamo\-vllm\-pd in the search box to view the status of related pods.


<span id=".5q2l6aqk5Zub77ya6YWN572u6Lev55Sx"></span>
### Step 3: Configure an Ingress

Configure model routing through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that is required in cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace where the qwen3\-dynamo\-vllm\-pd application template is deployed to associate the service exposed by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **cloud\-native API Gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you are using APIG to expose the model service in the clusters, we recommend that you configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the CLB instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance in the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong> When some GPU instances malfunction, common practice is taking the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If timeout is needed, you can configure it on the <a href="https://console.byteplus.com/veapig">API Gateway console</a>. For details, refer to <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: Monitoring alert and log feature are not turned on by default for the API Gateway instances created in the VKE console. If needed, we recommend you to turn on the log and monitoring alarm capabilities of the instances in the <a href="https://console.byteplus.com/veapig">APIG console</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This can help you to detect the anomalies in the whole system chain from the gateway entry level. For example: Unhealthy back end and back\-end crashes will cause the APIG to return <code>503</code> error code and specific errors.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select a service that is created when you deploy the qwen3\-dynamo\-vllm\-pd application template and set the port number to **8000**. The name of the service is in the format of `<application name>-qwen3-dynamo-vllm-pd`. |
   

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: On the left navigation bar, select **Consumer management**, and click **Create consumers**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: in the left navigation bar, select **Plugin Center \> Key Auth** and click **Create Plugin** on the page.

      1. **Effect level**: select the **Routing level** and configure the instance, service, and route to which the add\-on belongs.

      2. **Authentication configuration**: select the **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that the API Key will be included in the Authorization header of requests.

      3. **Consumer**: Select the consumer created in Step 1.

      4. Other options can remain as the default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP addresses.

   * **backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * In the production environment, configure the access domain name of Ingress among the domain name providers, and ensure the A record of the Ingress access domain name has been configured with the public IP address or private IP address of Ingress.


<span id=".5q2l6aqk5LqU77ya5byA5ZCv6KeC5rWL6YWN572u"></span>
### Step 4: enable observability

Basic observability provides the monitoring metrics for AI resources and inference services. Deep observability provides an end\-to\-end performance monitoring service for inference applications.

<span id=".5Z-656GA6KeC5rWL"></span>
#### Basic observability


1. In the left navigation bar of the page for a specific cluster, select **Overview** under the gray title **Cloud native observability**, then click **Enable** on the page to start monitoring. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After you enable observability, Dynamo\-based application metrics will be collected into VMP, and you can query the metrics on the Explore page in the VMP console. The following figure shows an example.

3. View Dynamo\-based application metrics.

   * You can view Dynamo\-based application metrics on the preset dashboards of VMP. In the left navigation bar of the [VMP console](https://console.byteplus.com/prometheus), click **Monitoring dashboard**. Then, enter `dynamo` in the search box to view the dashboards. The following figure shows the sample Dynamo\-based application dashboards.

   * You can install Grafana and create Dynamo monitoring dashboards. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the installed Grafana and import the following dashboard file.

         <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e42b249945b4c3b53e9b92b4251c31c.json" name="dynamo_default_dashboard.json">dynamo_default_dashboard.json</Attachment>
         

      2. The following figure shows the result after importing.


<span id=".5rex5bqm6KeC5rWL"></span>
#### Deep observability


1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation bar, click **Server\-side Monitoring**.

2. Search for the keyword `Dynamo` and click the service name to go to the monitoring dashboard page.

3. View metrics.

   * LLM metrics

      On tabs such as ** Service Overview**, **LLM Performance**, and **Token Usage**, you can view the core metrics of the LLM service, including the number of LLM calls, token usage, response latency, TTFT, TPOT, QPS, and request error rate.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">TTFT and TPOT are effective only when LLMs are called with streaming\-enabled requests.      </div>
      

      The example of streaming call is as follows:

      ```Bash
      curl localhost:8000/v1/chat/completions \
        -H "Content-Type: application/json" \
        -d '{
          "model": "Qwen/Qwen3-235B-A22B",
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

   On the Trace analysis tab, you can search for trace information based on different conditions. Click a Trace ID you want to open the details page of the trace. View Trace information in the list.


<span id=".5qih5Z6L6aqM6K-B"></span>
## Model verification

<span id=".5pa55byP5LiA77ya6YCa6L-HLXNlcnZpY2Ut6K6_6Zeu"></span>
### Method 1: Access through Service

After you deploy the qwen3\-dynamo\-vllm\-pd application template, the created service whose name is in the format of `<application name>-qwen3-dynamo-vllm-pd` will provide an HTTP API endpoint (port 8000). The endpoint can be called as you do with OpenAI APIs.

The sample code is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the value of <code>localhost:8000</code> with the endpoint of your <code><application name>-qwen3-dynamo-vllm-pd</code> service.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen/Qwen3-235B-A22B",
    "messages": [
      {
        "role": "user",
        "content": "In the heart of Eldoria, an ancient land of boundless magic and mysterious creatures, lies the long-forgotten city of Aeloria. Once a beacon of knowledge and power, Aeloria was buried beneath the shifting sands of time, lost to the world for centuries. You are an intrepid explorer, known for your unparalleled curiosity and courage, who has stumbled upon an ancient map hinting at ests that Aeloria holds a secret so profound that it has the potential to reshape the very fabric of reality. Your journey will take you through treacherous deserts, enchanted forests, and across perilous mountain ranges. Your Task: Character Background: Develop a detailed background for your character. Describe their motivations for seeking out Aeloria, their skills and weaknesses, and any personal connections to the ancient city or its legends. Are they driven by a quest for knowledge, a search for lost familt clue is hidden."
      }
    ],
    "stream": false,
    "max_tokens": 30
  }'
```


In the **Workload** section of the **Helm details** page that corresponds to the qwen3\-dynamo\-vllm\-pd application, you can select a network\-reachable workload to go to the details page. In the upper\-right corner of the details page, click **Console** to log in to the pod that corresponds to the application to call the API.

<span id=".5pa55byP5LqM77ya6YCa6L-HLWFwaWct5pa55byP6K6_6Zeu"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the <code>example.com</code> in <code>http://example.com</code> with the domain name of the back\-end services obtained in <strong>Step 3</strong><strong>: configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 3</strong><strong>: configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The <code>content</code> parameter specifies the text you input to chat with LLMs.</div>



```bash
curl http://example.com/v1/chat/completions -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "Qwen/Qwen3-235B-A22B",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
    ]
  }'
```
