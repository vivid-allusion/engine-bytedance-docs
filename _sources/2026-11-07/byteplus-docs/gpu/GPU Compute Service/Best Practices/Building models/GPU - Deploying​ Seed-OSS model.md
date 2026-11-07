---
title: "GPU - Deploying​ Seed-OSS model"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/GPU_Deploying_Seed_OSS_model"
---

This topic describes how to deploy the Seed\-OSS\-36B model on a GPU Compute Service (GPU) instance. In the example provided in this topic, the ecs.hpcpni3ln.45xlarge instance type is used.

<span id="UCgDQBfK"></span>
## Background

Seed\-OSS is an open\-source Large Language Model (LLM) launched by ByteDance for developers and researchers. Boasting a 512K ultra\-long context window, an innovative thinking budget mechanism, and top\-tier benchmark performance, Seed\-OSS has achieved breakthroughs in core capabilities such as long\-document processing and multi\-scenario reasoning. Its dual\-version design caters to both practical application and academic research needs, making it a high\-value option within the open\-source LLM ecosystem.


* 512K ultra\-long context window: It supports one\-time loading and comprehension of long documents with approximately 900,000 Chinese characters.

* Dynamic thinking budget for reasoning: It dynamically allocates reasoning resources based on task complexity, facilitating rapid responses for simple tasks and deeper reasoning for complex ones.complex tasks.


<span id="C8dULQ0q"></span>
## Software requirements


* **NVIDIA driver**

   GPU driver: A program used to drive NVIDIA GPUs. In the example provided in this topic, version 535.161.08 is used.

* **Runtime environment**

   vLLM: An open\-source, high\-performance inference and serving framework for LLMs. In the example provided in this topic, version v0.10.1.1.seedoss is used.


<span id="f23VCKvX"></span>
## Procedure

<span id="HdGPYm7G"></span>
### Step 1: Prepare the environment


1. Create a GPU Accelerated instance.

   Create an instance that meets the requirements in the following table. For more information, see [Purchasing HPC-optimized instances](https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances).

   
   |Configuration item |Recommended |
   |---|---|
   |**Basic configuration** ||
   |Instance type |ecs.hpcpni3ln.45xlarge<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Seed\-OSS\-36B: We recommend that you use the ecs.hpcpni3ln.45xlarge instance type.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The ecs.hpcpni3ln instance type is currently in Beta. If you need a trial, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> or contact your account manager.</div><br> |
   |Image |Ubuntu 22.04 with GPU Driver 535.161.08 and doca<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you choose an image of another version, you need to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">install the GPU driver</a> after creating the instance.</div><br> |
   |Storage |* Specification: TSSD TL0 EBS volume<br><br>* Capacity: no less than 200 GiB<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The Seed\-OSS\-36B model has a parameter count of 36 billion. We recommend that you configure at least 200 GiB of cloud volume capacity. You can modify the cloud volume capacity based on the actual parameter count of the model that you want to deploy.   </div><br>    |
   |**Network configuration** ||
   |EIP |Select Elastic IP (EIP). |
   

2. Install the required software and tools.

   1. [Log in to the target instance.](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance)

   2. Execute the following commands to install and configure Docker.

      ```Plain Text
      sudo apt update
      sudo apt install ca-certificates curl gnupg lsb-release
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
      

   4. Execute the following commands to configure Docker. This allows containers to use GPU resources of instances.

      ```Plain Text
      sudo nvidia-ctk runtime configure --runtime=docker
      sudo systemctl restart docker
      ```
      

   5. Execute the following command to create a directory for storing the model.

      ```Plain Text
      mkdir /data00
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the example provided in this topic, the <code>/data00</code> directory is created. You can replace <code>/data00</code> with the actual directory where your model is stored.      </div>
      

