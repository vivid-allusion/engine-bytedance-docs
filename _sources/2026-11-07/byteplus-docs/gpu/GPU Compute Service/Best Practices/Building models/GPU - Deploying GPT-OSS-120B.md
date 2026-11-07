---
title: "GPU - Deploying GPT-OSS-120B"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_-_Deploying_GPT-OSS-120B"
---

This topic, with one ecs.hpcpni3ln.45xlarge instance as an example, introduces how to deploy and run the GPT\-OSS\-120B model on a GPU Compute Service (GPU) instance.

> This topic may contain information about third\-party products. Related information is for reference only. BytePlus does not make any implied guarantees or other forms of commitments for the performance, reliability, or potential impacts of operations that involve any third\-party product.


<span id="YLGWywMJ"></span>
## Background

GPT\-OSS\-120B is a Mixture\-of\-Experts (MoE) language model. It has a total of 117 B arguments. The active arguments are 5.1 B. GPT\-OSS\-120B is open\-sourced based on the [Apache license 2.0](https://choosealicense.com/licenses/apache-2.0/) protocol.

<span id="E8dF2Nai"></span>
## Software requirements


* **NVIDIA driver**

   GPU driver: a program used to drive NVIDIA GPUs. This topic takes 535.161.08 as an example.

* **Runtime environment**

   vLLM framework: a high\-speed serving framework for large language models and visual language models. This topic takes the v0.10.1 version as an example.


<span id="ZYyDYNvP"></span>
## Procedure

<span id="gOHStWCj"></span>
### Step 1: Prepare the environment


1. Create a GPU Accelerated instance.

   Follow the guidance of [Purchasing HPC-optimized instances](https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances) to create one instance that meets the following conditions:

   
   |Configuration item |Recommended |
   |---|---|
   |**Basic configuration** ||
   |Instance type |ecs.hpcpni3ln.45xlarge<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The instance type ecs.hpcpni3ln.45xlarge is currently in Beta. If you need a trial, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> or contact your account manager to apply.</div><br> |
   |Image |Ubuntu 22.04 with GPU Driver 535.161.08 and doca<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you choose an image of another version, you need to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">install the GPU driver</a> after creating the instance.</div><br> |
   |Instance quantity |1 |
   |Storage |* Specification: TSSD TL0 EBS volume<br><br>* Capacity: no less than 512 GB |
   |**Network configuration** ||
   |Elastic IP (EIP) |Select "Elastic IP Address (EIP)". |
   

2. Install and configure Docker.

   1. Log in to the purchased GPU instance. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance)

   2. Execute the following commands to install Docker.

      ```Plain Text
      sudo apt update
      sudo apt install ca-certificates curl gnupg lsb-release -y
      sudo mkdir -p /etc/apt/keyrings
      curl -fsSL https://mirrors.ivolces.com/docker/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      sudo apt update
      sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
      ```
      

   3. Execute the following commands to install the NVIDIA Container Toolkit.

      ```Plain Text
      curl -s https://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/3bf863cc.pub | sudo apt-key add -
      cat <<EOF >/etc/apt/sources.list.d/nvidia.list
      deb http://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/ /
      EOF
      apt update
      apt install nvidia-container-toolkit -y
      ```
      

   4. Execute the following commands to configure Docker. This allows the container to use GPU resources of the instances.

      ```Plain Text
      sudo nvidia-ctk runtime configure --runtime=docker
      sudo systemctl restart docker
      ```
      

3.  **(Optional)**  initialize the local volume.

   If the instance type you choose has a local volume provided, we recommend that you execute the following commands to mount the local volume to the directory "/data01" where the model is stored. By doing this, you can improve the model loading speed.

   ```Plain Text
   mkfs -t ext4 /dev/nvme0n1
   mount -t ext4 /dev/nvme0n1 /data01
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/dev/nvme0n1</code> with the name of the local volume you use.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>ext4</code> with the file system you want to use.   </div>
   


<span id="TOiDKr5s"></span>
### Step 2: Download the GPT\-OSS\-120B model


1. Execute the following commands to download the onion.

   ```Plain Text
   curl -fsSL https://mirrors.ivolces.com/extra-tools/debian/GPG-KEY-system | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/volc-extra-tools.gpg
   
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/trusted.gpg.d/volc-extra-tools.gpg] http://mirrors.ivolces.com/extra-tools/debian buster main" > /etc/apt/sources.list.d/volctools.list && apt update && apt install -y onion-ai-data
   ```
   

2. Execute the following commands to download the GPT\-OSS\-120B model.

   1. Execute the following commands to create and enter the directory of the models.

      ```Plain Text
      cd /data01
      mkdir models
      cd models
      ```
      

   2. Execute the following command to view the model list.

      ```Plain Text
      oniond list model
      ```
      

   3. Execute the following command to download the model.

      ```Plain Text
      oniond download model gpt-oss-120b
      ```
      


<span id="PMeIpSlz"></span>
### Step 3: Run tests


1. Execute the following command to pull a Docker image.

   ```Plain Text
   docker pull ai-containers-cn-beijing.cr.volces.com/deeplearning/vllm:community_v0.10.1.gptoss_pure
   ```
   

2. Execute the following commands to start a Docker container with the pulled image.

   ```Plain Text
   docker run --gpus all -itd \
     --entrypoint /bin/bash \
     --net=host \
     --shm-size=100g \
     --ulimit memlock=-1 \
     --ulimit stack=67108864 \
     --privileged \
     --ipc=host \
     --security-opt seccomp=unconfined \
     --cap-add=ALL \
     -v /data01/models/:/data01/models/ \
     ai-containers-cn-beijing.cr.volces.com/deeplearning/vllm:community_v0.10.1.gptoss_pure \
     -c "tail -f /dev/null"
   ```
   

3. Enter the Docker container.

   1. Execute the following command to view the container ID.

      ```Plain Text
      docker ps
      ```
      

   2. Execute the following commands to enter the container.

      ```Plain Text
      docker exec -it <CONTAINER_ID> bash
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><CONTAINER_ID></code> with your actual container ID.      </div>
      

4. Execute the following command to start the vllm port.

   ```Plain Text
   vllm serve /data01/models/gpt-oss-120b --port 8000 -tp 8 --async-scheduling
   ```
   

   If the following information is returned, the service starts.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a07640f94448fd93fad44a37ea75ab1c.png) </span>

   **Argument descriptions**

   
   |Argument​ |Description |
   |---|---|
   |`/data01/models/gpt-oss-120b` |The local path of the model files. This parameter is used to specify the storage path for the GPT\-OSS\-120B model. The default storage path is `/root/models/gpt-oss-120b`. |
   |`--PORT` |The ​number of the port that the service listens on. The default value is `8000`. You can change it to the actual port that you need in the curl command. |
   |`-TP` |The Tensor Parallelism degree. Valid values:`1`, `2`, `4`, and`8`. Default value is`1`. |
   

6. Execute the following commands to call the model. Make sure that the deployed model can perform inference normally.

   ```Plain Text
   curl -X POST http://localhost:8000/v1/chat/completions -H "Content-Type: application/json" -d '{
       "model": "/root/models/gpt-oss-120b",
       "messages": [
           {
               "role": "user",
               "content": "Please prove the Riemann hypothesis"
           }
       ],
       "stream": false,
       "max_tokens": 1000,
       "temperature": 0.7
   }'
   ```
   

   If the following information is returned, the service is running normally. This indicates that you have deployed the GPT\-OSS\-120B model. You can now use the model inference service by calling the API via the local curl command.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f716c81a22162f7c30619336dd85f1de.png) </span>
