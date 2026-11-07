---
title: "Building ChatGLM-6B LLM"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-a-ChatGLM-6B-LLM"
---

This topic describes how to deploy the ChatGLM\-6B Large Language Model (LLM) on an ECS instance. In the example provided in this topic, a Compute\-optimized ECS instance of type ecs.c3i.24xlarge is used, which is equipped with the 4th\-generation Intel® Xeon® Scalable processor (Sapphire Rapids).

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

ChatGLM\-6B is a conversational language model with 6.2 billion parameters, and it supports Chinese\-English bilingual question answering. The model is built on the General Language Model (GLM) architecture and leverages model quantization technology. This technical design enables its local deployment on consumer\-grade graphics cards, requiring as little as 6 GB of VRAM when the INT4 quantization level is used. ChatGLM\-6B shares the same technology as ChatGLM, with specific optimizations for Chinese question answering and dialogue scenarios. The 6.2\-billion\-parameter ChatGLM\-6B model undergoes bilingual training on approximately 1 trillion tokens, supplemented by techniques including supervised fine\-tuning, automated feedback collection, and reinforcement learning from human feedback (RLHF). Through this comprehensive training and optimization process, the model can now generate responses that closely align with human preferences.

<span id=".546v5aKD6KaB5rGC"></span>
## Environmental requirements

**Instance configurations**

We recommend that you use the following instance configurations to deploy the ChatGLM\-6B model:


|Type |Instance type |vCPU |Memory (GiB) |Operating systems |
|---|---|---|---|---|
|Recommended |ecs.c3i.24xlarge |96 |192 |Ubuntu 22.04 |
|Best cost\-effectiveness |ecs.g3i.8xlarge |32 |128 |Ubuntu 22.04 |
|Minimum configuration |ecs.r3i.4xlarge |16 |128 |Ubuntu 22.04 |


**Runtime environment**


* Anaconda is a package acquisition and management tool. It comes pre\-installed with over 180 scientific computing packages and their dependencies, including Conda and Python, and enables the creation of isolated Python virtual environments. In the example provided in this topic, Anaconda 3 and Python 3.8.3 are used.

* Transformers: A neural network architecture used for tasks such as language modeling, text generation, and machine translation. In the example provided in this topic, Transformers 4.33.2 is used.

* Gradio: An open\-source Python library designed for quickly building web\-based interfaces to showcase machine learning models. In the example provided in this topic, Gradio 3.44.4 is used.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a6e5L6L"></span>
### Step 1: Create an instance


1. Create an instance that meets the following conditions. For more information, see [Purchasing instances by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   * Basic configuration:

      * Compute specification: ecs.c3i.24xlarge

      * Image: Ubuntu 22.04

      * Storage: Volume capacity must be greater than 100 GiB

   * Network configuration: Select "Assign Elastic IP (EIP)".

2. After you create an instance, add an inbound rule to the security group associated with the instance to allow TCP port 7860. For more information, see [Modifying security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).


<span id=".5q2l6aqk5LqM77ya5Yib5bu66Jma5ouf546v5aKD"></span>
### Step 2: Create a virtual environment


1. Execute the following command to download the Anaconda installation package.

   ```Bash
   wget https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh
   ```
   

2. Execute the following command to install Anaconda.

   ```Bash
   bash Anaconda3-2022.05-Linux-x86_64.sh
   ```
   

   1. Keep pressing the "Enter" key to install Anaconda.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68ebc4169ab18b556dfafdb559998aa6.png) </span>

   2. Enter "yes", and press the "Enter" key to confirm the information.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ebfebb1976552ae84176af1845791704.png) </span>

   3. The installation path for Anaconda is `/root/anaconda3`. Press the Enter key to confirm installation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc180461264376b3e9c8c2ca57007f3d.png) </span>

   4. Enter "yes", and press the "Enter" key to confirm the initialization of Anaconda.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6654afb9ba9ca4dc3a21bd53f2a222fb.png) </span>

3. Execute the following command to make the configuration take effect.

   ```Bash
   source ~/.bashrc
   ```
   

   If the following output is displayed, the configuration is successful and you have entered the base environment.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b74938aaf46aaa2d6ccde533f350d20c.png) </span>

4. Create a virtual environment named "SPR", and set the Python version in that environment to 3.8.3.

   1. Execute the following command.

      ```Bash
      conda create -n SPR python=3.8.3
      ```
      

   2. When `Proceed ([y]/n)?` is displayed, enter "y" and press Enter to confirm the creation.

   3. Execute the following command to activate the virtual environment.

      ```Bash
      conda activate SPR
      ```
      

      If the following output is displayed, the activation is successful.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c04d755769ff190836fe01ac69127579.png) </span>


<span id=".5q2l6aqk5LiJ77ya6YOo572y5qih5Z6L5bm26aqM6K-B"></span>
### Step 3: Deploy and verify the model


1. Execute the following command to download the weight file for the ChatGLM\-6B model.

   ```Bash
   wget https://ai-llm.tos-cn-beijing.volces.com/chatglm-6b/GLM-6B-SPR.tar.gz
   ```
   

2. Execute the following command to decompress the file package.

   ```Bash
   tar -zxvf GLM-6B-SPR.tar.gz
   ```
   

   Execute the `ll` command to view the list of files after decompression, as shown in the following figure.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_844d063b4e88931109f0e191053c90cd.png) </span>

3. Execute the following command to install the corresponding Intel dependency packages.

   ```Python
   pip install mkl==2023.1.0 intel-openmp==2023.1.0
   ```
   

