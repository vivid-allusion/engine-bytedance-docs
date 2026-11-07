---
title: "Best Practices for DeepSeek-V2-Lite Models in MLP"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Best_Practices_for_DeepSeek-V2-Lite_Models_in_MLP"
---

Machine Learning Platform is a set of services for professional algorithm engineers, integrating cloud\-native tools + computing power (GPU, CPU Cloud as a Service), for one\-stop AI algorithm development and iteration platform. This solution will introduce you how to fine\-tune the DeepSeek\-V2\-Lite model and implement inference services deployment in MLP based on Megatron\-Core.

<span id="使用前提"></span>
# premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself.</div>


This solution takes the DeepSeek\-V2\-Lite model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* Activated network/TOS/CFS. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [Console Quick Start -- Torch Object Storage - BytePlus ](https://www.volcengine.com/docs/6349/74830), [Access File Storage Instance -- Cloud File System - BytePlus ](https://www.volcengine.com/docs/6720/107803).

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

   * Resource Specifications: Configure the following resource specifications.

      * CPU instance: 8C/64G/20GB cloud disk.

      * GPU card count: at least 8 cards, best practice is to use one ml.pni2.

   * Mount configuration: Mount TOS bucket and CFS, see [training code how to access TOS - Machine Learning Platform - BytePlus ](https://www.volcengine.com/docs/6459/72362).

   * Mirror address: Configure the following mirror at the custom mirror, fill in the SSH key and Mount TOS. Creating Dev boxes for the first time is expected to take 20 minutes due to the large mirror being pulled.

      ```bash
       vemlp-cn-beijing.cr.volces.com/preset-images/llm:megatron-lm-1.0
      ```
      


<span id="步骤一：准备-deepseek-v2-lite-模型"></span>
# Step 1: Prepare the DeepSeek\-V2\-Lite model


1. Enter the Dev boxes.

   1. Login [Account Login - BytePlus ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/dashboard).

   2. Click Dev boxes in the left navigation bar, and click the name of the Dev boxes to be operated on the Dev boxes list page to enter the corresponding Dev boxes.

   3. Remote login Dev boxes through SSH, for details, see [Remote connection through SSH Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Remote_connection_to_Dev_boxes_via_SSH).

2. Configure volc configure. For details, please refer to [the usage documentation -- Machine Learning Platform - BytePlus ](https://www.volcengine.com/docs/6459/72394).

3. Execute the following command in Terminal to download the deepseek\-v2 model from the mirror source and open the bucket path to Mount.


```bash
cd /vemlp-demo-models
mkdir model-deepseek-v2-lite
cd model-deepseek-v2-lite
export HF_ENDPOINT=https://hf-mirror.com
pip3 install -U huggingface_hub
huggingface-cli download --token $HF_TOKEN --resume-download deepseek-ai/DeepSeek-V2-Lite --local-dir $ORIGINAL_MODEL_PATH
```


To run the **huggingface\-cli** command line, the list of parameters that need to be passed in is as follows:


|Parameter |Description |
|---|---|
|hf_token |hf_token for Huggingface accounts with deepseek permissions. |
|original_model_path |Source safetensor path. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">\-\-Token/\-\- hf_username/\-\- hf_token and other parameters are not necessary, only some Repo has license restrictions, you need to log in to apply for permission. If necessary, download the token after https://huggingface.co/settings/tokens.</div>


2. <div data-tips="true" data-tips-type="tip">It is recommended that you set the model file, the download and storage address of the training dataset in the shared storage such as TOS/VEPFS/SCFS, so that it can be more easily mounted on different machines when performing cross\-node tasks such as training and inference.</div>


3. <div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself. In this case, please try to choose a larger cloud disk capacity (e.g. 100G).</div>



<span id="步骤二：准备数据集"></span>
# Step 2: Prepare the dataset

Execute the following command in the Terminal to directly download the training and fine\-tuning dataset that Volcano presets in the mirror.

```bash
cd /vemlp-demo-models
mkdir datasets-deepseek-v2-lite
cd datasets-deepseek-v2-lite
wget https://mlp-opentrail-demo.tos-cn-beijing.volces.com/dataset/oscar-en.tar.gz
tar -xzvf oscar-en.tar.gz
wget https://mlp-opentrail-demo.tos-cn-beijing.volces.com/dataset/finetune-dataset.tar.gz
tar -xzvf finetune-dataset.tar.gz
```


<span id="步骤三：模型训练"></span>
# Step 3: Model training

<span id="_3-1-模型格式转换（safetensor-to-ckpt）"></span>
## 3.1 Model format conversion (safetensor to ckpt)

Execute the following command in Terminal to lossless convert the safetensor to checkpoint format and output it to the target checkpoint path configured by the Start parameter ( **MEGATRON_LM_MODEL_PATH** ). The format conversion is expected to take 9 to 10 minutes.

```bash
cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-utils/deepseek_convertor
bash convertor.sh -m A2.4B -s $ORIGINAL_MODEL_PATH -t $MEGATRON_LM_MODEL_PATH -tp 2 -pp 1 -ep 4 -te true -hf $ORIGINAL_MODEL_PATH -pr bf16
```


The parameters required to run **convertor.sh** script are described as follows:


|Parameter |Description |
|---|---|
|**original_model_path** |Source safetensor path. |
|**megatron_lm_model_path** |Target checkpoint path. |
|**tp** |Model parallelism. |
|**pp** |Parallelism. |
|**ep** |Parallel computing. |
|**te** |Using Transformer Engine, the values are as follows:<br><br><br>* true<br><br>* false |
|**hf** |The path to the HuggingFace checkpoint. |
|**pr** |Training accuracy: fp16 or bf16. |


<span id="_3-2-自定义任务分布式训练（指令微调）"></span>
## 3.2 Distributed training for custom tasks (instruction fine\-tuning)

The best practices document provides instructions for both the console and the command line.

<span id="方式一：控制台"></span>
### Method 1: Console


1. Enter custom tasks [console](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/customTask/create)

2. configuration environment

   1. Select megatron\-lm\-1.0 at the prefabricated mirror or configure the following mirror at the mirror URL.

   ```bash
   vemlp-cn-beijing.cr.volces.com/preset-images/llm:megatron-lm-1.0
   ```
   

   2. Fill in the entry commands and define environment variables. Please note that the path mounted by tos on the development machine is inconsistent with the path mounted in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path mounted in custom tasks.

   ```bash
   cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-examples/deepseek2/
   bash run_pretrain_mcore-deepseek2.sh --model_size A2.4B --batch_size 1 --global_batch_size 8 --learning_rate 1e-5 --min_learning_rate 1e-6 --sequence_length 4096 --padding_length 4096 --precision bf16 --tensor_parallel 2 --pipeline_parallel 1 --context_parallel_size 1 --expert_parallel 4 --activation_checkpoint false --distributed_optimizer false --flash_attention true --sequence_parallel true --save_interval 10000 --dataset_path /data/datasets-deepseek-v2-lite/oscar-en/oscar-en-llama_text_document --pretrain_checkpoint_path $CHECKPOINT_PATH --train_tokens 10000000 --warmup_tokens 100 --output_basepath $OUTPUT_PATH --sft true --optimizer_offload false --train_iters 10000 --lr_warmup_iters 100
   ```
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e266e2ba21643a7879ecde0e0d8eff2~tplv-goo7wpa0wc-image.image) </span>


3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 8\-card ml.pni2.

   2. Mount TOS and CFS. It should be noted that the path mounted by tos on the development machine is inconsistent with the path mounted in custom tasks. When filling in the model path in environment variables, you need to ensure that it is the path mounted in custom tasks.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9177bc9d376c4f428e3abe393f3b0def~tplv-goo7wpa0wc-image.image) </span>

<span id="方式二：命令行"></span>
### Method 2: Command Line

Pre\-train DeepSeek\-V2\-Lite in the Terminal using the following commands.


1. Create a **demo.yaml** file.

2. Edit the YAML file and fill in the mirror, resource specifications, environment variables, and entry commands.

3. Run the task command. If the result is run, the words " **Create task was successful, task_id** " will appear in the Terminal. The complete training duration is expected to be around 5 hours.


```bash
volc ml_task submit --conf=/vemlp-demo-models/demo.yaml
```


**Example demo.yaml** file:

```bash
TaskName: "deepseek-v2-lite"
Description: ""

Tags: []
ImageUrl: "vemlp-cn-beijing.cr.volces.com/preset-images/llm:megatron-lm-1.0"

ResourceQueueID: "q-**************" #Please replace with your own queue ID

# DL framework, support: TensorFlow PS,PyTorch DDP,Horovod,BytePS
Framework: "PyTorchDDP"
#Flavor represents the model, go to https://www.volcengine.com/docs/6459/72363 query
TaskRoleSpecs:
    - RoleName: "worker"
      RoleReplicas: 1                                                   
      Flavor: "custom"
      ResourceSpec:
          Family: "ml.pni2"
          CPU: 105.000
          Memory: 1875.000
          GPUNum: 8

Envs:
  - Name: "CHECKPOINT_PATH"
    Value: "/data/model-deepseek-v2-lite/deepseek-v2-lite-tp2-pp1-ep4/"
  - Name: "OUTPUT_PATH"
    Value: "/data/model-deepseek-v2-lite/ckpt"

AccessType: "Queue"

Storages:
    - Type: "Tos"                     
      MountPath: "/data"
      Bucket: "vemlp-demo-models"
      Prefix: "/"
      FsName: "testmodel"
      MetaCacheExpiryMinutes: "-1"

Entrypoint: |
  cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-examples/deepseek2/  && bash run_pretrain_mcore-deepseek2.sh --model_size A2.4B --batch_size 1 --global_batch_size 8 --learning_rate 1e-5 --min_learning_rate 1e-6 --sequence_length 4096 --padding_length 4096 --precision bf16 --tensor_parallel 2 --pipeline_parallel 1 --context_parallel_size 1 --expert_parallel 4 --activation_checkpoint false --distributed_optimizer false --flash_attention true --sequence_parallel true --save_interval 10000 --dataset_path /data/datasets-deepseek-v2-lite/oscar-en/oscar-en-llama_text_document --pretrain_checkpoint_path $CHECKPOINT_PATH --train_tokens 10000000 --warmup_tokens 100 --output_basepath $OUTPUT_PATH --sft true --optimizer_offload false --train_iters 10000 --lr_warmup_iters 100
```


To run **run_finetune_megatron_llama.sh** script, the list of parameters that need to be passed in is described as follows:


|Parameter |Description |
|---|---|
|**model_size** |Model size: such as A21B, A2.4B, etc. |
|**batch_size** |The number of samples in one data parallelism at a time. |
|**global_batch_size** |Total number of samples for multiple data parallelisms in one iteration. |
|**learning_rate** |Learning rate. |
|**min_learning_rate** |Minimum learning rate. |
|**sequence_length** |Sequence length. |
|**padding_length** |Padding length. |
|**precision** |Training accuracy: fp16, bf16, or fp8. |
|**tensor_parallel** |Model parallelism. |
|**pipeline_parallel** |Parallelism. |
|**context_parallel_size** |Content parallelism. |
|**expert_parallel** |Parallel computing. |
|**activation_checkpoint** |Activate checkpoint mode with the following values:<br><br><br>* sel<br><br>* full<br><br>* offload<br><br>* none |
|**distributed_optimizer** |Whether to use the Distributed optimizer, the values are as follows:<br><br><br>* true<br><br>* false |
|**flash_attention** |Whether to use Flash Attention first, the values are as follows:<br><br><br>* true<br><br>* false |
|**sequence_parallel** |Whether to use sequence parallelism, the values are as follows:<br><br><br>* true<br><br>* false |
|**save_interval** |The interval at which the checkpoint file is saved. |
|**dataset_path** |Training dataset path. |
|**pretrain_checkpoint_path** |Pre\-trained model paths. |
|**train_tokens** |Number of tokens trained. |
|**warmup_tokens** |Number of tokens warmed up. |
|**output_basepath** |Training output log file path. |
|**sft** |Whether to use Soft fine\-tuning, the values are as follows:<br><br><br>* true<br><br>* false |
|**train_iters** |Training Iter Numbers. |
|**lr_warmup_iters** |Preheat Iter number. |


<span id="_3-3-模型格式转换（ckpt-to-safetensor）"></span>
## 3.3 Model format conversion (ckpt to safetensor)

Execute the following command in Terminal to losslessly convert the checkpoint back to the safetensor format and output it to the target checkpoint path configured by the Start parameter ( **ORIGINAL_MODEL_PATH** ).


1. First make sure that there is a tokenizer.model vocabulary file in the $MEGATRON_LM_MODEL_PATH path. If not, execute the following command line to copy the file.


```bash
cp -f /vemlp-demo-models/model-deepseek-v2-lite/deepseek-v2-lite-tp2-pp1-ep4/tokenizer.json /vemlp-demo-models/model-deepseek-v2-lite/ckpt/checkpoint/finetune-mcore-deepseek-v2-A2.4B-lr-1e-5-minlr-1e-6-bs-1-gbs-8-seqlen-4096-pr-bf16-tp-2-pp-1-cp-1/iter_0010000/
```



2. Run **convertor.sh** script with an estimated conversion time of 2min.


```bash
cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-utils/deepseek_convertor
bash convertor.sh -m A2.4B -s /vemlp-demo-models/model-deepseek-v2-lite/ckpt/checkpoint/finetune-mcore-deepseek-v2-A2.4B-lr-1e-5-minlr-1e-6-bs-1-gbs-8-seqlen-4096-pr-bf16-tp-2-pp-1-cp-1 -t /vemlp-demo-models/model-deepseek-v2-lite/deepseek-v2-lite-tp2-pp1-ep4-vllm -tp 2 -pp 1 -ep 4 -te true -hf /vemlp-demo-models/model-deepseek-v2-lite/deepseek-v2-lite -pr bf16 -M
```


<span id="步骤四：部署在线服务进行推理"></span>
# Step 4: Deploy inference services for inference

<span id="_4-1-复制文件"></span>
## 4.1 Copying files

After the model is converted to the vllm inference format model, execute the following command line in the Terminal to copy all the JSON suffix format files in the path of the pre\-training model to the path under the inference model file, which is the same level as the .bin file.

```bash
cp -f /vemlp-demo-models/model-deepseek-v2-lite/deepseek-v2-lite-tp2-pp1-ep4/*.json /vemlp-demo-models/model-deepseek-v2-lite/deepseek-v2-lite-tp2-pp1-ep4-vllm/
```


<span id="_4-2-创建推理服务"></span>
## 4.2 Creating inference services


1. Go to the inference services [console ](https://console.volcengine.com/ml-platform/region:ml-platform+cn-beijing/serviceNew/create).

2. Create inference services and deploy resources.

   1. Service network configuration.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7affaa2abb34a77a126f909ddc19792~tplv-goo7wpa0wc-image.image) </span>

   2. In [Service Management] \- [Deployment], click Add Deployment.

      1. Fill in the mirror URL.

      ```bash
      vemlp-cn-beijing.cr.volces.com/preset-images/llm:vllm-1.0
      ```
      

      2. Enter the entry command. Notice the path of the TOS Mount on the inference services.

      ```bash
      python  -m vllm.entrypoints.openai.api_server  --model /vemlp-demo-models/model-deepseek-v2-lite/deepseek-v2-lite-tp2-pp1-ep4-vllm  --served-model-name deepseek  --tensor-parallel-size 2   --max-num-seqs 64  --trust-remote-code
      ```
      

      3. Allocate resources. The best practice is to use a 2\-card ml.pni2.

      4. Mount TOS and CFS.

      5. Configure subnet and SecurityGroup.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dc7f7b656f74658b29426e2837776d0~tplv-goo7wpa0wc-image.image) </span>

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/056bc1c86eec422db8d4e0a104d67cea~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-3-定义请求文件-request-py-并执行"></span>
## 4.3 Define the request file request.py and execute it


