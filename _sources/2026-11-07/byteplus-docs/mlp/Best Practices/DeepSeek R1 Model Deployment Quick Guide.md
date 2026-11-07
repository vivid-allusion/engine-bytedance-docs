---
title: "DeepSeek R1 Model Deployment Quick Guide"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/DeepSeek_R1_Model_Deployment_Quick_Guide"
---

As an open cloud and AI service provider, BytePlus offers both Skylark large\-scale and open\-source model solutions to meet the AI business needs of enterprises. As the complexity of open\-source model building increases significantly, BytePlus can provide a complete solution of open\-source model reinforcement learning fine tuning, distillation, and large\-scale inference, including DeepSeek, to help you achieve the ultimate balance between efficiency, performance, and optimal inference cost.

The DeepSeek\-R1 (MoE architecture, 671B) and series of DeepSeek\-R1\-Distill models released by DeepSeek achieve the same level of performance as similar models, with a cost reduction of 90% to 95%. They attract global attention with open\-source models, algorithm innovation, and extreme cost performance.

Now, you have the flexibility to choose from BytePlus ModelArk, Machine Learning Platform, and GPU server deployments to call DeepSeek\-R1 full\-scale models. In the coming months, BytePlus will continue to introduce PD separation, performance optimization capabilities, and provide an end\-to\-end AI Infra solution for the training and inference of your self\-developed vertical domain model.

To provide you with a complete set of solutions for better open\-source models, I believe BytePlus is also a better choice.

<span id="18afba33"></span>
# Procedure

Provides an example of DeepSeek\-R1\-Distill\-Llama\-32B model deployment based on Hopper (ml.hpcpni3ln.45xlarge) specification, so that you can use the DeepSeek R1 model more intuitively, flexibly and safely.

<span id="f5e06d67"></span>
## Resource preparation

Prepare resources for cloud infrastructure, mirror vaults, VPCs, Machine Learning Platform related products, Create machine learning platform queues. For details, please contact BytePlus sales or other preferred communication methods.

<span id="419a24b5"></span>
## Model download (choose one of the two)

<span id="e775c42b"></span>
### Machine Learning Platform Preset Model Download (Recommended)

For mainstream and leading open\-source models, BytePlus can provide TOS Torch Object Storage preset model weight files to facilitate customer self\-replication and accelerate testing.

Log in to the WebIDE of the Machine Learning Platform Dev boxes, open the end point, and download the preset model weight file:

