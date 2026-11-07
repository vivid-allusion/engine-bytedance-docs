---
title: "Using ComfyUI to implement digital human lip-sync podcasts"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_ComfyUI_to_implement_digital_human_lip-sync_podcasts"
---

This topic describes how to deploy and use ComfyUI in ServingKit and use it to implement the basic capability of digital human lip\-sync podcasts based on Wan2.1 and InfiniteTalk.

## Solution introduction

ServingKit provides a ComfyUI Workflow tailored for digital human lip\-sync podcasts. This Workflow integrates acceleration nodes from ServingKit, adopts FP8 precision for models, and enables 8\-GPU parallelism, FP8 activation quantization, and asynchronous offloading via the acceleration nodes. As a result, the generation time for a 1\-minute podcast video is shortened to **437.72 seconds** (compared to 2451.9 seconds with a non\-accelerated workflow that has identical configurations). This ComfyUI workflow reduces the generation time by 80% and significantly improves creative efficiency.

The following content describes the parameters of each node in the workflow.

### Resource Pool

|Parameter |Description |
|---|---|
|works_per_node |`works_per_node` indicates the number of workers per node in the resource pool. `nnodes` indicates the total number of cluster nodes.<br><br>The values must meet the following condition: `works_per_node` × `nnodes` = `gpu_num`.<br><br><br>* If you do not use Mergepool (resource pool merging solution), `works_per_node` equals `gpu_num`, and `nnodes` is 1.<br><br>* If you use Mergepool, `works_per_node` is 1, and `nnodes` equals `gpu_num`. |
|nnodes ||
|use_gpu |Whether to use GPU resources. Valid values:<br><br><br>* **true**: Yes<br><br>* **false**: No |
|max_colocate_count |The maximum number of workers. If the model requires three loaders: `DiT`, `CLIP`, and `VAE`, `max_colocate_count` needs to be set to 3. |
|pool_num |The name of the resource pool. |

### OpenVefuser WanVideo Model Loader

|Parameter |Description |
|---|---|
|ulysess_degree |The Ulysses parallelism degree.<br><br>The value needs to be divisible by `head_num` of the model. For example, if `head_num` of the Wan2.1\-14B model is 40, `ulysess_degree` can be set to 40, 80, or another value that is divisible by 40. |
|ring_degree |The Ring Attention parallelism degree. |
|cfg_degree |The Classifier\-Free Guidance (CFG) parallelism degree. Maximum value: 2. The Wan and HiDream models are supported.<br><br>The values must meet the following condition: `ulysess_degree` x `ring_degree x cfg_degree` = `gpu_num`. |
|base_precision |Base computation precision during model inference:<br><br><br>* **fp32**: 32\-bit single\-precision floating\-point computation.<br><br>* **bf16**: 16\-bit bfloat16 (brain floating\-point) computation.<br><br>* **fp16**: 16\-bit half\-precision floating\-point computation.<br><br>* **fp16_fast**: Optimized fast version of 16\-bit half\-precision floating\-point computation. |
|quantization |Quantization configuration of the model. To obtain FP8 activation quantization, select the `xxx_fast` mode. |
|load_device |Model storage location:<br><br><br>* **main_device**: GPU<br><br>* **offload_device**: CPU |
|attention_mode |Attention operator type. It is recommended to use `sageattn` in this scenario. This type indicates Sage Attention.<br><br>‌Sage Attention‌ significantly reduces VRAM usage through 8\-bit quantization technology while maintaining performance. Sage Attention‌ is suitable for devices with limited VRAM resources. |
|rms_norm_function |RMS Normalization (RMSNorm) implementation:<br><br><br>* **default**: Use the native RMSNorm implementation defined by the model itself.<br><br>* **pytorch**: Use the standard RMSNorm implementation provided by the PyTorch framework. |

### OpenVefuser WanVideo Sampler

> **tip**

> Compared with native nodes, only the offloading logic is modified, while all other input items remain unchanged.

