---
title: "Quickly deploying DeepSeek-R1-0528/V3-0424 (full version) with SGLang (PD disaggregation)"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_SGLang-based_DeepSeek-R1-0528_V3-0424_full_version_with_PD_disaggregation"
---

This article mainly introduces using the Vital Kubernetes Engine (VKE) to quickly deploy the model inference service of the SGLang\-based DeepSeek\-R1\-0528/DeepSeek\-V3\-0324 full version (with PD disaggregation).

## Solution introduction

This solution provides the method to achieve the Prefill\-Decode (PD) separated deployment capability of the DeepSeek\-R1\-0528/DeepSeek\-V3\-0324 Large Language Model (LLM) in the Kubernetes clusters.

* **DeepSeek\-R1\-0528 model**: Released by the Chinese AI startup company DeepSeek, the DeepSeek\-R1 model is an inference model trained based on DeepSeek\-V3\-Base. This model is good at mathematics, code, and natural language inference, which has gained wide attention due to its open source availability, algorithm innovation, and cost\-effectiveness.

* **DeepSeek\-V3\-0324 model**: Released by the Chinese AI startup DeepSeek, the DeepSeek\-V3\-0324 model is a general\-purpose LLM with 671 billion parameters and 37 billion activated parameters, featuring a mixture of experts (MoE) architecture. Pre\-trained on 14.8 trillion tokens, the DeepSeek\-V3 model provides services such as information retrieval, data analysis, and natural language processing, which apply to various application scenarios such as customer service, educational tutoring, and content creation.

* **PD disaggregation technology**: The technology divides the inference process into two phases, which are deployed in different hardware resources to optimize performance:

   * Prefill: A compute\-intensive phase

   * Decode: A memory\-intensive phase

**Core advantages of the solution**

* **Improved resource utilization**: Separately handling Prefill and Decode phases which respectively require high and low computing power.

* **Increased throughput**: New requests are being processed in the Prefill phase while the old ones are being handled in the Decode phase.

* **Reduce latency**: The wait time of concurrent requests is reduced and the overall efficiency is improved.

### Deployment information

* Models: DeepSeek\-R1\-0528\-671B, DeepSeek\-V3\-671B

* Inference engine: SGlang

* Instance specification: ecs.hpcpni3ln.45xlarge

   * Prefill: 4 instances

   * Decode: 4 instances

### Supported capabilities

* Parallel strategy: PD disaggregation, Data Parallelism (DP), Tensor Parallelism (TP), and Expert Parallelism (EP).

* Data precision: FP8

* Observability: Vital Managed Service for Prometheus (VMP) and Application Performance Management Plus (APMPlus).

* Access: API Gateway (APIG)

### Performance evaluation

The following table shows the comparison between the open\-source version and the optimized version of the model.

> **tip**

> The performance results are related to machine specifications, distribution configuration, and network bandwidth. A more optimal network topology can bring better inference performance**.** The final outcome will be subject to the actual test results.

|**Category** |**open source** |**Optimized** |
|---|---|---|
|Inference engine |SGLang (open source) |SGLang (BytePlus optimized version) |
|Input/Output |3500/1500 |3500/1500 |
|TTFT (ms) |<=5000 |<=5000 |
|TPOT (ms) |<=50 |<=50 |
|Parallel policy |TP |PD disaggregation, DP, TP, and EP. |
|Single\-GPU throughput (TPS) |167.4 |715 |

## Notes

* In this example, many add\-ons are used, which are dependent on each other and have complex configurations. To achieve the expected results, you must perform operations according to the guidance in this article.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The Deepseek model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |

## Prerequisites

### Creating an HPC cluster

