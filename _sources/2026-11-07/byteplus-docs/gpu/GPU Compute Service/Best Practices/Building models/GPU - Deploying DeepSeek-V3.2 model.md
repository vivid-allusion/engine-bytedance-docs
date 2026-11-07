---
title: "GPU - Deploying DeepSeek-V3.2 model"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_Deploying_DeepSeek_Exp_model"
---

This topic, with two ecs.ebmhpcpni3l.48xlarge instances as an example, introduces how to deploy the DeepSeek\-V3.2 series models model on GPU instances.

<span id="LAFdXjrz"></span>
## Background

<span id="8Cbj6KIw"></span>
### DeepSeek\-V3.2

DeepSeek\-V3.2 is an official general\-purpose model, designed for daily applications and general agents. Building on V3.2\-Exp, DeepSeek\-V3.2 inherits and optimizes the DeepSeek Sparse Attention (DSA) mechanism, incorporates large\-scale agent training data and dual\-mode tool calling capabilities, and is adapted for daily Q&A and real\-world tool requirements.

<span id="lBEUMz6z"></span>
### DeepSeek\-V3.2\-Speciale

DeepSeek\-V3.2\-Speciale is an enhanced long\-thinking model and a research\-oriented version that explores the inference limits of open\-source models. V3.2\-Speciale, built on V3.2, has less limit on the chain\-of\-thought length, and has been deeply reinforced for complex logical reasoning, mathematical proofs, and professional competition tasks.

<span id="4lAMNPe2"></span>
### DeepSeek\-V3.2\-Exp

DeepSeek\-V3.2\-Exp is an experimental version that serves as an intermediate version during generation of the next\-generation architecture. Built on V3.1\-Terminus, DeepSeek\-V3.2\-Exp integrates the DeepSeek Sparse Attention (DSA) mechanism and has been optimized and verified in training and inference efficiency for long texts.

<span id="0KIdZHpo"></span>
## Software requirements


* NVIDIA driver:


GPU driver: a program used to drive NVIDIA GPUs. This topic takes 535.161.08 as an example.


* Runtime environment:


SGLang framework: a high\-performance service framework specifically built for Large Language Models (LLMs) and vision\-language models. With the collaborative design of the frontend structured generation language and the backend runtime system, the SGLang framework supports efficient interaction with models and ensures controllability of the generation process.

<span id="Lj6UCmpH"></span>
## Procedure

<span id="ozzrj5g7"></span>
### Step 1: Prepare the environment


1. Create a GPU Accelerated instance.