|Parameter |Description |
|---|---|
|steps |The number of sampling steps, which is the number of denoising iterations. More steps achieve higher generation quality but take longer. |
|cfg |The guidance strength of the prompt. A higher value exerts a stronger influence on the generated result, but excessively high values may cause image distortion. |
|shift |A node extension parameter that controls the offset during the sampling process. |
|seed |The seed value, which is a random number generated during denoising. When the `seed` value and other parameter configurations are consistent, the generated image is reproducible. Different `seed` values achieve different random results. |
|control after generate |Controls the behavior of the `seed` after it is generated. Valid values:``<br><br><br>* **fixed**: Keeps the seed unchanged.<br><br>* **increment**: Increases the seed by 1 each time.<br><br>* **decrement**: Decreases the seed by 1 each time.<br><br>* **randomize**: Selects a new random seed for each generation to prevent repetitive results. |
|force_offload |Whether to forcibly offload model components to devices such as CPU temporarily after sampling:<br><br><br>* **true**: Yes.<br><br>* **false**: No (This alleviates video memory pressure). |
|scheduler |The noise scheduling policy, which controls the pace of noise variation during sampling. This parameter affects generation quality and efficiency. |
|riflex_freq_index |Frequency channel index targeted by the RIFLEX module. A value of 0 disables the module. The default value is 6, which enables new frame generation without looping. |
|denoise_strength |The level of denoising applied to the initial noise. A value of 1.0 indicates complete denoising. A lower value indicates higher randomness of the generated image.<br><br>The value range is 0 to 1.0. A value of 1.0 means complete denoising, generating entirely new content based on the initial latent variables. Values less than 1.0 mean modifying the original content. |
|batched_cfg |Whether to calculate CFG (Classifier\-Free Guidance) in batch mode:<br><br><br>* **true**: Enable batch CFG calculation. In this mode, CFG computations for multiple samples are merged to reduce redundant operations and significantly accelerate batch generation speed.<br><br>* **false**: Disable batch CFG calculation. In this mode, CFG is calculated sample by sample in the conventional way. |
|rope_function |Rotary Position Embedding (RoPE) implementation logic:<br><br><br>* **default**: Use the native RoPE implementation defined by the model itself.<br><br>* **comfy**: Use the native universal RoPE implementation of ComfyUI.<br><br>* **comfy_chunked**: Use the chunk\-based RoPE implementation of ComfyUI. |
|start_step |The starting step for sampling. 0 means full sampling. Otherwise, sampling starts from the specified step. |
|end_step |The ending step for sampling. \-1 indicates full sampling. Otherwise, sampling stops at the specified step. |
|add_noise_to_samples |The sample noise addition switch for specifying whether to add initial noise to video samples before sampling:<br><br><br>* **true**: Add noise.<br><br>* **false**: Do not add noise. |

## Preparation

Before you use the ComfyUI application, you need to prepare the required cloud service resources, environment, and other dependencies for ComfyUI.

