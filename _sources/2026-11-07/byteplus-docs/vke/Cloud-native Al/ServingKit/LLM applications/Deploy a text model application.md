---
title: "Deploy a text model application"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deploying_a_text_model_AI_inference_application"
---

This topic describes how to deploy LLM\-based AI inference applications such as DeepSeek, Qwen, GLM, Kimi, and Gemma by using the AI application templates from the ServingKit.

## Usage instructions

* To ensure the successful deployment of the text model, which involves multiple add\-ons that depend on each other and have complex configurations, you need to strictly follow the instructions in this topic.

* To achieve the expected results and conform to the [limits](https://docs.byteplus.com/en/docs/vke/Limits) of Vital Kubernetes Engine (VKE), you need to perform operations by following the solution described in this topic or on the recommended resources. If you need to change your solution, you can consult the Account Manager of the BytePlus.

* Do not use mGPU on GPU resources.

* The complete deployment process may depend on the following BytePlus beta capabilities. In your deployment, apply for beta capabilities that are necessary in your actual business scenarios.

   |**Beta feature/resource** |**Related service** |**Description** |
   |---|---|---|
   |High Performance Computing Optimized instance family |[GPU Compute Service](https://www.byteplus.com/en/product/gpu) |The instance families of GPU Compute Service, which provide computing power for AI inference applications.<br><br>In GPU Compute Service, some instance types of the High Performance Computing Optimized instance family and the instance types of the GPU Accelerated instance family are at the beta stage. For example, the ecs.hpcpni3ln instance type, which is required for deploying most AI application templates for ServingKit, is currently at the beta stage. |
   |GPU Accelerated instance family |||
   |Capability of mounting nodes to local disks |[Vital Kubernetes Engine](https://www.byteplus.com/en/product/vke) |You can configure the local disk mounting in the VKE cluster. |
   |Elastic Instant Cache (EIC) |EIC |A high\-performance distributed KV Cache service launched by the BytePlus storage team for large language model (LLM) inference.<br><br>Only some AI application templates support KV Cache. Apply to use this service based on your business requirements and the capabilities supported by the template. |

## Preparation

* You can create a managed heterogeneous computing cluster of VKE in advance or create a cluster when you deploy the model. For details, see [Creating managed heterogeneous computing clusters](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster).

* (Optional) If you want to expose the service by using API Gateway (APIG), you need to prepare an APIG instance. You can create an APIG instance in advance or when you deploy the model. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* (Optional) To enable intelligent routing, you need to install the apig\-controller add\-on in the cluster. For detailed instructions, see [apig-controller](https://docs.byteplus.com/en/docs/vke/apig-controller-add-on?lang=en).

## Procedure

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **ServingKit \> AI application templates**.

3. On the **ServingKit AI application templates** page, find the target text model and click **Deploy** in the model section.

4. On the **Deploy** page, specify the parameters of the model.

   |**Parameter** |**Description** |
   |---|---|
   |**Select framework and orchestration** ||
   |Selected templates |The name of the selected template, the inference engine that corresponds to the model, and the parallel policy are displayed.<br><br><br>* Inference engine and framework: Compatible with mainstream inference engines and frameworks such as vLLM, SGLang, and Dynamo. Provided models include LLM models such as DeepSeek and Qwen, and vision language models such as ComfyUI.<br><br>   This topic uses LLM models such as DeepSeek and Qwen as an example.<br><br>* Parallelism policy: Application templates for LLM models such as DeepSeek and Qwen support the **PD co\-location** architecture and the **PD disaggregation** architecture.<br><br>   Certain templates may not support PD disaggregation. For support status of a template, see the content in the VKE console. |
   |Image |The image of the inference engine. You can select **Built\-in** to specify a built\-in image or select **Custom** to provide the address of a third\-party image or an image in Container Registry (CR). |
   |**Application configuration** ||
   |Application name |Set an application name that complies with the on\-screen naming requirements and a description. You can also use the automatically generated name. |
   |**Instance configuration**<br><br>> **warning**<br><br><br><br>* > If you select the **PD disaggregation** architecture, you need to apply the following **instance configuration** respectively to **Decode**, **Prefill**, and **Sglang\-router** (optional). For details about PD disaggregation architecture, see [Terms](https://docs.byteplus.com/en/docs/vke/Servingkit_overview#gbZqhB2i).<br><br><br>* > **Sglang\-router** is a SGLang\-based high\-performance request router and load balancer for PD disaggregation architecture.<br> ||
   |Instance specification |Instances are the entities that implement inference models. Set the **Number of instances** and **Single instance GPUs** for running the inference model as needed.<br><br>ServingKit automatically configures the **number of GPUs per instance** based on the inference engine and parallel strategy you select. |
   |RDMA settings |You can select **Enable RDMA network** to achieve interconnection between instances through high\-speed RDMA networks and to improve communication efficiency.<br><br>After enabling the RDMA network, you can click the ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4ea1311d39bf75b2730341f9bebec63.png)icon to enter the number of RDMA cards, or leave it blank. The system will automatically specify the number based on the value of **Resource configuration**. We recommend enabling the system automatic calculation feature.<br><br>> **tip**<br><br><br>> By default, RDMA is enabled for Prefill and Decode and disabled for Sglang\-router. You can modify the settings as needed.<br> |
   |Resource configuration |Select the resources of the managed heterogeneous computing cluster for VKE to deploy the model application, and prepare deployment resources based on the on\-screen **Deployment checklist**.<br><br><br>* **Select existing**: Select a created managed heterogeneous computing cluster of VKE and select the resources of the cluster, such as the namespace and the node pool, based on on\-screen prompts.<br><br>* **Automatically create**: When you deploy the model, you can create a custom managed heterogeneous computing cluster of VKE. For a detailed parameter description, see [Creating managed heterogeneous computing clusters](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster).<br><br><br>> **warning**<br><br><br>> If you select **Enable RDMA network**, you need to select a pool of **GPU Accelerated** nodes. Only this node type supports interconnections through a high\-speed RDMA network.<br> |
   |Start command |Set the startup script and port number for the AI application. No modification is required by default. To specify a custom port, install additional node configuration during startup and make modifications as needed. |
   |More configurations |* **Health check**: Configure health checking for the AI application as needed. You can specify the **Liveness check**, **Ready check**, and **Start check** parameters. You can test whether workloads are normal by using an HTTP, TCP, gRPC, or command check.<br><br>* **Environment variables**: Create environment variables. Environment variables are injected into the container during application deployment.<br><br>* **Privileged container**: After you enable this feature, privileged containers deployed on Linux systems can control the network stack or access devices on hosts.<br><br>* **KV Cache**: Specify a data cache mechanism of the AI application. ServingKit supports high\-performance distributed KV cache based on Elastic Instant Cache (EIC).<br><br>   > **tip**<br>   <br><br>   > Only some models support **KV Cache**. You can check the supported models in the console and configure this item as needed.<br>    |
   |**Service configuration** ||
   |API Gateway |If you want to configure Ingress by using APIG to process inbound traffic to the model, **enable** APIG and select the target APIG instance.<br><br><br>* **Select existing**: Use an existing APIG instance as the route for the current application. You can also click **Create API Gateway instances** to go to the [APIG console](https://console.byteplus.com/veapig) to create a custom instance. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).<br><br>* **Automatically create**: When you deploy the AI application, an APIG instance with fixed instance specifications and configurations is automatically created by ServingKit. A newly created APIG instance will incur fees. For details, see [APIG service billing](https://docs.byteplus.com/en/docs/apig/Billing_overview).<br><br><br>> **tip**<br><br><br>> When you use an existing APIG instance to expose the model service in the cluster, take note of the following parameter or feature configurations:<br><br><br><br>* > **Region**: It needs to be consistent with the region of the AI application.<br><br><br>* > **Circuit breaking**: When some GPU instances malfunction, the common method is to take the faulty instances offline to eliminate failures. At the same time, it is necessary to retain the faulty instances for troubleshooting later. You can isolate the faulty instances by configuring a circuit breaking rule for the APIG instance. For details, see [Circuit breaking policies](https://docs.byteplus.com/en/docs/apig/Circuit_breaking_policy).<br> |
   |Intelligent routing |Enable it to use AI Gateway to distribute inference traffic. The [AI Gateway](https://docs.byteplus.com/en/docs/apig/What_is_the_AI_Gateway) provides a standardized interface for calls to different models, improving the availability and observability of model calls. |
   |**More configurations** ||
   |Update policy |The update policy is enabled by default.  It follows the InPlaceUpdate policy, which performs in\-place updates. The InPlaceUpdate policy allows you to directly update the existing RoleSet. During the update, additional GPU resources are not used. |
   |Model download |Select the model download method. The model will be automatically downloaded to all nodes in the node pool for the application. For the descriptions of related terms, see [Terms](https://docs.byteplus.com/en/docs/vke/Servingkit_overview#gbZqhB2i). |

5. Click **Confirm** to complete the configuration.

   Please wait patiently as the application creation takes approximately 15 to 20 minutes. You can also click **Back to AI application list** to view the application status, or click **Go to AI application template** to view AI application template details or create another AI application.

## Subsequent operations

After you deploy the AI application, you can manage, view, and use the AI model application on the **List of AI applications** page. For details, see the following documentation:

* [Managing and using AI applications](https://docs.byteplus.com/en/docs/vke/Managing_and_using_AI_applications)

* [AI application observability](https://docs.byteplus.com/en/docs/vke/AI_application_observability)
