---
title: "GPTQ Quantization -- LlaMA3.1-8B Best Practices Document"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/GPTQ_Quantization_--_LlaMA3_1-8B_Best_Practices_Document"
---

Machine Learning Platform is a platform for professional algorithm engineers to integrate cloud\-native tools + computing power (GPU, CPU Cloud as a Service) for one\-stop AI algorithm development and iteration. This program will show you how to perform GPTQ quantization on the open source model of Meta \- Llama \- 3.1\-8 B in MLP.

<span id="使用前提"></span>
# Premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself.</div>


This program takes the GPTQ quantization of the Meta \- Llama \- 3.1\-8 B model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* Activated network/TOS/CFS. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [Console Quick Start -- Torch Object Storage - BytePlus ](https://www.volcengine.com/docs/6349/74830), [Access File Storage Instance -- Cloud File System - BytePlus ](https://www.volcengine.com/docs/6720/107803).

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

* Resource Specifications: Configure the following resource specifications.

   \* CPU instance: 8C/64G/20GB cloud disk.

   \* GPU card count: Best practice is to use one ml.gni3cgd.

   * Mount configuration: Mount TOS bucket and CFS, see [training code how to access TOS - Machine Learning Platform - BytePlus ](https://www.volcengine.com/docs/6459/72362).

   * Mirror address: Configure the following mirror at the custom mirror, fill in the SSH key and Mount TOS. Creating Dev boxes for the first time is expected to take 20 minutes due to the large mirror being pulled.

      ```bash
      vemlp-demo-cn-shanghai.cr.volces.com/demo/quantization:1.0
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
mkdir model-llama-gptq
cd model-llama-gptq
pip3 install -U huggingface_hub
export HF_ENDPOINT=https://hf-mirror.com
huggingface-cli download --token $HF_TOKEN --resume-download meta-llama/Meta-Llama-3.1-8B-Instruct --local-dir $ORIGINAL_MODEL_PATH
```


The list of parameters required to run **huggingface\-cli** is described as follows:


|Parameter |Description |
|---|---|
|**hf_token** |hf_token for Huggingface accounts with llama usage permissions. |
|**original_model_path** |Source safetensor path. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">\-\-Token/\-\- hf_username/\-\- hf_token and other parameters are not necessary, only some Repo has license restrictions, you need to log in to apply for permission. If necessary, download the token after https://huggingface.co/settings/tokens.</div>


2. <div data-tips="true" data-tips-type="tip">It is recommended that you set the model file, the download and storage address of the training dataset in the shared storage such as TOS/VEPFS/SCFS, so that it can be more easily mounted on different machines when performing cross\-node tasks such as training and inference.</div>



<span id="步骤二：准备数据集"></span>
# Step 2: Prepare the dataset

Execute the following command in the Terminal to directly download the open\-source wikitext2 dataset to assist with GPTQ quantification calibration.

```bash
cd /vemlp-demo-models
mkdir datasets-llama-gptq
cd datasets-llama-gptq
pip3 install -U huggingface_hub
export HF_ENDPOINT=https://hf-mirror.com
huggingface-cli download --repo-type dataset --resume-download carlosejimenez/wikitext__wikitext-2-raw-v1 --local-dir $CALIB_DATASET_PATH
```


The parameters are described as follows:


|Parameter |Description |
|---|---|
|**calib_dataset_path** |The path to the dataset used to validate the quantization results. |


<span id="步骤三：在开发机中执行量化"></span>
# Step 3: Perform quantization in Dev boxes

<span id="_3-1-使用autogptq量化模型"></span>
## 3.1 Using the AutoGPTQ Quantization Model


1. Create quantization script **gptq\-quant.py** by executing the following command in Terminal.


```bash
cd /vemlp-demo-models
touch gptq-quant.py
```



2. Edit the script content and replace it with the information that needs to be configured.


```bash
import os
from transformers import AutoTokenizer
from auto_gptq import AutoGPTQForCausalLM
from auto_gptq import BaseQuantizeConfig

def get_wikitext2_dataset(nsamples, seed, seqlen, tokenizer):
    import numpy as np
    import torch
    import torch.nn as nn
    from datasets import load_dataset

    traindata = load_dataset(dataset_path, split="train")
    testdata = load_dataset(dataset_path, split="test")

    trainenc = tokenizer("\n\n".join(traindata["text"]), return_tensors="pt")
    testenc = tokenizer("\n\n".join(testdata["text"]), return_tensors="pt")

    import random

    random.seed(seed)
    np.random.seed(0)
    torch.random.manual_seed(0)

    traindataset = []
    for _ in range(nsamples):
        i = random.randint(0, trainenc.input_ids.shape[1] - seqlen - 1)
        j = i + seqlen
        inp = trainenc.input_ids[:, i:j]
        attention_mask = torch.ones_like(inp)
        traindataset.append({"input_ids": inp, "attention_mask": attention_mask})
    return traindataset, testenc

#Configure the model and dataset address
os.environ['BASE_MODEL_PATH'] = '/vemlp-demo-models/model-llama-gptq/Meta-Llama-3.1-8B'
os.environ['CALIB_DATASET_PATH'] = '/vemlp-demo-models/datasets-llama-gptq/'
os.environ['QUANT_MODEL_PATH'] = '/vemlp-demo-models/model-quant-gptq'

model_path = os.getenv('BASE_MODEL_PATH')
dataset_path = os.getenv('CALIB_DATASET_PATH')
quant_path = os.getenv('QUANT_MODEL_PATH')

#Set quantization hyperparameters
quantize_config = BaseQuantizeConfig(
    bits=4,  #Quantify with GPTQ INT4
    group_size=128,  #The GPTQ recommended packet size is 128
    desc_act=False,  #Set to False to significantly speed up inference, but model confusion may be slightly worse
)


model = AutoGPTQForCausalLM.from_pretrained(model_path, quantize_config)
tokenizer = AutoTokenizer.from_pretrained(model_path)

traindataset, testenc = get_wikitext2_dataset(128, 0, 2048, tokenizer)


model.quantize(traindataset)


model.save_quantized(quant_path, use_safetensors=True)
tokenizer.save_pretrained(quant_path)
```


<span id="_3-2-创建shell脚本并执行"></span>
## 3.2 Creating Shell Scripts and Executing Them


1. Create shell script **qptq\-quant.sh** by executing the following command in Terminal. Make sure qptq\-quant.sh qptq\-quant.py two files in the same directory level.


```bash
cd /vemlp-demo-models/
touch gptq-quant.sh
```



2. Edit the script content and replace it with the information that needs to be configured.


```bash
set  -ex
pip install git+https://gh-proxy.com/https://github.com/AutoGPTQ/AutoGPTQ.git@097dd04e2f
python3 gptq-quant.py
echo "Finished Model Quantization Task"
```



3. Execute the script.


```bash
cd /vemlp-demo-models/
bash ./gptq-quant.sh
```


After the execution is complete, the output path file is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_09066de55ec03b536a17531c9f27902f.png) </span>

<span id="_3-3-量化后模型对比"></span>
## 3.3 Comparison of models after quantification


1. Execute the following command in Terminal to compare the base model and the quantized model before quantization.


```bash
du -sh $BASE_MODEL_PATH $QUANT_MODEL_PATH
```


The list of parameters that need to be passed in is described as follows:


|Parameter |Description |
|---|---|
|**base_model_path** |Llama3\-8b model path. |
|**quant_model_path** |Model path after GPTQ quantization. |


The comparison results are as follows: It can be seen that the size of the model after GPTQ 4\-bit quantization is about 1/3 of the model before quantization.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9559919cf3379db15112b71abfc52c98.png) </span>


