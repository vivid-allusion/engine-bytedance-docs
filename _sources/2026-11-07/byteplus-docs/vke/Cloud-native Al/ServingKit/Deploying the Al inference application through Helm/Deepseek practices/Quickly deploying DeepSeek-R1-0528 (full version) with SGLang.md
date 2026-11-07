---
title: "Quickly deploying DeepSeek-R1-0528 (full version) with SGLang"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_full-version_model_DeepSeek-R1-0528_based_on_SGLang"
---

This topic mainly describes how to quickly deploy a model inference service with the DeepSeek\-R1\-0528 full version based on SGLang by using Vital Kubernetes Engine (VKE).

## Solution introduction

The solution integrates multiple acceleration technologies of BytePlus to quickly deploy the DeepSeek\-R1\-0528 large language model (LLM) in a Kubernetes cluster.

* **DeepSeek\-R1\-0528 model**: Released by the Chinese AI startup DeepSeek, DeepSeek\-R1\-0528 is a minor upgrade to DeepSeek R1. In the latest update, by increasing computing resources and introducing algorithm optimization mechanisms in post\-training, DeepSeek has significantly improved the inference and reasoning capabilities of DeepSeek\-R1\-0528.

* **GDKV model acceleration**: a fast model loading solution achieved through the Remote Direct Memory Access (RDMA) and GPU Direct RDMA (GDR) technologies provided by BytePlus.

Advantages of the solution

* **Quick model loading**: Multiple acceleration technologies are used to decrease the loading time of the DeepSeek\-R1\-0528 model to 13 seconds, accelerating loading by more than 40 times.

* **Cache pooling**: The idle memory and disk of GPU clusters are gathered to build a distributed cache pool, overcoming the limitation of single\-machine memory size.

### Deployment information

* Model: DeepSeek\-R1\-0528

* Inference engine: SGLang

* Instance specification: ecs.hpcpni3ln.45xlarge \* 2 units

### Capabilities

* Precision: FP8

* Model acceleration: GDKV

* Monitoring: Vital Managed Service for Prometheus (VMP) and Application Performance Management Plus (APMPlus)

* Access: API Gateway (APIG)

## Notes

* To ensure successful deployment, which involves a bunch of add\-ons dependent on each other and a variety of configurations, you need to exactly follow the instructions in this document.

* To achieve the expected results and comply with the VKE [limit](https://docs.byteplus.com/en/docs/vke/Limits), follow the solution described in this topic (or use the recommended resources listed here). If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln HPC\-optimized instance |[GPU Elastic Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The Deepseek model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |

## Prerequisites

### Creating an HPC cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

> **tip**

> The **region and availability zone** where the high\-performance compute cluster is located needs to be consistent with the **region and availability zone** of the VKE nodes.

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
|Number of nodes |2 nodes. |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   > **Warning**<br>   <br><br>   * > The `data01` directory is required by subsequent steps and must not be changed or customized.<br>   <br><br>   * > Ensure the data that needs long\-term storage has been [backed up](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) properly in case of computer crashes or disk damage which causes data loss.<br>    |
|Node labels |When you deploy the DeepSeek model by using VKE, you need to specify the RDMA usage mode by using node labels.<br><br>Set the label key to `vke.node.rdma.mode` and the label value to `shared`. |
|Kubelet configs |The non\-uniform memory access (NUMA) affinity policy for RDMA devices needs to be configured by using custom parameters with the Kubelet when deploying DeepSeek model in VKE.<br><br>Select the parameter `topology-manager-policy` and parameter value `best-effort`. |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) The NVIDIA device driver. It allows use of management add\-ons for GPUs in containers. |
|rdma\-device\-plugin |(Required) The add\-on manages RDMA network interface cards (NICs) and enables pod containers to use RDMA devices. |
|apig\-controller |(Required) The API Gateway controller provides a cloud\-native AI gateway capability and enables intelligent load balancing for inference traffic based on different policies. |
|csi\-ebs |(Required) It allows VKE clusters to use the standard Container Storage Interface (CSI).  |
|prometheus\-agent |(Required) VMP monitoring add\-on collects the monitoring metrics data of the Kubernetes cluster and sends it to VMP. |
|apmplus\-opentelemetry\-collector |(Required) Collect OpenTelemetry data and Prometheus metrics, and send them to APMPlus. |
|apmplus\-server\-agent |(Required) Collect service and host monitoring data and send it to APMPlus. |
|cr\-credential\-controller |(Recommended) It can pull Container Registry (CR) images without passwords, which simplifies deployment operations. |
|keda |(Recommended) The event\-driven autoscaler based on Kubernetes completes the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) The add\-on deploys CPU workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |

