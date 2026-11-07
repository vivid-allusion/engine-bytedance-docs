---
title: "Quickly deploying Seed-OSS-36B-Instruct with vLLM"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_Seed-OSS-36B-Instruct_based_on_vLLM"
---

This topic describes how to quickly deploy a Seed\-OSS\-36B\-Instruct model inference service based on vLLM by using Vital Kubernetes Engine (VKE).

<span id="5cEdYAoA"></span>
## Solution introduction

The solution leverages multiple acceleration technologies from BytePlus to enable rapid deployment of the Seed\-OSS\-36B model within a Kubernetes cluster.

**Seed\-OSS\-36B** is a family of open\-source large language models developed by ByteDance's Seed team to address a range of AI tasks that require powerful long\-context processing, reasoning, agent and general capabilities, and versatile developer\-friendly features.

<span id="8xKRjVgT"></span>
### **Deployment information**


* Model: Seed\-OSS\-36B\-Instruct

* Inference engine: vLLM (open source)

* Recommended specification: ecs.hpcpni3ln.45xlarge \* 1 unit


<span id="hjmjXEX6"></span>
### **Supported capabilities**


* Observability: Vital Managed Service for Prometheus (VMP)

* Access: API Gateway (APIG)


<span id="DloOiS2K"></span>
## Notes


* To ensure successful deployment, which involves multiple interdependent add\-ons and a variety of configurations, you need to exactly follow the instructions in this document.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU cloud computing servers](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. The model has a large number of parameters and therefore requires a GPU instance with large memory, e.g., `ecs.hpcpni3ln.45xlarge`. |
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   


<span id="wMPWu0iZ"></span>
## Prerequisites

<span id="sQ7foTvN"></span>
### Creating an HPC cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The HPC cluster must be deployed in the same <strong>region and availability zone</strong> as the VKE nodes.</div>


<span id="1m5j8g7K"></span>
### Creating a VKE cluster

The following parameters need to be configured as described in the table when creating a cluster by using the VKE. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). You can also use the [managed cluster template for heterogeneous computing](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster) to quickly create a VKE cluster for this scenario.


|Parameter |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select version v1.28 or later. |
|Network model |Select **VPC\-CNI**. |
|**Node pool configuration** ||
|Managed node pool |**Enable** Managed node pool. |
|Availability zone |Same availability zone as the **High\-Performance Compute Cluster**. |
|Instance type |Select the `ecs.hpcpni3ln.45xlarge` instance family of the High Performance Computing Optimized type that you applied for the beta trial. |
|High Performance Computing Cluster |Select the HPC cluster you created. |
|Number of nodes |1 |
|Operating system |Click **Public images** \> **Ubuntu** \> **Ubuntu 20.04 with GPU Driver 535.161.08 and doca**. |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory will be used as a dependency later and therefore cannot be modified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure the data that needs long\-term storage has been <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backed up</a> properly in case of computer crashes or disk damage which causes data loss.   </div><br>    |
|Node labels |When you deploy the model by using VKE, you need to specify the RDMA usage mode by using node labels.<br><br>Set the label key to `vke.node.rdma.mode` and the label value to `shared`. |
|Kubelet configs |The non\-uniform memory access (NUMA) affinity policy for RDMA devices needs to be configured by using custom parameters with the Kubelet when deploying the model in the VKE.<br><br>Select` topology-manager-policy` and set the value to `best-effort`. |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) NVIDIA device driver, which is a management add\-on that allows use of GPU devices in containers. |
|rdma\-device\-plugin |(Required) Management add\-on for RDMA NICs, which enables pod containers to use RDMA devices. |
|apig\-controller |(Required) APIG controller, which works as a cloud\-native AI gateway providing intelligent load balancing for inference traffic based on policies. |
|csi\-ebs |(Required) To ensure successful deployment, which involves multiple interdependent add\-ons and various configurations, you need to precisely follow the instructions in this document. |
|prometheus\-agent |(Recommended) Monitoring add\-on for Vital Managed Service for Prometheus (VMP), which collects and sends metrics of Kubernetes clusters to VMP. |
|keda |(Recommended) Event\-driven autoscaler based on Kubernetes. It completes the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id="RuJaRpLA"></span>
## Procedure

<span id="IZQOeE9T"></span>
### Step 1: Deploy seed\-oss\-36b\-instruct

VKE allows you to quickly deploy the  Seed\-OSS\-36B\-Instruct model based on the vLLM framework by using an **application template**.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, select **Application center \> Application template**.

