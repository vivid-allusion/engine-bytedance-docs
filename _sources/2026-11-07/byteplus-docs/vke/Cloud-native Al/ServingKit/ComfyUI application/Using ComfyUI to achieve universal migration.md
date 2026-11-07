---
title: "Using ComfyUI to achieve universal migration"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_the_ComfyUI_application"
---

ComfyUI provides a node\-based interface built on Stable Diffusion, which helps you efficiently construct complex AIGC workflows to accomplish tasks such as short video content generation, advertising and marketing product design, game scene design, and animation production. This topic describes how to deploy and use ComfyUI in ServingKit to achieve the basic capability of universal migration based on Qwen\-Image.

## Solution introduction

This practice provides a ComfyUI workflow that incorporates acceleration nodes from ServingKit. The model uses FP8 precision and achieves 2\-card parallelism and 4\-step LoRA by using acceleration nodes. As a result, it takes **17 seconds** to generate a 720 × 1280 picture, with image generation time decreasing by 77%. If you use a non\-accelerated workflow, it takes 75 seconds to generate a single picture under the same configuration. If you generate a picture with a higher resolution, the picture generation duration will increase.

The following content describes the parameters of each node in the workflow.

### Resource Pool

|Parameter |Description |
|---|---|
|works_per_node |`works_per_node` indicates the number of workers per node in the resource pool. `nnodes` indicates the total number of cluster nodes.<br><br>The values must meet the following condition: `works_per_node` × `nnodes` = `gpu_num`.<br><br><br>* If you do not use Mergepool (resource pool merging solution), `works_per_node` equals `gpu_num`, and `nnodes` is 1.<br><br>* If you use Mergepool, `works_per_node` is 1, and `nnodes` equals `gpu_num`. |
|nnodes ||
|use_gpu |Whether to use GPU resources. Valid values:<br><br><br>* **true**: Yes<br><br>* **false**: No |
|max_colocate_count |The maximum number of workers. If the model requires three loaders: `DiT`, `CLIP`, and `VAE`, `max_colocate_count` needs to be set to 3. |
|pool_num |The name of the resource pool. |

### OpenVefuser DiT Loader

|Parameter |Description |
|---|---|
|dit name |The name or path of the Diffusion Transformer (DiT) model. |
|weight type |The quantization precision of the DiT model. |
|ulysess_degree |The Ulysses parallelism degree.<br><br>The value needs to be divisible by `head_num` of the model. For example, if `head_num` of the Wan2.1\-14B model is 40, `ulysess_degree` can be set to 40, 80, or another value that is divisible by 40. |
|ring_degree |The Ring Attention parallelism degree. |
|cfg_degree |The Classifier\-Free Guidance (CFG) parallelism degree. Maximum value: 2. The Wan and HiDream models are supported.<br><br>The values must meet the following condition: `ulysess_degree` x `ring_degree x cfg_degree` = `gpu_num`. |
|sage_type |The computing precision and hardware adaptation logic at model runtime. Valid values:<br><br><br>* **none**: Does not enable special precision optimization and uses the default precision of the model.<br><br>* **auto**: Automatically adapts to the hardware and model to select the optimal precision policy.<br><br>* **fp8**: Uses FP8 low\-precision computing to significantly reduce memory usage and increase speed. The GPU resources need to support FP8 calculation.<br><br>* **fp8_sm90**: FP8 precision optimized for NVIDIA SM9.0 GPUs, such as H100 and H20.<br><br>* **fp16**: Uses FP16 half\-precision computing, which is a commonly used balanced precision for AI models due to its high quality and efficiency.<br><br>* **fp16_triton**: FP16 precision optimized through the Triton framework for faster computing. |
|offload_policy |Whether to enable the offload policy. Valid values:<br><br><br>* **all**: enable<br><br>* **off**: (default) disable |
|offload_step |The execution step size of resource unloading. One unloading operation is performed per step. |
|offload_batch |The batch size for resource unloading, which affects the efficiency of the unloading operation and the fluctuation range of GPU memory. |
|bf16_to_fp8 |Whether to quantize activation values from BF16 to FP8.<br><br><br>* **all**: enable.<br><br>* **off**: (Default) Does not enable it.<br><br><br>> **warning**<br><br><br>> This feature only applies to GPU resources in the ecs.hpcpni3ln instance family and the ecs.pni3l instance family.<br> |

### OpenVefuser LoraLoader ModelOnly

|Parameter |Description |
|---|---|
|mode name |The name or path of the LoRA model. |
|strength |The strength of applying the LoRA model. A higher value results in a more distinct style. |