|Cloud service |Required |Preparation |Reference |
|---|---|---|---|
|GPU Cloud Computing |Yes |Provides GPU computing resources. For the video generation scenario described in this topic, it is recommended to use the following GPU Cloud Computing instance types:<br><br><br>* **ecs.hpcpni3ln.45xlarge**: Recommended for this scenario<br><br>* **ecs.pni3l.22xlarge**: Prioritized for cost\-effectiveness<br><br><br>> **tip**<br><br><br>> [**Beta**] The preceding GPU Cloud Computing instance types are in beta. Contact your account manager of BytePlus to apply for a beta trial.<br> |[GPU Cloud Computing instance types](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types) |
|TOS |Recommended |Achieves persistent storage for the ComfyUI application.<br><br>> **tip**<br><br><br>> TOS storage can be mounted to containers only via [FSX](https://docs.byteplus.com/en/docs/vke/FSX_client_introduction). If you use existing managed VKE clusters for heterogeneous computing, make sure that [csi\-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on) and [fsx\-service](https://docs.byteplus.com/en/docs/vke/fsx-service-add-on) add\-ons are installed in the clusters. These add\-ons are automatically installed in newly created managed clusters for heterogeneous computing.<br> |[TOS storage types](https://docs.byteplus.com/en/docs/tos/docs-storage-type) |
|IAM |Required when TOS is used |Obtains the API access keys (AK and SK) of IAM to access TOS through VKE. |[Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys) |
|VKE |Yes |Provides managed clusters for heterogeneous computing for deploying the ComfyUI application. |[Managed clusters for heterogeneous computing of VKE](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster) |
|APIG |Optional |Achieves Layer 7 routing through APIG instances. These instances are required in session persistence scenarios.<br><br>> **warning**<br><br><br><br>* > We recommend using a standard API Gateway instance that is **v4.0.0** or later. You can view gateway details on the**Instance Overview** page of the target instance in the [API Gateway](https://console.byteplus.com/veapig) console.<br><br><br>* > If the API Gateway instance version does not meet the requirements, contact your BytePlus account manager to upgrade the instance version.<br> |[APIG instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance) |
|Internet express |Recommended |Add\-on installation requires content pulled from GitHub and HuggingFace, and the Internet Express service.<br><br>> **warning**<br><br><br><br>* > Internet express needs to be associated with the VPC of the cluster where the ComfyUI application is deployed.<br><br><br>* > [**Beta**] Internet express is currently in beta. Contact your account manager of BytePlus to apply for a beta trial.<br> |None |

## Step 1: Deploy the ComfyUI application

Deploy your ComfyUI application by using the ComfyUI application template provided by ServingKit. The following table describes specific configurations in this example. For other parameter configurations and detailed operations, see [Deploying the ComfyUI application](https://docs.byteplus.com/en/docs/vke/Deploying_ComfyUI).

|Parameter |Description |
|---|---|
|**Select framework and orchestration** ||
|Deployment method |Select **Predefined template deployment**. |
|Model |Select **Wan2.1 **  and **Infinite Talk**. |
|**Application configuration** ||
|ComfyUI configuration |We recommend selecting **Permanent storage** for **Storage location**. You can configure other parameters according to your application.<br><br>ServingKit will create the commonly used directories of ComfyUI in the corresponding paths, including the `custom_nodes`, `input`, `output`, `models`, and `user` directories. |
|**Instance configuration** ||
|Instance specification |Set **Number of GPU cards** to **8** and set other parameters as needed. |
|More configuration |* **Environment variables**: When you install add\-on nodes, you need to pull content from GitHub. Therefore, we recommend that you configure Internet express by using environment variables to accelerate the network. This prevents installation failures.<br><br>   Configure the following environment variables for Internet express in **Proxy mode**.<br><br>   * For Environment variable 1, set Key to `http_proxy` and set Value to `http://{acceleration IP}:3128`.<br><br>   * For Environment variable 2, set Key to `https_proxy` and set Value to `http://{acceleration IP}:3128`.<br><br>   * For Environment variable 3, set Key to `no_proxy` and set Value to `mirrors.ivolces.com`.<br><br>   > **warning**<br>   <br><br>   * > Make sure that Internet express is associated with the VPC of the cluster where the ComfyUI application is deployed.<br>   <br><br>   * > Internet Express is available in two modes: **proxy mode** and **routing mode**. If you enable **routing mode** for Internet Express, you do not need to configure this environment variable.<br>   <br><br>* Keep the default values of other parameters. |
|**Service configuration** ||
|API Gateway |Enable API Gateway and associate the prepared APIG instance.<br><br>> **warning**<br><br><br>> Make sure that the selected APIG instance and the cluster where the application is deployed are located in the same VPC.<br> |

## Step 2: Access the ComfyUI application

After you deploy the application, go to the **Application details** page. Click the **Service overview** tab and copy the value of the **Service domain names** parameter in the **Service configuration** section. Enter the domain name in the address bar of your browser to access the ComfyUI application.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81cdaf82321bb8ae8b9dd2bfa3859daf.png)

## Step 3: Use the ComfyUI application to implement the digital human lip\-sync podcast capability

1. Prepare the audio and images required for the digital human lip\-sync podcast.

   You can use the test audio and images provided by ServingKit, or use your own audio and images.

   [ServingKit-Infinite-talk-demo-bp.zip](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e43c6ed27564d0765725275abdbaa2eb.zip)

2. On the ComfyUI application page, click the dropdown menu icon in the upper left corner. Click **Browse Templates**, click the **vefuser_comfyui** series templates in the **EXTENSIONS** section, and find the **vefuser\-infinitetalk\-lipsync\-8gpus** template.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4dba6219e6d46002d8315c4808f07b5c.png)

3. Import the audio and images into the workflow.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5bac6b5385d1098e60b91c3c5f10d31a.png)

4. Click **Run**. Wait for the job to finish.

   After the job execution is complete, the "Little Raccoon Digital Human Podcast" is created.

5. If the output meets your expectations, click the drop\-down menu icon in the upper\-left corner and click **File** \> **Save** to save the pipeline. You can use this workflow later to easily create podcasts based on your custom audio, images, and scenes.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dff731592416004922d2626aa5da747c.png)

## Subsequent operations

You can modify parameter configurations based on the workflow node parameter descriptions in the **Solution introduction** section to achieve different results.
