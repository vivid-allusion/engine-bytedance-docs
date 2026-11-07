---
title: "Accelerating Llama with veTuner and veTurboIO - 3.1-8 B Model Best Practices in MLP"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Accelerating_Llama_with_veTuner_and_veTurboIO_-_3-1-8_B_Model_Best_Practices_in_MLP"
---

Machine Learning Platform is a set of services for professional algorithm engineers, integrating cloud\-native tools + computing power (GPU, CPU Cloud as a Service), for one\-stop AI algorithm development and iteration platform. This solution will show you how to use veTuner and veTurboIO in MLP to accelerate the fine\-tuning of Meta \- Llama \- 3.1\-8 B models and enable offline evaluation.

<span id="使用前提"></span>
# premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself.</div>


This solution takes the Meta \- Llama \- 3.1\-8 B model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* Activated network/TOS/CFS. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [Console Quick Start -- Torch Object Storage - BytePlus ](https://www.volcengine.com/docs/6349/74830), [Access File Storage Instance -- Cloud File System - BytePlus ](https://www.volcengine.com/docs/6720/107803).

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

   * Resource Specifications: Configure the following resource specifications.

      * CPU instance: 8C/64G/20GB cloud disk.

      * GPU card count: at least 8 cards, best practice is to use one ml.pni2l.

   * Mounting configuration:

      * Mount SFCS file system, this feature requires grant whitelist access. For more configuration information, please visit the [Cloud File System ](https://console.byteplus.com/cfs/region:cfs+ap-southeast-1/resource).

   * Mirror address: Configure the bottom mirror at the custom mirror, fill in the SSH key and Mount SFCS. Creating Dev boxes for the first time is expected to take 20 minutes due to the large mirror being pulled.

      ```bash
       vemlp-cn-beijing.cr.volces.com/preset-images/vetuner:0.0.1
      ```
      


<span id="步骤一：准备-llama-3-1-8b-模型"></span>
# Step 1: Prepare the Llama 3.1\-8 B model


1. Enter the Dev boxes.

   1. Login [Account Login - BytePlus ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/dashboard).

   2. Click Dev boxes in the left navigation bar, and click the name of the Dev boxes to be operated on the Dev boxes list page to enter the corresponding Dev boxes.

   3. Remote login Dev boxes through SSH, for details, see [Remote connection through SSH Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Remote_connection_to_Dev_boxes_via_SSH).

2. Configure volc configure. For details, please refer to [the usage documentation -- Machine Learning Platform - BytePlus ](https://www.volcengine.com/docs/6459/72394).

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

<span id="_2-1-数据准备"></span>
## 2.1 **Data preparation**

Execute the following command in Terminal to download the open source dataset [Clinton/Text-to-sql-v1 ](https://huggingface.co/datasets/Clinton/Text-to-sql-v1)on huggingface.

```bash
cd /vemlp-demo-models
mkdir datasets-vetuner
cd datasets-vetuner
pip3 install -U huggingface_hub
HF_ENDPOINT=[https://hf-mirror.com](https://hf-mirror.com/)
huggingface-cli download --repo-type dataset --resume-download Clinton/Text-to-sql-v1 --local-dir $DATA_DIR --token=$HF_TOKEN
```


To run the **huggingface\-cli** file, the list of parameters that need to be passed in is as follows:


|Parameter |Description |
|---|---|
|**hf_token** |hf_token for Huggingface accounts with access to download models, datasets, etc. |
|**data_dir** |Dataset download path. |


<span id="_2-2-数据预处理"></span>
## 2.2 Data preprocessing

This scheme randomly filters 100,000 pieces of data with short answers as the training dataset and 5,000 pieces of data as the test set.


1. Create makedataset.py file. An example of script content is as follows.


```bash
import json
import random
import pandas as pd
import pyarrow as pa
import pyarrow.parquet as pq
import os


#Read paths from environment variables
data_dir = os.getenv('DATA_DIR', '/vemlp-demo-models/datasets-vetuner/Text-to-sql')
data_path = os.getenv('DATA_PATH', '/vemlp-demo-models/datasets-vetuner/Text-to-sql/texttosqlv2.jsonl')
train_file_path = os.getenv('TRAIN_FILE_PATH','/vemlp-demo-models/datasets-vetuner/Text-to-sql/train.parquet')
val_file_path = os.getenv('VAL_FILE_PATH', '/vemlp-demo-models/datasets-vetuner/Text-to-sql/validation.parquet')


data = []
max_response_length = 100
with open(data_path, 'r', encoding="utf-8") as f:
    for line in f:
        data.append(json.loads(line))
keep_data = [d for d in data if len(d['response']) < max_response_length]
random.shuffle(keep_data)

validation_list=random.sample([i for i in range(0, len(keep_data))],5000)
validation_data = [keep_data[index] for index in validation_list]
train_list=random.sample([i for i in range(0, len(keep_data))],100000)
train_data = [keep_data[index] for index in train_list]

df = pd.DataFrame(validation_data)
table = pa.Table.from_pandas(df)
pq.write_table(table, val_file_path)

df = pd.DataFrame(train_data)
table = pa.Table.from_pandas(df)
pq.write_table(table, train_file_path)
```



2. Execute makedataset.py file inside the Dev box.


```bash
python makedataset.py
```


<span id="步骤三：模型训练"></span>
# Step 3: Model training

The best practices document provides instructions for both the console and the command line.

<span id="方式一：控制台"></span>
## Method 1: Console


1. Enter custom tasks [console](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/customTask/create)

2. configuration environment

   1. Configure mirrors at Custom mirrors.

   ```bash
   vemlp-cn-beijing.cr.volces.com/preset-images/vetuner:0.0.1
   ```
   

   2. Fill in the entry commands and define environment variables. Please note that the path mounted by tos on the development machine is inconsistent with the path mounted in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path mounted in custom tasks.

   ```bash
   bash ./vemlp/train/train.sh vemlp/train/configs/sft_llama3.yaml checkpointing.save_dir=/vemlp-demo-models/demo-vetuner/ckpt/experiments/ checkpointing.load_dir=/vemlp-demo-models/demo-vetuner/ckpt/experiments/ training.micro_batch_size=5 tokenizer.pretrained_model_name_or_path=/vemlp-demo-models/model-llama/Meta-Llama-3.1-8B model.pretrained_model_name_or_path=/vemlp-demo-models/model-llama/Meta-Llama-3.1-8B dataset.train_file=/vemlp-demo-models/datasets-vetuner/Text-to-sql/train.parquet checkpointing.use_veturboio=False logging.use_wandb_log=True training.train_iters=1000 model.attn_impl=flash_attn
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f3ffceca0f44cafa40f957bfd4b2077~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca85549f02254c8dab1f77782d4afa50~tplv-goo7wpa0wc-image.image) </span>

3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 8\-card ml.hpcpni2l.

   2. Mount SFCS and configure AK/SK.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1078da4e09684523892647dccad03f06~tplv-goo7wpa0wc-image.image) </span>


<span id="方式二：命令行"></span>
## Method 2: Command Line

Use the following command in Terminal to fine tune the Llama \- 3.1\-8 B model.


1. Create a **demo\-vetuner\-train.yaml** file.

2. Edit the YAML file and fill in the mirror, resource specifications, environment variables, and entry commands.

3. Run the task command. If the result is run, the words " **Create task was successful, task_id** " will appear in the Terminal. The complete training duration is expected to be around 13 minutes.


```bash
volc ml_task submit --conf=/vemlp-demo-models/demo-vetuner-train.yaml
```


**Example demo\-vetuner\-train.yaml** file:

```bash
TaskName:  "finetine-with-veTuner-for-llama3"
Description:  ""

Tags: []
ImageUrl:  "vemlp-cn-beijing.cr.volces.com/preset-images/vetuner:0.0.1"

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
    - Name:  "VETURBOIO_USE_SFCS_SDK"
        Value:  "false" 
    - Name:  "AK"
        Value:  "****************" Please replace it with your own AK.
    - Name:  "SK"
        Value:  "****************" Please replace it with your own SK.
    - Name:  "WANDB_REGION"
        Value:  "cn-beijing" 
AccessType:  "Queue"

Storages:
        - Type:  "Sfcs"                     
            MountPath:  "/vemlp-demo-models"
            Bucket:  "vemlp-demo-models"
            Prefix:  "/"
      FsName:  "****"
      CachePolicyId:  "****************" #Please replace with your own cache policy ID
            SfcsId:  "****************" Please replace it with your own SFCSID.

Entrypoint: |
  bash ./vemlp/train/train.sh vemlp/train/configs/sft_llama3.yaml checkpointing.save_dir=/vemlp-demo-models/ckpt/experiments/ checkpointing.load_dir=/vemlp-demo-models/ckpt/experiments/ training.micro_batch_size=5 tokenizer.pretrained_model_name_or_path=/vemlp-demo-models/model-llama/Meta-Llama-3.1-8B model.pretrained_model_name_or_path=/vemlp-demo-models/model-llama/Meta-Llama-3.1-8B dataset.train_file=/vemlp-demo-models/datasets-vetuner/Text-to-sql/train.parquet checkpointing.use_veturboio=False logging.use_wandb_log=True training.train_iters=1000 model.attn_impl=flash_attn
```


<span id="步骤四：模型离线评测"></span>
# Step 4: Model offline evaluation

After completing training, you can validate the fine\-tuned model performance through offline evaluation. The best practices document provides instructions for both the console and the command line.

<span id="方式一：控制台"></span>
## Method 1: Console


1. Enter custom tasks [console](https://console.volcengine.com/ml-platform/region:ml-platform+cn-beijing/customTask/create)

2. configuration environment

   1. Configure mirrors at Custom mirrors.

   ```bash
   vemlp-cn-beijing.cr.volces.com/preset-images/vetuner:0.0.1
   ```
   

   2. Fill in the entry commands and define environment variables. Please note that the path mounted by tos on the development machine is inconsistent with the path mounted in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path mounted in custom tasks.

   ```bash
   bash ./vemlp/eval/eval.sh ./vemlp/eval/configs/eval_text2sql.yaml dataset.validation_file=/vemlp-demo-models/datasets-vetuner/Text-to-sql/validation.parquet tokenizer.pretrained_model_name_or_path=/vemlp-demo-models/model-llama/Meta-Llama-3.1-8B model.pretrained_model_name_or_path=/vemlp-demo-models/demo-vetuner/ckpt/experiments/step-1000
   ```
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b088016091b410781d546ba6737882c~tplv-goo7wpa0wc-image.image) </span>


3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 1\-card ml.hpcpni2l.

   2. Mount SFCS and configure AK/SK.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12613cd50d60495691330724f33aac01~tplv-goo7wpa0wc-image.image) </span>


<span id="方式二：命令行"></span>
## Method 2: Command Line

In Terminal, use the following command to perform offline evaluation of the fine\-tuning model. The specific operation steps are as follows.


1. Create a **demo\-vetuner\-validation .yaml** file.

2. Edit the YAML file and fill in the mirror, resource specifications, environment variables, and entry commands.

3. Run the task command. If the result is run, the words " **Create task was successful, task_id** " will appear in the Terminal. The full operating time is expected to be around 12 minutes.


```bash
volc ml_task submit --conf=/vemlp-demo-models/demo-vetuner-validation.yaml
```


**demo\-vetuner\-validation .yaml** file example:

```bash
TaskName:  "interference-with-veTuner-for-llama3"
Description:  ""

Tags: []
ImageUrl:  "vemlp-cn-beijing.cr.volces.com/preset-images/vetuner:0.0.1"

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
                GPUNum: 1

Envs:
    - Name:  "VETURBOIO_USE_SFCS_SDK"
        Value:  "false" 
    - Name:  "AK"
        Value:  "****************" Please replace it with your own AK.
    - Name:  "SK"
        Value:  "****************" Please replace it with your own SK.
    - Name:  "WANDB_REGION"
        Value:  "cn-beijing" 
        
AccessType:  "Queue"

Storages:
    - Type:  "Sfcs"                     
        MountPath:  "/vemlp-demo-models"
        Bucket:  "vemlp-demo-models"
        Prefix:  "/"
         FsName:  "****" #Please replace it with your own instance name
         CachePolicyId:  "****************" #Please replace with your own cache policy ID
        SfcsId:  "****************" Please replace it with your own SFCSID.

Entrypoint: |
  bash ./vemlp/eval/eval.sh ./vemlp/eval/configs/eval_text2sql.yaml dataset.validation_file=/vemlp-demo-models/datasets-vetuner/Text-to-sql/validation.parquet tokenizer.pretrained_model_name_or_path=/vemlp-demo-models/model-llama/Meta-Llama-3.1-8B model.pretrained_model_name_or_path=/vemlp-demo-models/demo-vetuner/ckpt/experiments/step-1000
```
