---
title: "GPU - Deploying DeepSeek-R1 model with large-scale Expert Parallelism"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_-_Large_EP_deployment_of_DeepSeek-R1_model"
---

This topic describes how to deploy the DeepSeek\-R1 model on six ecs.ebmhpcpni3l.48xlarge instances. This example shows how to integrate the SGLang framework through large\-scale expert parallelism (EP) technology to improve cluster throughput performance and achieve efficient model inference and training.

<span id="ehwNuI9A"></span>
## Background

<span id="VK2nWp9j"></span>
### EP

EP (Expert Parallelism) is a core parallelism strategy in Mixture of Experts (MoE) models. The key idea is to distribute Experts in MoE models across multiple computational devices (for example, GPUs), addressing memory and computing power bottlenecks on individual cards. In addition, a balance between performance and resource efficiency is achieved through load balancing, communication optimization, and hardware affinity design.

<span id="QNVZtiLN"></span>
### DeepSeek\-R1

DeepSeek\-R1 is an inference model trained and generated based on DeepSeek\-V3\-Base. Compared with the DeepSeek\-V3 model, DeepSeek\-R1 excels in complex tasks such as mathematics, coding, and natural language reasoning. It attracts global users for its open\-source model, innovative algorithms, and high cost\-effectiveness. [Learn more](https://api-docs.deepseek.com/zh-cn/news/news250120).

<span id="6cw5Dk3R"></span>
## Solution architecture

In this topic, the Disaggregation Mode and xPyD elastic scheduling framework is taken as a basis for building a high\-performance distributed inference cluster with six ecs.ebmhpcpni3l.48xlarge instances. The cluster is divided into dedicated Prefill node pools and Decode node pools, which respectively carry out the tasks of preprocessing input prompts and generating output tokens. This helps in achieving directional allocation of computing resources and deep decoupling in the inference stage. Among the instances, two Prefill node instances adopt the DP4+EP16 deployment scheme to enhance batch processing capabilities with data parallelism. This meets the high bandwidth requirements during the prompt preprocessing stage. The other four Decode node instances adopt the DP32+EP32 deployment scheme to enhance low\-latency during the generation of each token.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07498f8dfde6ad07f24f05c0a3abd8d7.png) </span>

<span id="qt3cfIYj"></span>
## Software requirements


* NVIDIA driver:

   GPU driver: A program used to drive NVIDIA GPUs. This topic takes 535.161.08 as an example.

* Runtime environment:

   SGLang framework: a high\-speed serving framework for large language models and visual language models. This topic takes the v0.4.5.post3 version as an example.


<span id="KTKjlrFw"></span>
## Procedure

<span id="w1mHL9no"></span>
### Step 1: Prepare the environment


