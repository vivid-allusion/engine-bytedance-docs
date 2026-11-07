---
title: "Quickly deploying gpt-oss-120b with vLLM"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deploying_the_gpt-oss-120b_inference_service"
---

This topic mainly describes the procedure for deploying the gpt\-oss\-120b inference service by using Vital Kubernetes Engine (VKE).

<span id="DyLztsCW"></span>
## Solution introduction

This solution implements a quick deployment of the gpt\-oss\-120b large language model in a Kubernetes cluster:

**gpt\-oss\-120b** is a model released by [OpenAI ](https://openai.com/open-models) in August 2025. The gpt\-oss\-120b model matches OpenAI's o4\-mini model in core inference benchmarks and operates efficiently on just one 80 GiB GPU.

<span id="6bxISEht"></span>
### Deployment information


* Model: gpt\-oss\-120b

* Inference engine: vLLM (open source)

* Recommended specification: ecs.hpcpni3ln.45xlarge \* 1 unit


<span id="VG90paiq"></span>
## Supported capabilities


* Observability: Vital Managed Service for Prometheus (VMP)

* Access: API Gateway (APIG)


<span id="3VckFtvB"></span>
## Notes


* To ensure successful deployment, which involves multiple interdependent add\-ons and various configurations, you need to precisely follow the instructions in this document.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this topic or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* A full deployment depends on some beta capabilities of the BytePlus. Contact the Account Manager of the BytePlus to apply for the beta trial of the following features:

   
   |Beta feature/resource |Product involved |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU cloud computing servers](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. We recommend that you apply for a GPU instance with large GPU memory, for example, `ecs.hpcpni3ln.45xlarge`. |
   


<span id="0iD634Nn"></span>
## Prerequisites

<span id="QFb44eIF"></span>
### Creating an HPC cluster

The high\-performance compute cluster is used to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The HPC cluster must be deployed in the same <strong>region and availability zone</strong> as the VKE nodes.</div>


<span id="B56N0yZL"></span>
### Creating a VKE cluster

When you create a cluster in VKE, take note of the configuration of the following parameters. For details on other parameters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). You can also use the [managed cluster template for heterogeneous computing](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster) to quickly create a VKE cluster for this scenario.


|Configuration item |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select version v1.28 or later. |
|Network model |Select **VPC\-CNI**. |
|Public NAT for internet endpoint |Enable **Public NAT for internet endpoint**. |
|**Node pool configuration** ||
|Managed node pool |**Enable ** Managed node pool. |
|Availability zone |Same availability zone as the **High\-Performance Compute Cluster**. |
|Instance type |Select the `ecs.hpcpni3ln.45xlarge` instance family of the High Performance Computing Optimized type that you applied for the beta trial. |
|High Performance Computing Cluster |Select the HPC cluster you created. |
|Number of nodes |1 |
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory will be used as a dependency later and therefore cannot be modified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the physical host fails or the local disk is damaged, data loss may occur. Do not store data that must be retained long\-term on the local disk, and make sure <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backups</a> are in place.   </div><br>    |
|**Addon configuration** ||
|nvidia\-device\-plugin |(Required) NVIDIA device driver, which is a management add\-on that allows use of GPU devices in containers. |
|apig\-controller |(Required) APIG controller, which works as a cloud\-native AI gateway providing intelligent load balancing for inference traffic based on policies. |
|csi\-ebs |(Required) It enables VKE clusters to use the standard CSI implementation for Elastic Block Storage (EBS). |
|prometheus\-agent |(Required) Monitoring add\-on for Vital Managed Service for Prometheus (VMP), which collects and sends metrics of Kubernetes clusters to VMP. |
|cr\-credential\-controller |(Recommended) It can pull images from Container Registry (CR) without passwords, which facilitates the deployment process. |
|keda |(Recommended) Event\-driven autoscaler based on Kubernetes. Complete the autoscaler tasks of the inference service based on complex metrics. |
|vci\-virtual\-kubelet |(Recommended) It can deploy CPU\-consuming workloads such as system add\-ons by using Vital Container Instance (VCI), which eliminates the need for operation and maintenance (O&M) and does not occupy the computing resources of GPU nodes. |


<span id="FYo8guVM"></span>
## Procedure

