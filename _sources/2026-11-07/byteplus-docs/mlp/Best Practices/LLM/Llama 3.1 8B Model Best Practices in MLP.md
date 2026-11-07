---
title: "Llama 3.1 8B Model Best Practices in MLP"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Llama_3_1_8B_Model_Best_Practices_in_MLP"
---

Machine Learning Platform is a platform for professional algorithm engineers to integrate cloud\-native tools + computing power (GPU, CPU Cloud as a Service) for one\-stop AI algorithm development and iteration. This program will introduce you how to fine tune the model and implement inference services deployment in MLP based on the open source model of Meta \- Llama \- 3.1\-8 B and the training process of Megatron.

<span id="使用前提"></span>
# premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself.</div>


This solution takes the Meta \- Llama \- 3.1\-8 B model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* Activated network/TOS/CFS. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [Console Quick Start -- Torch Object Storage - BytePlus ](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

   * Resource Specifications: Configure the following resource specifications.

      * CPU instance: 8C/64G/20GB cloud disk.

      * GPU card count: at least 8 cards, best practice to use 1 ml.pni2.

   * Mount configuration: Mount TOS bucket and CFS, see [How the training code accesses the TOS](https://docs.byteplus.com/docs/mlp/53984).

   * Mirror address: Configure the following mirror at the custom mirror, fill in the SSH key and Mount TOS. Creating Dev boxes for the first time is expected to take 20 minutes due to the large mirror being pulled.

      ```bash
        vemlp-boe-cn-beijing.cr.volces.com/preset-images/megatron-lm:trail-2
      ```
      


<span id="步骤一：准备-llama-3-1-8b-模型"></span>
# Step 1: Prepare the Llama 3.1\-8 B model


1. Enter the Dev boxes.

   1. Login [Account Login - BytePlus ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/dashboard).

   2. Click Dev boxes in the left navigation bar, and click the name of the Dev boxes to be operated on the Dev boxes list page to enter the corresponding Dev boxes.

   3. Remote login Dev boxes through SSH, for details, see [Remote connection through SSH Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Remote_connection_to_Dev_boxes_via_SSH).

2. Configure volc configure. For details, please refer to .

3. Execute the following command in Terminal to download the Llama \- 3.1\-8 B model from the mirror source and open the bucket path to Mount.


```bash
cd /vemlp-demo-models
mkdir model-llama 
cd model-llama
wget https://hf-mirror.com/hfd/hfd.sh
chmod a+x hfd.sh
export HF_ENDPOINT=https://hf-mirror.com
apt-get update
apt-get install aria2
apt-get install git-lfs
./hfd.sh meta-llama/Meta-Llama-3-8B --hf_username $HF_USER_NAME --hf_token $HF_TOKEN --exclude "*pth" --local-dir $ORIGINAL_MODEL_PATH
```


To run the  **./hfd.sh** file, the list of parameters that need to be passed in is described as follows:


|Parameter |Description |
|---|---|
|**hf_user_name** |Huggingface account with llama usage rights. |
|**hf_token** |hf_token for Huggingface accounts with llama usage permissions. |
|**original_model_path** |Source safetensor path. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">\-\-Token/\-\- hf_username/\-\- hf_token and other parameters are not necessary, only some Repo has license restrictions, you need to log in to apply for permission. If necessary, download the token after https://huggingface.co/settings/tokens.</div>


2. <div data-tips="true" data-tips-type="tip">It is recommended that you set the model file, the download and storage address of the training dataset in the shared storage such as TOS/VEPFS/SCFS, so that it can be more easily mounted on different machines when performing cross\-node tasks such as training and inference.</div>



<span id="步骤二：准备数据集"></span>
# Step 2: Prepare the dataset

Execute the following command in the Terminal to download the dataset prepared by the MLP.

```bash
cd /vemlp-demo-models
mkdir datasets-llama
cd datasets-llama
wget https://mlp-opentrail-demo.tos-cn-beijing.volces.com/dataset/finetune-dataset.tar.gz
tar -zxf finetune-dataset.tar.gz
```


<span id="步骤三：模型训练"></span>
# Step 3: Model training

<span id="_3-1-模型格式转换（safetensor-to-ckpt）"></span>
## 3.1 Model format conversion (safetensor to ckpt)

Execute the following command in Terminal to lossless convert the safetensor to checkpoint format and output it to the target checkpoint path configured by the Start parameter ( **MEGATRON_LM_MODEL_PATH** ). The format conversion is expected to take 3 to 4 minutes.

```bash
cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-utils/llama_convertor
bash convertor.sh -s $ORIGINAL_MODEL_PATH -t $MEGATRON_LM_MODEL_PATH -tp 8 -pp 1 -n llama3.1-8b -e 0
```


The parameters required to run **convertor.sh** script are described as follows:


|Parameter |Description |
|---|---|
|**original_model_path** |Source safetensor path. |
|**megatron_lm_model_path** |Target checkpoint path. |
|**tp** |Model parallelism. |
|**pp** |Parallelism. |
|**n** |Model names such as Llama\-7b, Llama\-13b, Llama\-30b, Llama\-65b, Llama\-7b, Llama\-13b, Llama\-70b, Llama\-3\-8b, Llama\-70b, etc. |
|**e** |Extra vocabulary size (default: 0). |


<span id="_3-2-自定义任务分布式训练（指令微调）"></span>
## 3.2 Distributed training for custom tasks (instruction fine\-tuning)

The best practices document provides instructions for both the console and the command line.

<span id="方式一：控制台"></span>
### Method 1: Console


1. Enter custom tasks [console](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/customTask/create)

2. configuration environment

   1. Configure mirrors at Custom mirrors.

   ```bash
   vemlp-boe-cn-beijing.cr.volces.com/preset-images/megatron-lm:trail-2
   ```
   

   2. Fill in the entry commands and define environment variables. Please note that the path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path of Mount in custom tasks.

   ```bash
   cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-examples/llama3/ && /bin/bash run_finetune_megatron_llama.sh --model_size 8B --batch_size 1 --global_batch_size 32 --learning_rate 1e-5 --min_learning_rate 1e-6 --sequence_length 128 --padding_length 128 --extra_vocab_size 256 --precision bf16 --tensor_parallel 8 --pipeline_parallel 2 --activation_checkpoint sel --distributed_optimizer true --flash_attention false --sequence_parallel false --transformer_engine false --save_interval 100 --dataset_path /data/datasets-llama/finetune-dataset/alpaca_zh-llama3-train.json --valid_dataset_path /data/datasets-llama/finetune-dataset/alpaca_zh-llama3-valid.json --pretrain_checkpoint_path $CHECKPOINT_PATH --train_iters 1000 --lr_warmup_iters 10 --output_basepath $OUTPUT_PATH
   ```
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96fb33e8ce5947e2b5409a4884fd1063~tplv-goo7wpa0wc-image.image) </span>


3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 8\-card ml.pni2.

   2. Mount TOS and CFS. Note: The path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the environment variables, make sure it is the path of Mount in custom tasks.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9177bc9d376c4f428e3abe393f3b0def~tplv-goo7wpa0wc-image.image) </span>

