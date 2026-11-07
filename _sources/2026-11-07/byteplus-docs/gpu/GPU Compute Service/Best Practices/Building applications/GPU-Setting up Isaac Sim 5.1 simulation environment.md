---
title: "GPU-Setting up Isaac Sim 5.1 simulation environment"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/setting-up-isaac-sim-5-1-simulation-env"
---

This topic describes how to deploy the Isaac Sim 5.1.0 simulation environment, access it by using the Live Streaming Client, and complete the construction of the basic environment required for business scenarios such as robot simulation.

<span id="oQqGd8kG"></span>
## Isaac Sim

NVIDIA Isaac Sim<sup>TM</sup> is a robot simulation tool built on the NVIDIA Omniverse platform. It enables developers to simulate and test AI\-powered robotics solutions in a physically accurate simulation environment. Equipped with a high\-fidelity, GPU\-accelerated PhysX engine, Isaac Sim supports industrial\-grade RTX rendering for multi\-sensor setups. It also features direct GPU access, allowing it to simulate a wide range of sensors including cameras, LiDAR, and contact sensors. This enables digital twin simulation, making it possible to run end\-to\-end robotics development workflows without the need to deploy physical robots. [Learn more](https://developer.nvidia.com/isaac/sim).

<span id="doNWKLWr"></span>
## Software version


* Operating system: In the example provided in this topic, Ubuntu 22.04 with GRID 16.8 is used.

* The NVIDIA Grid driver enables the GPU to more effectively deliver high\-performance compute capabilities or provide smoother graphics display. In the example provided in this topic, the 16.8 version is used.


<span id="nURs0x7M"></span>
## Step 1: Prepare the environment


1. Purchase and configure a GPU instance.

   1. Create an instance that meets the following conditions. For more information, see [Purchasing instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

      
      |Configuration item |Recommended |
      |---|---|
      |**Basic configuration** ||
      |Instance type |ecs.gni3cl\-vws.5xlarge<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This instance type is currently in Beta. To apply for a trial, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> or contact your account manager.</div><br> |
      |Image |Ubuntu 22.04 with GRID 16.8 |
      |Storage |* Specification: TSSD TL0 EBS volume<br><br>* Capacity: We recommend that the capacity be no less than 100 GiB. |
      |**Network configuration** ||
      |EIP |Select "Assign Elastic IP (EIP)".<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Streaming transmission is involved. We recommend that the EIP bandwidth be no less than 80 Mbps.</div><br> |
      

   2. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   3. Execute the following commands to install and configure Docker.

      ```Bash
      sudo apt update
      sudo apt install ca-certificates curl gnupg lsb-release
      sudo mkdir -p /etc/apt/keyrings
      curl -fsSL https://mirrors.ivolces.com/docker/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://mirrors.ivolces.com/docker/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      sudo apt update
      sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
      ```
      

   4. Execute the following commands to install the NVIDIA Container Toolkit.

      ```Bash
      curl -s https://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/3bf863cc.pub | sudo apt-key add -
      cat <<EOF >/etc/apt/sources.list.d/nvidia.list
      deb http://mirrors.ivolces.com/nvidia_all/ubuntu2204/x86_64/ /
      EOF
      apt update
      apt install nvidia-container-toolkit -y
      ```
      

   5. Execute the following commands to configure Docker. This allows containers to use GPU resources of instances.

      ```Bash
      sudo nvidia-ctk runtime configure --runtime=docker
      sudo systemctl restart docker
      ```
      

2. Add inbound rules to allow TCP ports 22 and 49100, and UDP port 47998. For more information, see [Modifying security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


<span id="jfR9m8zo"></span>
## Step 2: Pull the Isaac Sim container image


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to verify whether you can pull the test image from nvcr.io and whether the nvidia\-container\-toolkit works as expected.

   ```Bash
   docker run --rm --runtime=nvidia --gpus all nvcr.io/nvidia/cuda:12.5.1-base-ubuntu22.04 nvidia-smi
   ```
   

   If the following output is displayed, you can pull the test image from nvcr.io and the nvidia\-container\-toolkit works as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60c340cd764ef0a5d0091766eff4df63.png) </span>

3. Execute the following command to confirm whether the test image has been pulled locally.

   ```Bash
   docker image ls
   ```
   

   If the following output is displayed, the test image has been pulled as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f288d7e57bd2f7f10f94c27836021c56.png) </span>

4. Execute the following command to create the file directory.

   ```Bash
   mkdir -p ~/docker/isaac-sim/cache/main/ov
   mkdir -p ~/docker/isaac-sim/cache/main/warp
   mkdir -p ~/docker/isaac-sim/cache/computecache
   mkdir -p ~/docker/isaac-sim/config
   mkdir -p ~/docker/isaac-sim/data/documents
   mkdir -p ~/docker/isaac-sim/data/Kit
   mkdir -p ~/docker/isaac-sim/logs
   mkdir -p ~/docker/isaac-sim/pkg
   sudo chown -R 1234:1234 ~/docker/isaac-sim
   ```
   

5. Execute the following command to pull and run the container image for Isaac Sim 5.1.0.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you exit the container, it will be automatically removed, but the cache, configuration, and data will all be retained.   </div>
   

   ```Bash
   docker run --name isaac-sim --entrypoint bash -it --gpus all -e "ACCEPT_EULA=Y" --rm --network=host \
       -e "PRIVACY_CONSENT=Y" \
       -v ~/docker/isaac-sim/cache/main:/isaac-sim/.cache:rw \
       -v ~/docker/isaac-sim/cache/computecache:/isaac-sim/.nv/ComputeCache:rw \
       -v ~/docker/isaac-sim/logs:/isaac-sim/.nvidia-omniverse/logs:rw \
       -v ~/docker/isaac-sim/config:/isaac-sim/.nvidia-omniverse/config:rw \
       -v ~/docker/isaac-sim/data:/isaac-sim/.local/share/ov/data:rw \
       -v ~/docker/isaac-sim/pkg:/isaac-sim/.local/share/ov/pkg:rw \
       -u 1234:1234 \
       nvcr.io/nvidia/isaac-sim:5.1.0
   ```
   

6. Execute the following command inside the Isaac Sim container to verify whether the current operating system is compatible with Isaac Sim.

   ```Bash
   ./isaac-sim.compatibility_check.sh --/app/quitAfter=10 --no-windowTitle
   ```
   

   If the output contains `System checking result: PASSED`, the compatibility check has passed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_328212677d572a066c3c2a519806d683.png) </span>