Follow the guidance of [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create two instances that meet the following conditions:



|Configuration item |Recommended |
|---|---|
|**Basic information** ||
|Instance type |ecs.ebmhpcpni3l.48xlarge<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The instance type ecs.ebmhpcpni3l.48xlarge is currently in Beta. If you need a trial, please contact your account manager to apply.</div><br> |
|Image |Ubuntu 22.04 with GPU Driver 535.161.08 and doca<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you choose an image of another version, you need to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">install the GPU driver</a> after creating the instance.</div><br> |
|Instance quantity |2<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The two GPU instances created in this topic are "Rank 0" and "Rank 1" respectively.</div><br> |
|Storage |* Specification: TSSD TL0 volume<br><br>* Capacity: no less than 1024 GiB<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The DeepSeek\-V3.2 series model used in this topic has 685 billion parameters. It is recommended to configure volume capacity of not less than 1024 GiB.</div><br> |
|**Network configuration** ||
|EIP |Select "Assign Elastic IP (EIP)". |


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
      

3. Execute the following command to create a directory for storing the model.

   ```Plain Text
   mkdir /data00
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/data00</code> with the actual directory name.   </div>
   

4.  **(Optional)**  Initialize the local volume.

   If the instance type you choose has local volume provided, we recommend that you execute the following commands to mount the local volume to the directory "/data00" where the model is stored. By doing this, you can improve the model loading speed.

   ```Plain Text
   mkfs -t ext4 /dev/nvme0n1
   mount -t ext4 /dev/nvme0n1 /data00
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/dev/nvme0n1</code> with the name of the actual local volume.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>ext4</code> with the file system you want to use.   </div>
   


<span id="9KbdtoDI"></span>
### Step 2: Deploy and run the model


1. Log in to the two purchased GPU instances. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Download the model file.

   1. Execute the following command to install and configure onion.

      ```Bash
      curl -fsSL https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/volc-extra-tools.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/trusted.gpg.d/volc-extra-tools.gpg] http://mirrors.ivolces.com/extra-tools/ubuntu jammy main" > /etc/apt/sources.list.d/volctools.list && apt update && apt install -y onion-ai-data
      ```
      

   2. Execute the following command to enter the directory where model is stored.

      ```Bash
      cd /data00
      ```
      

   3. Execute the following command to download the DeepSeek\-V3.2 model.

      ```Bash
      oniond download model DeepSeek-V3.2
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the example provided in this topic, the DeepSeek\-V3.2 model is downloaded. Supported: <code>DeepSeek-V3.2</code>, <code>DeepSeek-V3.2-Speciale</code>, and <code>DeepSeek-V3.2-Exp</code>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can also execute the <code>oniond list model</code> command to view the list of available models.      </div>
      

3. Execute the following commands separately on both GPU instances to download the Docker image.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, only the Asia Pacific (Johor) region is supported.   </div>
   

   ```Bash
   docker pull ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:community_v0.5.6
   ```
   

4. Execute the following commands separately on both GPU instances to start the Docker container.

   ```Bash
   docker run --gpus all  -itd --net=host --shm-size=100g --ulimit memlock=-1 --ulimit stack=67108864 --privileged --ipc=host  --security-opt seccomp=unconfined --cap-add=ALL -v /data00/:/data/ -v /var/run/nvidia-topologyd/:/var/run/nvidia-topologyd/  --entrypoint /bin/bash ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:community_v0.5.6
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Please replace <code>/data00</code> with the actual path where the model is stored.   </div>
   

5. Execute the following command to check whether the container and the model are started based on Docker logs.

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
      

   3. Start model service.

      1. Execute the following command to enter the Docker container:

         ```Plain Text
         docker exec -it <CONTAINER_ID> bash
         ```
         

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code><CONTAINER_ID></code> with the actual container ID.   </div>
   

      2. On both instances, execute the following commands to start the DeepSeek\-V3.2 model service.

         
         <Tabs>
         <Tab zoneid="XyzeU9nn" title="Rank 0 (Master node)">
         <TabTitle>Rank 0 (Master node)</TabTitle>
         
         ```Bash
         NCCL_IB_GID_INDEX=3 NCCL_IB_HCA=mlx5_ GLOO_SOCKET_IFNAME=eth0 NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         CUDA_CACHE_MAXSIZE=2147483648 python -m sglang.launch_server --tp 16 --dp 16 --enable-dp-attention --tool-call-parser deepseekv32 --reasoning-parser deepseek-v3 --cuda-graph-max-bs 32 --host 0.0.0.0 --port 8080 --dist-init-addr 192.168.0.167:12345 --nnodes 2 --node-rank 0 --model /data/DeepSeek-V3.2
         ```
         
         
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
         
         
         <div data-tips="true" data-tips-type="default">Please replace the <code>--dist-init-addr</code> value with the actual private IP address of the Rank 0 node instance.</div>
         
         
         If the following information is returned, the service on Rank 0 starts:
         
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5b7417cf44b166d720d0ae0b3e0803f3.png) </span>
         
         
         </Tab>
         <Tab zoneid="4ZsAjn4s" title="Rank 1">
         <TabTitle>Rank 1</TabTitle>
         
         ```Bash
         NCCL_IB_GID_INDEX=3 NCCL_IB_HCA=mlx5_ GLOO_SOCKET_IFNAME=eth0 NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         CUDA_CACHE_MAXSIZE=2147483648 python -m sglang.launch_server --tp 16 --dp 16 --enable-dp-attention --tool-call-parser deepseekv32 --reasoning-parser deepseek-v3 --cuda-graph-max-bs 32 --host 0.0.0.0 --port 8080 --dist-init-addr 192.168.0.167:12345 --nnodes 2 --node-rank 1 --model /data/DeepSeek-V3.2
         ```
         
         
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
         
         
         <div data-tips="true" data-tips-type="default">Please replace the <code>--dist-init-addr</code> value with the actual private IP address of the Rank 0 node instance.</div>
         
         
         If the following information is returned, the service on Rank 1 starts:
         
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c3b84bce20682919764761fa95ee0b8.png) </span>
         
         
         </Tab>
         </Tabs>
         

         **Parameter descriptions:** 

         In the example from the previous steps, the commands are used to start and deploy the DeepSeek\-V3.2 model. To deploy and start other models, replace the relevant environment variables and parameter values in the commands according to the parameter descriptions in the following table.

         
         |Parameter |Argument Type |Description |Sample value |
         |---|---|---|---|
         |python \-m sglang.launch_server |Startup command |The SGLang model server is start​ed via the Python module.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This item indicates not a parameter, but the command entry.</div><br> |\- |
         |\-\-model |Path/model ID |Specifies the loaded LLM mode. Valid values:<br><br><br>* Hugging Face model ID.<br><br>* Local model path. |/data/DeepSeek\-V3.2 |
         |\-\-tp |Integer |Configure tensor parallelism. Default value: `16`. |16 |
         |\-\-dp |Integer |Configure data parallelism. Default value: `8`. |16 |
         |\-\-enable\-dp\-attention |Boolean switch |Enables attention computation optimization in data parallel mode. |\- |
         |\-\-host |IP address |Specifies the host address associated with the service. |0.0.0.0 |
         |\-\-port |Integer |Specifies the number of the port the service listens on for connecting to the client side. |8080 |
         |\-\-dist\-init\-addr |IP: port |Indicates the initialization address of the distributed cluster (the primary node address), which is used for communication synchronization across nodes. |192.168.0.2:10240 |
         |\-\-nnodes |Integer |Specifies the total number of nodes in the distributed cluster, which is the number of servers involved in the service. |2 |
         |\-\-node\-rank |Integer |Specifies the sequence number of the current node in the cluster. The numbering starts from `0`. |* Rank 0：0<br><br>* Rank 1：1 |
         