Create Dev boxes in the Machine Learning Platform, select the queue computing resource configuration, access configuration, and mount shared file system. The user needs to use the mirror url at the mirror entrance: enter mirror [vemlp-ap-southeast-1.cr.volces.com/preset-images/pytorch:](https://docs.byteplus.com/en/docs/186/vemlp-ap-southeast-1.cr.volces.com/preset-images/pytorch:)`2.4.1 -cu12.4.1-py3.10-ubuntu20.04`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dc36727191e42b0b94aa300aa37451d~tplv-goo7wpa0wc-image.image) </span>

```Shell
# Install tmux on the development machine and create a new session to prevent the abnormal disconnection of the remote connection, which may cause the interruption of the model weight file download.
sudo apt update
sudo apt install tmux -y
tmux new -s model

# Initialize the configuration. Enter the corresponding Access Key ID (AK) and Secret Access Key (SK) of the account in access_key_id and secret_access_key respectively.
# In the tosutilconfig, it is recommended to use the internal network domain name of BytePlus for the endpoint, which enables faster transmission. 
vim ~/.tosutilconfig

# Tosutil is a command-line tool for accessing and managing the BytePlus Torch Object Storage (TOS). The tosutil tool is pre-installed on the Dev boxes and can be used with simple configuration.
# View the file directory in the tos bucket
tosutil ls tos://preset-models-ap-southeast-1/deepseek-ai // The part after this is the name of the configured remote connection bucket
 
# Execute the command to copy the preset model weight file from the object storage bucket to the PFS of the current account. Take the preset model weight file in the ap-southeast-1 region as an example, and the bucket name is: tos://preset-models-ap-southeast-1
# For more preset model weight files, you can contact BytePlus to obtain them.
# It takes about 8 minutes and 17 seconds for 320GB.
tosutil cp tos://preset-models-ap-southeast-1/deepseek-ai/DeepSeek-R1-Distill-Llama-32B/ /file_system/common-models/ -r -u -j=32 -p=4 -nfj=16 
# Similarly, if you need to synchronize the model weight file to the object storage of your own account, you can execute the command for the reverse operation.
tosutil cp /file_system/common-models/DeepSeek-R1-Distill-Llama-32B/ tos://${repleace_with_your_tos_bucket_name} -r -u -j=32 -p=4 -nfj=16 
```


Finally, the model DeepSeek\-R1\-Distill\-Llama\-32B: `/file_system/common-models/DeepSeek-R1-Distill-Llama-32B`You can continuously adjust the data parameters and model parameters through the Dev boxes, develop and build the model, and then package the model configuration to generate a new environment mirror.

> Tips：

> 1. Please note that the mirror and model paths need to be adjusted appropriately according to the location of the Region. For example, DeepSeek\-R1 file is located in the ap\-southeast\-1 Region, and the TOS path is tos://preset\-models\-ap\-southeast\-1/deepseek\-ai/DeepSeek\-R1; if the DeepSeek\-R1 file is located in the cn\-hongkong Region, the TOS path is adjusted to tos://preset\-models\-cn\-hongkong/deepseek\-ai/DeepSeek\-R1. The mirror address is the same.


<span id="206ed401"></span>
### HuggingFace Download

If you download the model file from HuggingFace and encounter various network problems, you can speed up the download through HuggingFace's domestic mirror. Here we use the Dev boxes of the Machine Learning Platform to download DeepSeek\-R1\-Distill\-Llama\-32B model as an example to provide a reference for you to download the model file from HuggingFace yourself. Log in to the WebIDE of the Machine Learning Platform Dev boxes, open the end point, and download the model weight file:

Also, in the Machine Learning Platform Create Dev box, select the queue computing resource configuration, access configuration, and mount shared file system to create. The user needs to use the mirror url at the mirror entrance: enter mirror `vemlp-ap-southeast-1.cr.volces.com/preset-images/pytorch: 2.4.1 -cu12.4.1-py3.10-ubuntu20.04`

```Shell
# Install tmux on the Dev boxes and create a new session to prevent the abnormal disconnection of the remote connection, which may lead to the interruption of the model weight file download.
sudo apt update
sudo apt install tmux -y
tmux new -s model
# Download HuggingFace_hub
pip install -U huggingface_hub

# Set the HF-mirror environment variable
export HF_ENDPOINT=https://hf-mirror.com

# Download the model, and you need to specify the saving location of the model
huggingface-cli download --resume-download deepseek-ai/DeepSeek-R1-Distill-Llama-32B --local-dir /file_system/common-models/DeepSeek-R1-Distill-Llama-32B 
```


<span id="1ee2785a"></span>
## Model deployment

<span id="dc94854a"></span>
### Service configuration

Create inference services and deploy model instances. In the process of deploying the model instance, select your exclusive VPC network environment, API gateway, mirror, configuration entry command, shared file system path and computing resources of the Mount model weight file to achieve one\-click model deployment.

Select enter mirror address in mirror entry: [vemlp-ap-southeast-1.cr.volces.com/preset-images/dockerhub-vllm: v0.7.1 ](http://vemlp-cn-beijing.cr.volces.com/preset-images/dockerhub-vllm:v0.7.1)entry command:

```Shell
# Entry command for the distilled DeepSeek-R1-Distill-Llama-32B model of vllm
python3 -m vllm.entrypoints.openai.api_server --port 50050 --model  /file_system/common-models/DeepSeek-R1-Distill-Llama-32B --served-model-name DeepSeek-R1-Distill-Llama-32B  --tensor-parallel-size 2   --max-num-seqs 64 --max_model_len=2048
sleep inf 30d
# Entry command for starting the distilled DeepSeek-R1-Distill-Llama-32B model with FP8 quantization
python3 -m vllm.entrypoints.openai.api_server --port 50050 --model  /file_system/common-models/DeepSeek-R1-Distill-Llama-32B --served-model-name DeepSeek-R1-Distill-Llama-32B  --tensor-parallel-size 2 --quantization fp8 --kv-cache-dtype fp8_e4m3  --max-num-seqs 64 --max_model_len=2048
sleep inf 30d
# It is recommended to use the SGLang image for DeepSeek R1, which consumes less video memory and has better inference performance optimization.
# vemlp-ap-southeast-1.cr.volces.com/preset-images/sglang:0.4.2
python3 -m sglang.launch_server --model-path  /file_system/common-models/DeepSeek-R1 --tp 8 --trust-remote-code --mem-fraction-static 0.9 --host 0.0.0.0 --port 50050
sleep inf
```


Submit the service, wait for the environment to initialize, and the service enters the running state.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbd6dc5988af4849a51403b52e0f195c~tplv-goo7wpa0wc-image.image) </span>

<span id="0e0587f3"></span>
### Service invocation

In the `inference services details page - deployment`page, to obtain the public network calling address of the instance, configure the calling parameters, and then enter the WebShell of the service instance to initiate a service call test.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cb2d95cde3d4ac3a2a3e85a31afaebc~tplv-goo7wpa0wc-image.image) </span>