<span id="03jxjbcO"></span>
## Step 3: Start the Isaac Sim service

Execute the following command inside the Isaac Sim container to start the Isaac Sim service.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you have already exited the Isaac Sim container, re\-execute the command above to pull and run the Isaac Sim 5.1.0 container image.</div>



* **Supported only for instances within the same VPC**

   ```Bash
   ./runheadless.sh
   ```
   

* **Supported for external servers over the public network.** 

   ```Bash
   PUBLIC_IP=$(curl -s ifconfig.me) && ./runheadless.sh --/app/livestream/publicEndpointAddress=$PUBLIC_IP --/app/livestream/port=49100
   ```
   


When the following output is displayed, the Isaac Sim service has been started.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b52c33a669e64edf5d9d6dea8b8e1d44.png) </span>

<span id="zees5ANR"></span>
## Step 4: Access the Isaac Sim service


1. Log in to the server from which you need to access the Isaac Sim service. In this example, a local macOS terminal is used.

2. Visit the [NVIDIA official website](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/download.html#isaac-sim-latest-release) to download and install the WebRTC client suitable for your instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0a82ad9bebb8d56dc272f044e285f2c.png) </span>

3. Start the WebRTC client. In the "Server" field, configure the EIP of the instance running the Isaac Sim service to allow access from external servers over the public network. Alternatively, you can configure the private IP address in the "Server" field to allow access only from instances within the same VPC. Then, click the "Connect" button to connect to the Isaac Sim service.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_882409fc67380f73da104d3c3ff516aa.png) </span>

4. Once the Isaac Sim service is connected successfully, you can load robot files and start simulation tasks.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1dc103d384528170dee9407cbaf09618.png) </span>
