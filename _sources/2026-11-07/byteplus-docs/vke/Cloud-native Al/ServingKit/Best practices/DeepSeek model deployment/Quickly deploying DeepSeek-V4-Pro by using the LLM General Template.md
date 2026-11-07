---
title: "Quickly deploying DeepSeek-V4-Pro by using the LLM General Template"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_DeepSeek-V4-Pro_by_using_the_LLM_General_Template"
---

This topic describes how to quickly deploy the DeepSeek\-V4\-Pro model in a VKE cluster by using the ServingKit LLM general\-purpose template.

<span id="13vXGdlr"></span>
## Background

DeepSeek\-V4\-Pro is the flagship large language model in the DeepSeek\-V4 preview series, built on a ‌sparse Mixture\-of\-Experts (MoE)‌ architecture. It contains ‌1.6 trillion (1.6T) parameters‌, with approximately ‌49B parameters dynamically activated per forward inference‌, which significantly reduces single\-token inference costs while maintaining high performance. In its maximum reasoning intensity mode (‌DeepSeek\-V4\-Pro\-Max‌), the model surpasses all previously released open\-source models on evaluations in mathematics, STEM subjects, and competition\-level programming. It performs comparably to leading closed\-source models. This model is suitable for cutting\-edge tasks, including complex reasoning, in\-depth long\-document analysis, and multi\-step AI agent orchestration.

