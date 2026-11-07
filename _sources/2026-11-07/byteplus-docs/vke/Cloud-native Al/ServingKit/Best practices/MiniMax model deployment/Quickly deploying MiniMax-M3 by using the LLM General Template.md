---
title: "Quickly deploying MiniMax-M3 by using the LLM General Template"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Quickly_deploying_MiniMax-M3_by_using_the_LLM_General_Template"
---

This topic describes how to quickly deploy the MiniMax\-M3 model in a VKE cluster by using the ServingKit LLM General Template.

<span id="ZFXRREHJ"></span>
## Background

MiniMax\-M3 is a natively multimodal large model open\-sourced by MiniMax. It supports a 1M context window, with approximately 428B total parameters and 23B active parameters during inference. This model is a large\-scale open model designed for long\-context processing, multimodal tasks, coding, and agent scenarios. This topic describes how to quickly deploy the MiniMax\-M3 model in a Kubernetes cluster by using the [LLM General Template](https://docs.byteplus.com/en/docs/vke/Deploying_general-purpose_LLM_template_applications).

<span id="GPVdGBWD"></span>
## Notes


* To ensure successful deployment, which involves multiple interdependent add\-ons and various configurations, you need to precisely follow the instructions in this document.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of VKE, you need to perform operations by following the solution described in this article or on the recommended resources. If you need to use a different solution, contact your BytePlus account manager for assistance.

* Do not use mGPU to partition GPU resources.


<span id="B48KlghQ"></span>
## Preparation


* Some resources of BytePlus at the beta stage are required to deploy AI services. To use the following resources, contact your account manager.

   
   |Beta resource |Related service |Description |
   |---|---|---|
   |hpcpni3ln HPC\-optimized instance |[GPU Cloud Computing](https://www.byteplus.com/en/product/gpu) |The HPC instance, providing computing power. When you deploy the MiniMax\-M3 model, we recommend requesting two `ecs.hpcpni3ln.45xlarge` GPU instances. |
   

* In this example, APIG is used to expose the service. Therefore, you need to prepare an APIG instance. You can create an APIG instance in advance, use an existing APIG instance, or leverage automatic instance creation during application deployment on ServingKit.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you create an APIG instance in advance or use an existing one, ensure that the <strong>region</strong> of the instance matches the <strong>region</strong> of the VKE cluster. We recommend an instance with both <strong>Public network</strong> and <strong>Private network</strong> selected for <strong>Network type</strong>. For details about creating APIG instances, see <a href="https://docs.byteplus.com/en/docs/apig/Creating_an_instance">Creating instances</a>.   </div>
   

* You need to create a high\-performance compute (HPC) cluster to achieve logical isolation of HPC GPU instances (compute nodes). Instances in the same cluster are interconnected by Remote Direct Memory Access (RDMA) networks. For details, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The HPC cluster must be deployed in the same <strong>region and availability zone</strong> as the VKE cluster.<strong></strong>   </div>
   

<span id="TBJcoh22"></span>
## Procedure

<span id="vIy3lyzG"></span>
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
|Data volume |Configure the following two data volumes:<br><br><br>* **ESSD**: Select **1024 GiB** and retain the default performance level **PL0**.<br><br>* **Local SSD**: Specify `/data01` as the mount directory.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <code>/data01</code> directory is required by subsequent steps and must not be changed or customized.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the physical host fails or the local disk is damaged, data loss may occur. Do not store data that must be retained long\-term on the local disk, and make sure <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">backups</a> are in place.   </div><br>    |


<span id="8Ds3Mutg"></span>
### Step 2: Deploy MiniMax\-M3


1. Download and deploy the model using the **LLM General Template** provided by ServingKit. During deployment, take note of the parameter configurations listed in the following table. For descriptions of other parameters and detailed procedures, see [Deploying general-purpose LLM template applications](https://docs.byteplus.com/en/docs/vke/Deploying_general-purpose_LLM_template_applications).

   
   |**Parameter** |**Description** |
   |---|---|
   |**Select framework and orchestration** ||
   |Image |Select **Custom** and select an appropriate image from the following image addresses based on the region where your business is deployed.<br><br><br>* China (Beijing): `ai-containers-cn-beijing.cr.volces.com/deeplearning/sglang:v0.5.13.byted.202606170000`<br><br>* China (Shanghai): `ai-containers-cn-shanghai.cr.volces.com/deeplearning/sglang:v0.5.13.byted.202606170000`<br><br>* Asia Pacific (Johor): `ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:v0.5.13.byted.202606170000` |
   |Inference engine |Select **sglang**. |
   |Model configuration |* **StorageClass type**: Select **Data volume**.<br><br>* **Select Models**: Click **Add predefined model**, select the **MiniMax\-M3** model, and set **Mount path** to `/data01` and **Container mounting path** to `/data/models`. The path settings specify that the model data will be downloaded to the `/data01` directory. |
   |Inference mode |Select **PD co\-location**. |
   |Instance specification |* **Number of instances**: Set the value to **1**.<br><br>* **Single instance GPUs**: Set the value to **16**. |
   |Resource configuration |Select the VKE heterogeneous computing cluster created in **Step 1** and the node pool containing nodes with the `ecs.hpcpni3ln.45xlarge` specification in the cluster. |
   |Start command |Add the following startup command. For a detailed description of each field in the startup command, see the "Startup command descriptions" table below.<br><br>```Bash```<br>```GLOO_SOCKET_IFNAME=eth0 NCCL_MIN_NCHANNELS=24 NCCL_IB_QPS_PER_CONNECTION=8 python -m sglang.launch_server --model-path /data/models/MiniMax-M3 --tp-size 4 --ep-size 4 --tool-call-parser minimax-m2 --reasoning-parser minimax-append-think --trust-remote-code --host 0.0.0.0 --port 8000 --mem-fraction-static 0.8 --enable-metrics```<br><br><br>Set **Port number** to **8000**. |
   |API Gateway |Select **Enable** and associate the prepared APIG instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also select <strong>Automatically create</strong> to have an automatically created APIG instance with a fixed instance specification and configuration specified by ServingKit. Creating an APIG instance will incur fees. For details, see <a href="https://docs.byteplus.com/en/docs/6569/185249">APIG billing</a>.</div><br> |
   

   **Startup command descriptions**

   
   |Parameter |Type |Description |Sample value |
   |---|---|---|---|
   |python \-m sglang.launch_server |Startup command |Start the SGLang model server by using the Python method.<br><br>This field is a command entry instead of a parameter. |None |
   |\-\-model |Path/Model ID |The loaded LLM model. You can set this field to the following values:<br><br><br>* Hugging Face model ID<br><br>* Local model path | /data/models/MiniMax\-M3/<br><br> |
   |\-\-tp |Integer |Configure tensor parallelism. |4 |
   |\-\-ep |Integer |Configure expert parallelism. |4 |
   |\-\-host |IP address |The host address bound to the service. |0.0.0.0 |
   |\-\-port |Integer |The port number that the service listens on, which is used to connect to the client. |8000 |
   |\-\-enable\-metrics |Command |Collect basic observability metrics. For detailed metric descriptions, see [SGLang documentation](https://docs.sglang.io/references/production_metrics.html). |None |
   

2. After successful application deployment, model startup time varies depending on model size. After the application status changes to **Running**, view the **logs** of the corresponding instance on the **Application details** page. If the log contains the following message: `The server is fired up and ready to roll!`, the model in the application has started successfully and is accessible.


<span id="1O0fLJ1R"></span>
### Step 3: Access the service

After you deploy the MiniMax\-M3 model service, obtain its domain name and access the service.


1. Obtain the domain name of the MiniMax\-M3 model service.

   1. In the left navigation pane of the [VKE console](https://console.byteplus.com/vke), click **ServingKit** \> **List of AI applications**. On the page that appears, find the deployed MiniMax\-M3 model application.

   2. Click the  **→**  icon in the application section to go to the application details page and view **Service domain names**.

2. In a terminal where the `curl` command is available, run the following command to access the MiniMax\-M3 model service.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>${your_service_domain_name}</code> with the <strong>service domain name</strong> obtained in the previous step.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no terminal is available, you can log in to the node where the model is deployed by using the ECS Terminal method and use the <code>curl</code> command to access the service. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal">ECS Terminal</a>.   </div>
   

   ```Bash
   curl -X POST http://${your_service_domain_name}/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
    "model": "MiniMax-M3",
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
   |model |The model to use. |MiniMax\-M3 |
   |messages |The message list of the conversation.<br><br><br>* role: The role that initiates the message.<br><br>* content: The content of the message. |None |
   |max_tokens |Specify the maximum number of tokens generated by the model for completion in a single request.<br><br><br>* Valid values: 1 to 8192. The value must be an integer.<br><br>* Default value: 4096. |500 |
   |temperature |The sampling temperature.<br><br><br>* Valid values: 0 to 2.<br><br>* A higher temperature (such as 1) results in more random output.<br><br>* A lower temperature (such as 0.2) results in more focused and deterministic output. |0.7 |
   

   The following figure displays the expected response after you run the command.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ffee9395284f6ad992fa4dfb1f1098dd.png) </span>


<span id="Vu5VMArH"></span>
## Subsequent operations

<span id="g88Y5Yxe"></span>
### Enhance service security

You can enhance the security of the MiniMax\-M3 service by using the API Key of APIG.


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
       "model": "MiniMax-M3",
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
   


<span id="9w9wQEgh"></span>
### Enabling observability

ServingKit AI applications support basic cloud\-native observability capabilities by default. You can view the application monitoring dashboard on the AI application details page.


1. In the left navigation pane of the [VKE console](https://console.byteplus.com/vke), click **ServingKit** \> **List of AI applications**. On the page that appears, find the deployed MiniMax\-M3 model application.

2. Click the  **→**  icon in the application section to go to the application details page and view the dashboard on the **Observability** tab.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not enabled the observability capability of the relevant cluster, enable observability based on the prompts in the console. For operations related to cloud\-native observability capabilities, see <a href="https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability">Enabling observability</a> and <a href="https://docs.byteplus.com/en/docs/vke/VKE-observability">VKE observability</a>.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1e5aa2f37795ab76d30f2ae698936f9.png) </span>
