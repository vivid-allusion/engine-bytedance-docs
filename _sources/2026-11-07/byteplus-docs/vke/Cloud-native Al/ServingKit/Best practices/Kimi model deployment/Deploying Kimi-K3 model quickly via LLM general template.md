---
title: "Deploying Kimi-K3 model quickly via LLM general template"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deploying_Kimi-K3_model_quickly_via_LLM_general_template"
---

This topic describes how to deploy the Kimi\-K3 model in a VKE cluster using the ServingKit LLM general template.

<span id="8UFaGNuL"></span>
## Background

Kimi K3 is an open\-source multimodal LLM released by Moonshot AI, and it is also the first open\-source model in the world to exceed the 3T\-parameter landmark. The model is built on the KDA architecture and attention residual (AttnRes) structure, with 2.8T parameters, native visual understanding, and a million\-token ultra\-long context window. Kimi K3 is designed for long\-horizon programming, complex reasoning, and deep knowledge work, and performs excellently across evaluations in multiple domains. This topic describes how to quickly deploy the Kimi\-K3 model on a Kubernetes cluster using the [LLM general template](https://docs.byteplus.com/en/docs/vke/Deploying_general-purpose_LLM_template_applications).

<span id="Z2iPUu9f"></span>
## Notes


* To ensure successful deployment, which involves multiple interdependent add\-ons and various configurations, you need to precisely follow the instructions in this document.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to use a different solution, contact your BytePlus account manager for assistance.

* Do not use mGPU to partition GPU resources.


<span id="H3gPvtkH"></span>
## Preparation


* Some resources of BytePlus at the beta stage are required to deploy AI services. To use the following resources, contact your account manager.

   
   |Beta resource |Related service |Description |
   |---|---|---|
   |hpcpni3ln HPC\-optimized instance |[GPU Cloud Computing](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. When deploying Kimi\-K3, we recommend requesting 4 GPU instances of the `ecs.hpcpni3ln.45xlarge` type. |
   

* In this example, APIG is used to expose the service. Therefore, you need to prepare an APIG instance. You can create an APIG instance in advance, use an existing APIG instance, or leverage automatic instance creation during application deployment on ServingKit.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you create an APIG instance in advance or use an existing one, ensure that the <strong>region</strong> of the instance matches the <strong>region</strong> of the VKE cluster. We recommend an instance with both <strong>Public network</strong> and <strong>Private network</strong> selected for <strong>Network type</strong>. For details about creating APIG instances, see <a href="https://docs.byteplus.com/en/docs/apig/Creating_an_instance">Creating instances</a>.   </div>
   

* You need to create a high\-performance compute (HPC) cluster to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The HPC cluster must be deployed in the same <strong>region and availability zone</strong> as the VKE cluster.<strong></strong>   </div>
   

<span id="bYFvptbO"></span>
## Procedure

<span id="UJc5HCVD"></span>
### Step 1: Create a VKE heterogeneous computing cluster

Quickly create a heterogeneous computing cluster by using a VKE cluster template. Take note of the parameter configurations listed in the following table. For more details, see [Using a cluster template to create managed clusters for heterogeneous computing](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster).


|Parameter |Description |
|---|---|
|**Cluster and node pool configuration** ||
|Region |The **Region** and **Availability zone** of the cluster must be consistent with those of the prepared HPC cluster.<br><br>You can switch regions in the top navigation bar. |
|Availability zone ||
|Instance type |Select the `ecs.hpcpni3ln.45xlarge` specification of the **High Performance Computing Optimized** type. |
|Number of nodes |Set it to **4**. |
|**Advanced settings** ||
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: Select **1024 GiB** and retain the default performance level **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>/data01</code> directory is required by subsequent steps and must not be changed or customized.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the physical host fails or the local disk is damaged, data loss may occur. Do not store data that must be retained long\-term on the local disk, and make sure <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backups</a> are in place.   </div><br>    |


<span id="3Q81qiuj"></span>
### Step 2: Deploy Kimi\-K3


1. Download and deploy the model using the **LLM General Template** provided by ServingKit. During deployment, take note of the parameter configurations listed in the following table. For descriptions of other parameters and detailed procedures, see [Deploying general-purpose LLM template applications](https://docs.byteplus.com/en/docs/vke/Deploying_general-purpose_LLM_template_applications).

   
   |**Parameter** |**Description** |
   |---|---|
   |**Select framework and orchestration** ||
   |Image |Select **Predefined**, then in the **Advanced filter** drop\-down list, select **POC** and **SGLang**, find the `v0.5.16.iaas.202607280000-kimi-k3-cu130` image, and select the image. |
   |Model configuration |* **StorageClass type**: Select **Data volume**.<br><br>* **Select models**: Click **Add predefined model**, select **Kimi\-K3** and **Kimi\-K3\-DSpark** models, and configure the **Mount path** as `/data01` and the **Container mounting path** as `/data/models`. The model data will be downloaded to the `/data01` directory. |
   |Inference mode |Select **PD co\-location**. |
   |Instance specification |* **Number of instances**: Set the value to **1**.<br><br>* Set **Single instance GPUs** to **32**. |
   |Resource configuration |Select the VKE heterogeneous computing cluster created in **Step 1** and the node pool containing nodes with the `ecs.hpcpni3ln.45xlarge` specification in the cluster. |
   |Start command |Add the following startup command. For a detailed description of each field in the startup command, see the "Startup command descriptions" table below.<br><br>```Bash```<br>```source /workspace/nccl_env.sh && GLOO_SOCKET_IFNAME=eth0 NCCL_MIN_NCHANNELS=24 NCCL_IB_QPS_PER_CONNECTION=8 NCCL_CUMEM_ENABLE=1 PYTORCH_CUDA_ALLOC_CONF=expandable_segments:True SGLANG_ENABLE_TP_MEMORY_INBALANCE_CHECK=0 SGLANG_K3_ATTN_RES_MODE=jit SGLANG_MOE_FUSED_GATE_RADIX=1 sglang serve --trust-remote-code \```<br>``` --model-path /data/models/Kimi-K3 \```<br>``` --served-model-name kimi-k3 \```<br>``` --tp-size 32 \```<br>``` --nnodes 4 \```<br>``` --node-rank $POD_GROUP_INDEX \```<br>``` --dist-init-addr "${ROLESET_NAME}-${ROLE_NAME}-${ROLE_TEMPLATE_HASH}-${ROLE_REPLICA_INDEX}-0.${STORM_SERVICE_NAME}:20000" \```<br>``` --ep-size 32 \```<br>``` --moe-runner-backend marlin \```<br>``` --decode-attention-backend flashmla \```<br>``` --mem-fraction-static 0.85 \```<br>``` --mamba-radix-cache-strategy extra_buffer_lazy \```<br>``` --dist-timeout 3600 \```<br>``` --reasoning-parser kimi_k3 \```<br>``` --tool-call-parser kimi_k3 \```<br>``` --mamba-full-memory-ratio 0.8 \```<br>``` --host 0.0.0.0 \```<br>``` --port 8080 \```<br>``` --speculative-algorithm DSPARK \```<br>``` --speculative-draft-model-path /data/models/Kimi-K3-DSpark \```<br>``` --speculative-dspark-block-size 7 \```<br>``` --enable-linear-replayssm-spec \```<br>``` --cuda-graph-max-bs 128 \```<br>``` --max-running-requests 128 \```<br>``` --enable-metrics \```<br>``` --enable-cache-report \```<br>``` --show-time-cost```<br><br><br>Set the **port** to **8080**. |
   |API Gateway |Select **Enable** and associate the prepared APIG instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also select <strong>Automatically create</strong> to have an automatically created APIG instance with a fixed instance specification and configuration specified by ServingKit. Creating an APIG instance will incur fees. For details, see <a href="https://docs.byteplus.com/en/docs/6569/185249">APIG billing</a>.</div><br> |
   

   **Startup command descriptions**

   
   |Parameter |Type |Description |Sample value |
   |---|---|---|---|
   |sglang serve |Startup command |Start the model service backend via the SGLang CLI.<br><br>This field is a command entry instead of a parameter. |None |
   |\-\-model |Path/Model ID |The loaded LLM model. You can set this field to the following values:<br><br><br>* Hugging Face model ID<br><br>* Local model path |/data/models/Kimi\-K3 |
   |\-\-tp\-size |Integer |Configure tensor parallelism. |32 |
   |\-\-nnodes |Integer |Specify the total number of nodes in the distributed cluster. |4 |
   |\-\-node\-rank |Integer |Specify the current node's index in the cluster, starting from `0`. |0 |
   |\-\-dist\-init\-addr |IP: Port |The initialization address (manager node address) of the distributed cluster, which is used for multi\-node communication synchronization. |Variable injection |
   |\-\-ep\-size |Integer |Configure expert parallelism. |32 |
   |\-\-host |IP address |The host address bound to the service. |0.0.0.0 |
   |\-\-port |Integer |The port number that the service listens on, which is used to connect to the client. |8000 |
   |\-\-mem\-fraction\-static |Float |Restricts the static GPU memory ratio, leaving more room for the runtime workspace. |0.85 |
   |\-\-cuda\-graph\-max\-bs |Integer |Used to set the maximum batch size for CUDA Graph, reducing batch GPU memory pressure during capture and replay. |128 |
   |\-\-max\-running\-requests |Integer |Limit the maximum number of concurrent requests being processed at the same time. |128 |
   |\-\-enable\-metrics |Command |Collect basic observability metrics. For detailed metric descriptions, see [SGLang documentation](https://docs.sglang.io/references/production_metrics.html). |None |
   

2. After successful application deployment, model startup time varies depending on model size. After the application status changes to **Running**, view the **logs** of the corresponding instance on the **Application details** page. If the log contains the following message: `The server is fired up and ready to roll!`, the model in the application has started successfully and is accessible.


<span id="7wD8unq3"></span>
### Step 3: Access the service

After successfully deploying the Kimi\-K3 model service, obtain the service domain name and access the service.


1. Obtain the Kimi\-K3 model service domain name.

   1. In the [VKE console](https://console.byteplus.com/vke), go to **ServingKit** \> **List of AI applications** and find the deployed Kimi\-K3 model applications.

   2. Click the  **→**  icon in the application section to go to the application details page and view **Service domain names**.

2. On a terminal where the `curl` command is available, execute the following command to access the Kimi\-K3 model service.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>${your_service_domain_name}</code> with the <strong>service domain name</strong> obtained in the previous step.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no terminal is available, you can log in to the node where the model is deployed by using the ECS Terminal method and use the <code>curl</code> command to access the service. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal">ECS Terminal</a>.   </div>
   

   ```Bash
   curl -X POST http://${your_service_domain_name}/v1/chat/completions \
     -H "Content-Type: application/json" \
     -d '{
       "model": "Kimi-K3",
       "messages": [
         {"role": "system", "content": "You are a helpful assistant."},
         {"role": "user", "content": "help me write a random generator in python"}
       ]
     }'
   ```
   

   The descriptions of parameters are as follows:

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |model |The model to use. |Kimi\-K3 |
   |messages |The message list of the conversation.<br><br><br>* role: The role that initiates the message.<br><br>* content: The content of the message. |None |
   

   The following figure displays the expected response after you run the command.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64d8f7a6f8850d094469893808d3bd7a.png) </span>


<span id="ymATTz7y"></span>
## Subsequent operations

<span id="G5aBF1Qd"></span>
### Enhance service security

You can enhance the security of the Kimi\-K3 service by using the API Gateway's API Key.


1. Create a consumer for the APIG instance. For detailed operations, see [Creating consumers](https://docs.byteplus.com/en/docs/apig/Creating_a_consumer).

2. Generate the Key Auth plugin credential based on the consumer. For detailed operations, see [Generating credentials](https://docs.byteplus.com/en/docs/apig/Generating_credentials).

3. Enable the Key Auth plugin: In the left navigation bar, click **Plugin Center**. On the page that appears, click Key Auth in the Plugin Category section and then click **Create Plugin**. Specify the parameters of the plugin.

   1. **Effective level**: Select **Routing level**, and specify the instance, service, and route to which the plugin belongs.

   2. **Authentication configuration**: Select **header**, and specify **Authorization** as the source, which indicates that the API Key is carried in the Authorization header of the request.

   3. **Consumer**: Select the consumer created in Step 1 or select all, which indicates that the configuration also applies to newly created consumers.

   4. Keep the default values for other parameters.

4. After you enable Key Auth plugin authentication, when you access the service by executing the corresponding command, credentials must be included. Otherwise, a message that indicates insufficient permissions will be returned.

   ```Bash
   curl http://${your_service_domain_name}/v1/chat/completions -X POST  \
     -H "Content-Type: application/json"  \
     -H "Authorization: Bearer ${your_api_key}" \
     -d '{
       "model": "Kimi-K3",
       "messages": [
           {
               "role": "user",
               "content": "help me write a random generator in python"
           }
       ],
       "max_tokens": 500,
       "temperature": 0.7
   }'
   ```
   


<span id="HY1o7B7P"></span>
### Enabling observability

ServingKit AI applications support basic cloud\-native observability capabilities by default. You can view the application monitoring dashboard on the AI application details page.


1. In the [VKE console](https://console.byteplus.com/vke), go to **ServingKit** \> **List of AI applications** and find the deployed Kimi\-K3 model applications.

2. Click the  **→**  icon in the application section to go to the application details page and view the dashboard on the **Observability** tab.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not enabled the observability capability of the relevant cluster, enable observability based on the prompts in the console. For operations related to cloud\-native observability capabilities, see <a href="https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability">Enabling observability</a> and <a href="https://docs.byteplus.com/en/docs/vke/VKE-observability">VKE observability</a>.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1db71be2af7ea44833b7de81cf75e17c.png) </span>