### OpenVefuser KSampler

|Parameter |Description |
|---|---|
|seed |The seed value, which is a random number generated during denoising. When the `seed` value and other parameter configurations are consistent, the generated image is reproducible. Different `seed` values achieve different random results. |
|control after generate<br><br> |Controls the behavior of the `seed` after it is generated. Valid values:``<br><br><br>* **fixed**: Keeps the seed unchanged.<br><br>* **increment**: Increases the seed by 1 each time.<br><br>* **decrement**: Decreases the seed by 1 each time.<br><br>* **randomize**: Selects a new random seed for each generation to prevent repetitive results. |
|steps |The number of sampling steps, which is the number of denoising iterations. More steps achieve higher generation quality but take longer. |
|cfg |The guidance strength of the prompt. A higher value exerts a stronger influence on the generated result, but excessively high values may cause image distortion. |
|sampler_name |The sampling algorithm. For the workflow described in this topic, `uni_pc` is selected, which performs sampling quickly. Different algorithms (such as `euler` and `ddim`) will affect the output and speed. |
|scheduler |The noise scheduling policy, which controls the pace of noise variation during sampling. This parameter affects generation quality and efficiency. |
|denoise |The denoising intensity. The value range is 0 to 1.0. The value 1.0 indicates complete denoising, which generates entirely new content based on the initial latent variable. A value less than 1 indicates that the original content is modified.<br><br>A higher value results in greater changes in the picture. In most cases, a low value is used for high\-definition retouching. |

## Usage instructions

