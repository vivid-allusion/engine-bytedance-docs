---
title: "Deploying DeepSeek-V3.1 with SGLang"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_DeepSeek-V3-1_based_on_SGLang"
---

This topic describes how to deploy the DeepSeek\-V3.1 large language model (LLM) as an inference service via SGLang in VKE.

<span id="IhyRwMb3"></span>
## Solution introduction

The solution leverages multiple acceleration technologies from BytePlus to enable rapid deployment of the DeepSeek\-V3.1 model within a Kubernetes cluster.

**DeepSeek\-V3.1**, developed by Chinese startup DeepSeek,  is a hybrid model that supports both thinking and non\-thinking modes.

<span id="ANNGloRS"></span>
## Deployment information


* Model: DeepSeek\-V3.1

* Inference engine: SGLang

* Instance specification: ecs.hpcpni3ln.45xlarge \* 2 units


<span id="FtBJiMm4"></span>
## Capabilities


* Precision: FP8

* Observability: Vital Managed Service for Prometheus (VMP)

* Access: API Gateway (APIG)


<span id="2hAgf6UK"></span>
## Notes


* To ensure successful deployment, which involves a bunch of add\-ons depending on each other and a variety of configurations, you need to exactly follow the instructions in this document.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of BytePlus. Contact the account manager of BytePlus to apply for the beta trial of the following features:

   
   |Beta features/resources |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU cloud computing servers](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The Deepseek model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id="WMfgm8HH"></span>
## Prerequisites

<span id="d29L0HNS"></span>
### Creating an HPC cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The HPC cluster must be deployed in the same <strong>region and availability zone</strong> as the VKE nodes.</div>


<span id="VVNJihIG"></span>
### Creating a VKE cluster

The following parameters need to be configured as described in the table when creating a cluster by using the VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). You can also use the [managed cluster template for heterogeneous computing](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster) to quickly create a VKE cluster for this scenario.


|Parameter |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select version v1.28 or later. |
|Network model |Select **VPC\-CNI**. |
|**Node pool configuration** ||
|Managed node pool |**Enable** managed node pool. |
|Availability zone |The VKE cluster is deployed in the same availability zone as the **HPC cluster**. |
|Instance type |Select the `ecs.hpcpni3ln.45xlarge` instance family of the High Performance Computing Optimized type that you applied for the beta trial. |
|High Performance Computing Cluster |Select the HPC cluster you created. |
|Number of nodes |2 |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory will be used as a dependency later and therefore cannot be modified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure the data that needs long\-term storage has been <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backed up</a> properly in case of computer crashes or disk damage which causes data loss.   </div><br>    |
|Node labels |When you deploy the DeepSeek model by using VKE, you need to specify the RDMA usage mode by using node labels.<br><br>Set the label key to `vke.node.rdma.mode` and the label value to `shared`. |
|Kubelet configs |The non\-uniform memory access (NUMA) affinity policy for RDMA devices needs to be configured by using custom parameters with the Kubelet when deploying DeepSeek model in the VKE.<br><br>Select `topology-manager-policy` and set the value to `best-effort`. |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) NVIDIA device driver, which is a management add\-on that allows the use of GPU devices in containers. |
|rdma\-device\-plugin |(Required) Management add\-on for RDMA NICs, which enables pod containers to use RDMA devices. |
|apig\-controller |(Required) APIG controller, which works as a cloud\-native AI gateway providing intelligent load balancing for inference traffic based on policies. |
|csi\-ebs |(Required) It allows VKE clusters to use the standard Container Storage Interface (CSI) of TOS. |
|prometheus\-agent |(Required) Monitoring add\-on for Vital Managed Service for Prometheus (VMP), which collects and sends metrics of Kubernetes clusters to VMP. |
|cr\-credential\-controller |(Recommended) It can pull images from Container Registry (CR) without passwords, which facilitates deployment process. |
|keda |(Recommended) Event\-driven autoscaler based on Kubernetes. It performs auto scaling for reference services based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id="qA3OUuRg"></span>
## Procedure

<span id="IFiMapJK"></span>
### Step 1: deploy LeaderWorkerSet

This topic uses the LeaderWorkerSet (LWS) to orchestrate inference workloads across multiple nodes (for example, DeepSeek\-V3.1 requires deployment across two nodes). LWS supports deploying a group of pods as a unit of replication.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Application template**. Scroll to the bottom of the page, click **More application templates**.

3. Click the **AI ** tab. Find the **leader\-worker\-set** application template, move the pointer over the application template, and then click **Deploy**.

4. On the **Deploy application** page, configure the parameters for **leader\-worker\-set**.

   
   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the latest Chart version of **leader\-worker\-set**. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster type |Keep the default value as **Managed version**. |
   |Cluster |Select the VKE cluster created in the **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |
   

5. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Find  leader\-worker\-set application by specifying target project, cluster, and namespace, and then click it to view detailed information of the application.


<span id="VphWkZ1S"></span>
### Step 2: Deploy deepseek\-v3.1\-sglang

