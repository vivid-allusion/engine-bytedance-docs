---
title: "Offline FP8 Static Quantization -- LlaMA3.1-8B Best Practices Document"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Offline_FP8_Static_Quantization_--_LlaMA31-8B_Best_Practices_Document"
---

Machine Learning Platform is a platform for professional algorithm engineers to integrate cloud\-native tools + computing power (GPU, CPU Cloud as a Service) for one\-stop AI algorithm development and iteration. This program will show you how to perform FP8 offline quantization on the open source model of Meta \- Llama \- 3.1\-8 B in MLP.

<span id="使用前提"></span>
# premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself.</div>


This solution takes the FP8 offline quantization of the Meta \- Llama \- 3.1\-8 B model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* Activated network/TOS/CFS. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [Console Quick Start -- Torch Object Storage - BytePlus ](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1), .

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

   * Resource Specifications: Configure the following resource specifications.

      * CPU instance: 8C/64G/20GB cloud disk.

      * GPU card count: Best practice is to use one ml.gni3cgd.

   * Mount configuration: Mount TOS bucket and CFS, see [How the training code accesses the TOS](https://docs.byteplus.com/docs/mlp/53984).

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

2. Configure volc configure. For details, please refer to .

3. Execute the following command in Terminal to download the Llama \- 3.1\-8 B model from the mirror source and open the bucket path to Mount.


```bash
cd /vemlp-demo-models
mkdir model-llama-fp8
cd model-llama-fp8
pip3 install -U huggingface_hub
export HF_ENDPOINT=https://hf-mirror.com
huggingface-cli download --token $HF_TOKEN --resume-download meta-llama/Meta-Llama-3.1-8B-Instruct --local-dir $ORIGINAL_MODEL_PATH
```


To run **huggingface\-cli** , the list of parameters that need to be passed in is as follows:


|Parameter |Description |
|---|---|
|**hf_token** |hf_token for Huggingface accounts with llama usage permissions. |
|**original_model_path** |Source safetensor path. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">\-\-Token/\-\- hf_username/\-\- hf_token and other parameters are not necessary, only some Repo has license restrictions, you need to log in to apply for permission. If necessary, download the token after https://huggingface.co/settings/tokens.</div>


2. <div data-tips="true" data-tips-type="tip">It is recommended that you set the model file, the download and storage address of the training dataset in the shared storage such as TOS/VEPFS/SCFS, so that it can be more easily mounted on different machines when performing cross\-node tasks such as training and inference.</div>



<span id="步骤二：准备数据集"></span>
# Step 2: Prepare the dataset

Execute the following command in Terminal to directly download the open source ultrachat_2k dataset to assist with FP8 static quantization calibration.

```bash
cd /vemlp-demo-models
mkdir datasets-llama-fp8
cd datasets-llama-fp8
export HF_ENDPOINT=https://hf-mirror.com
huggingface-cli download --repo-type dataset --resume-download mgoin/ultrachat_2k --local-dir $CALIB_DATASET_PATH
```


The parameters are described as follows:


|Parameter |Description |
|---|---|
|**calib_dataset_path** |The path to the dataset used to validate the quantization results. |


<span id="步骤三：在开发机中执行量化"></span>
# Step 3: Perform quantization in Dev boxes

<span id="_3-1-使用autofp8量化模型"></span>
## 3.1 Using AutoFP8 to quantify models


1. Create quantization script **fp8\-quant.py** by executing the following command in Terminal.


```bash
cd /vemlp-demo-models
touch fp8-quant.py
```



2. Edit the script content and replace it with the information that needs to be configured.


```bash
import os
from auto_fp8 import BaseQuantizeConfig
from auto_fp8 import AutoFP8ForCausalLM
from transformers import AutoTokenizer
from datasets import load_dataset

#Model, dataset address configuration
os.environ['BASE_MODEL_PATH'] = '/vemlp-demo-models/model-llama-fp8/Meta-Llama-3.1-8B'
os.environ['CALIB_DATASET_PATH'] = '/vemlp-demo-models/datasets-llama-fp8/'
os.environ['QUANT_MODEL_PATH'] = '/vemlp-demo-models/model-quant-fp8'

model_path = os.getenv('BASE_MODEL_PATH')
dataset_path = os.getenv('CALIB_DATASET_PATH')
quant_path = os.getenv('QUANT_MODEL_PATH')


quantize_config = BaseQuantizeConfig(
    quant_method="fp8",
    activation_scheme="static",
    ignore_patterns=["re:.*lm_head"],
)

tokenizer = AutoTokenizer.from_pretrained(model_path)
tokenizer.pad_token = tokenizer.eos_token
model = AutoFP8ForCausalLM.from_pretrained(model_path, quantize_config)

ds = load_dataset(dataset_path, split="train_sft").select(range(512))
examples = [tokenizer.apply_chat_template(batch["messages"], tokenize=False) for batch in ds]
examples = tokenizer(examples, padding=True, truncation=True, return_tensors="pt").to("cuda")

model.quantize(examples)

#Save model and tokenizer
model.save_quantized(quant_path)
tokenizer.save_pretrained(quant_path)
```


<span id="_3-2-创建shell脚本并执行"></span>
## 3.2 Creating Shell Scripts and Executing Them


1. Create shell script **fp8\-quant.sh** by executing the following command in Terminal. Make sure fp8\-quant.sh fp8\-quant.py two files in the same directory level.


```bash
cd /vemlp-demo-models/
touch fp8-quant.sh
```



2. Edit the script content and replace it with the information that needs to be configured.


```bash
set -ex
pip install git+https://github.com/neuralmagic/AutoFP8.git@2cd265ff
python3 fp8-quant.py
echo "Finished Model Quantization Task"
```



3. Execute the script.


```bash
cd /vemlp-demo-models/
bash ./fp8-quant.sh
```


After the execution is complete, the output path file is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da3e43b84f081a854df2ca6172d65d80.png) </span>