```Shell
# cURL statement: Configure the calling parameters for DeepSeek-R1-Distill-Llama-32B
curl https://xx.apigateway-ap-southeast-1.volceapi.com/mlp/s-20250202183843-***/v1/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "DeepSeek-R1-Distill-Llama-32B",
        "prompt": "San Francisco is a",
        "max_tokens": 7,
        "temperature": 0
    }'

# cURL statement: DeepSeek-R1-Distill-Llama-32B can also use the IP:Port format
curl 192.168.32.*:50050/v1/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "DeepSeek-R1-Distill-Llama-32B",
        "prompt": "San Francisco is a",
        "max_tokens": 7,
        "temperature": 0
    }'

# cURL statement: Reference calling example for DeepSeek-R1 or V3
curl -X POST \
  "192.168.32.*:50050/v1/chat/completions" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer EMPTY" \
  -d '{
    "model": "DeepSeek-R1",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful AI assistant"
      },
      {
        "role": "user",
        "content": "Who are you?"
      }
    ],
    "temperature": 0,
    "max_tokens": 8192
  }'
```


You can then view the service's throughput metrics in the live log on the service details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b7e7648f7cb42a8adb33a9ae92ce015~tplv-goo7wpa0wc-image.image) </span>

> For public network access, please confirm the network configuration.

> 1. Private network, subnet, SecurityGroup, select the private network where the load balancer is located, and release the incoming port for the SecurityGroup, such as 50050.

> 2. Port, Add custom port, listen to port 50050, call port arbitrary, use HTTP.

> 3. Load balancing, select the public network type of load balancing to support public network access.


<span id="e5f846fe"></span>
# Communication and reservation experience

If you need to communicate further, you can directly contact the BytePlus sales staff to book an experience. BytePlus provides you with the best framework selection and optimization options to accelerate AI innovation experiments.

<span id="dff99c8c"></span>
# Appendix

<span id="d8e7f726"></span>
## model weight list


