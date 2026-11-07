---
title: "Build online model inference services based on Ray Serve"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Build_online_model_inference_services_based_on_Ray_Serve"
---

Ray Serve is a model online service library built on top of the Ray distributed computing framework, providing the capability to build high\-performance, low\-latency online inference services based on given models. Building online inference services with Ray Serve offers the following advantages:


* **Heterogeneous computing**: Supports flexible deployment and operation of models on CPU or GPU nodes according to the resource requirements of the model.

* **Elastic scaling**: Supports automatic adjustment of cluster size within a preset range based on request load, balancing inference performance and resource overhead. Volcano EMR Ray further optimizes the community Autoscale capability, supporting custom scaling metrics and strategies.

* **Failure tolerance**: Supports multi\-replica deployment to withstand single replica failures, and provides system\-level and application\-level fault recovery capabilities. When replicas or nodes fail, service continuity is ensured through retry and rescheduling mechanisms.

* **Multi\-model integration**: Supports orchestrating and deploying multiple models within a single Ray Serve application. These models can provide services independently or in combination, and resource scheduling and elastic scaling can be configured separately for each model.

* **Dynamic batching**: Supports merging multiple requests based on request count and time span, then sending them in batches to the model for processing. By leveraging hardware parallel computing capabilities (such as GPUs), throughput can be significantly improved while maintaining low latency as much as possible.

* **Model multiplexing**: For use cases requiring the loading of a large number of models (such as personalized recommendation), a single application can load multiple models and provide services externally. However, due to resource considerations, the number of models that can be loaded per replica within the application is also limited. Meanwhile, Ray Serve will attempt to route requests to replicas where model loading has already been completed, in order to balance inference performance and resource consumption.

* **Support native integration with vLLM for inference acceleration**: Provides native integration capabilities with the vLLM engine. With simple configuration, you can leverage multiple optimization techniques introduced by vLLM in inference scenarios, such as PagedAttention and dynamic batching, to improve model inference performance and resource utilization.

* **Support integration with Nvidia Triton Inference Server for complementary advantages**: Triton has undergone extensive optimization for single\-node inference scenarios to enhance performance. However, production deployment also requires capabilities such as load balancing, elastic scaling, fault tolerance, and model orchestration. By integrating Triton, both sides' advantages can be effectively combined. In the integrated setup, Triton serves as the single\-node model inference service, while Ray Serve is responsible for upper\-level routing and management, providing overall request routing, load balancing, multi\-model orchestration, and elastic scaling capabilities.

* The concise programming model facilitates local development and debugging, and only minor modifications are needed for online deployment.

* Python Native。


<span id="fb0a09a0"></span>
## Deploy Ray Serve jobs

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the EMR on VKE mode only supports deploying Ray Serve applications in already created Ray Clusters and does not support deployment via RayService.</div>