VKE allows you to quickly deploy the DeepSeek\-V3.1 model based on the SGLang framework by using an **application template**.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find **deepseek\-v3.1\-sglang**, and click **Deploy**.

3. On the **Deploy application** page, configure parameters for deploying **deepseek\-v3.1\-sglang**.

   
   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of deepseek\-v3.1\-sglang. We recommend that you select the latest version. |
   |Parameter configuration |Configure parameters for the application deployment. Click the Edit icon to view the configuration description of various parameters in the `values.yaml` file or edit the YAML file. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it. |
   

4. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace, find the application deployed based on the deepseek\-v3.1\-sglang template, and click the application name to go to the details page. On the details page, view basic information about the application, workload, service, and other resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The services whose names match the pattern <code><application name>-api-svc</code> are external access points of their applications and will be used in subsequent steps such as routing configuration and model verification.   </div>
   

5. On the **StatefulSet** page of the VKE cluster, view the status of the workload that corresponds to the deepseek\-v3.1\-sglang application.

   1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Cluster**. Find the target cluster and click the cluster name.

   2. In the left navigation bar, click **Workload** \> **StatefulSet**. In the search box, enter the application name of deepseek\-v3.1\-sglang and click the search icon to view the status.


<span id="eZ3upx8u"></span>
### Step 3: Configure the Ingress

Configure routing for the model through APIG Ingress. Built based on [BytePlus APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), APIG Ingress functions as a managed cloud\-native gateway that features Ingress traffic management that ensures high availability and scalability of cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace where you want to deploy the deepseek\-v3.1\-sglang application template. The  namespace is used to associate the service exposed externally by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing** APIG instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you use the API Gateway to expose the model service in the clusters, we recommend you to configure the following parameters or features (some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the CLB instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance in the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong> When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. You can configure a timeout setting in the <a href="https://console.byteplus.com/veapig">API Gateway</a> console. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: By default, the alerting and logging capabilities are disabled for APIG instances that are created via the VKE console. You can enable logging and alerting in the <a href="https://console.byteplus.com/veapig">APIG console</a> to meet your requirements.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This feature helps you detect the issues of the entire system link from the perspective of the Ingress in a timely manner. For example, when the back end is unhealthy or crashes, the API Gateway reports error code <code>503</code>  and error details.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Poll**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select the service that was named in the pattern `<application name>-api-svc` and associated with the application created based on the deepseek\-v3.1\-sglang application template, and then set the port number to **8080**. |
   

2. (Optional) Configure APIG authentication.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: On the left navigation bar, select **Consumer management**, and click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level** and configure the instance, Service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in step 1.

      4. Other options can remain as default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP addresses.

   * **Backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * To test in the production environment, you need to register the Ingress domain name with your DNS provider and add public or private IPs correspondingly.


<span id="13mKeVbI"></span>
### Step 4: enable observability


1. In the left navigation bar of the page for a specific cluster, select **Overview** under the gray title **Cloud native observability**, then click **Enable** on the page to start monitoring. For more configuration details, refer to [Enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

2. After turning on observability, the application metrics of SGLang will be collected into the Vital Managed Service for Prometheus (VMP). You can use Explore to query metrics in the VMP console. An example is as follows:

   * There is a built\-in VMP dashboard that allows you to view the metrics collected from SGLang\-based applications. To do that, you can go to the [VMP console](https://console.byteplus.com/prometheus), select **Monitor dashboard** in the left navigation bar and search for `SGLang` to open the dashboard as shown below:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee08ac4b96e555506273b350e2c3a30e.png) </span>

   * You can also use self\-built Grafana and set up an SGLang monitoring dashboard. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

      1. Log in to the above Grafana and select Import the JSON file of the following dashboard:

         <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8a819899c3bab3f2b507a0d738b02aa.json" name="SGLang Dashboard-1747206543364.json">SGLang Dashboard-1747206543364.json</Attachment>
         

      2. The effect after import is shown in the figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7817f01eac7e278f43ffc08f3dcd5da4.png) </span>

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a40d0b078d252304401d12dc08fd843.png) </span>


<span id="OpfiCouV"></span>
## Model verification

<span id="F1g9fQah"></span>
### Method 1: Access through Service

After you deploy the deepseek\-v3.1\-sglang application template, the created service whose name is in the format of `<application name>-api-svc` serves an HTTP API endpoint (port 8080). The endpoint can be called as you do with OpenAI APIs.

The sample code is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>******</code> in <code>http://******</code> with the endpoint of your <code><application name>-api-svc</code> service.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> specifies the text you input to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "/data/models/DeepSeek-V3.1",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```


In the **Workload** section of the **Helm details** page that corresponds to the deepseek\-v3.1\-sglang application, click the name of the created StatefulSet to go to the **StatefulSet** page. In the upper\-right corner of the details page, click **Console** to log in to the pod that corresponds to the application to perform API calls.

<span id="bAsMuRYb"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace the <code>example.com</code> in <code>http://example.com</code> with the domain name of the back\-end services obtained in S<strong>tep 3: Configure the Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 4: configure Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "/models/deepseek",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