<span id="方式二：命令行"></span>
### Method 2: Command Line

Pretrain Meta \- Llama \- 3.1\-8 B in Terminal using the following command.


1. Create a **demo.yaml** file.

2. Edit the YAML file and fill in the mirror, resource specifications, environment variables, and entry commands.

3. Run the task command. If the result is run, the words " **Create task was successful, task_id** " will appear in the Terminal. The complete training duration is expected to be around 2 hours.


```bash
volc ml_task submit --conf=/vemlp-demo-models/demo.yaml
```


**Example demo.yaml** file:

```bash
TaskName:  "llama-8b"
Description:  ""
Tags: []

ImageUrl:  "vemlp-boe-cn-beijing.cr.volces.com/preset-images/megatron-lm:trail-2"
ResourceQueueID:  "q-**************"  #Please replace with your own queue ID
# DL framework, support: TensorFlow PS,PyTorch DDP,Horovod,BytePS
Framework:  "PyTorchDDP"
#Flavor represents the model, go to https://www.volcengine.com/docs/6459/72363 query
TaskRoleSpecs:
        - RoleName:  "worker"
            RoleReplicas: 1                                                   
            Flavor:  "custom"
            ResourceSpec:
                    Family:  "ml.pni2"
                    CPU: 105.000
                    Memory: 1875.000
                    GPUNum: 8

Envs:
    - Name:  "CHECKPOINT_PATH"
        Value:  "/data/model-llama/Meta-Llama-3.1-8B-to-megatron2/"
    - Name:  "OUTPUT_PATH"
        Value:  "/data/model-llama/ckpt"
AccessType:  "Queue"
Storages:
        - Type:  "Tos"                     
            MountPath:  "/data"
            Bucket:  "vemlp-demo-models"
            Prefix:  "/"
            FsName:  "testmodel"
            MetaCacheExpiryMinutes:  "-1"
Entrypoint: |
  cd  /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-examples/llama3/ && /bin/bash run_finetune_megatron_llama.sh --model_size 8B --batch_size 1 --global_batch_size 32 --learning_rate 1e-5 --min_learning_rate 1e-6 --sequence_length 128 --padding_length 128 --extra_vocab_size 256 --precision bf16 --tensor_parallel 8 --pipeline_parallel 2 --activation_checkpoint sel --distributed_optimizer  true  --flash_attention  false  --sequence_parallel  false  --transformer_engine  false  --save_interval 100 --dataset_path /data/datasets-llama/finetune-dataset/alpaca_zh-llama3-train.json --valid_dataset_path /data/datasets-llama/finetune-dataset/alpaca_zh-llama3-valid.json --pretrain_checkpoint_path  $CHECKPOINT_PATH  --train_iters 1000 --lr_warmup_iters 10 --output_basepath  $OUTPUT_PATH
```