3.  **(Optional)**  Initialize the local volume.

   If the instance type you choose has local volume provided, we recommend that you execute the following commands to mount the local volume to the directory "/data00" where the model is stored. By doing this, you can improve the model loading speed.

   ```Plain Text
   mkfs -t ext4 /dev/nvme0n1
   mount -t ext4 /dev/nvme0n1 /data00
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/dev/nvme0n1</code> with the name of the local volume you use.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>ext4</code> with the file system you want to use.   </div>
   


<span id="5VdAoWHi"></span>
### Step 2: Deploy and run the model


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Download the model file.

   1. Execute the following command to install and configure onion.

      ```Plain Text
      curl -fsSL https://mirrors.ivolces.com/extra-tools/ubuntu/GPG-KEY-system | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/volc-extra-tools.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/trusted.gpg.d/volc-extra-tools.gpg] http://mirrors.ivolces.com/extra-tools/ubuntu jammy main" > /etc/apt/sources.list.d/volctools.list && apt update && apt install -y onion-ai-data
      ```
      

   2. Execute the following command to enter the directory where model is stored.

      ```Plain Text
      cd /data00
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">We recommend that you select a disk directory with sufficient capacity to store the model files. In this topic, <code>/data00</code> is taken as an example. Please replace it with the actual directory path.      </div>
      

   3. Execute the following command to download the Seed\-OSS\-36B model by using the onion tool.

      ```Plain Text
      oniond download model Seed-OSS-36B-Instruct
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can also execute the <code>oniond list model</code> command to view the model list and learn about supported models.      </div>
      

3. Execute the following commands based on the region of the instance to download the Docker image.

   ```Plain Text
   docker pull ai-containers-ap-southeast-1.cr.volces.com/deeplearning/vllm:community_v0.10.1.1.seedoss
   ```
   

4. Execute the following commands based on the region of the instance to start the Docker container.

   ```Plain Text
   docker run --gpus all  -itd --net=host --shm-size=100g --ulimit memlock=-1 --ulimit stack=67108864 --privileged --ipc=host  --security-opt seccomp=unconfined --cap-add=ALL -v /data00/:/data/ -v /var/run/nvidia-topologyd/:/var/run/nvidia-topologyd/  --entrypoint /bin/bash ai-containers-ap-southeast-1.cr.volces.com/deeplearning/vllm:community_v0.10.1.1.seedoss
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please replace <code>/data00</code> with the actual directory path where the model is stored.   </div>
   

5. Execute the following command to check whether the container and the model are started based on Docker logs.

   1. View the container ID.

      ```Plain Text
      docker ps
      ```
      

   2. View the running log of the corresponding container.

      ```Plain Text
      docker logs <CONTAINER_ID>
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><CONTAINER_ID></code> with the actual container ID.      </div>
      

6. Start model service.

   1. Execute the following command to enter the Docker container:

      ```Plain Text
      docker exec -it <CONTAINER_ID> bash
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><CONTAINER_ID></code> with the actual container ID.      </div>
      

   2. Execute the following command to enter the Python directory.

      ```Plain Text
      cd /vllm-workspace/
      ```
      

   3. Execute the following command to start the Seed\-OSS\-36B model service.

      ```Plain Text
      python3 -m vllm.entrypoints.openai.api_server \
          --host 127.0.0.1 \
          --port 4321 \
          --enable-auto-tool-choice \
          --tool-call-parser seed_oss \
          --trust-remote-code \
          --model /data/Seed-OSS-36B-Instruct \
          --chat-template /data/Seed-OSS-36B-Instruct/chat_template.jinja \
          --tensor-parallel-size 8 \
          --dtype bfloat16 \
          --served-model-name seed_oss
      ```
      

      If the following output is displayed, the service is started.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ecb1da3588b5a3b2421a45e2c6ee49e7.png) </span>

      **Parameter descriptions:** 

      In the example from the previous step, the commands are used to start and deploy the Seed\-OSS\-36B model. To deploy and start other models, replace the relevant environment variables and parameter values in the commands according to the parameter descriptions in the following table.

      
      |Parameter |Description |Sample value |
      |---|---|---|
      |host |The IP address associated with the vLLM API server for network access. The value of this parameter is fixed as `127.0.0.1` and cannot be changed. |127.0.0.1 |
      |port |The number of the port the service listens on. The port is used to connect to the API service. |4321 |
      |model |The path or name of the model that you want to load, that is, the model storage path in the container. |/data/Seed\-OSS\-36B\-Instruct |
      |tensor\-parallel\-size |The number of GPUs for tensor parallelism. Valid value: `1–8`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Determine the maximum value of this parameter based on the actual number of GPUs.</div><br> |8 |
      |dtype bfloat16 |The type of data that you want the model to load and run. |bfloat16 |
      |served\-model\-name |The name of the model that you want to deploy. |seed_oss |
      


<span id="NCdr7nJY"></span>
### Step 3: Call the model


1. [Log in to the target instance running the model service](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to call the model. Make sure that the deployed model can perform inference normally.

   ```Plain Text
   curl -X POST http://127.0.0.1:4321/v1/chat/completions -H "Content-Type: application/json" -d '{
       "model": "seed_oss",
       "messages": [
           {
               "role": "user",
               "content": "Introduce the Forbidden City"
           }
       ],
       "max_tokens": 500,
       "temperature": 0.7
   }'
   ```
   

   If the following output is displayed, the service runs as expected. At this point, the deployment of the Seed\-OSS\-36B model has been completed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_20a32b0f118faca6b8ffd4d4cfb8b2cd.png) </span>