3. On the **Application template** page, find the **seed\-oss\-36b\-instruct\-vllm** application template, move the pointer over this application template, and then click **Deploy**.

4. On the **Deploy application** page, configure deployment parameters for **seed\-oss\-36b\-instruct\-vllm**.

   
   |Parameter |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select a Chart version for seed\-oss\-36b\-instruct\-vllm. We recommend that you select the latest version. |
   |Parameter configuration |Configure parameters for the application deployment. Click the Edit icon to view the configuration description of various parameters in the `values.yaml` file or edit the YAML file. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |
   

5. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace and click the name of the deployed seed\-oss\-36b\-instruct\-vllm application to go to the details page. On the details page, view the basic information about the application, workload, service, and other resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The services whose names are in the format of <code><application name>-api-svc</code> indicate those services that work as the external access points of their applications, and therefore are supposed to be used during routing configuration and model verification.   </div>
   

6. On the **Deployment** page of the VKE cluster, view the status of the workload that corresponds to the seed\-oss\-36b\-instruct\-vllm application.

   1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Cluster.**  Find the target cluster and click the cluster name.

   2. In the left navigation bar, click **Workload** \> **Deployment**. In the search box, enter the application name of seed\-oss\-36b\-instruct\-vllm and click the search icon to view the status.


<span id="RpyP9X91"></span>
### Step 2: Configure the Ingress

Configure model routing through APIG Ingress. Built based on [BytePlus APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), APIG Ingress functions as a managed cloud\-native gateway that features Ingress traffic management that ensures high availability and scalability of cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Parameter |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace where the seed\-oss\-36b\-instruct\-vllm application template is deployed to associate the service exposed by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you use the API Gateway to expose the model service in the clusters, we recommend that you configure the following parameters or features (some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to ensure high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the Classic Load Balancer (CLB) instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entries</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong> When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. You can configure a timeout setting in the <a href="https://console.byteplus.com/veapig">API Gateway</a> console. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: By default, the alerting and logging capabilities are disabled for APIG instances that are created via the VKE console. You can enable logging and alerting in the <a href="https://console.byteplus.com/veapig">APIG console</a> to meet your requirements.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This feature helps you detect the issues of the entire system link from the perspective of the Ingress in a timely manner. For example, when the back end is unhealthy or crashes, the API Gateway reports error code <code>503</code>  and error details.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Round Robin**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select the service that was named in the pattern `<application name>-api-svc` and associated with the application created based on the seed\-oss\-36b\-instruct\-vllm application template, and then set the port number to **8080**. |
   

2. (Optional) Configure APIG authentication and authorization.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: On the left navigation bar, select **Consumer management**, and click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credential information.

   6. Enable Key Auth add\-on: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level** and configure the instance, Service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in Step 1.

      4. Other options can remain as default.

3. Obtain the Ingress address.

   * **VIP**: includes both public and private IP.

   * **Backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can implement a domain\-to\-IP resolution locally.

   * In the production environment, configure the access domain name of Ingress among the domain name providers, and ensure that the A record of the Ingress access domain name points to the public or private IP address of the Ingress.


<span id="mcUrpIRx"></span>
## Model verification

<span id="KYY1bm9Z"></span>
### Method 1: Access through Service

After you deploy the seed\-oss\-36b\-instruct\-vllm application template, the created service whose name is in the format of `<application name>-api-svc` serves an HTTP API endpoint (port 8080). The endpoint can be called as you do with OpenAI APIs.

The sample code is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip </div>



* <div data-tips="true" data-tips-type="tip">Replace <code>******</code> in <code>http://******</code> with the endpoint of your <code><application name>-api-svc</code> service.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions     -H "Content-Type: application/json"     -d '{
        "model": "seed_oss",
        "messages": [
            {"role": "user", "content": "Who are you?"}
        ]
    }'
```


You can directly log in to the pod to perform API calls. To do that, go to the **Helm details page** of the seed\-oss\-36b\-instruct\-vllm application, click the name of the associated Deployment in the **Workload ** section, and on the **Deployment ** page that opens, click **Console ** in the upper\-right corner to open the console where commands can be executed.

<span id="y9lhYrf4"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>example.com</code> in the <code>http://example.com</code> with the Ingress backend service access domain name obtained in <strong>Step 2: Configure the Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace<code> eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 2: Configure the Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "seed_oss",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