To run **run_finetune_megatron_llama.sh** script, the list of parameters that need to be passed in is described as follows:


|Parameter |Description |
|---|---|
|**model_size** |Model structure parameter magnitude: 8B, 70B or 405B. |
|**batch_size** |The number of samples in one data parallelism at a time. |
|**global_batch_size** |Total number of samples for multiple data parallelisms in one iteration. |
|**learning_rate** |Learning rate. |
|**min_learning_rate** |Minimum learning rate. |
|**sequence_length** |Sequence length. |
|**padding_length** |Padding length. |
|**extra_vocab_size** |The number of words added to the base vocabulary size. |
|**precision** |Training accuracy: fp16, bf16, or fp8. |
|**tensor_parallel** |Model parallelism. |
|**pipeline_parallel** |Parallelism. |
|**activation_checkpoint** |Activate checkpoint mode with the following values:<br><br><br>* sel<br><br>* full<br><br>* offload<br><br>* none |
|**distributed_optimizer** |Whether to use the Megatron version of the Zero\-1 down memory optimizer, the values are as follows:<br><br><br>* true<br><br>* false |
|**flash_attention** |Whether to use Flash Attention first, the values are as follows:<br><br><br>* true<br><br>* false |
|**sequence_parallel** |Whether to use sequence parallelism, the values are as follows:<br><br><br>* true<br><br>* false |
|**transformer_engine** |Whether to use tranformer_engine, the values are as follows:<br><br><br>* true<br><br>* false |
|**save_interval** |The interval at which the checkpoint file is saved. |
|**dataset_path** |Training dataset path. |
|**valid_dataset_path** |Validate the dataset path. |
|**pretrain_checkpoint_path** |Pre\-trained model paths. |
|**train_iters** |Training Iter Numbers. |
|**lr_warmup_iters** |Preheat Iter number. |
|**output_basepath** |Training output log file path. |


<span id="_3-3-模型格式转换（ckpt-to-safetensor）"></span>
## 3.3 Model format conversion (ckpt to safetensor)