The following document introduces the officially proven practices. To achieve the expected results and comply with the Vital Kubernetes Engine (VKE) [Limits](https://docs.byteplus.com/en/docs/vke/Limits), you need to strictly follow the procedures (or operate on the recommended resources) in this document. If you would like do it in your own way, please contact the corresponding BytePlus account manager first for consultation.

## Preparation

Before you use the ComfyUI application, you need to prepare the required cloud service resources, environment, and other dependencies for ComfyUI.

|Cloud service |Required |Preparation |Reference |
|---|---|---|---|
|GPU Cloud Computing |Yes |Provides GPU computing resources. The **ecs.gni3cl.11xlarge** instance type is recommended for image generation described in this topic.<br><br>> **tip**<br><br><br>> [**Beta**] The preceding GPU Cloud Computing instance types are in beta. Contact your account manager of BytePlus to apply for a beta trial.<br> |[GPU Cloud Computing instance types](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types) |
|VKE |Yes |Provides managed clusters for heterogeneous computing for deploying the ComfyUI application. |[Managed clusters for heterogeneous computing of VKE](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster) |
|TOS |Recommended |Achieves persistent storage for the ComfyUI application.<br><br>> **tip**<br><br><br>> TOS storage can be mounted to containers only via [FSX](https://docs.byteplus.com/en/docs/vke/FSX_client_introduction). If you use existing managed VKE clusters for heterogeneous computing, make sure that [csi\-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on) and [fsx\-service](https://docs.byteplus.com/en/docs/vke/fsx-service-add-on) add\-ons are installed in the clusters. These add\-ons are automatically installed in newly created managed clusters for heterogeneous computing.<br> |[TOS storage types](https://docs.byteplus.com/en/docs/tos/docs-storage-type) |
|IAM |Required when TOS is used |Obtains the API access keys (AK and SK) of IAM to access TOS through VKE. |[Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys) |
|APIG |Optional |Achieves Layer 7 routing through APIG instances. These instances are required in session persistence scenarios.<br><br>> **warning**<br><br><br><br>* > We recommend using a standard API Gateway instance that is **v4.0.0** or later. You can view gateway details on the**Instance Overview** page of the target instance in the [API Gateway](https://console.byteplus.com/veapig) console.<br><br><br>* > If the API Gateway instance version does not meet the requirements, contact your BytePlus account manager to upgrade the instance version.<br> |[APIG instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance) |
|Internet express |Recommended |Add\-on installation requires content pulled from GitHub and HuggingFace, and the Internet Express service.<br><br>> **warning**<br><br><br><br>* > Internet express needs to be associated with the VPC of the cluster where the ComfyUI application is deployed.<br><br><br>* > [**Beta**] Internet express is currently in beta. Contact your account manager of BytePlus to apply for a beta trial.<br> |None |

## Step 1: Deploy the ComfyUI application

Deploy your ComfyUI application by using the ComfyUI application template provided by ServingKit. The following table describes specific configurations in this example. For other parameter configurations and detailed operations, see [Deploying the ComfyUI application](https://docs.byteplus.com/en/docs/vke/Deploying_ComfyUI).

|Parameter |Description |
|---|---|
|**Select framework and orchestration** ||
|Deployment method |Select **Predefined template deployment**. |
|Model |Select **Qwen\-Image\-Edit **  and **Qwen\-Image\-Edit2509**. |
|**Application configuration** ||
|ComfyUI configuration |We recommend selecting **Permanent storage** for **Storage location**. You can configure other parameters according to your application.<br><br>ServingKit will create the commonly used directories of ComfyUI in the corresponding paths, including the `custom_nodes`, `input`, `output`, `models`, and `user` directories. |
|**Instance configuration** ||
|Instance specification |Set the **Number of GPU cards** parameter to **2**. Specify other parameters based on your business requirements. |
|More configuration |* **Environment variables**: When you install add\-on nodes, you need to pull content from GitHub. Therefore, we recommend that you configure Internet express by using environment variables to accelerate the network. This prevents installation failures.<br><br>   Configure the following environment variables for Internet express in **Proxy mode**.<br><br>   * For Environment variable 1, set Key to `http_proxy` and set Value to `http://{acceleration IP}:3128`.<br><br>   * For Environment variable 2, set Key to `https_proxy` and set Value to `http://{acceleration IP}:3128`.<br><br>   * For Environment variable 3, set Key to `no_proxy` and set Value to `mirrors.ivolces.com`.<br><br>   > **warning**<br>   <br><br>   * > Make sure that Internet express is associated with the VPC of the cluster where the ComfyUI application is deployed.<br>   <br><br>   * > Internet Express is available in two modes: **proxy mode** and **routing mode**. If you enable **routing mode** for Internet Express, you do not need to configure this environment variable.<br>   <br><br>* Keep the default values of other parameters. |
|**Service configuration** ||
|API Gateway |Enable API Gateway and associate the prepared APIG instance.<br><br>> **warning**<br><br><br>> Make sure that the selected APIG instance and the cluster where the application is deployed are located in the same VPC.<br> |

## Step 2: Access the ComfyUI application

After you deploy the application, go to the **application details** page. Click the **Service overview** tab and copy the value of the **Service domain names** parameter in the **Service configuration** section. Enter the domain name in the address bar of your browser to access the ComfyUI application.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81cdaf82321bb8ae8b9dd2bfa3859daf.png)

## Step 3: Use the ComfyUI application to achieve the universal migration capability

1. Download the workflow JSON file and prepare images for testing.

   **Workflow JSON file**

[ServingKit-Workflow-Qwen-Image.json](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2209cf09dcfcf5e990370c755cc0863f.json)

   **Test case image**

> **tip**

   > The test case pictures are AI\-generated. You can prepare your test case pictures.

   [demo-pictures.zip](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_333e16b83890089e9ad735b19fd28649.zip)

2. On the interface of the ComfyUI application, click the drop\-down arrow icon in the upper\-left corner, and click **File** \> **Open** to open the workflow JSON file downloaded in the previous step.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b8bcf77adcb07425377e41b7b258255.png)

   After you open the JSON file, you will be prompted that nodes are missing. Click **Open Manager**. In the pop\-up message, click **Install All Missing Nodes**.

   > **tip**

   > The ComfyUI application deployed through the ServingKit application template has comfyui\-manager installed by default. Therefore, you can directly install missing nodes on the interface of the ComfyUI application.

   After you install the nodes, restart the service based on the on\-screen prompts. After the service is restarted, you can check that all workflow nodes are normal.

   > **tip**

   > The content installed by add\-on nodes is saved in the mounted TOS bucket. Therefore, no reinstallation is required for subsequent restarts or updates.

3. In the image loading section, upload the test case pictures prepared in Step 1, and update the prompt in the TextEncodeQwenlmageEdit section.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a8429900c0e51ddd7bcab7acbf0ed9b.png)

4. Click **Run** and wait for the task to complete. Then, you will see that the clothing of the model has been replaced, which achieves the migration result.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a65585ba563706b50b2a56c01ba4f60.png)

5. After you confirm that the expected result is achieved, click the drop\-down arrow icon in the upper\-left corner and click **File** \> **Save** to save the pipeline. Subsequently, you can directly open this workflow on the workflow interface and select appropriate pictures and scenarios to perform the universal migration operation.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b0efaba39091838272cb7c062e044d25.png)

## Subsequent operations

You can modify parameter configurations based on the workflow node parameter descriptions in the **Solution introduction** section to achieve different results.