2. Execute the following command in Terminal to compare the config.json files before and after quantization.


```bash
diff $QUANT_MODEL_PATH/config.json $BASE_MODEL_PATH/config.json
```


The comparison results are as follows: It can be seen that the model after quantification has more information about quantification \- quantization_config.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_334114cd0b38bf7e3f508f69e84c0d3a.png) </span>

<span id="步骤四：在自定义任务中执行量化"></span>
# Step 4: Quantify in custom tasks

<span id="方式一：控制台"></span>
## Method 1: Console


1. Enter custom tasks [console](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/customTask/create)

2. configuration environment

   1. Configure mirrors at Custom mirrors.

   ```bash
   vemlp-demo-cn-shanghai.cr.volces.com/demo/quantization:1.0
   ```
   

   3. Fill in the entrance command. Please note that the path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path of Mount in custom tasks.

   ```python
   cat > gptq-quant.py <<EOF
   import os
   from transformers import AutoTokenizer
   from auto_gptq import AutoGPTQForCausalLM
   from auto_gptq import BaseQuantizeConfig
   
   def get_wikitext2_dataset(nsamples, seed, seqlen, tokenizer):
       import numpy as np
       import torch
       import torch.nn as nn
       from datasets import load_dataset
   
       traindata = load_dataset(dataset_path, split="train")
       testdata = load_dataset(dataset_path, split="test")
   
       trainenc = tokenizer("\n\n".join(traindata["text"]), return_tensors="pt")
       testenc = tokenizer("\n\n".join(testdata["text"]), return_tensors="pt")
   
       import random
   
       random.seed(seed)
       np.random.seed(0)
       torch.random.manual_seed(0)
   
       traindataset = []
       for _ in range(nsamples):
           i = random.randint(0, trainenc.input_ids.shape[1] - seqlen - 1)
           j = i + seqlen
           inp = trainenc.input_ids[:, i:j]
           attention_mask = torch.ones_like(inp)
           traindataset.append({"input_ids": inp, "attention_mask": attention_mask})
       return traindataset, testenc
   
   
   #Model, dataset address configuration
   os.environ['BASE_MODEL_PATH'] = '/vemlp-demo-models/model-llama/Meta-Llama-3.1-8B'
   os.environ['CALIB_DATASET_PATH'] = '/vemlp-demo-models/datasets-llama-quant/'
   os.environ['QUANT_MODEL_PATH'] = '/vemlp-demo-models/model-quant-gptq'
   
   model_path = os.getenv('BASE_MODEL_PATH')
   dataset_path = os.getenv('CALIB_DATASET_PATH')
   quant_path = os.getenv('QUANT_MODEL_PATH')
   
   #Set quantization hyperparameters
   quantize_config = BaseQuantizeConfig(
       bits=4,  #Quantify with GPTQ INT4
       group_size=128,  #The GPTQ recommended packet size is 128
       desc_act=False,  #Set to False to significantly speed up inference, but model confusion may be slightly worse
   )
   
   model = AutoGPTQForCausalLM.from_pretrained(model_path, quantize_config)
   tokenizer = AutoTokenizer.from_pretrained(model_path)
   
   traindataset, testenc = get_wikitext2_dataset(128, 0, 2048, tokenizer)
   
   model.quantize(traindataset)
   
   model.save_quantized(quant_path, use_safetensors=True)
   tokenizer.save_pretrained(quant_path)
   
   EOF
   
   pip install git+https://gh-proxy.com/https://github.com/AutoGPTQ/AutoGPTQ.git@097dd04e2f
   python3 gptq-quant.py
   ```
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/950161c13ff74cfa989a357e9936d06f~tplv-goo7wpa0wc-image.image) </span>