1. Create a GPU Accelerated instance.

   Follow the guidance of [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create six instances that meet the following conditions:

   
   |**Configuration item** |**Recommended** |
   |---|---|
   |**Basic configuration** ||
   |Instance type |ecs.ebmhpcpni3l.48xlarge<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The instance type ecs.ebmhpcpni3l.48xlarge is currently in Beta. If you need a trial, please contact your account manager to apply.</div><br> |
   |Image |Ubuntu 22.04 with GPU Driver 535.161.08 and doca<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you choose an image of another version, you need to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">install the GPU driver</a> after creating the instance.</div><br> |
   |Instance quantity |6<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Among the six GPU instances created in the example under this document:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Two instances work as Prefill nodes, named "Prefill_0" and "Prefill_1," respectively.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Four instances work as Decode nodes, named "Decode_0," "Decode_1," "Decode_2," and "Decode_3," respectively.</div><br> |
   |Storage |* Specification: TSSD TL0 volume<br><br>* Capacity: no less than 1 TiB<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The DeepSeek\-R1 model used in this topic has a parameter count of 671 billion. You can adjust the volume capacity according to the parameter scale of the model you actually deploy.</div><br> |
   |**Network configuration** ||
   |Virtual Private Cloud |The six instances need to be in the same VPC. |
   |EIP |Select Elastic IP (EIP). |
   

2. Install the required software and tools.

   1. Log in to the six purchased GPU instances separately. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following commands on each instance to install and configure Docker.

      ```Plain Text
      sudo apt update
      sudo apt install ca-certificates curl gnupg lsb-release
      sudo mkdir -p /etc/apt/keyrings
      curl -fsSL https://mirrors.ivolces.com/docker/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      sudo apt update
      sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
      ```
      

   3. Execute the following commands on each instance to install NVIDIA Container Toolkit.

      ```Plain Text
      curl -s https://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/3bf863cc.pub | sudo apt-key add -
      cat <<EOF >/etc/apt/sources.list.d/nvidia.list
      deb http://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/ /
      EOF
      apt update
      apt install nvidia-container-toolkit -y
      ```
      

   4. Execute the following commands on each instance to configure Docker. This allows the containers to use GPU resources of the instances.

      ```Plain Text
      sudo nvidia-ctk runtime configure --runtime=docker
      sudo systemctl restart docker
      ```
      

3.  **(Optional)**  Initialize the local volume.

   If the instance type you choose has local volume provided, we recommend that you execute the following commands to mount the local volume to the directory "/data00" where the model is stored. By doing this, you can improve the model loading speed.

   1. Execute the following command to create a GPT partition.

      ```Plain Text
      sudo parted /dev/nvme0n1 --script mklabel gpt
      sudo parted /dev/nvme0n1 --script mkpart primary ext4 0% 100%
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>/dev/nvme0n1</code> with the name of the actual local volume.      </div>
      

   2. Execute the following command to format the partition file system type as `ext4`.

      ```Plain Text
      sudo mkfs.ext4 /dev/nvme0n1p1
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>ext4</code> with the file system you want to use.      </div>
      

   3. Execute the following commands to create and mount the partition to the "/data00" mount point.

      ```Plain Text
      sudo mkdir -p /data00
      sudo mount /dev/nvme0n1p1 /data00
      ```
      


<span id="w9e1fLm5"></span>
### Step 2: Deploy and run the model


1. Log in to the six purchased GPU instances separately. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to download the Docker image.

   ```Plain Text
   docker pull ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:v0.4.5.post3.byted.0.0.3.202506061308
   ```
   

3. Execute the following command to start the Docker container.

   ```Plain Text
   docker run --runtime=nvidia -itd \
       --net=host \
       --ipc=host \
       --privileged \
       --shm-size=300g \
       --ulimit memlock=-1 \
       --ulimit stack=67108864 \
       --security-opt seccomp=unconfined \
       --entrypoint /bin/bash \
       --cap-add=ALL \
       --user=root \
       -v /data00/:/data00 -v /var/run/nvidia-topologyd/:/var/run/nvidia-topologyd/ \
       ai-containers-ap-southeast-1.cr.volces.com/deeplearning/sglang:v0.4.5.post3.byted.0.0.3.202506061308
   ```
   

4. Execute the following commands separately in the six instances. Then, confirm whether the container and model have started through Docker logs.

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
      

   3. Run the following command to enter the Docker container.

      ```Plain Text
      docker exec -it <CONTAINER_ID> bash
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><CONTAINER_ID></code> with the actual container ID.      </div>
      

   4. Download the model file.

      1. Execute the following command to enter the directory where model is stored.

         ```Plain Text
         cd /data00
         ```
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">We recommend that you select a disk directory with sufficient capacity to store the model files. In this topic, <code>/data00</code> is taken as an example. Please replace it with the actual directory path.         </div>
         

      2. Execute the following command to download the target model using the onion tool.

         ```Plain Text
         oniond download model DeepSeek-R1
         ```
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>DeepSeek-R1</code> with the name of the model you want to download. Supported: <code>DeepSeek-R1</code>.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">You can also execute the <code>oniond list model</code> command to view the list of available models.         </div>
         

   5. Execute the following commands to download the service startup configuration script:

      ```Plain Text
      wget -P '/sgl-workspace/' 'https://iaas-debug-southeast-1.tos-ap-southeast-1.ivolces.com/tool/DeepSeek/DeepSeek-R1_prefill_ep16_3500_1500.json'
      wget -P '/sgl-workspace/' 'https://iaas-debug-southeast-1.tos-ap-southeast-1.ivolces.com/tool/DeepSeek/DeepSeek-R1_decode_ep32_3500_1500.json'
      ```
      

   6. Execute the corresponding commands based on the instance nodes to start the model service:

      
      <Tabs>
      <Tab zoneid="p3jEokK6" title="Prefill node instance">
      <TabTitle>Prefill node instance</TabTitle>
      
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
      
      
      <div data-tips="true" data-tips-type="default">Replace <code>192.168.0.4:10240</code> with the private IP address of the "Prefill_0" instance and the port number for inter\-node communication.</div>
      
      
      
      * **Instance "Prefill_0"** 
      
         This instance will serve as the primary node for the 2 Prefill instances.
      
         ```Plain Text
         GLOO_SOCKET_IFNAME=eth0 NCCL_IB_HCA=mlx5_ NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 NCCL_IB_GID_INDEX=3 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         SGL_ENABLE_JIT_DEEPGEMM=1 \
         python3 -m sglang.launch_server \
         --attention-backend flashmla --disaggregation-ib-device  "mlx5_1,mlx5_2,mlx5_3,mlx5_4" \
         --model-path /data00/DeepSeek-R1/ \
         --tp 16 --disaggregation-mode prefill  \
         --host 0.0.0.0 --port 30300 --trust-remote-code --dist-init-addr 192.168.0.2:10240 --enable-deepep-moe --deepep-mode normal  --disable-radix-cache  --max-running-requests 16  --moe-dense-tp-size 1 --chunked-prefill-size 0 \
         --trust-remote-code --watchdog-timeout 1000000  \
         --enable-dp-attention --dp-size 4  --init-expert-location /sgl-workspace/DeepSeek-R1_prefill_ep16_3500_1500.json --ep-num-redundant-experts 32 --mem-fraction-static 0.7 \
         --nnodes 2 --node-rank 0 --page-size 64
         ```
         
      
      * **Instance "Prefill_1"** 
      
         ```Plain Text
         GLOO_SOCKET_IFNAME=eth0 NCCL_IB_HCA=mlx5_ NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 NCCL_IB_GID_INDEX=3 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         SGL_ENABLE_JIT_DEEPGEMM=1 \
         python3 -m sglang.launch_server \
         --attention-backend flashmla --disaggregation-ib-device  "mlx5_1,mlx5_2,mlx5_3,mlx5_4" \
         --model-path /data00/DeepSeek-R1/ \
         --tp 16 --disaggregation-mode prefill  \
         --host 0.0.0.0 --port 30300 --trust-remote-code --dist-init-addr 192.168.0.2:10240 --enable-deepep-moe --deepep-mode normal  --disable-radix-cache  --max-running-requests 16  --moe-dense-tp-size 1 --chunked-prefill-size 0 \
         --trust-remote-code --watchdog-timeout 1000000  \
         --enable-dp-attention --dp-size 4  --init-expert-location /sgl-workspace/DeepSeek-R1_prefill_ep16_3500_1500.json --ep-num-redundant-experts 32 --mem-fraction-static 0.7 \
         --nnodes 2 --node-rank 1 --page-size 64
         ```
         
      
          
      
      
      </Tab>
      <Tab zoneid="Kh4cSSwQ" title="Decode node instance">
      <TabTitle>Decode node instance</TabTitle>
      
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
      
      
      <div data-tips="true" data-tips-type="default">Replace <code>192.168.0.4:10240</code> with the private IP address of the "Decode_0" instance and the port number for inter\-node communication.</div>
      
      
      
      *  **"Decode_0" instance**
      
         This instance will serve as the primary node for 4 Decode instances.
      
         ```Plain Text
         GLOO_SOCKET_IFNAME=eth0 NCCL_IB_HCA=mlx5_ NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 NCCL_IB_GID_INDEX=3 SGLANG_HACK_DEEPEP_NUM_MAX_DISPATCH_TOKENS_PER_RANK=32 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         SGL_ENABLE_JIT_DEEPGEMM=1 \
         SGLANG_HACK_PD_DECODE_NUM_RESERVED_DECODE_TOKENS=514 \
         python3 -m sglang.launch_server \
         --attention-backend flashmla \
         --model-path /data00/DeepSeek-R1/ \
         --tp 32 --disaggregation-mode decode  --disaggregation-ib-device  "mlx5_1,mlx5_2,mlx5_3,mlx5_4" \
         --host 0.0.0.0 --port 30300 --trust-remote-code --dist-init-addr 192.168.0.4:10240 --enable-deepep-moe --deepep-mode low_latency  --disable-radix-cache --mem-fraction-static 0.8 --max-running-requests 640  --moe-dense-tp-size 1 --cuda-graph-bs 1 2 4 8 16 20 32   --watchdog-timeout 1000000  \
         --enable-dp-attention --dp-size 32 \
         --decode-log-interval 1 --context-length 6500 \
         --nnodes 4 --node-rank 0 --trust-remote-code  --mem-fraction-static 0.7  --page-size 64
         ```
         
      
      *  **"Decode_1" instance**
      
         ```Plain Text
         GLOO_SOCKET_IFNAME=eth0 NCCL_IB_HCA=mlx5_ NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 NCCL_IB_GID_INDEX=3 SGLANG_HACK_DEEPEP_NUM_MAX_DISPATCH_TOKENS_PER_RANK=32 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         SGL_ENABLE_JIT_DEEPGEMM=1 \
         SGLANG_HACK_PD_DECODE_NUM_RESERVED_DECODE_TOKENS=514 \
         python3 -m sglang.launch_server \
         --attention-backend flashmla \
         --model-path /data00/DeepSeek-R1/ \
         --tp 32 --disaggregation-mode decode  --disaggregation-ib-device  "mlx5_1,mlx5_2,mlx5_3,mlx5_4" \
         --host 0.0.0.0 --port 30300 --trust-remote-code --dist-init-addr 192.168.0.4:10240 --enable-deepep-moe --deepep-mode low_latency  --disable-radix-cache --mem-fraction-static 0.8 --max-running-requests 640  --moe-dense-tp-size 1 --cuda-graph-bs 1 2 4 8 16 20 32   --watchdog-timeout 1000000  \
         --enable-dp-attention --dp-size 32 \
         --decode-log-interval 1 --context-length 6500 \
         --nnodes 4 --node-rank 1 --trust-remote-code  --mem-fraction-static 0.7  --page-size 64
         ```
         
      
      *  **"Decode_2" instance**
      
         ```Plain Text
         GLOO_SOCKET_IFNAME=eth0 NCCL_IB_HCA=mlx5_ NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 NCCL_IB_GID_INDEX=3 SGLANG_HACK_DEEPEP_NUM_MAX_DISPATCH_TOKENS_PER_RANK=32 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         SGL_ENABLE_JIT_DEEPGEMM=1 \
         SGLANG_HACK_PD_DECODE_NUM_RESERVED_DECODE_TOKENS=514 \
         python3 -m sglang.launch_server \
         --attention-backend flashmla \
         --model-path /data00/DeepSeek-R1/ \
         --tp 32 --disaggregation-mode decode  --disaggregation-ib-device  "mlx5_1,mlx5_2,mlx5_3,mlx5_4" \
         --host 0.0.0.0 --port 30300 --trust-remote-code --dist-init-addr 192.168.0.4:10240 --enable-deepep-moe --deepep-mode low_latency  --disable-radix-cache --mem-fraction-static 0.8 --max-running-requests 640  --moe-dense-tp-size 1 --cuda-graph-bs 1 2 4 8 16 20 32   --watchdog-timeout 1000000  \
         --enable-dp-attention --dp-size 32 \
         --decode-log-interval 1 --context-length 6500 \
         --nnodes 4 --node-rank 2 --trust-remote-code  --mem-fraction-static 0.7  --page-size 64
         ```
         
      
      *  **"Decode_3" instance**
      
         ```Plain Text
         GLOO_SOCKET_IFNAME=eth0 NCCL_IB_HCA=mlx5_ NCCL_IB_DISABLE=0 NCCL_SOCKET_IFNAME=eth0 NCCL_IB_GID_INDEX=3 SGLANG_HACK_DEEPEP_NUM_MAX_DISPATCH_TOKENS_PER_RANK=32 \
         SGL_DISABLE_TP_MEMORY_INBALANCE_CHECK=1 \
         NCCL_MIN_NCHANNELS=24 \
         NCCL_IB_QPS_PER_CONNECTION=8 \
         SGL_ENABLE_JIT_DEEPGEMM=1 \
         SGLANG_HACK_PD_DECODE_NUM_RESERVED_DECODE_TOKENS=514 \
         python3 -m sglang.launch_server \
         --attention-backend flashmla \
         --model-path /data00/DeepSeek-R1/ \
         --tp 32 --disaggregation-mode decode  --disaggregation-ib-device  "mlx5_1,mlx5_2,mlx5_3,mlx5_4" \
         --host 0.0.0.0 --port 30300 --trust-remote-code --dist-init-addr 192.168.0.4:10240 --enable-deepep-moe --deepep-mode low_latency  --disable-radix-cache --mem-fraction-static 0.8 --max-running-requests 640  --moe-dense-tp-size 1 --cuda-graph-bs 1 2 4 8 16 20 32   --watchdog-timeout 1000000  \
         --enable-dp-attention --dp-size 32 \
         --decode-log-interval 1 --context-length 6500 \
         --nnodes 4 --node-rank 3 --trust-remote-code  --mem-fraction-static 0.7  --page-size 64
         ```
         
      
      
      
      
      
      </Tab>
      </Tabs>
      



<Tabs>
<Tab zoneid="cp5Xaw6tKt" title="">
<TabTitle></TabTitle>




</Tab>
</Tabs>



**Parameter descriptions:** 

      The above commands use starting the DeepSeek\-R1 model as an example. You can replace the corresponding runtime parameter values based on the following descriptions.

      
      |Running argument |Description |**Sample value** |
      |---|---|---|
      |\-\-model\-path |Model storage path inside the container. |/data00/DeepSeek\-R1/ |
      |\-\-tp |The Tensor Parallelism degree.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The recommended value is <code>16</code> for Prefill node instances and <code>32</code> for Decode node instances.</div><br> |16 |
      |\-\-disaggregation\-mode |The decoupling mode. Value:<br><br><br>* prefill: Indicates that the instance is used for Prefill (preprocessing).<br><br>* decode: Indicates that the instance is used for Decode (decoding). |prefill |
      |\-\-port |Port number for service listening. |30300 |
      |\-\-dist\-init\-addr |Configure the IP address and port number for accessing the node with Rank `0` in the format of `IP address:Port number`.<br><br><br>* IP address: We recommend that you set the IP address to the private IP address of node `0`.<br><br>* Port number: the port number for communication between nodes. |192.168.0.2:10240 |
      |\-\-nnodes |The total number of nodes. |2 |
      |\-\-node\-rank |The rank of the current node. |0 |
      |\-\-kv\-cache\-dtype |The data type of KV Cache. |fp8_e4m3 |
      

5. Start the agent service.

   1. [Log in to the “Prefill_0” instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following command to enter the Docker container:

      ```Plain Text
      docker exec -it <CONTAINER_ID> bash
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><CONTAINER_ID></code> with the actual container ID.      </div>
      

   3. Execute the following command to start the agent service:

      ```Plain Text
      python3 -m sglang.srt.disaggregation.mini_lb --prefill "http://<Prefill_Master_IP>:30300" --decode "http://<Decode_Master_IP>:30300"
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><Prefill_Master_IP></code> with the private IP address of the "Prefill_0" instance.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><Decode_Master_IP></code> with the private IP address of the "Decode_0" instance.      </div>
      


<span id="cDT4RRBd"></span>
### Step 3: Call the model


1. [Log in to the "Prefill_0" instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to call the model. Make sure that the deployed model can perform inference normally.

   ```Plain Text
   curl http://127.0.0.1:8000/v1/chat/completions -H "Content-Type: application/json" -d '{
       "model": "/data00/DeepSeek-R1",
       "messages": [
           {
               "role": "user",
               "content": "Please prove the Riemann Hypothesis."
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
   |model |The model in use. Supported:<br><br><br>* DeepSeek\-R1 |/data00/DeepSeek\-R1 |
   |messages |The list of messages in the conversation.<br><br><br>* role: the role that initiates the message.<br><br>* content: the content of the message. |\- |
   |max_tokens |Specifies the maximum number of tokens for the model\-generated Completion in one request. Value:<br><br><br>* An integer between 1 and 8192.<br><br>* The default value is 4096. |100 |
   |temperature |Sampling temperature: The higher the temperature (for example 1), the more random the output is. Therefore, a lower temperature value (for example 0.2) makes the output more focused and deterministic. Value: between 0 and 2. |0.7 |
   


<span id="kHpinEcm"></span>
##