The HPC cluster can achieve the logical isolation of high\-performance computing GPU instances (computing nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, refer to [Creating High-Performance Compute Clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters)

> **tip**

> The**region and availability zone** where the high\-performance compute cluster is located need to be consistent with those of the VKE nodes.

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
|Number of nodes |8 |
|Operating system |Select **Public images** \> **Ubuntu** \> **Ubuntu 20.04**. |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   > **Warning**<br>   <br><br>   * > The `data01` directory has subsequent dependencies. Therefore, the directory cannot be modified or specified.<br>   <br><br>   * > Ensure the data that needs long\-term storage has been [backed up](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) properly in case of computer crashes or disk damage which causes data loss.<br>    |
|Node labels |When deploying DeepSeek model through VKE, you need to set the node label to configure the RDMA usage mode.<br><br>The label key is set to: `vke.node.rdma.mode`, and the label value is set to: `shared`. |
|Kubelet configs |The non\-uniform memory access (NUMA) affinity policy for RDMA devices needs to be configured by using custom parameters with the Kubelet when deploying DeepSeek model in the VKE.<br><br>Select the parameter `topology-manager-policy` and its value `best-effort`. |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
|rdma\-device\-plugin |(Required) The add\-on manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. |
|apig\-controller |(Required) The APIG controller provides cloud\-native AI Gateway capabilities, which intelligently balances inference traffic based on different policies. |
|prometheus\-agent |(Required) The VMP monitoring add\-on collects the metrics data of the Kubernetes cluster and sends the data to VMP. |
|apmplus\-opentelemetry\-collector |(Required) Collect OpenTelemetry data and Prometheus metrics, and send them to APMPlus. |
|apmplus\-server\-agent |(Required) Send in parallel the collection service and host monitoring data to APMPlus. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) The event\-driven autoscaler based on Kubernetes completes the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |

## Procedure

### Step 1: Deploy LeaderWorkerSet

This article uses the LeaderWorkerSet (LWS) to orchestrate the inference loads of multiple nodes, for example, DeepSeek\-R1\-0528 needs to be deployed across two nodes. In addition, LWS supports taking a group of Pods as the object of replication.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Application center \> Application template**. Scroll to the bottom of the page, click **More application templates**.

3. On the **Application template** page, find **leader\-worker\-set**. Move your cursor over this application template, and then click **Deploy**.

4. On the **Deploy application** page, configure the service parameters of **leader\-worker\-set**.

   |Configuration item |Description |
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

   After deploying the application, it will be displayed on the **Helm ** page. Find  leader\-worker\-set  application by specifying target project, cluster, and namespace, then click it to view detailed information of the application.

### Step 2: Deploy the application template

The VKE provides Prefill\-Decode\-separated DeepSeek\-R1/DeepSeek\-V3 model application based on SGLang framework. You can quickly deploy it through **an application template**.

1. In the [Vital Kubernetes Engine console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Application center \> Application template**.

3. On the **Application template** page, find **deepseek\-r1\-0528\-sglang\-pd** or **deepseek\-v3\-0324\-sglang\-pd**. Application template, click **Deploy**.

4. On the **Deploy application** page, configure the parameters of the application templates **deepseek\-r1\-0528\-sglang\-pd** or **deepseek\-v3\-0324\-sglang\-pd**.

   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of deepseek\-r1\-0528\-sglang\-pd or deepseek\-v3\-0324\-sglang\-pd. We recommend that you select the latest version. |
   |Parameter configuration |The configuration method of deepseek\-r1\-0528\-sglang\-pd / deepseek\-v3\-0324\-sglang\-pd. Click the Edit icon to view the configuration description of various parameters in the `values.yaml` file or edit the YAML file. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |

5. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace, and find the deployed applications deepseek\-r1\-0528\-sglang\-pd / deepseek\-v3\-0324\-sglang\-pd. Click the application names to go to the details page to view the basic information of this application, and the workloads, services, and other resources created in association with the application.

   > **tip**

   > The service names that match the pattern `<application name>-api-svc` indicate those services will be working as the external access points of their applications, and therefore are supposed to be used when configuring routing and verifying model deployment.

6. On the **StatefulSet** page of the VKE clusters, view the load status of the applications deepseek\-r1\-0528\-sglang\-pd / deepseek\-v3\-0324\-sglang\-pd.

   1. On the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Cluster**, and find the target cluster and click the cluster name.

   2. On the target cluster management page, select **Workload** \> **StatefulSet**, and then search the names of the applications deepseek\-r1\-0528\-sglang\-pd / deepseek\-v3\-0324\-sglang\-pd, to view the relevant load status.

### Step 3: Configure the Ingress

Configure routing for the model through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that are required in cloud\-native applications.

1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   |Configuration Item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace of the deepseek\-r1\-0528\-sglang\-pd or deepseek\-v3\-0324\-sglang\-pd application template to be deployed, which is used to associate with the services exposed externally of this application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br>> **tip**<br><br><br>> When you are using the API Gateway to expose the model service in the clusters, we recommend you to configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):<br><br><br><br>* > **Instance specification**: We recommend that you select **4c8g**, with two availability zones to realize high availability by default.<br><br><br>* > **Bandwidth limit**: This option is used to set the maximum bandwidth of the Classic Load Balancer (CLB) instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the [APIG console](https://console.byteplus.com/veapig). For details, see [Adding access entrance](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).<br><br><br>* > **Circuit breaking:** When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.<br><br><br>* > **Request timeout**: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If timeout is needed, you can configure it on the [API Gateway console](https://console.byteplus.com/veapig). For details, refer to [Advanced routing policy](https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy).<br><br><br>* > **Observability**: By default, the alerting, monitoring, and logging capabilities are disabled for APIG instances that are created via the VKE console. If needed, we recommend that you enable the logging, monitoring, and alerting capabilities of the instances in the [APIG console](https://console.byteplus.com/veapig).<br><br><br>   * > **Instance monitoring**: This can help you to detect the anomalies in the whole system chain from the gateway entry level. For example: Unhealthy back end and back\-end crashes will cause the APIG to return `503` error code and specific errors.<br><br><br>   * > **Instance logs**: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.<br> |
   |Backend upstream |We recommend that you set the **LoadBalancer algorithm** parameter to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |When selecting to deploy the application template deepseek\-r1\-0528\-sglang\-pd / deepseek\-v3\-0324\-sglang\-pd, associate it with the service created in the `<application>-api-svc` format, and set the port number to **8080**. |

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: On the left navigation bar, select **Consumer management**, and click **Create consumer**.

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

   * In the production environment, configure the access domain name of Ingress among the domain name providers, and ensure the A record of the Ingress access domain name has been configured with the public IP address or private IP address of Ingress.

### Step 4: Enable observability

Basic observability provides the monitoring metrics for AI resources and inference service. Deep observability provides full\-link performance monitoring service for inference application.

#### Basic observability

1. In the left navigation bar of the page for a specific cluster, select **Overview** under the gray title **Cloud native observability**, then click **Enable** on the page to start monitoring. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitoring dashboard** in the left navigation bar and search for `SGlang` to open dashboard as shown below:

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png)

   * You can also use Grafana to build a custom monitoring dashboard for SGlang\-based applications. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

      1. Log in to the above Grafana and select to import the following dashboard JSON file:

         [SGLang Dashboard-1747206543364.json](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8a819899c3bab3f2b507a0d738b02aa.json)

      2. The effect after importing is shown in the figure:

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png)

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png)