Execute the following command in Terminal to losslessly convert the checkpoint back to the safetensor format and output it to the target checkpoint path configured by the Start parameter ( **ORIGINAL_MODEL_PATH** ).


1. First make sure that there is a tokenizer.model vocabulary file in the $MEGATRON_LM_MODEL_PATH path. If not, execute the following command line to copy the file.


```bash
cp -f /vemlp-demo-models/model-llama/Meta-Llama-3.1-8B-to-megatron2/tokenizer.json /vemlp-demo-models/model-llama/ckpt/checkpoint/finetune-megatron-llama3-8B-tp-8-pp-2/iter_0001000/
```



2. Run **convertor.sh** script with an estimated conversion time of 2min.


```bash
cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-utils/llama_convertor
bash convertor.sh -m /opt/ml-platform/third_party/vemlp-open-trial/third_party -s /vemlp-demo-models/model-llama/ckpt/checkpoint/finetune-megatron-llama3-8B-tp-8-pp-2/iter_0001000 -t /vemlp-demo-models/model-llama/vllm/ -tp 8 -pp 1 -n llama3.1-8b -e 0 -M
```


<span id="步骤四：部署在线服务进行推理"></span>
# Step 4: Deploy inference services for inference

<span id="_4-1-复制文件"></span>
## 4.1 Copying files

After the model is converted to the vllm inference format model, execute the following command line in the Terminal to copy all the JSON suffix format files in the path of the pre\-training model to the path under the inference model file, which is the same level as the .bin file.

```bash
cp -f /vemlp-demo-models/model-llama/Meta-Llama-3.1-8B-to-megatron2/*.json /vemlp-demo-models/model-llama/vllm/
```


<span id="_4-2-创建推理服务"></span>
## 4.2 Creating inference services


1. Go to the inference services [console ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/serviceNew/create).

2. Create inference services and deploy resources.

   1. Service network configuration.

      1. Configure a private network

      2. Turn on load balancing and configure ports.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7affaa2abb34a77a126f909ddc19792~tplv-goo7wpa0wc-image.image) </span>


2. In [Service Management] \- [Deployment], click Add Deployment.

   1. Fill in the mirror URL.

   ```bash
   vemlp-boe-cn-beijing.cr.volces.com/preset-images/vllm:default
   ```
   

   2. Enter the entry command. Notice the path of the TOS Mount on the inference services.

   ```bash
   python  -m vllm.entrypoints.openai.api_server  --model /vemlp-demo-models/model-llama/vllm/  --served-model-name \"llama3\"  --tensor-parallel-size 1   --max-num-seqs 64
   ```
   

   3. Allocate resources. The best practice is to use 1\-card ml.pni2.

   4. Mount TOS and CFS.

   5. Configure subnet and SecurityGroup.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dc7f7b656f74658b29426e2837776d0~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/056bc1c86eec422db8d4e0a104d67cea~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-定义请求文件-request-py-并执行"></span>
## 4.3 Define the request file request.py and execute it


1. Create **request.py** file. An example of script content is as follows.


```bash
import requests
import json

#Define the request and change the specific IP address
url = "http://101.*.*.138:8000/v1/completions"

headers = {
    "Content-Type": "application/json"
}
data = {
    "model": "llama3",
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
{'id': 'cmpl-a40535c337134dd090863e69a7fbb240', 'object': 'text_completion', 'created': 1725420936, 'model': 'llama3', 'choices': [{'index': 0, 'text': " city of many neighborhoods, each with its own unique character and charm. Whether you're looking for a hipster haven, a family-friendly area, or a place to party, there's a neighborhood for you. Here are some of the best neighborhoods in San Francisco to check out:\nThe Mission: The Mission is a hipster haven with a vibrant arts scene, great food, and a lively nightlife. It's also home to the city's largest Latino population, making it a great place to experience authentic", 'logprobs': None, 'finish_reason': 'length', 'stop_reason': None, 'prompt_logprobs': None}], 'usage': {'prompt_tokens': 5, 'total_tokens': 105, 'completion_tokens': 100}}
```