<span id="_3-3-量化后模型对比"></span>
## 3.3 Comparison of models after quantification


1. Execute the following command in Terminal to compare the base model and the quantized model before quantization.


```bash
du -sh $BASE_MODEL_PATH $QUANT_MODEL_PATH
```


The comparison results are as follows: It can be seen that in terms of model capacity, the size of the model after AWQ 4\-bit quantization is about 1/3 of the model before quantization.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80340de928aafe1d3806c71a48727573.png) </span>


2. Execute the following command in Terminal to compare the config.json files before and after quantization.


```bash
diff $QUANT_MODEL_PATH/config.json $BASE_MODEL_PATH/config.json
```


The comparison results are as follows: It can be seen that the model after quantification has more information about quantification \- quantization_config.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_38ab79ad195393406b2061880831bf83.png) </span>

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
   cat > fp8-quant.py <<EOF
   import os
   from auto_fp8 import BaseQuantizeConfig
   from auto_fp8 import AutoFP8ForCausalLM
   from transformers import AutoTokenizer
   from datasets import load_dataset
   
   #Model, dataset address configuration
   os.environ['BASE_MODEL_PATH'] = '/vemlp-demo-models/model-llama-fp8/Meta-Llama-3.1-8B'
   os.environ['CALIB_DATASET_PATH'] = '/vemlp-demo-models/datasets-llama-fp8/'
   os.environ['QUANT_MODEL_PATH'] = '/vemlp-demo-models/model-quant-fp8'
   
   model_path = os.getenv('BASE_MODEL_PATH')
   dataset_path = os.getenv('CALIB_DATASET_PATH')
   quant_path = os.getenv('QUANT_MODEL_PATH')
   
   
   quantize_config = BaseQuantizeConfig(
       quant_method="fp8",
       activation_scheme="static",
       ignore_patterns=["re:.*lm_head"],
   )
   
   tokenizer = AutoTokenizer.from_pretrained(model_path)
   tokenizer.pad_token = tokenizer.eos_token
   model = AutoFP8ForCausalLM.from_pretrained(model_path, quantize_config)
   
   ds = load_dataset(dataset_path, split="train_sft").select(range(512))
   examples = [tokenizer.apply_chat_template(batch["messages"], tokenize=False) for batch in ds]
   examples = tokenizer(examples, padding=True, truncation=True, return_tensors="pt").to("cuda")
   
   model.quantize(examples)
   
   #Save model and tokenizer
   model.save_quantized(quant_path)
   tokenizer.save_pretrained(quant_path)
   EOF
   
   git clone https://github.com/neuralmagic/AutoFP8.git model-quant/AutoFP8
   cd model-quant/AutoFP8 && git checkout 2cd265ff
   python3 fp8-quant.py
   ```
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b40ab8ca0e7743d8b7978b5759a66125~tplv-goo7wpa0wc-image.image) </span>


3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use a stand\-alone 8\-card ml.gni3cgd.

   2. Mount TOS and CFS. Note: The path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the environment variables, make sure it is the path of Mount in custom tasks.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5eaaa258f5db44aca83dfffe2875840c~tplv-goo7wpa0wc-image.image) </span>

<span id="方式二：命令行"></span>
## Method 2: Command Line


1. Execute the following command in Terminal to edit fp8\-quant.py. Change the cloud disk access path in the Dev boxes to the access path in custom tasks.


```bash
import os
from auto_fp8 import BaseQuantizeConfig
from auto_fp8 import AutoFP8ForCausalLM
from transformers import AutoTokenizer
from datasets import load_dataset