#### Deep observability

1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation bar, click ** Server\-side monitoring**.

2. Search for `SGlang` and click the service name in the results to open the monitoring dashboard page.

3. View metrics.

   * LLM metrics

      On tabs such as ** Service Overview**, **LLM performance**, and **Token usage**, you can view the core metrics of the LLM service, including number of LLM calls, token usage, response latency, TTFT, TPOT, QPS, and request error rate.

      > **tip**

      > TTFT and TPOT are effective only when LLMs are called with streaming\-enabled requests.

      The example of a streaming call is as follows:

      ```Bash
      curl localhost:8080/v1/chat/completions \
        -H "Content-Type: application/json" \
        -d '{
          "model": "/data/models/DeepSeek-R1-0528",
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

## Model verification

### Method 1: Access through Service

After deploying the application templates of deepseek\-r1\-0528\-sglang\-pd or deepseek\-v3\-0324\-sglang\-pd, associate them with the services whose names are in the format of `<application name>-api-svc` , which provides an HTTP API endpoint (port 8080).

The sample code is as follows.

> **tip**

* > Replace `******` in `http://******` with the endpoint of your `<application name>-api-svc` Service.

* > The parameter `content` is what you want to type to chat with LLMs.

```bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "/data/models/DeepSeek-R1-0528",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```

You can select **Workload** \> **StatefulSet** on the target cluster management page in the [VKE console](https://console.byteplus.com/vke). Then search for the names of the applications deepseek\-r1\-0528\-sglang\-pd or deepseek\-v3\-0324\-sglang\-pd, and find the StatefulSet created in association with the applications. Enter the load details page, click the **Console** in the upper\-right corner of the page, and log in to the Pod corresponding to the application, to execute API invocations.

### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

> **tip**

* > Replace the `example.com` in `http://example.com` with the domain name of the back\-end services obtained in S**tep 4: Configure the Ingress**.

* > Replace `eyJhbGciOiJSUzI******` with the API Key generated in **Step 4: Configure the Ingress**.

* > The parameter `content` is what you want to type to chat with LLMs.

```bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "DeepSeek-R1-0528",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
