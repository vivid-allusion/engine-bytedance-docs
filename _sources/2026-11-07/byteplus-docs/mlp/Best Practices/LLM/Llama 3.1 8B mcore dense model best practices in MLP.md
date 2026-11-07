---
title: "Llama 3.1 8B mcore dense model best practices in MLP"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Llama_3_1_8B_mcore_dense_model_best_practices_in_MLP"
---

Machine Learning Platform is a platform for professional algorithm engineers to integrate cloud\-native tools + computing power (GPU, CPU Cloud as a Service) for one\-stop AI algorithm development and iteration. This solution will show you how to pre\-train/continue pre\-train, fine\-tune, and deploy a Llama 3.1B mcore dense model based on Megatron\-Core in MLP.

<span id="使用前提"></span>
# premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself.</div>


This solution takes the Meta \- Llama \- 3.1\-8 B mcore dense model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* Activated network/TOS/CFS. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [Console Quick Start -- Torch Object Storage - BytePlus](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1)

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

   * Resource Specifications: Configure the following resource specifications.

      * CPU instance: 8C/64G/20GB cloud disk.

      * Number of GPU cards: at least 8 cards, best practice to use 1 ml.pni2l.

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

2. Configure volc configure. For details, please refer to[ ](https://www.volcengine.com/docs/6459/72394).

3. Execute the following command in Terminal to download the Llama \- 3.1\-8 B model from the mirror source and open the bucket path to Mount.


```bash
cd /vemlp-demo-models
mkdir model-llama-mcore-dense
cd model-llama-mcore-dense
pip3 install -U huggingface_hub
export HF_ENDPOINT=https://hf-mirror.com
huggingface-cli download --token $HF_TOKEN --resume-download meta-llama/Meta-Llama-3.1-8B-Instruct --local-dir $ORIGINAL_MODEL_PATH
```


To run the **huggingface\-cli** file, the list of parameters that need to be passed in is as follows:


|Parameter |Description |
|---|---|
|**hf_token** |hf_token for Huggingface accounts with llama usage permissions. |
|**original_model_path** |Source safetensor path. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">\-\-Token/\-\- hf_username/\-\- hf_token and other parameters are not necessary, only some Repo has license restrictions, you need to log in to apply for permission. If necessary, download the token after https://huggingface.co/settings/tokens.</div>


2. <div data-tips="true" data-tips-type="tip">It is recommended that you set the model file, the download and storage address of the training dataset in the shared storage such as TOS/VEPFS/SCFS, so that it can be more easily mounted on different machines when performing cross\-node tasks such as training and inference.</div>



<span id="步骤二：准备数据集"></span>
# Step 2: Prepare the dataset

Execute the following command in the Terminal to directly download the training and fine\-tuning dataset that Volcano presets in the mirror.

```bash
cd /vemlp-demo-models
mkdir datasets-llama-mcore-dense
cd datasets-llama-mcore-dense
wget https://mlp-opentrail-demo.tos-cn-beijing.volces.com/dataset/oscar-en.tar.gz 
tar -xzvf oscar-en.tar.gz
wget https://mlp-opentrail-demo.tos-cn-beijing.volces.com/dataset/finetune-dataset.tar.gz
tar -xzvf finetune-dataset.tar.gz
```


<span id="步骤三：模型训练"></span>
# Step 3: Model training

<span id="_3-1-模型格式转换（safetensor-to-mcore）"></span>
## 3.1 Model format conversion (safetensor to mcore)

Execute the following command in Terminal to lossless convert the safetensor to the mcore format that supports megatron training and output to the target mcore path configured by the Start parameter ( **MEGATRON_LM_MODEL_PATH** ). The format conversion is expected to take 3 to 4 minutes.

```bash
cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-utils/llama_convertor
bash hf2mcore_convertor.sh -s $ORIGINAL_MODEL_PATH -t $MEGATRON_LM_MODEL_PATH -tp 8 -pp 1 -M false -c false -C false -p bf16 -H $ORIGINAL_MODEL_PATH
```


The parameters required to run **hf2mcore_convertor.sh** script are described as follows:


|Parameter |Description |
|---|---|
|**original_model_path** |Source safetensor path. |
|**megatron_lm_model_path** |Target mcore path. |
|**tp** |Model parallelism. |
|**pp** |Parallelism. |
|**M** |Megatron is converted to HuggingFace with the following values:<br><br><br>* true<br><br>* false |
|**c** |Start alignment check with the following values:<br><br><br>* true<br><br>* false |
|**C** |Perform the check without saving, and the values are as follows:<br><br><br>* true<br><br>* false |
|**p** |Training accuracy: fp16 or bf16. |
|**H** |The path to the HuggingFace checkpoint, given when M is true. |


<span id="_3-2-自定义任务分布式训练（指令微调）"></span>
## 3.2 Distributed training for custom tasks (instruction fine\-tuning)

The best practices document provides instructions for both the console and the command line.

<span id="方式一：控制台"></span>
### Method 1: Console


1. Enter custom tasks [consol](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/customTask/create)

2. configuration environment

   1. Configure mirrors at Custom mirrors.

   ```bash
   vemlp-boe-cn-beijing.cr.volces.com/preset-images/megatron-lm:trail-2
   ```
   

   2. Fill in the entry commands and define environment variables. Please note that the path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path of Mount in custom tasks.

   ```bash
   cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-examples/llama3-mocre/ &&  /bin/bash run_finetune_mcore_llama3.sh  --batch-size 1 --global-batch-size 32 --lr 1e-5 --min-lr 1e-6 --seq-len 4096 --pad-len 4096 --pr bf16 --tp 8 --pp 1 --cp 1 --sp true --do true --fl true --ac false --optimizer-offload false --save-interval 10000 --dataset-path /data/dataset/oscar-en/oscar-en-llama_text_document  --pretrain-checkpoint-path $CHECKPOINT_PATH --train-tokens 10000000 --warmup-tokens 100 --output-basepath $OUTPUT_PATH --train-iters 10000 --lr-warmup-iters 100
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96fb33e8ce5947e2b5409a4884fd1063~tplv-goo7wpa0wc-image.image) </span>

3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 8\-card ml.pni2l.

   2. Mount TOS and CFS. Note: The path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the environment variables, make sure it is the path of Mount in custom tasks.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9177bc9d376c4f428e3abe393f3b0def~tplv-goo7wpa0wc-image.image) </span>


<span id="方式二：命令行"></span>
### Method 2: Command Line

Use the following commands in Terminal to fine tune the Meta \- Llama \- 3.1\-8 B mcore dense model, as follows.


1. Create a **demo.yaml** file.

2. Edit the YAML file and fill in the mirror, resource specifications, environment variables, and entry commands.

3. Run the task command. If the result is run, the words " **Create task was successful, task_id** " will appear in the Terminal. The complete training duration is expected to be around 2 hours.


```bash
volc ml_task submit --conf=/vemlp-demo-models/demo.yaml
```


**Example demo.yaml** file:

```bash
TaskName:  "llama-8b-mcore-dense"
Description:  ""
Tags: []

ImageUrl:  "vemlp-boe-cn-beijing.cr.volces.com/preset-images/megatron-lm:trail-2"
ResourceQueueID:  "q-**************" #Please replace with your own queue ID
# DL framework, support: TensorFlow PS,PyTorch DDP,Horovod,BytePS
Framework:  "PyTorchDDP"
#Flavor represents the model, go to https://www.volcengine.com/docs/6459/72363 query
TaskRoleSpecs:
        - RoleName:  "worker"
            RoleReplicas: 1                                                   
            Flavor:  "custom"
            ResourceSpec:
                    Family:  "ml.pni2l"
                    CPU: 105.000
                    Memory: 1875.000
                    GPUNum: 8

Envs:
    - Name:  "CHECKPOINT_PATH"
        Value:  "/data/model-llama-mcore-dense/Meta-Llama-3.1-8B-to-mcore-tp8-pp1/"
    - Name:  "OUTPUT_PATH"
        Value:  "/data/model-llama-mcore-dense/ckpt"
AccessType:  "Queue"
Storages:
        - Type:  "Tos"                     
            MountPath:  "/data"
            Bucket:  "vemlp-demo-models"
            Prefix:  "/"
            FsName:  "testmodel"
            MetaCacheExpiryMinutes:  "-1"
Entrypoint: |
  cd  /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-examples/llama3-mocre/ &&  /bin/bash run_finetune_mcore_llama3.sh  --batch-size 1 --global-batch-size 32 --lr 1e-5 --min-lr 1e-6 --seq-len 4096 --pad-len 4096 --pr  bf16 --tp 8 --pp 1 --cp  1 --sp  true  --do true  --fl  true  --ac  false  --optimizer-offload  false  --save-interval 10000 --dataset-path /data/datasets-llama-mcore-dense/oscar-en/oscar-en-llama_text_document  --pretrain-checkpoint-path  $CHECKPOINT_PATH  --train-tokens 10000000 --warmup-tokens 100 --output-basepath  $OUTPUT_PATH  --train-iters 10000 --lr-warmup-iters 100
```


To run **run_finetune_mcore_llama3.sh** script, the list of parameters that need to be passed in is described as follows:


|Parameter |Description |
|---|---|
|**batch_size** |The number of samples in one data parallelism at a time. |
|**global_batch_size** |Total number of samples for multiple data parallelisms in one iteration. |
|**lr** |Learning rate. |
|**min\-lr** |Minimum learning rate. |
|**seq\-len** |Sequence length. |
|**pad\-len** |Padding length. |
|**pr** |Training accuracy: fp16, bf16, or fp8. |
|**tp** |Model parallelism. |
|**pp** |Parallelism. |
|**sp** |Whether to use sequence parallelism, the values are as follows:<br><br><br>* true<br><br>* false |
|**do** |Whether to use a distributed optimizer, the values are as follows:<br><br><br>* true<br><br>* false |
|**fl** |Whether to use Flash Attention first, the values are as follows:<br><br><br>* true<br><br>* false |
|**ac** |Whether to use Activation checkpointing with the following values:<br><br><br>* full<br><br>* sel<br><br>* none |
|**optimizer\-offload** |Whether to use Optimizer offloading, the values are as follows:<br><br><br>* true<br><br>* false |
|**save_interval** |The interval at which the checkpoint file is saved. |
|**dataset_path** |Training dataset path. |
|**pretrain_checkpoint_path** |Pre\-trained model paths. |
|**train\-tokens** |Number of tokens trained. |
|**warmup\-tokens** |Number of tokens warmed up. |
|**output_path** |Training output log file path. |
|**train_iters** |Training Iter Numbers. |
|**lr_warmup_iters** |Preheat Iter number. |


<span id="_3-3-模型格式转换（mcore-to-safetensor）"></span>
## 3.3 **Model format conversion (mcore to safetensor)** 

Execute the following command in Terminal to lossless convert the mcore format back to the safetensor format and output to the target path configured by the Start parameter ( **ORIGINAL_MODEL_PATH** ).


1. First make sure that there is a tokenizer.model vocabulary file in the $MEGATRON_LM_MODEL_PATH path. If not, execute the following command line to copy the file.


```bash
cp -f /vemlp-demo-models/model-llama-mcore-dense/Meta-Llama-3.1-8B-to-mcore-tp8-pp1/tokenizer.json /vemlp-demo-models/model-llama-mcore-dense/ckpt/checkpoint/finetune-megatron-llama3-8B-tp-8-pp-2/iter_0001000/
```



2. Run **hf2mcore_convertor.sh** script with an estimated conversion time of 2 min.


```bash
cd /opt/ml-platform/third_party/vemlp-open-trial/third_party/veMLP-utils/llama_convertor
bash hf2mcore_convertor.sh -t /vemlp-demo-models/model-llama-mcore-dense/vllm/ -s vemlp-demo-models/model-llama-mcore-dense/ckpt/checkpoint/finetune-megatron-llama3-8B-tp-8-pp-2/iter_0001000 -tp 8 -pp 1 -M true -c false -C false -p bf16 -H /vemlp-demo-models/model-llama-mcore-dense/ckpt/checkpoint/finetune-megatron-llama3-8B-tp-8-pp-2/iter_0001000
```


<span id="步骤四：部署在线服务进行推理"></span>
# Step 4: Deploy inference services for inference

<span id="_4-1-复制文件"></span>
## 4.1 Copying files

After the model is converted to the vllm inference format model, execute the following command line in the Terminal to copy all the JSON suffix format files in the path of the pre\-training model to the path under the inference model file, which is at the same level as the .bin file.

```bash
cp -f /vemlp-demo-models/model-llama-mcore-dense/Meta-Llama-3.1-8B-to-mcore-tp8-pp1/*.json /vemlp-demo-models/model-llama-mcore-dense/vllm/
```


<span id="_4-2-创建推理服务"></span>
## 4.2 Creating inference services


1. Go to the inference services [console ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/serviceNew/create).

2. Create inference services and deploy resources.

   1. Service network configuration.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7affaa2abb34a77a126f909ddc19792~tplv-goo7wpa0wc-image.image) </span>

   2. In [Service Management] \- [Deployment], click Add Deployment.

      1. Fill in the mirror URL.

      ```bash
      vemlp-boe-cn-beijing.cr.volces.com/preset-images/vllm:default
      ```
      

      3. Enter the entry command. Notice the path of the TOS Mount on the inference services.

      ```bash
      python  -m vllm.entrypoints.openai.api_server  --model /vemlp-demo-models/model-llama-mcore-dense/vllm/  --served-model-name llama3  --tensor-parallel-size 2   --max-num-seqs 64
      ```
      

      5. Allocate resources. The best practice is to use a 2\-card ml.pni2.

      6. Mount TOS and CFS.

      7. Configure subnet and SecurityGroup.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dc7f7b656f74658b29426e2837776d0~tplv-goo7wpa0wc-image.image) </span>

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/056bc1c86eec422db8d4e0a104d67cea~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-3-定义请求文件-request-py-并执行"></span>
## 4.3 Define the request file request.py and execute it


1. Create **request.py** file. An example of script content is as follows.


```bash
import requests
import json

#Define the request and change the specific IP address
url = "http://192.*.*.24:8080/v1/completions"
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
{'id': 'cmpl-5e9858992470485583d8b12e6cbe741b', 'object': 'text_completion', 'created': 1726644124, 'model': 'llama3', 'choices': [{'index': 0, 'text': " city of many neighborhoods, each with its own unique character and charm. Whether you're looking for a hipster haven, a family-friendly area, or a quiet retreat, there's a neighborhood for you. Here are some of the best neighborhoods in San Francisco to consider for your next visit.<|im_end|>", 'logprobs': None, 'finish_reason': 'stop', 'stop_reason': None, 'prompt_logprobs': None}], 'usage': {'prompt_tokens': 5, 'total_tokens': 69, 'completion_tokens': 64}}
```