3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 8\-card ml.gni3cgd.

   2. Mount TOS and CFS. It should be noted that the path mounted by tos on the development machine is inconsistent with the path mounted in custom tasks. When filling in the model path in environment variables, you need to ensure that it is the path mounted in custom tasks.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9177bc9d376c4f428e3abe393f3b0def~tplv-goo7wpa0wc-image.image) </span>

<span id="方式二：命令行"></span>
## Method 2: Command Line


1. Execute the following command in Terminal to edit the **gptq\-quant.py** . Change the cloud disk access path in the Dev boxes to the access path in custom tasks.


```bash
import os
from transformers import AutoTokenizer
from auto_gptq import AutoGPTQForCausalLM
from auto_gptq import BaseQuantizeConfig

def get_wikitext2_dataset(nsamples, seed, seqlen, tokenizer):
    import numpy as np
    import torch
    import torch.nn as nn
    from datasets import load_dataset

    traindata = load_dataset(dataset_path, split="train")
    testdata = load_dataset(dataset_path, split="test")

    trainenc = tokenizer("\n\n".join(traindata["text"]), return_tensors="pt")
    testenc = tokenizer("\n\n".join(testdata["text"]), return_tensors="pt")

    import random

    random.seed(seed)
    np.random.seed(0)
    torch.random.manual_seed(0)

    traindataset = []
    for _ in range(nsamples):
        i = random.randint(0, trainenc.input_ids.shape[1] - seqlen - 1)
        j = i + seqlen
        inp = trainenc.input_ids[:, i:j]
        attention_mask = torch.ones_like(inp)
        traindataset.append({"input_ids": inp, "attention_mask": attention_mask})
    return traindataset, testenc

#Configure the model and dataset address
os.environ['BASE_MODEL_PATH'] = '/data/model-llama-gptq/Meta-Llama-3.1-8B'
os.environ['CALIB_DATASET_PATH'] = '/data/datasets-llama-gptq/'
os.environ['QUANT_MODEL_PATH'] = '/data/model-quant-gptq'

model_path = os.getenv('BASE_MODEL_PATH')
dataset_path = os.getenv('CALIB_DATASET_PATH')
quant_path = os.getenv('QUANT_MODEL_PATH')

#Set quantization hyperparameters
quantize_config = BaseQuantizeConfig(
    bits=4,  #Quantify with GPTQ INT4
    group_size=128,  #The GPTQ recommended packet size is 128
    desc_act=False,  #Set to False to significantly speed up inference, but model confusion may be slightly worse
)


model = AutoGPTQForCausalLM.from_pretrained(model_path, quantize_config)
tokenizer = AutoTokenizer.from_pretrained(model_path)

traindataset, testenc = get_wikitext2_dataset(128, 0, 2048, tokenizer)


model.quantize(traindataset)


model.save_quantized(quant_path, use_safetensors=True)
tokenizer.save_pretrained(quant_path)
```