This topic describes how to quickly deploy the **DeepSeek\-V4\-Pro** model in a Kubernetes cluster by using the [LLM general-purpose template](https://docs.byteplus.com/en/docs/vke/Deploying_general-purpose_LLM_template_applications).

<span id="XUqh7Hhq"></span>
## Notes


* To ensure successful deployment, which involves multiple components depending on each other and a variety of configurations, you need to exactly follow the instructions in this document.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.


<span id="AXQMhLnk"></span>
## Preparation


* Some resources of BytePlus at the beta stage are required to deploy AI services. To use the following resources, contact your account manager.

   
   |Beta resource |Related service |Description |
   |---|---|---|
   |hpcpni3ln instance optimized for High\-Performance Computing based on GPU  |[GPU Compute Service](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. For DeepSeek\-V4\-Pro model deployment, we recommended applying for 2 `ecs.hpcpni3ln.45xlarge` GPU\-accelerated instance. |
   

* In this example, APIG is used to expose the service. Therefore, you need to prepare an APIG instance. You can create an APIG instance in advance, use an existing APIG instance, or leverage automatic instance creation during application deployment on ServingKit.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">If you tip   </div>
   

create an APIG instance in advance or use an existing one, ensure that the **region** of the instance matches the **region** of the VKE cluster. We recommend an instance with both **Public network** and **Private network** selected for **Network type**. For details about creating APIG instances, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).


* You need to create a high\-performance compute (HPC) cluster to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The HPC cluster must be deployed in the same <strong>region and availability zone</strong> as the VKE cluster.   </div>
   

<span id="Rrpms23t"></span>
## Procedure

<span id="rigRgn6s"></span>
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
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: set capacity to **1024 GiB** and the performance level to the default **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>data01</code> directory will be used as a dependency later and therefore cannot be modified.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure the data that needs long\-term storage has been <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backed up</a> properly in case of computer crashes or disk damage which causes data loss.   </div><br>    |


<span id="UwP3dKV4"></span>
### Step 2: Deploy DeepSeek\-V4\-Pro


1. Download and deploy the model using the **LLM General Template** provided by ServingKit. During deployment, take note of the parameter configurations listed in the following table. For descriptions of other parameters and detailed procedures, see [Deploying general-purpose LLM template applications](https://docs.byteplus.com/en/docs/vke/Deploying_general-purpose_LLM_template_applications).

   
   |**Parameter** |**Description** |
   |---|---|
   |**Select framework and orchestration** ||
   |Image |Select **Custom** and select an appropriate image from the following image addresses based on the region where your business is deployed.<br><br><br>* Asia Pacific (Johor): `ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:deepseek-v4-community-enhancements` |
   |Model configuration |* **StorageClass type**: Select **Data volume**.<br><br>* **Select Models**: Click **Add predefined model**, select the **DeepSeek\-V4\-Pro** model, and set **Mount path** to `/data01` and **Container mounting path** to `/data/models`. The path settings specify that the model data will be downloaded to the `/data01` directory. |
   |Inference mode |Select **PD co\-location**. |
   |Instance specification |* **Number of instances**: Set the value to **1**.<br><br>* **Single instance GPUs**: Set the value to **16**. |
   |Resource configuration |Select the VKE heterogeneous computing cluster created in **Step 1** and the node pool containing nodes with the `ecs.hpcpni3ln.45xlarge` specification in the cluster. |
   |Start command |Add the following startup command. For a detailed description of each field in the startup command, see the "Startup command descriptions" table below.<br><br>```Bash```<br>```source /workspace/nccl_env.sh && SGLANG_ENABLE_THINKING=1 SGLANG_DSV4_FP4_EXPERTS=1 SGLANG_JIT_DEEPGEMM_PRECOMPILE=0 GLOO_SOCKET_IFNAME=eth0 NCCL_MIN_NCHANNELS=24 NCCL_IB_QPS_PER_CONNECTION=8 sglang serve --trust-remote-code --model-path /data/models/DeepSeek-V4-Pro --tp 16 --dp-size 2 --enable-dp-attention --cuda-graph-max-bs 8 --max-running-requests 16 --enable-metrics --host 0.0.0.0 --port 8080 --mem-fraction-static 0.9 --moe-runner-backend marlin --dist-init-addr ${ROLESET_NAME}-${ROLE_NAME}-${ROLE_TEMPLATE_HASH}-${ROLE_REPLICA_INDEX}-0.${STORM_SERVICE_NAME}:30300 --nnodes 2 --node-rank $POD_GROUP_INDEX --tool-call-parser deepseekv4 --reasoning-parser deepseek-v4 --chunked-prefill-size 4096```<br><br><br>Set the **port** to 8080. |
   |API Gateway |Select **Enable** and associate the prepared APIG instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also select <strong>Automatically create</strong> to have an automatically created APIG instance with a fixed instance specification and configuration specified by ServingKit. Creating an APIG instance will incur fees. For details, see <a href="https://docs.byteplus.com/en/docs/6569/185249">APIG billing</a>.</div><br> |
   

   **Startup command descriptions**

   
   |Parameter |Type |Description |Sample value |
   |---|---|---|---|
   |\-\-trust\-remote\-code |Command |Custom code in the model repository that can be loaded and executed. |No |
   |\-\-nnodes |Integer |The total number of nodes in the distributed cluster (that is, the number of physical servers or Pods). |2 |
   |\-\-node\-rank |Integer |The index of the node in the cluster. Numbering starts from 0, with index 0 generally being the master node. |0 |
   |\-\-dist\-init\-addr |String |The initialization communication address for the multi\-node distributed cluster. All nodes connect to this address to establish the communication network. The format is `IP_address:Port`.<br><br><br>* IP_address: The private IP address of the master node.<br><br>* Port: The port number for communication between nodes. |192.168.0.1:30300 |
   |\-\-dp\-size |Integer |Data parallelism. |16 |
   |\-\-tp |Integer |Tensor parallelism. |16 |
   |\-\-mem\-fraction\-static |Float |The maximum node memory usage. The value range is 0 to 1. An excessively high value may cause OOM (Out Of Memory) or fragmentation, whereas an excessively low value reduces throughput. |0.95 |
   |\-\-max\-running\-requests |Integer |The maximum number of requests running in parallel in the inference engine. |16 |
   

2. After successful application deployment, model startup time varies depending on model size. After the application status changes to **Running**, view the **logs** of the corresponding instance on the **Application details** page. If the log contains the following message: `The server is fired up and ready to roll!`, the model in the application has started successfully and is accessible.


<span id="OLLmnm0s"></span>
### Step 3: Access the service

After the DeepSeek\-V4\-Pro model service is deployed, obtain the service domain name and access the service.


1. Obtain the domain name of the DeepSeek\-V4\-Pro model service.

   1. In the left navigation pane of the [VKE console](https://console.byteplus.com/vke), click **ServingKit** \> **List of AI applications**. On the page that appears, find the deployed DeepSeek\-V4\-Pro model application.

   2. Click the  **→**  icon in the application section to go to the application details page and view the **service domain name** on the **Service overview** tab.

2. In a terminal where the `curl` command is available, run the following command to access the DeepSeek\-V4\-Pro model service.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">In tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>${your_service_domain_name}</code> with the <strong>service domain name</strong> obtained in the previous step.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no terminal is available, you can log in to the node where the model is deployed by using the ECS Terminal method and use the <code>curl</code> command to access the service. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal">ECS Terminal</a>.   </div>
   

   ```Bash
   curl -X POST http://${your_service_domain_name}/v1/chat/completions \
     -H "Content-Type: application/json" \
     -d '{
       "model": "/data/models/DeepSeek-V4-Pro",
       "messages": [
         {
           "role": "user",
           "content": "Who won the world series in 2020?"
         }
       ],
       "max_tokens": 500,
       "temperature": 0.7
     }'
   ```
   

   The descriptions of parameters are as follows:

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |model |The used model. |/data/models/DeepSeek\-V4\-Pro |
   |messages |The message list of the conversation.<br><br><br>* role: The role that initiates the message.<br><br>* content: The content of the message. |No |
   |max_tokens |Specify the maximum number of tokens generated by the model for completion in a single request.<br><br><br>* Valid values: 1 to 8192. The value must be an integer.<br><br>* Default value: 4096. |500 |
   |temperature |The sampling temperature.<br><br><br>* Valid values: 0 to 2.<br><br>* A higher temperature (such as 1) results in more random output.<br><br>* A lower temperature (such as 0.2) results in more focused and deterministic output. |0.7 |
   

   The following figure displays the expected response after you run the command.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0cc219d6c9fe71f6f94edd93e4001162.png) </span>


<span id="twuKyXp2"></span>
## Subsequent operations

<span id="iuNrqRAH"></span>
### Enhance service security

You can use the API key of APIG to enhance the security of the DeepSeek\-V4\-Pro service.


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
       "model": "/data/models/DeepSeek-V4-Pro",
       "messages": [
           {
               "role": "user",
               "content": "Who won the world series in 2020?"
           }
       ],
       "max_tokens": 500,
       "temperature": 0.7
   }'
   ```
   


<span id="uxvmJBUH"></span>
### Enabling observability

ServingKit AI applications support basic cloud\-native observability capabilities by default. You can view the application monitoring dashboard on the AI application details page.


1. In the left navigation pane of the [VKE console](https://console.byteplus.com/vke), click **ServingKit** \> **List of AI applications**. On the page that appears, find the deployed DeepSeek\-V4\-Pro model application.

2. Click the  **→**  icon in the application section to go to the application details page and view the dashboard on the **Observability** tab.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not enabled the observability capability of the relevant cluster, enable observability based on the prompts in the console. For operations related to cloud\-native observability capabilities, see <a href="https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability">Enabling observability</a> and <a href="https://docs.byteplus.com/en/docs/vke/VKE-observability">VKE observability</a>.   </div>