|Model |model size |Model (recommended) |Model weight file **address (ap\-southeast\-1 as an example)**  |Inference Engine Start parameter configuration (recommended) |
|---|---|---|---|---|
|DeepSeek\-V3 |FP8:<br><br>700 GB |Hopper GPU 96GiB \* 8 |* https://huggingface.co/deepseek\-ai/DeepSeek\-V3<br><br>* `tos://preset-models-ap-southeast-1/deepseek-ai/DeepSeek-V3` |```Python```<br>```# Using SGLang python3 -m sglang.launch_server --model-path  /file_system/common-models/DeepSeek-V3 --tp 8 --trust-remote-code --mem-fraction-static 0.9 --host 0.0.0.0 --port  50050sleep inf```<br> |
|DeepSeek\-R1 |FP8:<br><br>700 GB |Hopper GPU 96GiB \* 8 |* https://huggingface.co/deepseek\-ai/DeepSeek\-R1/tree/main<br><br>* `tos://preset-models-ap-southeast-1/deepseek-ai/DeepSeek-R1`<br><br>> Notice: Update tokenizer_config json model_max_length to 163840, consistent with the model.<br><br>> Specific huggingface official update issue [https://huggingface.co/deepseek-ai/DeepSeek-R1/commit/2ea4a0b868818283cd62d67f5454971e286eb6a4](https://huggingface.co/deepseek-ai/DeepSeek-R1/commit/2ea4a0b868818283cd62d67f5454971e286eb6a4) |```Python```<br>```# Using SGLang python3 -m sglang.launch_server --model-path  /file_system/common-models/DeepSeek-R1 --tp 8 --trust-remote-code --mem-fraction-static 0.9 --host 0.0.0.0 --port  50050sleep inf```<br> |
|DeepSeek\-R1\-Distill\-Qwen\-7B |BF16: 15.23 GB |Hopper GPU 96GiB \* 1<br><br>L20 48GiB \* 1 |* https://huggingface.co/deepseek\-ai/DeepSeek\-R1\-Distill\-Qwen\-7B<br><br>* `tos://preset-models-ap-southeast-1/deepseek-ai/DeepSeek-R1-Distill-Qwen-7B/` |```Python```<br>```python3 -m vllm.entrypoints.openai.api_server --port 50050 --model /file_system/common-models/DeepSeek-R1-Distill-Qwen-7B --served-model-name DeepSeek-R1-Distill-Qwen-7B  --tensor-parallel-size 2   --max-num-seqs 64 --max_model_len=2048sleep inf 30d```<br> |
|DeepSeek\-R1\-Distill\-Qwen\-32B |BF16:<br><br>65.53 GB |Hopper GPU 96GiB \* 1<br><br>L20 48GiB \* 2 |* https://huggingface.co/deepseek\-ai/DeepSeek\-R1\-Distill\-Qwen\-32B<br><br>* `tos://preset-models-ap-southeast-1/deepseek-ai/DeepSeek-R1-Distill-Qwen-32B/` |```Python```<br>```python3 -m vllm.entrypoints.openai.api_server --port 50050 --model /file_system/common-models/DeepSeek-R1-Distill-Qwen-32B --served-model-name DeepSeek-R1-Distill-Qwen-32B --tensor-parallel-size 2   --max-num-seqs 64 --max_model_len=2048sleep inf 30d```<br> |


<span id="53b7e306"></span>
## Inference engine mirror


|**Environmental requirements** |Docker mirror address |
|---|---|
|Basic environment mirror |cuda124+pytorch2.4<br><br>mlp\-ap\-southeast\-1.cr.bytepluses.com/preset\-images/pytorch:2.4.1\-cu12.4.1\-py3.10\-ubuntu20.04 |
|Preset mirror for vLLM |Version: 0.7.1\-post1<br><br>mlp\-ap\-southeast\-1.cr.bytepluses.com/preset\-images/vllm:v0.8.2 |
|SGLang preset mirror |Version: 0.4.2<br><br>mlp\-ap\-southeast\-1.cr.bytepluses.com/preset\-images/sglang:sglang\-edge0.4.2 |


<span id="763b707f"></span>
## Deployment instance

You can view the deployed instance running status and other information on the instance list tab.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab0b7249307e4de1b09dbb6b8094c42b~tplv-goo7wpa0wc-image.image) </span>
