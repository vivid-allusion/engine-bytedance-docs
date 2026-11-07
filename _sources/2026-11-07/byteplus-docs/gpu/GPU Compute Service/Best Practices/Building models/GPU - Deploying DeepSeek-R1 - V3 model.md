---
title: "GPU - Deploying DeepSeek-R1/V3 model"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_-_Deploy_DeepSeek-R1_V3_Model"
---

This topic, with two ecs.ebmhpcpni3l.48xlarge instances as an example, introduces how to deploy and run the DeepSeek\-R1 or DeepSeek\-V3 model on GPU Compute Service (GPU) instances.

<span id="6BA8o3jQ"></span>
## Background

<span id="68Yae9yM"></span>
### DeepSeek\-V3

DeepSeek\-V3 is a powerful Mixture\-of\-Experts (MoE) language model with a total of 671 B parameters. Each token activates 37 B parameters, and DeepSeek\-V3 was pre\-trained on 14.8 T tokens. [Learn more](https://api-docs.deepseek.com/zh-cn/news/news1226).

<span id="qm4eBOOB"></span>
### DeepSeek\-V3\-0324

DeepSeek\-V3\-0324 is a ​minor version of V3 released by DeepSeek, with 685 B parameters. Compared with the DeepSeek\-V3 model, DeepSeek\-V3\-0324 excels in reasoning, coding, and language capacities. [Learn more](https://api-docs.deepseek.com/zh-cn/news/news250325).

<span id="FyBlNHlP"></span>
### DeepSeek\-V3.1

DeepSeek\-V3.1 is an inference model post\-trained from the DeepSeek\-V3.1\-Base model. Compared with previous versions of the DeepSeek series, it supports hybrid inference architecture and delivers higher reasoning efficiency and agent capabilities.​ [Learn more](https://api-docs.deepseek.com/zh-cn/news/news250821).

<span id="SvPMkYya"></span>
### DeepSeek\-V3.1\-Terminus

DeepSeek\-V3.1\-Terminus is an inference model modified based on DeepSeek\-V3.1. It fixes issues in DeepSeek\-V3.1, such as mixed Chinese and English content and occasional abnormal characters, and further optimizes the performance of Code Agent and Search Agent. [Learn more](https://api-docs.deepseek.com/zh-cn/news/news250922).

<span id="SvPMkYya"></span>
### DeepSeek\-R1

DeepSeek\-R1 is an inference model trained and generated based on DeepSeek\-V3\-Base. Compared with the DeepSeek\-V3 model, DeepSeek\-R1 excels in complex tasks such as mathematics, coding, and natural language reasoning. It attracts global users for its open\-source model, innovative algorithms, and high cost\-effectiveness. [Learn more](https://api-docs.deepseek.com/zh-cn/news/news250120).

<span id="WG7Jzwkf"></span>
### DeepSeek\-R1\-0528

DeepSeek\-R1\-0528 is a ​minor version of R1 released by DeepSeek, with a parameter scale of 685 B. Compared with the DeepSeek\-R1 model, the DeepSeek\-R1\-0528 model has shown significant improvements in coding and deep reasoning. [Learn more](https://api-docs.deepseek.com/zh-cn/news/news250528).

<span id="e6AfCQ8L"></span>
## Software requirements


* NVIDIA driver:


GPU driver: a program used to drive NVIDIA GPUs. This topic takes 535.161.08 as an example.


* Runtime environment:


SGLang framework: a high\-speed serving framework for large language models and visual language models. This topic takes the v0.5.0.rc1 version as an example.

<span id="mqizp78Y"></span>
## Procedure

<span id="t6lNjhYv"></span>
### Step 1: Prepare the environment


1. Create a GPU Accelerated instance.


Follow the guidance of [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create two instances that meet the following conditions:



|Configuration item |Recommended |
|---|---|
|**Basic information** ||
|Instance type |ecs.ebmhpcpni3l.48xlarge<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The instance type ecs.ebmhpcpni3l.48xlarge is currently in Beta. If you need a trial, please contact your account manager to apply.</div><br> |
|Image |Ubuntu 22.04 with GPU Driver 535.161.08 and doca<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you choose an image of another version, you need to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">install the GPU driver</a> after creating the instance.</div><br> |
|Instance quantity |2<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The two GPU instances in this topic are "Node 0" and "Node 1" respectively.</div><br> |
|Storage |* Specification: TSSD TL0 EBS volume<br><br>* Capacity: no less than 1 TiB<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The DeepSeek\-R1 and DeepSeek\-V3 models used in this topic both have 671 B parameters, and the DeepSeek\-R1\-0528, DeepSeek\-V3\-0324, DeepSeek\-V3.1, and DeepSeek\-V3.1\-Terminus models have 685 B parameters. You can adjust the cloud volume capacity based on the parameter scale of the model actually deployed.</div><br> |
|**Network configuration** ||
|Virtual Private Cloud |Two instances need to be in the same VPC. |
|EIP |Select Elastic IP (EIP). |


2. Install the required software and tools.

   1. Log in to the two purchased GPU instances separately. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following commands separately on the two instances to install and configure Docker.

      ```Plain Text
      sudo apt update
      sudo apt install ca-certificates curl gnupg lsb-release
      sudo mkdir -p /etc/apt/keyrings
      curl -fsSL https://mirrors.ivolces.com/docker/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      sudo apt update
      sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
      ```
      

   3. Execute the following commands separately on the two instances to install NVIDIA Container Toolkit.

      ```Plain Text
      curl -s https://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/3bf863cc.pub | sudo apt-key add -
      cat <<EOF >/etc/apt/sources.list.d/nvidia.list
      deb http://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/ /
      EOF
      apt update
      apt install nvidia-container-toolkit -y
      ```
      

   4. Execute the following commands on both instances to configure Docker. This allows the containers to use GPU resources of the instances.

      ```Plain Text
      sudo nvidia-ctk runtime configure --runtime=docker
      sudo systemctl restart docker
      ```
      

3.  **(Optional)**  Initialize the local volume.

   If the instance type you choose has a local volume provided, we recommend that you execute the following commands to mount the local volume to the directory "/data01" where the model is stored. By doing this, you can improve the model loading speed.

   ```Plain Text
   mkfs -t ext4 /dev/nvme0n1
   mount -t ext4 /dev/nvme0n1 /data01
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/dev/nvme0n1</code> with the name of the local volume you use.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>ext4</code> with the file system you want to use.   </div>
   


<span id="PEM5WNpX"></span>
### Step 2: Deploy and run the model


1. Log in to the two purchased GPU instances separately. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Start the Docker container and model services on the instances of the corresponding nodes.

   
   <Tabs>
   <Tab zoneid="s7ro1wlPae" title="Instance "Node 0"">
   <TabTitle>Instance "Node 0"</TabTitle>
   
   Execute the commands based on the  to deploy and run the model.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">The following command is used to pull model files through the internet, where the internet bandwidth of the target instance is consumed. For billing details, see <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">Elastic IP</a>.</div>
   
   
   ```Plain Text
   docker run -d --network host --privileged --gpus=all --ipc=host -v /var/run/nvidia-topologyd/:/var/run/nvidia-topologyd/ -v /data01:/data -e MODEL_LENGTH=131072 -e TP=16 -e TOTAL_RANKS=2 -e RANKS=0 -e RANK0_ADDR=192.168.0.2:10240 -e NCCL_MIN_NCHANNELS=24 -e NCCL_IB_QPS_PER_CONNECTION=8 -e TORCHINDUCTOR_FX_GRAPH_CACHE=1 -e TORCHINDUCTOR_AUTOGRAD_CACHE=1 -e TORCHINDUCTOR_CACHE_DIR="/data/cache/torch_compile/" -e SGL_ENABLE_JIT_DEEPGEMM=1 -e CMD_ARGS="--enable-torch-compile --torch-compile-max-bs 64 --cuda-graph-bs 1 2 4 8 10 16 20 24 28 32 40 44 48 52 56 64 --cuda-graph-max-bs 64 --attention-backend fa3 --speculative-algo NEXTN --speculative-draft /data/models/DeepSeek-R1-NextN --speculative-num-steps 4 --speculative-eagle-topk 1 --speculative-num-draft-tokens 4" ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:v0.4.6.post2.byted.0.0.2.202505271222
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="Inboceuqy9" title="Instance "Node 1"">
   <TabTitle>Instance "Node 1"</TabTitle>
   
   Execute the commands based on the  to deploy and run the model.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">The following command is used to pull model files through the internet, where the internet bandwidth of the target instance is consumed. For billing details, see <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">Elastic IP</a>.</div>
   
   
   ```Plain Text
   docker run -d --network host --privileged --gpus=all --ipc=host -v /var/run/nvidia-topologyd/:/var/run/nvidia-topologyd/ -v /data01:/data -e MODEL_LENGTH=131072 -e TP=16 -e TOTAL_RANKS=2 -e RANKS=1 -e RANK0_ADDR=192.168.0.2:10240 -e NCCL_MIN_NCHANNELS=24 -e NCCL_IB_QPS_PER_CONNECTION=8 -e TORCHINDUCTOR_FX_GRAPH_CACHE=1 -e TORCHINDUCTOR_AUTOGRAD_CACHE=1 -e TORCHINDUCTOR_CACHE_DIR="/data/cache/torch_compile/" -e SGL_ENABLE_JIT_DEEPGEMM=1 -e CMD_ARGS="--enable-torch-compile --torch-compile-max-bs 64 --cuda-graph-bs 1 2 4 8 10 16 20 24 28 32 40 44 48 52 56 64 --cuda-graph-max-bs 64 --attention-backend fa3 --speculative-algo NEXTN --speculative-draft /data/models/DeepSeek-R1-NextN --speculative-num-steps 4 --speculative-eagle-topk 1 --speculative-num-draft-tokens 4" ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:v0.4.6.post2.byted.0.0.2.202505271222
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

   **Parameter descriptions:** 

   In the example, the above commands are used for deploying and starting the DeepSeek\-R1 model. If you need to deploy and start other models, replace the argument values of the corresponding environment variables by referring to the following descriptions.

   
   |**Environment variable** |Description |**Sample value** |
   |---|---|---|
   |MODEL_PATH |The model storage path within the container. The default path is `/data/models`. |/data/models |
   |MODEL_NAME |The name of the model to be deployed. Value:<br><br><br>* DeepSeek\-R1: Deploy the DeepSeek\-R1 model (default).<br><br>* DeepSeek\-V3: Deploys the DeepSeek\-V3 model.<br><br>* DeepSeek\-V3\-0324: Deploy the DeepSeek\-V3\-0324 model.<br><br>* DeepSeek\-R1\-0528: Deploy the DeepSeek\-R1\-0528 model.<br><br>* DeepSeek\-V3.1: Deploy the DeepSeek\-V3.1 model.<br><br>* DeepSeek\-V3.1\-Terminus: Deploy the DeepSeek\-V3.1\-Terminus model. |DeepSeek\-R1 |
   |MODEL_LENGTH |The model maximum length (in tokens). Default value is `131072`. |131072 |
   |TP |Tensor Parallelism degree. Default value is `16`. |16 |
   |TOTAL_RANKS |The total number of nodes. Default value is `1`. |2 |
   |RANKS |Specifies rank of the current node. Default value is `0`. |0 |
   |RANK0_ADDR |Configures the IP address and port number for accessing the node with rank `0` node, in the format: `IP address: port number`.<br><br><br>* IP address: (Recommended) Configure the IP address as the private IP address of node `0` .<br><br>* Port number: the port number for communication between nodes. |192.168.0.2:10240 |
   |PORT |The ​number of the port that the service listens on. Default value is `8000`. |8080 |
   |CMD_ARGS |Specifies additional parameters to start the SGLang framework. Format: ` -e  CMD_ARGS="<argument argument value>"`. Example:<br><br>When you add the `--mem-fraction-static`, `--disable-cuda-graph`, and `--api-key` arguments, append the following parameters: `-e  CMD_ARGS="--mem-fraction-static 0.95 --disable-cuda-graph --api-key 89LTsDxxxxx"`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When specifying additional parameters for starting the SGLang framework via Shell, you need to use <code>\</code> to escape the characters <code>$</code>、<code>`</code>、<code>\</code>、<code>!</code> contained in parameter values to prevent the Shell interpreter from treating them as metacharacters.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For more SGLang framework startup parameters, refer to <a href="https://docs.sglang.ai/backend/server_arguments.html">Server arguments</a>.</div><br> |"\-\-mem\-fraction\-static 0.95" |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To improve model inference performance, BytePlus has optimized the community edition of the SGLang v0.5.0rc1 framework as follows:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Tune the <code>fused_moe</code> parameter through the configuration file.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Add the runtime arguments <code>--speculative-num-steps 3 --speculative-eagle-topk 2 --speculative-num-draft-tokens 4</code> to optimize the MTP (Multi\-Token Prediction) module of the DeepSeek model.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you start the container via command, the system will automatically pull the inference engine image and weight files. Due to the large size of the model files, the installation process may take some time. Please wait patiently.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you need to download the inference engine and model files manually, refer to the <a href="https://docs.byteplus.com/en/docs/gpu/GPU_-_Deploy_DeepSeek-R1_V3_Model#Zc6yNw5N">appendix</a> for download instructions.   </div>
   

3. Execute the following commands separately in the two instances. Then, confirm whether the container and model have started through Docker logs.

   1. View the container ID.

      ```Plain Text
      docker ps
      ```
      

   2. View the running log of the corresponding container.

      ```Plain Text
      docker logs -f <CONTAINER_ID>
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><CONTAINER_ID></code> with the actual container ID.      </div>
      

<span id="amj2m4G3"></span>
### Step 3: Call the model


1.  [Log in to the instance "Node 0"](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to call the model. Make sure that the deployed model can perform inference normally.

   ```Plain Text
   curl -X POST http://0.0.0.0:8080/v1/chat/completions -H "Content-Type: application/json" -d '{
       "model": "/data/models/DeepSeek-R1",
       "messages": [
           {
               "role": "user",
               "content": "Please prove the Riemann hypothesis."
           }
       ],
       "max_tokens": 100,
       "temperature": 0.7
   }'
   ```
   

   **Parameter descriptions:** 

   This topic only includes parameters used for verification. For more parameter details, refer to [DeepSeek API documentation](https://api-docs.deepseek.com/api/create-chat-completion).

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |model |The model in use. |/data/models/DeepSeek\-R1 |
   |messages |The list of messages in the conversation.<br><br><br>* role: the role that initiates the message.<br><br>* content: the content of the message. |\- |
   |max_tokens |Specifies the maximum number of tokens for the model\-generated Completion in one request. Value:<br><br><br>* an integer between `1` and `8192`.<br><br>* Default value: `4096` |100 |
   |temperature |The sampling temperature. The higher the value (for example `1`), the more random the output is. Therefore, a lower temperature value (for example `0.2`) makes the output more focused and deterministic. Valid value: between `0`and `2`. |0.7 |
   


<span id="G14a1807"></span>
## FAQ

**How to resolve the error "torch.distributed.DistStoreError: Time out after 601 seconds waiting for clients."?** 


* Cause:

   The two nodes failed to establish communication within 600 seconds after the model service started.

* Solutions:

   * Make sure that all parameters in the command used to start Docker containers and model services are configured correctly.

   * Execute the commands used to start Docker containers and model services on the two instances separately as soon as possible to avoid timeouts.


<span id="Zc6yNw5N"></span>
## Appendix

You can manually download the BytePlus cached inference engine and model files, or visit the [DeepSeek official website](https://www.deepseek.com/) to download the relevant content.


* Download the inference engine.

   
   |Region |Download method |
   |---|---|
   |Asia Pacific (Johor) |```Plain Text```<br>```docker pull ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:v0.4.6.post2.byted.0.0.2.202505271222```<br> |
   

* Download the model file.

   1. Execute the following commands to install the Oniond tool.

      ```Plain Text
      curl -fsSL https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/volc-extra-tools.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/trusted.gpg.d/volc-extra-tools.gpg] http://mirrors.ivolces.com/extra-tools/ubuntu jammy main" > /etc/apt/sources.list.d/volctools.list && apt update && apt install -y onion-ai-data
      ```
      

   2. Download the model file.

      ```Plain Text
      oniond download model DeepSeek-V3
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>DeepSeek-V3</code> with the model name you need to download. Supported models: <code>DeepSeek-V3</code>, <code>DeepSeek-V3-0324</code>, <code>DeepSeek-V3.1</code>, <code>DeepSeek-V3.1-Terminus</code>, <code>DeepSeek-R1</code>, and <code>DeepSeek-R1-0528</code>.      </div>