Refer to [EMR Ray on VKE product documentation](https://docs.byteplus.com/docs/E-MapReduce/109433) to create a Ray Cluster on the cluster details page via the  **“Service List \- Ray \- Deployment Topology \- KubeRayOperator \- Add Ray Cluster”**  path, and create it using YAML. Since Ray Serve applications need to open ports to provide HTTP services externally, you must modify the Ingress configuration in the YAML template and add the following content:

```YAML
- backend:
    service:
      name: ingress-release-name-head-svc
      port:
        number: 8000
  path: /ingress-namespace/ingress-release-name-serve/(.*)
  pathType: Exact
```


After the Ray Cluster is successfully created, you need to go to the VKE product console, log in to the cluster's head node, and then execute the `serve deploy` command to submit your Ray Serve application.

<span id="28f7ef74"></span>
## Inference acceleration

vLLM and Triton Inference Server (strictly speaking, Triton Inference Server + Backend) are currently the two mainstream inference acceleration engines on the market, each providing efficient solutions for different scenarios. The core differences between the two are shown in the following table:


| |vLLM |Triton |
|---|---|---|
|**Functionality** |Designed specifically for LLM inference, optimized for high throughput and low GPU memory usage scenarios |General\-purpose inference server, supports mixed deployment of multiple models and frameworks, focuses on flexibility and enterprise\-grade features |
|**Model support** |Focused on the Transformer architecture, but currently only supports models based on the PyTorch framework |Supports multiple deep learning framework models, including TensorFlow, PyTorch, ONNX, and more, as well as other types of models such as computer vision models, speech models, and language models. |
|**Performance optimization** |* Uses PagedAttention technology to manage the KV Cache in pages, reducing memory fragmentation and improving GPU memory utilization.<br><br>* Supports dynamic request batching, increasing throughput by dynamically merging inference requests. |Enhances service throughput through dynamic batching and multi\-GPU parallel inference, while reducing latency with backend integrations such as TensorRT and ONNX. |
|**Deployment complexity** |Relatively easy; for some simple scenarios, it can even be started without complex configuration. |Relatively complex; requires writing a series of configuration files to describe the model's input and output, data types, batch size, and more. |


Although vLLM and Triton demonstrate outstanding performance in inference scenarios, they primarily focus on single\-machine scenarios, whereas online model inference typically requires multi\-machine distributed collaboration to ensure service availability and scalability. By integrating with Ray Serve, it is possible to leverage the inherent advantages of both vLLM and Triton while compensating for their shortcomings in distributed scenarios.

<span id="f7f84b6b"></span>
### Integrate vLLM to accelerate inference

vLLM is an open\-source LLM inference and serving engine developed by the University of California, Berkeley (UC Berkeley), featuring high throughput and memory efficiency. This engine utilizes various optimization techniques such as PagedAttention, dynamic batching, and multi\-GPU parallel inference to provide fast, flexible, and user\-friendly inference and serving for LLM scenarios. For more information about vLLM, you can visit the [official documentation](https://docs.vllm.ai/en/latest/index.html).

Ray Serve has provided native support for vLLM since version 2.43. By integrating vLLM, it is possible to further optimize inference speed and resource utilization for LLM serving scenarios while leveraging the inherent advantages of Ray Serve.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LLM APIs, as a newly introduced feature in Ray, greatly simplify the complexity of deploying LLMs with Ray Data/Serve integrated inference acceleration engines (such as vLLM and SGLang). However, the related APIs are rapidly iterating and evolving. If the above example does not run properly, visit <a href="https://docs.ray.io/en/latest/serve/llm/serving-llms.html">the official documentation</a> to learn about the latest API definitions.</div>


This section uses the Llama 3.2 model to demonstrate how to integrate Ray Serve with vLLM, as shown in the following example:

```Python
from ray.serve.llm import LLMConfig, LLMServer, LLMRouter

llm_config = LLMConfig(
    model_loading_config=dict(
        model_id="meta-llama/Llama-3.2-1B-Instruct",
        model_source="/opt/workspace/models/llama/Llama-3.2-1B-Instruct"
    ),
    deployment_config=dict(
        autoscaling_config=dict(
            min_replicas=1, max_replicas=5,
        )
    ),

    # Pass the desired accelerator type (e.g. A10G, L4, etc.)
    accelerator_type="A10G",

    # You can customize the engine arguments (e.g. vLLM engine kwargs)
    engine_kwargs=dict(
        tensor_parallel_size=2,
        pipeline_parallel_size=2,
        dtype='half'
    )
)

# Deploy the application
deployment = LLMServer \
    .as_deployment(llm_config.get_serve_options(name_prefix="vLLM:")) \
    .bind(llm_config)
app = LLMRouter.as_deployment().bind([deployment])
```


By executing the `serve deploy` command, you can deploy the above Ray Serve application to the target Ray Cluster. After the application starts successfully, you can send inference requests to the model using the following POST request:

```Bash
curl --location 'http://127.0.0.1:8000/v1/chat/completions' \
--header 'Content-Type: application/json' \
--data '{
  "model": "meta-llama/Llama-3.2-1B-Instruct",
  "messages": [
    {
      "role": "user",
      "content": "介绍一下 Ray Serve 集成 vLLM 的优势"
    }
  ]
}'
```


<span id="076f2a0d"></span>
### Integrate Triton to accelerate inference

Triton Inference Server (referred to as Triton) is a high\-performance inference server developed by Nvidia, supporting multiple model frameworks and hardware platforms. For more information about Triton, refer to the [official documentation](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/introduction/index.html). Triton and Ray Serve have similar roles, but each also has its own advantages:


* Ray Serve natively supports distributed operation, allowing orchestration and deployment of multiple models within a single application to meet the needs of complex inference scenarios. At the same time, its built\-in elastic scaling capability effectively balances user requests and resource overhead.

* Triton mainly focuses on single\-machine inference scenarios and is compatible with various hardware platforms. By introducing technologies such as dynamic batching and multi\-GPU parallel inference, the system enhances model inference performance, supports integration of various model frameworks as Backend plugins, and provides a unified external access API.


As shown in the figure below, integrating Ray Serve with Triton allows the advantages of both to complement each other:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/279295887eb74a4884f779e58e6a764d~tplv-goo7wpa0wc-image.image" width="3809px" /></div>


This subsection will explain how to achieve integration between Ray Serve and Triton. In integration mode, Ray Serve primarily handles traffic handling, load balancing, model orchestration, and elastic scaling, while Triton acts as a standalone model inference service, providing model loading, inference, and acceleration capabilities. Taking the Llama 3.2 model as an example, before starting the integration, you need to ensure the following are completed:


1. Compile the model file to generate a TensorRT engine, and use the TensorRT\-LLM Backend to integrate with Triton. For specific operations, refer to the [official documentation](https://github.com/NVIDIA/TensorRT-LLM/tree/main/examples/llm-api).

2. Configure the Triton model repository using the built\-in model integration configuration template of the TensorRT\-LLM Backend, so that Triton can recognize and deploy the above model. For specific operations, refer to the [official documentation](https://github.com/triton-inference-server/tutorials/blob/main/Popular_Models_Guide/Llama2/trtllm_guide.md).


As shown below, the built\-in model integration configuration template of the TensorRT\-LLM Backend is located in the `all_models/inflight_batcher_llm` directory and mainly consists of four modules, each corresponding to a different stage of the model execution process.

```Plain
.
|-- ensemble
|   |-- 1
|   `-- config.pbtxt
|-- postprocessing
|   |-- 1
|   |   `-- model.py
|   `-- config.pbtxt
|-- preprocessing
|   |-- 1
|   |   `-- model.py
|   `-- config.pbtxt
`-- tensorrt_llm
    |-- 1
    |   |-- config.json
    |   |-- model.py
    |   `-- rank0.engine
    `-- config.pbtxt
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The preprocessing module contains scripts for tokenizing input, supporting the conversion of user\-entered prompt strings into input_id lists.</div>


* <div data-tips="true" data-tips-type="tip">The postprocessing module contains scripts for de\-tokenizing output, supporting the conversion of the model's output_id lists into strings that users can understand.</div>


* <div data-tips="true" data-tips-type="tip">The tensorrt_llm module contains model files compiled and generated by the user, which are loaded and used to call the user\-defined model for inference operations.</div>


* <div data-tips="true" data-tips-type="tip">The ensemble module is used to connect the preprocessing, tensorrt_llm, and postprocessing modules together, instructing Triton on how to transfer data between these modules to build a complete inference workflow.</div>



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Since the ensemble module serves as the external interface for the entire inference model workflow, the loaded model is named ensemble.</div>


* <div data-tips="true" data-tips-type="warning">For models that require GPU resources, the <code>num_gpus</code> parameter must be configured; otherwise, Ray Serve will not schedule the Deployment to GPU nodes, resulting in Triton failing to load.</div>



Triton provides the [In-Process Python API](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/client_guide/python.html) to support integration with the Python ecosystem, which is more convenient compared to sending HTTP requests. The following example demonstrates the integration of Ray Serve and Triton using the Triton In\-Process Python API:

```Python
import ctypes
from typing import Iterable

import numpy as np
import tritonserver
from fastapi import FastAPI
from ray import serve

api = FastAPI()


@serve.deployment(
    ray_actor_options=dict(
        num_gpus=1
    )
)
@serve.ingress(api)
class Generator:

    def __init__(self, model_path: str):
        import torch
        assert torch.cuda.is_available(), RuntimeError("CUDA is not available")

        self._server = tritonserver.Server(
            tritonserver.Options(
                model_repository=model_path,
                log_info=True,
                log_warn=True,
                log_error=True
            )
        )
        self._server.start(wait_until_ready=True)
        self._model = self._server.model("ensemble")

    @api.get("/generate")
    def generate(self, query: str):
        if not self._model.ready():
            raise RuntimeError("Model is not ready, Please try again later.")

        resp = list(self._model.infer(inputs={
            "text_input": [[query]],
            "max_tokens": np.array([[1024]], dtype=np.int32)
        }))[0]

        return self._to_string(resp.outputs["text_output"])

    def _to_string(self, tensor: tritonserver.Tensor) -> str:
        """
        This method is copied from https://github.com/triton-inference-server/server
        """
        ...


app = Generator.bind("/opt/workspace/models/llama/triton")
```


By executing the `serve deploy` command, you can deploy the above Ray Serve application to the target Ray Cluster. After the application starts successfully, you can send inference requests to the model using the following POST request:

```Bash
curl --location 'http://127.0.0.1:8000/v1/chat/completions' \
--header 'Content-Type: application/json' \
--data '{
  "model": "meta-llama/Llama-3.2-1B-Instruct",
  "messages": [
    {
      "role": "user",
      "content": "介绍一下 Ray Serve 集成 Triton Inference Server 的优势"
    }
  ]
}'
```
