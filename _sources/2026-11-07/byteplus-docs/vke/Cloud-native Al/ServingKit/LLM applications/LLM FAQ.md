---
title: "LLM FAQ"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/LLM_FAQ"
---

This topic provides frequently asked questions and solutions related to deploying LLM applications using ServingKit.


<span id="Wypxci8w"></span>
### How do I download a custom model to a node?

When deploying an AI application with ServingKit using a custom model, you need to download the custom model to the GPU node where the application resides. Follow the steps below to download the model.


1. Log in to the GPU node where the application resides via ECS Terminal. For detailed operations, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Run the following command to install the Oniond (model downloader) tool on the node.

   ```Bash
   curl -fsSL https://mirrors.ivolces.com/extra-tools/debian/GPG-KEY-system | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/volc-extra-tools.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/trusted.gpg.d/volc-extra-tools.gpg] http://mirrors.ivolces.com/extra-tools/debian buster main" > /etc/apt/sources.list.d/volctools.list && apt update && apt install -y onion-ai-data
   ```
   

3. Run the following command to enter the specified mount directory on the node's local disk.

   ```Bash
   cd /data01
   ```
   

   The specified mount directory on the node's local disk is the directory specified under the **Data volume** parameter in the **Advanced settings** section when creating the managed heterogeneous computing cluster for your ServingKit application. By default, the mount directory is `/data01`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b2c0b5691002e1a40a3484b3bde0436e.png) </span>

4. Run the following command to download the custom model to the specified mount directory on the node's local disk, that is, the `/data01` directory.

   ```Bash
   oniond download model <your_model_name>  
   # Replace <your_model_name> with the name of the model that you want to download. The following uses the GLM-5.2 model as an example. The complete command is as follows:
   # oniond download model GLM-5.2-FP8
   ```
   

   After the model is downloaded, the expected response is as follows.

   ```Bash
   Download Results:
   gid   |stat|avg speed  |path/URI
   ======+====+===========+=======================================================
   600657|OK  |   136MiB/s|GLM-5.2-FP8/model-00077-of-00141.safetensors
   524cb4|OK  |   149MiB/s|GLM-5.2-FP8/model-00079-of-00141.safetensors
   852a47|OK  |   150MiB/s|GLM-5.2-FP8/model-00080-of-00141.safetensors
   85febd|OK  |   151MiB/s|GLM-5.2-FP8/model-00081-of-00141.safetensors
   d52b39|OK  |   150MiB/s|GLM-5.2-FP8/model-00082-of-00141.safetensors
   f22383|OK  |   150MiB/s|GLM-5.2-FP8/model-00083-of-00141.safetensors
   ......
   b90f80|OK  |   164MiB/s|GLM-5.2-FP8/model-00130-of-00141.safetensors
   47bff4|OK  |   164MiB/s|GLM-5.2-FP8/model-00131-of-00141.safetensors
   b9049f|OK  |   163MiB/s|GLM-5.2-FP8/model-00132-of-00141.safetensors
   134e45|OK  |   166MiB/s|GLM-5.2-FP8/model-00133-of-00141.safetensors
   373a9f|OK  |   164MiB/s|GLM-5.2-FP8/model-00134-of-00141.safetensors
   c0a415|OK  |   165MiB/s|GLM-5.2-FP8/model-00136-of-00141.safetensors
   73cb8f|OK  |   165MiB/s|GLM-5.2-FP8/model-00135-of-00141.safetensors
   eaccd1|OK  |   165MiB/s|GLM-5.2-FP8/model-00137-of-00141.safetensors
   481532|OK  |    66MiB/s|GLM-5.2-FP8/model.safetensors.index.json
   82a118|OK  |    87MiB/s|GLM-5.2-FP8/tokenizer.json
   2be1f2|OK  |        n/a|GLM-5.2-FP8/tokenizer_config.json
   e7d2ae|OK  |   171MiB/s|GLM-5.2-FP8/model-00138-of-00141.safetensors
   6dde28|OK  |   205MiB/s|GLM-5.2-FP8/model-00139-of-00141.safetensors
   820aaf|OK  |   226MiB/s|GLM-5.2-FP8/model-00141-of-00141.safetensors
   ea5d87|OK  |   244MiB/s|GLM-5.2-FP8/model-00140-of-00141.safetensors
   
   Status Legend:
   (OK):download completed.
   Download completed successfully (elapsed 396 s). Repo directory: /data01/GLM-5.2-FP8
   ```