4. Execute the following commands in sequence to install the memory allocator Jemalloc in a Conda environment.

   ```Python
   conda install jemalloc
   pip install torch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 --index-url https://download.pytorch.org/whl/cpu
   pip install transformers==4.27.1
   ```
   

5. Install Gradio.

   1. Execute the following command to install Gradio.

      ```Python
      pip install gradio==3.44.4 sentencepiece
      ```
      

   2. Execute the following command to verify.

      ```Python
      pip list | grep gradio
      ```
      

      When the output includes Gradio version information as shown below, the installation was successful.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_75f652e3f744f448d0501e29cc9aa9c6.png) </span>

6. Change the software source.

   1. Execute the `vim /etc/apt/sources.list` command to open the source file.

   2. Press `i` to enter edit mode and add the following content.

      ```Plain Text
      deb http://mirrors.ivolces.com/ubuntu/ jammy main restricted universe multiverse
      deb-src http://mirrors.ivolces.com/ubuntu/ jammy main restricted universe multiverse
      
      deb http://mirrors.ivolces.com/ubuntu/ jammy-security main restricted universe multiverse
      deb-src http://mirrors.ivolces.com/ubuntu/ jammy-security main restricted universe multiverse
      
      deb http://mirrors.ivolces.com/ubuntu/ jammy-updates main restricted universe multiverse
      deb-src http://mirrors.ivolces.com/ubuntu/ jammy-updates main restricted universe multiverse
      
      # deb http://mirrors.ivolces.com/ubuntu/ jammy-proposed main restricted universe multiverse
      # deb-src http://mirrors.ivolces.com/ubuntu/ jammy-proposed main restricted universe multiverse
      
      deb http://mirrors.ivolces.com/ubuntu/ jammy-backports main restricted universe multiverse
      deb-src http://mirrors.ivolces.com/ubuntu/ jammy-backports main restricted universe multiverse
      ```
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and press `Enter` to save and exit the file.

7. Execute the `apt update` command to update software packages.

8. Execute the following commands in sequence to install the dependency packages.

   ```Bash
   cd /root/bloom
   pip install bloom_fp16-0.0.0-cp38-cp38-linux_x86_64.whl
   pip install chatglm_hybrid-0.0.0-cp38-cp38-linux_x86_64.whl
   pip install chatglm_fp32-0.0.0-cp38-cp38-linux_x86_64.whl
   apt install numactl 
   ```
   

9. After installation is complete, execute the `cd` command to exit the current directory.

10. Modify the export path of the demo file in the `chatglm/webui` directory, and load the local ChatGLM model.

   1. Execute the `vim /root/chatglm/read_path.py` command to create a path lookup script. Add the following content to the file.

      ```Python
      import torch
      import os
      import sys
      
      def get_pytorch_install_dir():
          return os.path.dirname(os.path.abspath(torch.__file__))
      
      pytorch_install_dir = get_pytorch_install_dir()
      python_dir = sys.prefix
      
      print("PyTorch Library Path: " + pytorch_install_dir)
      print("Python Library Path: " + python_dir + "/lib")
      print("MKL Dynamic Library Path: " + python_dir + "/lib/libmkl_rt.so.2")
      ```
      

   2. Press the `Esc` key to exit edit mode, enter `:wq`, and press `Enter` to save and exit the file.

   3. Execute the following commands in sequence to view the Dynamic path.

      ```Python
      python /root/chatglm/read_path.py
      ```
      

      As shown in the following figure, the Dynamic path in this example is `/root/anaconda3`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6c319e9f0f904c8241a44fb03efcf79.png) </span>

   4. Execute the following command to open the demo file.

      ```Bash
      vim /root/chatglm/webui/start_demo.sh*
      ```
      

   5. Press `i` to enter edit mode and change the export path to the Dynamic path, which is `/root/anaconda3` in this example, as shown in the following figure.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63bc36325d8b5a42c112dd50fe41a778.png) </span>

11. Execute the following commands in sequence to execute the `start_demo.sh*` script.

   ```Bash
   cd /root/chatglm/webui
   ./start_demo.sh*
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bfa260b2422ec76843ceb9ef3b74a073.png) </span>

12. Use a browser to access the public URL (`https://<EIP>.gradio.live`).


&nbsp;

<span id="91wqiY3T"></span>
## FAQ

**When I start the model service via script, the error "Could not create share link. Missing file: /root/anaconda3/envs/SPR/lib/python3.8/site\-packages/gradio/frpc_linux_amd64_v0.2." occurs. How can this be resolved?** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2bef3399e341692cf9cf25229b82a9b3.png) </span>

This issue is usually caused by network or security software preventing Gradio from automatically downloading the required intranet penetration component. Please refer to the following solution.


1. Execute the following command to download the missing file and rename it to frpc_linux_amd64_v0.2.

   ```Bash
   wget https://cdn-media.huggingface.co/frpc-gradio-0.2/frpc_linux_amd64 -O frpc_linux_amd64_v0.2
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When direct download is not possible, please follow the <a href="https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview?lang=zh"> Uploading or downloading files</a> instructions to download it locally and then upload it to the server.   </div>
   

2. Execute the following command to move the file to the Gradio package directory.

   ```Bash
   mv frpc_linux_amd64_v0.2 /root/anaconda3/envs/SPR/lib/python3.8/site-packages/gradio/
   ```
   

3. Execute the following command to grant executable permission to the file.

   ```Bash
   chmod +x /root/anaconda3/envs/SPR/lib/python3.8/site-packages/gradio/frpc_linux_amd64_v0.2
   ```
   

4. Run the start_demo.sh\* script again to verify whether the issue is resolved.

   ```Bash
   cd /root/chatglm/webui
   ./start_demo.sh*
   ```