#Model, dataset address configuration
os.environ['BASE_MODEL_PATH'] = '/data/model-llama-fp8/Meta-Llama-3.1-8B'
os.environ['CALIB_DATASET_PATH'] = '/data/datasets-llama-fp8/'
os.environ['QUANT_MODEL_PATH'] = '/data/model-quant-fp8'

model_path = os.getenv('BASE_MODEL_PATH')
dataset_path = os.getenv('CALIB_DATASET_PATH')
quant_path = os.getenv('QUANT_MODEL_PATH')

quantize_config = BaseQuantizeConfig(
    quant_method="fp8",
    activation_scheme="static",
    ignore_patterns=["re:.*lm_head"],
)

tokenizer = AutoTokenizer.from_pretrained(model_path)
tokenizer.pad_token = tokenizer.eos_token
model = AutoFP8ForCausalLM.from_pretrained(model_path, quantize_config)

ds = load_dataset(dataset_path, split="train_sft").select(range(512))
examples = [tokenizer.apply_chat_template(batch["messages"], tokenize=False) for batch in ds]
examples = tokenizer(examples, padding=True, truncation=True, return_tensors="pt").to("cuda")

model.quantize(examples)

#Save model and tokenizer
model.save_quantized(quant_path)
tokenizer.save_pretrained(quant_path)
```



2. Create a **fp8\-quantization\-task .yaml** file in Terminal to perform the quantified custom tasks.


```bash
cd /vemlp-demo-models/
touch fp8-quantization-task.yaml
```



3. Edit the YAML file submitted by the quantification task.


```bash
TaskName:  "Quant-Meta-Llama-3-1-8B-Instruct-FP8-INT4"
Description:  "Use FP8 static to quantize Meta-Llama-3.1-8B-Instruct"
Entrypoint: |
    cd  /data && bash ./fp8-quant.sh

Tags: []

Envs: []

ResourceQueueID:  "q-**************"        #replace_with_your_ResourceQueueID
Framework:  "PyTorchDDP"
TaskRoleSpecs:                                                              #replace_with_your_TaskRoleSpecs
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

Storages:                                                                #replace_with_your_Storages
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
volc ml_task submit --conf=/vemlp-demo-models/fp8-quantization-task.yaml
```



5. Please refer to the above for the comparison of the quantitative model before and after.
