---
title: "Quickly deploying GLM-5.2 by using the LLM General Template"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly-deploying-GLM-5-2-by-using-the-LLM-General-Template"
---

This topic describes how to quickly deploy the GLM\-5.2 model in a VKE cluster by using the ServingKit LLM General Template.

<span id="22xXb8xi"></span>
## Background

GLM\-5.2\-FP8 is an FP8\-quantized version of the open\-source MoE LLM. It supports a 1M context window, with approximately 753B total parameters and approximately 40B active parameters during inference. This model is optimized for long\-context processing, code generation, complex inference, and agent scenarios. This FP8\-quantized version reduces inference memory usage and is suitable for high\-performance deployments and local inference environments.

<span id="VyAto2xw"></span>
## Notes


* To ensure successful deployment, which involves multiple interdependent add\-ons and various configurations, you need to precisely follow the instructions in this document.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to use a different solution, contact your BytePlus account manager for assistance.

* Do not use mGPU to partition GPU resources.


<span id="2sjUAMVL"></span>
## Preparation


* Some resources of BytePlus at the beta stage are required to deploy AI services. To use the following resources, contact your account manager.

   
   |Beta resource |Related service |Description |
   |---|---|---|
   |hpcpni3ln HPC\-optimized instance |[GPU Cloud Computing](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. When you deploy the GLM\-5.2 model, we recommend requesting two `ecs.hpcpni3ln.45xlarge` GPU instances. |
   

* In this example, APIG is used to expose the service. Therefore, you need to prepare an APIG instance. You can create an APIG instance in advance, use an existing APIG instance, or leverage automatic instance creation during application deployment on ServingKit.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you create an APIG instance in advance or use an existing one, ensure that the <strong>region</strong> of the instance matches the <strong>region</strong> of the VKE cluster. We recommend an instance with both <strong>Public network</strong> and <strong>Private network</strong> selected for <strong>Network type</strong>. For details about creating APIG instances, see <a href="https://docs.byteplus.com/en/docs/apig/Creating_an_instance">Creating instances</a>.   </div>
   

* You need to create a high\-performance compute (HPC) cluster to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The HPC cluster must be deployed in the same <strong>region and availability zone</strong> as the VKE cluster.<strong></strong>   </div>
   

<span id="hB97YZBR"></span>
## Procedure

<span id="ekj7T4Py"></span>
### Step 1: Create a VKE heterogeneous computing cluster

Quickly create a heterogeneous computing cluster by using a VKE cluster template. Take note of the parameter configurations listed in the following table. For more details, see [Using a cluster template to create managed clusters for heterogeneous computing](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster).


|Parameter |Description |
|---|---|
|**Cluster and node pool configuration** ||
|Region |The **Region** and **Availability zone** of the cluster must be consistent with those of the prepared HPC cluster.<br><br>You can switch regions in the top navigation bar. |
|Availability zone ||
|Instance type |Select the `ecs.hpcpni3ln.45xlarge` specification of the **High Performance Computing Optimized** type. |
|Number of nodes |Set the value to **2**. |
|**Advanced settings** ||
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: Select **1024 GiB** and retain the default performance level **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>The /data01</code> directory is required by subsequent steps and must not be changed or customized.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the physical host fails or the local disk is damaged, data loss may occur. Do not store data that must be retained long\-term on the local disk, and make sure <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backups</a> are in place.   </div><br>    |


<span id="CFmVblzR"></span>
### Step 2: Deploy GLM\-5.2


1. Download and deploy the GLM\-5.2 model using the **LLM General Template** provided by ServingKit. During deployment, take note of the parameter configurations listed in the following table. For descriptions of other parameters and detailed procedures, see [Deploying general-purpose LLM template applications](https://docs.byteplus.com/en/docs/vke/Deploying_general-purpose_LLM_template_applications).

   
   |**Parameter** |**Description** |
   |---|---|
   |**Select framework and orchestration** ||
   |Image |Select **Custom** and select an appropriate image from the following image addresses based on the region where your business is deployed.<br><br><br>* China (Beijing): `ai-containers-cn-beijing.cr.volces.com/deeplearning/sglang:v0.5.13.post1.iaas.dev.202606172008`<br><br>* China (Shanghai): `ai-containers-cn-shanghai.cr.volces.com/deeplearning/sglang:v0.5.13.post1.iaas.dev.202606172008`<br><br>* Asia Pacific (Johor): `ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:v0.5.13.post1.iaas.dev.202606172008` |
   |Model configuration |* **StorageClass type**: Select **Data volume**.<br><br>* **Select Models**: Click **Add predefined model**, select the **GLM\-5.2\-FP8** model, and set **Mount path** to `/data01` and **Container mounting path** to `/data/models`. The path settings specify that the model data will be downloaded to the `/data01` directory. |
   |Inference mode |Select **PD co\-location**. |
   |Instance specification |* **Number of instances**: Set the value to **1**.<br><br>* **Single instance GPUs**: Set the value to **16**. |
   |Resource configuration |Select the VKE heterogeneous computing cluster created in **Step 1** and the node pool containing nodes with the `ecs.hpcpni3ln.45xlarge` specification in the cluster. |
   |Startup command |Add the following startup command. For a detailed description of each field in the startup command, see the "Startup command descriptions" table below.<br><br>```Bash```<br>```source /workspace/nccl_env.sh && cd /sgl-workspace/sglang && GLOO_SOCKET_IFNAME=eth0 MODEL_LENGTH=262144 NCCL_MIN_NCHANNELS=24 NCCL_IB_QPS_PER_CONNECTION=8 CUDA_CACHE_MAXSIZE=2147483648 SGLANG_ENABLE_SPEC_V2=1 sglang serve --model-path /data/models/GLM-5.2-FP8/ --served-model-name glm-5.2 --host 0.0.0.0 --port 8000 --trust-remote-code --tp 16 --nnodes 2 --node-rank $POD_GROUP_INDEX --dist-init-addr ${ROLESET_NAME}-${ROLE_NAME}-${ROLE_TEMPLATE_HASH}-${ROLE_REPLICA_INDEX}-0.${STORM_SERVICE_NAME}:20000 --chunked-prefill-size 32768 --enable-metrics --enable-cache-report --show-time-cost --reasoning-parser glm45 --tool-call-parser glm47 --speculative-algorithm EAGLE --speculative-num-steps 3 --speculative-eagle-topk 1 --speculative-num-draft-tokens 4 --cuda-graph-max-bs 8 --mem-fraction-static 0.82 --enable-metrics-for-all-schedulers```<br><br><br>Set **Port number** to **8000**. |
   |API Gateway |Select **Enable** and associate the prepared APIG instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also select <strong>Automatically create</strong> to have an automatically created APIG instance with a fixed instance specification and configuration specified by ServingKit. Creating an APIG instance will incur fees. For details, see <a href="https://docs.byteplus.com/en/docs/6569/185249">APIG billing</a>.</div><br> |
   

   **Startup command descriptions**

   
   |Parameter |Type |Description |Sample value |
   |---|---|---|---|
   |sglang serve |Startup command |The entry point of the SGLang service.<br><br>This field is a command entry instead of a parameter. |None |
   |\-\-model\-path |Path/Model ID |The LLM to load, that is, the mount path inside the container. Available values include:<br><br><br>* Hugging Face model ID<br><br>* Local model path |/data/models/GLM\-5.2\-FP8/<br><br> |
   |\-\-tp |Integer |Configure tensor parallelism. Default value: 16. |16 |
   |\-\-host |IP address |The host address bound to the service. |0.0.0.0 |
   |\-\-port |Integer |The port number that the service listens on, which is used to connect to the client. |8000 |
   |\-\-dist\-init\-addr |IP: Port |The initialization address (manager node address) of the distributed cluster, which is used for multi\-node communication synchronization. |Variable injection |
   |\-\-nnodes |Integer |The total number of nodes in the distributed cluster, which is the number of servers participating in the service. |2 |
   |\-\-enable\-metrics |Command |Collect basic observability metrics. For detailed metric descriptions, see [SGLang documentation](https://docs.sglang.io/references/production_metrics.html). |None |
   

2. After successful application deployment, model startup time varies depending on model size. After the application status changes to **Running**, view the **logs** of the corresponding instance on the **Application details** page. If the log contains the following message: `The server is fired up and ready to roll!`, the model in the application has started successfully and is accessible.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44978e9607e12747b7e981d8af478e46.png) </span>


<span id="hV20p39Q"></span>
### Step 3: Access the service

After successfully deploying the GLM\-5.2 model service, obtain its service domain name and access the service.


1. Obtain the domain name of the GLM\-5.2 model service.

   1. In the left navigation pane of the [VKE console](https://console.byteplus.com/vke), click **ServingKit** \> **List of AI applications**. On the page that appears, find the deployed GLM\-5.2 model application.

   2. Click the  **→**  icon in the application section to go to the application details page and view **Service domain names**.

2. In a terminal where the `curl` command is available, run the following command to access the GLM\-5.2 model service.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>${your_service_domain_name}</code> with the <strong>service domain name</strong> obtained in the previous step.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no terminal is available, you can log in to the node where the model is deployed by using the ECS Terminal method and use the <code>curl</code> command to access the service. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal">ECS Terminal</a>.   </div>
   

   ```Bash
   curl -X POST http://${your_service_domain_name}/v1/chat/completions \
     -H "Content-Type: application/json" \
     -d '{
       "model": "GLM-5.2-FP8",
       "messages": [
         {
           "role": "user",
           "content": "Where is the 2026 FIFA World Cup being held?"
         }
       ],
       "max_tokens": 500,
       "temperature": 0.7
     }'
   ```
   

   The descriptions of parameters are as follows:

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |model |The model to use. |GLM\-5.2\-FP8 |
   |messages |The message list of the conversation.<br><br><br>* role: The role that initiates the message.<br><br>* content: The content of the message. |None |
   |max_tokens |Specify the maximum number of tokens generated by the model for completion in a single request.<br><br><br>* Valid values: 1 to 8192. The value must be an integer.<br><br>* Default value: 4096. |500 |
   |temperature |The sampling temperature.<br><br><br>* Valid values: 0 to 2.<br><br>* A higher temperature (such as 1) results in more random output.<br><br>* A lower temperature (such as 0.2) results in more focused and deterministic output. |0.7 |
   

   The following figure displays the expected response after you run the command.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_378520bdb302185a4a160fb1a6a95f3b.png) </span>


<span id="XzlJ2FVC"></span>
## Subsequent operations

<span id="iSgW95gO"></span>
### Enhance service security

You can enhance the security of the GLM\-5.2 service by using the API Key of APIG.


1. Create a consumer for the APIG instance. For detailed operations, see [Creating consumers](https://docs.byteplus.com/en/docs/apig/Creating_a_consumer).

2. Generate the Key Auth plugin credential based on the consumer. For detailed operations, see [Generating credentials](https://docs.byteplus.com/en/docs/apig/Generating_credentials).

3. Enable the Key Auth plugin: In the left navigation bar, click **Plugin Center**. On the page that appears, click Key Auth in the Plugin Category section and then click **Create Plugin**. Specify the parameters of the plugin.

   1. **Effective level**: Select **Routing level**, and specify the instance, service, and route to which the plugin belongs.

   2. **Authentication configuration**: Select **header**, and specify **Authorization** as the source, which indicates that the API Key is carried in the Authorization header of the request.

   3. **Consumer**: Select the consumer created in Step 1 or select all, which indicates that the configuration also applies to newly created consumers.

   4. Keep the default values for other parameters.

4. After you enable Key Auth plugin authentication, when you access the service by executing the corresponding command, credentials must be included. Otherwise, a message that indicates insufficient permissions will be returned.

   ```Bash
   curl http://example.com/v1/chat/completions -X POST  \
     -H "Content-Type: application/json"  \
     -H "Authorization: Bearer ${your_api_key}" \
     -d '{
       "model": "GLM-5.2-FP8",
       "messages": [
           {
               "role": "user",
               "content": "Where is the 2026 FIFA World Cup being held?"
           }
       ],
       "max_tokens": 500,
       "temperature": 0.7
   }'
   ```
   


<span id="4quIipkl"></span>
### Enabling observability

ServingKit AI applications support basic cloud\-native observability capabilities by default. You can view the application monitoring dashboard on the AI application details page.


1. Click **ServingKit** \> **List of AI applications** in the left navigation bar of the [VKE console](https://console.byteplus.com/vke). On the page that appears, find the deployed GLM model application.

2. Click the  **→**  icon in the application section to go to the application details page and view the dashboard on the **Observability** tab.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not enabled the observability capability of the relevant cluster, enable observability based on the prompts in the console. For operations related to cloud\-native observability capabilities, see <a href="https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability">Enabling observability</a> and <a href="https://docs.byteplus.com/en/docs/vke/VKE-observability">VKE observability</a>.   </div>