1. Create request.py file. An example of script content is as follows.


```bash
import requests
import json

#Define the request and change the specific IP address
url = "http://192.*.*.49:8000/v1/completions"
headers = {
    "Content-Type": "application/json"
}
data = {
    "model": "deepseek",
    "prompt": "San Francisco is a",
    "max_tokens": 100,
    "temperature": 0
}

#Send a POST request
response = requests.post(url, headers=headers, data=json.dumps(data))

#Print the response content
print(response.json())
```



2. Execute the command request.


```bash
python request.py
```


The results are as follows.

```bash
{{'id': 'cmpl-c4f2849f328f4a96ab756036745ec8ad', 'object': 'text_completion', 'created': 1733131866, 'mmodel': 'deepseek', 'choices': [{'index': 0, 'text':' city of many neighborhoods, each with its own unique character and charm. From the bustling streets of Chinatown to the quiet streets of the Marina, there is something for everyone in this vibrant city.\nOne of the most popular neighborhoods in San Francisco is the Mission District. This neighborhood is known for its vibrant nightlife, eclectic restaurants, and unique shops. The Mission District is also home to many art galleries and museums, making it a great place to explore the city's culture.\nAnother popular', 'logprobs': None, 'finish_reason': 'length','sstop_reason': None, 'prompt_logprobs': None}],'usage': {'prompt_tokens': 5, 'total_tokens's:105,'completion_tokens': 100}}
```