2. Create a **gptq\-quantization\-task .yaml** file in Terminal to perform the quantified custom tasks.


```bash
cd /vemlp-demo-models/
touch gptq-quantization-task.yaml
```



3. Edit the YAML file submitted by the quantification task.


```bash
TaskName:  "Quant-Meta-Llama-3-1-8B-Instruct-GPTQ-INT4"
Description:  "Use GPTQ to quantize Meta-Llama-3.1-8B-Instruct in INT4 format"
Entrypoint: |
    cd  /data && bash ./gptq-quant.sh

Tags: []

Envs: []

ResourceQueueID:  "q-**************"        #Please replace with your own ResourceQueueID
Framework:  "PyTorchDDP"
TaskRoleSpecs:                                                              #Please replace with your own TaskRoleSpecs
        - RoleName:  "worker"
            RoleReplicas: 1
            Flavor:  "custom"
            ResourceSpec:
                    Family:  "ml.gni3cgd"
                    CPU: 165.000
                    Memory: 865.000
                    GPUNum: 8

ActiveDeadlineSeconds: 3600

EnableTensorBoard: False

Storages:                                                                #Please replace it with your own Storages
        - Type:  "Tos"
            MountPath:  "/data"
            Bucket:  "vemlp-demo-models"
            FsName": "testmodel"
            MetaCacheExpiryMinutes: "-1"

ImageUrl: "vemlp-demo-cn-shanghai.cr.volces.com/demo/quantization:1.0"

CacheType: "Cloudfs"

RetryOptions:
        EnableRetry: False
        MaxRetryTimes: 5
        IntervalSeconds: 120
        PolicySets: []
```



4. Execute the following command in Terminal to commit custom tasks.


```bash
volc ml_task submit --conf=/vemlp-demo-models/gptq-quantization-task.yaml
```



5. Please refer to the above for the comparison of the quantitative model before and after.