<span id="6U8OfStf"></span>
### Step 1: Deploy gpt\-oss\-120b

VKE allows you to quickly deploy the gpt\-oss\-120b model based on the vLLM framework by using an **application template**.


1. In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Application center \> Application template**.

2. On the **Application template** page, find **gpt\-oss\-120b\-vllm**, and click **Deploy**.

3. On the **Deploy application** page, configure parameters for deploying **gpt\-oss\-120b\-vllm**. Some parameters need to be configured according to the following descriptions. Other parameters can be configured according to the prompts of the interface, or refer to the descriptions in [Application template](https://docs.byteplus.com/en/docs/vke/Application-templates).

   
   |Configuration item |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select a Chart version for gpt\-oss\-120b\-vllm. We recommend that you select the latest version. |
   |Parameter configuration |Configure parameters for the application deployment. Click the edit icon next to `values.yaml` to edit the YAML file of the current application. For the descriptions of some parameters, refer to the following table. |
   |Name |Customize the application name according to the naming requirements prompted by the interface. |
   |**Deployment environment** ||
   |Cluster |Select the VKE cluster created as described in **Prerequisites**. |
   |Namespace |Select a namespace under the target cluster. |
   |Protocol |Read and understand the agreement before selecting it.  |
   

4. Click **Confirm** to start deployment.

   The applications that are already deployed can be found on the **Helm** page. Select the target project, cluster, and namespace and click the name of the deployed gpt\-oss\-120b\-vllm application to go to the details page. On the details page, view the basic information about the application, workload, service, and other resources.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The services whose names are in the format of <code><application name>-api-svc</code> indicate those services that work as the external access points of their applications, and therefore are supposed to be used during routing configuration and model verification.   </div>
   

5. On the **Deployment** page of the VKE cluster, view the status of the workload that corresponds to the gpt\-oss\-120b\-vllm application.

   In the left navigation bar of the [VKE console](https://console.byteplus.com/vke), click **Cluster**. On the page that appears, find the target cluster and click the cluster name.

   In the left navigation bar, click **Workload** \> **Deployment**. In the search box, enter the application name of gpt\-oss\-120b\-vllm and click the search icon to view the status.


<span id="Jm9zOYfY"></span>
### Step 2: Configure the Ingress

Configure model routing through APIG Ingress. Built based on [BytePlus APIG](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), APIG Ingress functions as a managed cloud\-native gateway that features Ingress traffic management that ensures high availability and scalability of cloud\-native applications.


1. On the left navigation bar on the cluster management page, select **Services and Ingresses** \> **Ingress**, and click **Create Ingress**. Use API Gateway to expose the model service externally in the cluster. The parameters mentioned below need to be configured as described. Other parameters can be configured by referring to the [Creating APIG Ingress through the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

   
   |Configuration item |Description |
   |---|---|
   |**Basic configuration** ||
   |Namespace |Select the namespace where the gpt\-oss\-120b\-vllm application template is deployed to associate the service exposed by the application. |
   |**Ingress configuration** ||
   |Ingress type |Select **Cloud\-native API gateway**. |
   |**APIG specification settings** ||
   |Gateway specifications |You can select **Automatically create**, or select **Use existing**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you use the API Gateway to expose the model service in the clusters, we recommend that you configure the following parameters or features (some parameters can only be configured in the APIG console, and cannot be configured in the VKE console):</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Instance specification</strong>: We recommend that you select <strong>4c8g</strong>, with two availability zones to realize high availability by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Bandwidth limit</strong>: This option is used to set the maximum bandwidth of the Classic Load Balancer (CLB) instance working with the APIG instance. If more bandwidth is required, you can specify a custom CLB instance on the <a href="https://console.byteplus.com/veapig">APIG console</a>. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Circuit breaking: </strong> When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Request timeout</strong>: Timeout is not applied to API Gateway by default. We recommend that you keep the default settings. You can configure a timeout setting in the <a href="https://console.byteplus.com/veapig">API Gateway</a> console. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy">Advanced routing policy</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Observability</strong>: By default, the alerting and logging capabilities are disabled for APIG instances that are created via the VKE console. You can enable logging and alerting in the <a href="https://console.byteplus.com/veapig">APIG console</a> to meet your requirements.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance monitoring</strong>: This feature helps you detect the issues of the entire system link from the perspective of the Ingress in a timely manner. For example, when the back end is unhealthy or crashes, the API Gateway reports error code <code>503</code> and error details.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip"><strong>Instance logs</strong>: You can view the request errors, request time consumption, and the allocation of requests in various Pods in the back end from the access logs.</div><br> |
   |Backend upstream |We recommend that you set the **Load balancing algorithm** parameter to **Round Robin**. It is more applicable to the scenarios of upgrading back\-ends if the back\-end loads are approximately balanced. |
   |**Listener configuration** ||
   |Protocol |Select a protocol as needed. If HTTPS is selected, you need to configure the certificate as described in the document [APIG Ingress](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console). |
   |**Forwarding configuration** ||
   |Domain name |Fill in the Ingress domain name to be exposed. The A (Address) record of this domain name needs to be configured later with the public or private IP address generated when the Ingress is successfully created. |
   |Service |Select the service that was named in the pattern `<application name>-api-svc` and associated with the application created based on the gpt\-oss\-120b\-vllm application template, and then set the port number to **8080**. |
   

2. (Optional) Configure APIG authentication.

   1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

   2. Create consumer: On the left navigation bar, select **Consumer management**, and click **Create consumer**.

   3. Generate an API\-KEY: In the consumer list, click the name of the target consumer, to enter the consumer details page. In the API Key information area, click **Generate API Key**.

   4. In the pop\-up dialog box, select **Automatically create**. 

   5. Click **Confirm** to generate API Key credentials.

   6. Enable Key Auth add\-on: In the left navigation bar, click **Plugin Center**. On the page that appears, select **Key Auth** and then click **Create Plugin**.

      1. **Effective level**: Select **Routing level** and configure the instance, service, and route to which the add\-on belongs.

      2. **Authentication configuration**: Select **header** and enter the text  **"Authorization"**  in the textbox on the right side to indicate that API Key will be included in the Authorization header of requests.

      3. **Consumer**: select the consumer created in Step 1.

      4. Other options can remain as default.

3. Obtain Ingress address.

   * **VIP**: includes both public and private IP addresses.

   * **Backend service**: includes the backend service name and access domain name.

4. Configure domain name resolution.

   * To test the DNS in the local environment, you can perform a domain\-to\-IP resolution.

   * In the production environment, configure the access domain name of Ingress among the domain name providers, and ensure the A record of the Ingress access domain name is configured with the public IP address or private IP address of Ingress.


<span id="0xWoZEIV"></span>
## Model verification

<span id="uJFHqVEY"></span>
### Method 1: Access through Service

After you deploy the gpt\-oss\-120b\-vllm application template, the created service whose name is in the format of `<application name>-api-svc` serves an HTTP API endpoint (port 8080). The endpoint can be called as you do with OpenAI APIs.

The sample code is as follows.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>******</code> in <code>http://******</code> with the endpoint of your <code><application name>-api-svc</code> service.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://******/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "/data/models/gpt-oss-120b",
    "messages": [
      {
        "role": "user",
        "content": "Who are you?"
      }
    ]
  }'
```


You can directly log in to the pod to perform API calls. To do that,  go to the **Helm details page** of the gpt\-oss\-120b\-vllm application, click the name of the associated Deployment in the **Workload ** section, and on the **Deployment list page** that opens, click **Console** in the top\-right corner to open the console where commands can be executed.

<span id="VJCPq5lj"></span>
### Method 2: Access via APIG

When enabling the authentication feature of the APIG, you need to add an authentication token in the request.

The following example is provided for reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>example.com</code> in the <code>http://example.com</code> with the Ingress backend service access domain name obtained in <strong>Step 2: Configure the Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>eyJhbGciOiJSUzI******</code> with the API Key generated in <strong>Step 2: Configure the Ingress</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The parameter <code>content</code> is what you want to type to chat with LLMs.</div>



```Bash
curl http://example.com/v1/chat/completions -X POST  \
  -H "Content-Type: application/json"  \
  -H "Authorization: Bearer eyJhbGciOiJSUzI******" \
  -d '{
    "model": "/data/models/gpt-oss-120b",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "Who won the world series in 2020?"}
        ]
    }'
```