## Procedure

### Step 1: Deploy LeaderWorkerSet

This topic uses LeaderWorkerSet (LWS) to orchestrate multi\-node inference workloads (for example, DeepSeek R1 needs to be deployed across two nodes). LWS supports treating a group of pods as a single replication unit.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Application template**. Scroll to the bottom of the page, click **More application templates**.

3. Find **leader\-worker\-set**, hover the mouse over it and click **Deploy**.

4. On the **Deploy application** page, configure the parameters for **leader\-worker\-set**.

   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the latest Chart version of **leader\-worker\-set**. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster type ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |

5. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace, and click the name of the application deployed based on the leader\-worker\-set template to go to the details page. On the details page, view the basic information about the application and the created workloads, services, and other resources.

### Step 2: Deploy deepseek\-r1\-0528\-sglang

VKE provides the DeepSeek\-R1\-0528 model application based on the SGLang framework. The application can be quickly deployed through the **Application template** page of the VKE console.

1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find **deepseek\-r1\-0528\-sglang** and click **Deploy**.

3. On the **Deploy application** page, specify the parameters of **deepseek\-r1\-0528\-sglang**.

   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of deepseek\-r1\-0528\-sglang. We recommend that you select the latest version. |
   |Parameter configuration |The configuration method of deepseek\-r1\-0528\-sglang. If you need to enable EIC, click the edit icon to modify the `values.yaml file` based on the **EIC\-related parameters in the YAML file** section below the table. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster you created as required in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |

   **EIC\-related parameters in the YAML file**:

   ```yaml
     eic:
     enabled: true
     # EIC instance ID. Log in to the EIC console and click the EIC instance to find the endpoint on the "Instance Information" tab.
     instanceID: "eicydx97nk******" 
     # Endpoint of the EIC instance. Log in to the EIC console and click the EIC instance to find the endpoint on the "Instance Information" tab.
     remoteURL: "eic://192.168.xx.xx:12500;192.168.xx.xx:12500;192.168.xx.xx:12500"
     # EIC node network interface card. Log in to the EIC console and click the EIC instance to find the NIC on the "Node List" tab.
     netLocalInterfaceNames: "eth1;eth2;eth3;eth4"
     # Deploy the VKE node pool ID corresponding to the EIC nodes. Log in to the VKE console. In the left navigation bar of the cluster management page, click Nodes > Node pool to view the ID.
     machinePool: "pd0ve352******"
   ```

4. Click **Confirm ** to deploy the application.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace, and click the name of the deployed deepseek\-r1\-0528\-sglang application to go to the details page. On the details page, view the basic information about the application and the created workloads, services, and other resources.

   > **tip**

   > The service names that match the pattern `<application name>-api-svc` indicate those services that work as the external access points of their applications, and therefore are supposed to be used during routing configuration and model verification.