<span id="lHUWbVzy"></span>
### Step 3: Call the model


1. [Log in to the Rank 0 node instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) and enter the Docker container.

2. Execute the following commands to call the model. Make sure that the deployed model can perform inference normally.

   ```Plain Text
   curl -X POST http://0.0.0.0:8080/v1/chat/completions -H "Content-Type: application/json" -d '{
       "model": "DeepSeek-V3.2",
       "messages": [
           {
               "role": "user",
               "content": "Introduce the Forbidden City in Beijing"
           }
       ],
       "max_tokens": 500,
       "temperature": 0.7
   }'
   ```
   

   **Parameter descriptions:** 

   This topic only includes parameters used for verification. For more parameter details, refer to [DeepSeek API documentation](https://api-docs.deepseek.com/api/create-chat-completion).

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |model |Indicates the actual model used. |DeepSeek\-V3.2 |
   |messages |The list of messages in the conversation.<br><br><br>* role: the role that initiates the message.<br><br>* content: the content of the message. |\- |
   |max_tokens |Specifies the maximum number of tokens for the model\-generated Completion in one request. Value:<br><br><br>* An integer between `1` and `8192`.<br><br>* The default value is `4096`. |100 |
   |temperature |Sampling temperature: The higher the temperature (for example `1`), the more random the output is. Therefore, a lower temperature value (for example `0.2`) makes the output more focused and deterministic. Value: between `0` and `2`. |0.7 |
   


<span id="Kogmkhu2"></span>
## FAQ

**How to resolve the error "torch.distributed.DistStoreError: Time out after 601 seconds waiting for clients."?** 


* Cause:

   The two nodes failed to establish communication within 600 seconds after the model service started.

* Solution:

   * Make sure that all parameters in the command used to start Docker containers and model services are configured correctly.

   * Execute the commands used to start Docker containers and model services on the two instances separately as soon as possible to avoid timeouts.