5. On the **StatefulSet** page of the VKE cluster, view the load status of the deepseek\-r1\-0528\-sglang application.

   1. On the left navigation bar of the [VKE console](https://console.byteplus.com/vke), select **Cluster**, and find the target cluster and click the cluster name.

   2. In the left navigation bar, click **Workload** \> **StatefulSet**. Then, enter the application name deepseek\-r1\-0528\-sglang in the search box to view the status of the related workload.

### Step 3: Configure Ingress

Configure model routing through APIG Ingress. APIG Ingress can function as a managed cloud\-native gateway based on the BytePlus [APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), realizing high availability and scalability in Ingress traffic management that are required in cloud\-native applications.

1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace where the deepseek\-r1\-0528\-sglang application template is deployed to associate the service exposed by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br>> **tip**<br><br><br>> When you are using the API Gateway to expose the model service in the clusters, we recommend you to configure the following parameters or features (Some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):<br><br><br><br>* > **Instance specification**: We recommend that you select **4c8g**, with two availability zones to achieve high availability by default.<br><br><br>* > **Bandwidth limit**: This option is used to set the maximum bandwidth of the Classic Load Balancer (CLB) instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the [APIG console](https://console.byteplus.com/veapig). For details, see [Adding access entrance](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).<br><br><br>* > **Circuit breaking:** When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.<br><br><br>* > **Request timeout**: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. If timeout is needed, you can configure it on the [API Gateway console](https://console.byteplus.com/veapig). For details, refer to [Advanced routing policy](https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy).<br><br><br>* > **Observability**: By default, the alerting, monitoring, and logging capabilities are disabled for APIG instances that are created via the VKE console. If needed, we recommend that you enable the logging, monitoring, and alerting capabilities of the instances in the [APIG console](https://console.byteplus.com/veapig).<br><br><br>   * > **Instance monitoring**: This can help you to detect anomalies in the whole system chain from the gateway entry level. For example: Unhealthy back end and back\-end crashes will cause the APIG to return `503` error code and specific errors.<br><br><br>   * > **Instance logs**: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.<br> |
   |Backend upstream |We recommend that you set the **LoadBalancer algorithm** parameter to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select a service that is created when you deploy the deepseek\-r1\-0528\-sglang application template and set the port number to **8080**. The name of the service is in the format of `<application name>-api-svc`. |

2. (Optional) Configure authentication for an APIG.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: On the left navigation bar, select **Consumer management**, and click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**.

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth plugin: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level**: and configure the instance, service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in step 1.

      4. Other options can remain as default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP.

   * **backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * In the production environment, configure the access domain name of Ingress among the domain name providers, and ensure the A record of the Ingress access domain name has been configured with the public IP address or private IP address of Ingress.

### Step 4: enable observability

Basic observability provides monitoring metrics for AI resources and inference services, while deep observability provides end\-to\-end performance monitoring for inference applications.

#### Basic observability

1. In the left navigation bar of the page for a specific cluster, select **Overview** under the gray title **Cloud native observability.**  Then, click **Enable** on the page to start monitoring. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitoring dashboard** in the left navigation bar and search for `SGlang` to open dashboard as shown below:

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png)

   * You can also use Grafana to build a custom monitoring dashboard for SGlang\-based applications. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the above Grafana and select to import the following dashboard JSON file:

         [SGLang Dashboard-1747206543364.json](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8a819899c3bab3f2b507a0d738b02aa.json)

      2. The effect after importing is shown in the figure:

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png)

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png)

#### Deep observability

1. Log in to the [APMPlus console](https://console.byteplus.com/apmplus-server/region:apmplus-server+cn-beijing/console/overview/server?monitorType=server). In the left navigation bar, click **Server\-side monitoring**.

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

4. View trace analysis.

   From the Trace analysis tab of the SGLang application, you can retrieve the link information according to different conditions. Click the ID of the target trace to go to the details page of the trace. View the trace information in the list.

## Model verification

### Method 1: Access through service

After you deploy the deepseek\-r1\-0528\-sglang application template, the created service whose name is in the format of `<application name>-api-svc` will provide an HTTP API endpoint (port 8080). You can call the endpoint by using an OpenAI\-compatible API format.

The sample code is as follows.

> **tip**

* > Replace `******` in `http://******` with the endpoint of your `<application name>-api-svc` Service.

* > The parameter `content` is the conversation content you want to send to the model.

```Bash
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

In the **Workload** section of the **Helm details page** that corresponds to the deepseek\-r1\-0528\-sglang application, click the name of the created StatefulSet to go to the **StatefulSet** page. In the upper\-right corner of the details page, click **Console** to log in to the pod that corresponds to the application to call the API.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_efc34d5222444ba3342ca7f8c442307c.png)

### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token to the request.

The following example is provided for reference.

> **tip**

* > Replace the `example.com` in `http://example.com` with the domain name of the back\-end services obtained in **Step 3****: Configure Ingress**.

* > Replace `eyJhbGciOiJSUzI******` with the API Key generated in **Step 3****: Configure Ingress**.

* > The parameter `content` is what you want to type to chat with LLMs.

```bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "/models/DeepSeek-R1-0528",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
