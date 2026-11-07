---
title: "AWQ Quantization - Best Practices for LlaMA3.1-8B in MLP"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/AWQ_Quantization_-_Best_Practices_for_LlaMA3-1-8B_in_MLP"
---

Machine Learning Platform is a platform for professional algorithm engineers to integrate cloud\-native tools + computing power (GPU, CPU Cloud as a Service) for one\-stop AI algorithm development and iteration. This solution will show you how to perform AWQ quantization on the open source model of Meta \- Llama \- 3.1\-8 B in MLP.

<span id="使用前提"></span>
# premise of use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In practice, if the model, dataset or quantization tool cannot be downloaded to the TOS bucket due to network problems, it is recommended that you download it to the Dev boxes cloud disk first, and then copy it to the TOS path by yourself.</div>


This solution takes AWQ quantization of the Meta \- Llama \- 3.1\-8 B model as an example. Before starting the operation, please confirm that you have completed the following preparations:


* Activated network/TOS/CFS. For details, please refer to [Change the load network of the Prepaid resource group VPC -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Change_the_load_network_VPC_of_a_prepaid_resource_group), [Console Quick Start -- Torch Object Storage - BytePlus ](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1), .

* Purchased MLP resources, see [Create Resource Group -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_a_resource_queue). For resource pricing details, see [Instance Specifications and Pricing -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).

* Created Dev boxes instance with key parameters configured as follows. For details, see [Create Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes).

   * Resource Specifications: Configure the following resource specifications.

      * CPU instance: 8C/64G/20GB cloud disk.

      * GPU card count: Best practice is to use one xni3c.

   * Mount configuration: Mount TOS bucket and CFS, see [How the training code accesses the TOS](https://docs.byteplus.com/docs/mlp/53984).

   * Mirror address: Configure the following mirror at the custom mirror, fill in the SSH key and Mount TOS. Creating Dev boxes for the first time is expected to take 20 minutes due to the large mirror being pulled.

      ```bash
        vemlp-demo-cn-shanghai.cr.volces.com/demo/quantization:1.0
      ```
      


<span id="步骤一：环境配置"></span>
# Step 1: Environment Configuration


1. Enter the Dev boxes.

   1. Login [Account Login - BytePlus ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/dashboard).

   2. Click Dev boxes in the left navigation bar, and click the name of the Dev boxes to be operated on the Dev boxes list page to enter the corresponding Dev boxes.

   3. Remote login Dev boxes through SSH, for details, see [Remote connection through SSH Dev boxes -- Machine Learning Platform - BytePlus ](https://docs.byteplus.com/en/docs/mlp/Remote_connection_to_Dev_boxes_via_SSH).

2. Configure volc configure. For details, please refer to[ ](https://www.volcengine.com/docs/6459/72394).


```bash
#Configure AK/SK, and the Region of the environment
volc configure
```



3. Configure the Huggingface environment.


```bash
export HF_TOKEN=<User Specific Huggingface Access Token> 
export HF_ENDPOINT=https://hf-mirror.com 、
pip3 install -U huggingface_hub
```


The parameters are described as follows:


|Parameter |Description |
|---|---|
|**hf_token** |hf_token for Huggingface accounts with llama usage permissions. |
|**hf_endpoint** |Mirror address. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">\-\-Token/\-\- hf_username/\-\- hf_token and other parameters are not necessary, only some Repo has license restrictions, you need to log in to apply for permission. If necessary, download the token after https://huggingface.co/settings/tokens.</div>


2. <div data-tips="true" data-tips-type="tip">It is recommended that you set the model file, the download and storage address of the training dataset in the shared storage such as TOS/VEPFS/SCFS, so that it can be more easily mounted on different machines when performing cross\-node tasks such as training and inference.</div>



<span id="步骤二：准备-llama-3-1-8b-模型"></span>
# Step 2: Prepare the Llama 3.1\-8 B model


1. Execute the following command in Terminal to download the Llama \- 3.1\-8 B model from the mirror source and open the bucket path to Mount.


```bash
cd /vemlp-demo-models
mkdir model-llama-awq
cd model-llama-awq
huggingface-cli download --token $HF_TOKEN --resume-download meta-llama/Meta-Llama-3.1-8B-Instruct --local-dir $ORIGINAL_MODEL_PATH
```


To run the **huggingface\-cli** command line, the list of parameters that need to be passed in is as follows:


|Parameter |Description |
|---|---|
|**hf_token** |hf_token for Huggingface accounts with llama usage permissions. |
|**original_model_path** |The local storage path for the underlying model. |


<span id="步骤三：准备数据集"></span>
# Step 3: Prepare the dataset

Execute the following command in Terminal to directly download the open\-source wikitext2 dataset to assist AWQ with quantification calibration.

```bash
cd /vemlp-demo-models
mkdir datasets-llama-awq
huggingface-cli download --repo-type dataset --resume-download carlosejimenez/wikitext__wikitext-2-raw-v1 --local-dir $CALIB_DATASET_PATH
```


The parameters are described as follows:


|Parameter |Description |
|---|---|
|**calib_dataset_path** |The path to the dataset used to validate the quantization results. |


<span id="步骤四：在开发机中执行量化"></span>
# Step 4: Perform quantization in Dev boxes

<span id="_4-1-创建量化脚本"></span>
## 4.1 Creating quantitative scripts


1. Create quantization script **awq\-quant.py** by executing the following command in Terminal.


```bash
cd /vemlp-demo-models
touch awq-quant.py
```



2. Edit the script content and replace it with the information that needs to be configured.


```bash
import os
from awq import AutoAWQForCausalLM
from transformers import AutoTokenizer
from datasets import load_dataset

#Configure the model and dataset address
os.environ['BASE_MODEL_PATH'] = '/vemlp-demo-models/model-llama-awq/Meta-Llama-3.1-8B'
os.environ['CALIB_DATASET_PATH'] = '/vemlp-demo-models/datasets-llama-awq/'
os.environ['QUANT_MODEL_PATH'] = '/vemlp-demo-models/model-quant-awq'

model_path = os.getenv('BASE_MODEL_PATH')
dataset_path = os.getenv('CALIB_DATASET_PATH')
quant_path = os.getenv('QUANT_MODEL_PATH')

#Load base model and tokenizer
tokenizer = AutoTokenizer.from_pretrained(model_path)
model = AutoAWQForCausalLM.from_pretrained(model_path, device_map="auto", safetensors=True)

Load the calibration dataset and prepare the data for calibration.
data = load_dataset(dataset_path, split="train")
dataset = [text for text in data["text"] if text.strip() != '' and len(text.split(' ')) > 20]

#Set the hyperparameters of AWQ quantization. At present, AutoAWQ only supports 4bit quantization, and the w_bit needs to be set to 4.
quant_config = { "zero_point": True, "q_group_size": 128, "w_bit": 4, "version": "GEMM" }
model.quantize(tokenizer, quant_config=quant_config, calib_data=dataset)

model.save_quantized(quant_path, safetensors=True, shard_size="4GB")
tokenizer.save_pretrained(quant_path)
```


<span id="_4-2-创建shell脚本并执行"></span>
## 4.2 Creating Shell Scripts and Executing Them


1. Create shell script **awq\-quant.sh** by executing the following command in Terminal. Make sure awq\-quant.sh awq\-quant.py two files in the same directory level.


```bash
cd /vemlp-demo-models/
touch awq-quant.sh
```



2. Edit the script content and replace it with the information that needs to be configured.


```bash
set  -ex

pip install autoawq==0.2.6
python3 awq-quant.py
echo "Finished Model Quantization Task"

#If you use ml.pni2 and the GPU driver is 470, you can run the following command
pip install autoawq==0.2.1 torch==2.1.0+cu118
pip install autoawq==0.2.1
pip install torch==2.1.0+cu118  --index-url [https://download.pytorch.org/whl](https://download.pytorch.org/whl)
python3 awq-quant.py
echo "Finished Model Quantization Task"
```



3. Execute the script.


```bash
cd /vemlp-demo-models/
bash ./awq-quant.sh
```


After the execution is complete, the output path file is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51ae2dbd6bdc73bd48a379ef83bfc943.png) </span>

<span id="_4-3-量化后模型对比"></span>
## 4.3 Comparison of models after quantification


1. Execute the following command in Terminal to compare the base model and the quantized model before quantization.


```bash
du -sh $BASE_MODEL_PATH $QUANT_MODEL_PATH
```


The comparison results are as follows: It can be seen that in terms of model capacity, the size of the model after AWQ 4\-bit quantization is about 1/3 of the model before quantization.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77488fcb1b9eca6a308e1e70fa42130c.png) </span>


2. Execute the following command in Terminal to compare the config.json files before and after quantization.


```bash
diff $QUANT_MODEL_PATH/config.json $BASE_MODEL_PATH/config.json
```


The comparison results are as follows: It can be seen that the model after quantification has more information about quantification \- quantization_config.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66bf4332436f1ba17670dcd3c060178d.png) </span>

<span id="步骤五：在自定义任务中执行量化"></span>
# Step 5: Quantify in custom tasks

<span id="方式一：控制台"></span>
## Method 1: Console


1. Enter custom tasks [console](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/customTask/create)

2. configuration environment

   1. Configure mirrors at Custom mirrors.

   ```bash
   vemlp-cn-beijing.cr.volces.com/preset-images/pytorch:2.1.0
   ```
   

   3. Fill in the entrance command. Please note that the path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the entry command to fill in the dataset path environment variables, you need to ensure that it is the path of Mount in custom tasks.

   ```python
   cat > awq-quant.py <<EOF
   import os
   from awq import AutoAWQForCausalLM
   from transformers import AutoTokenizer
   from datasets import load_dataset
   
   #Model, dataset address configuration
   os.environ['BASE_MODEL_PATH'] = '/vemlp-demo-models/model-llama-awq/Meta-Llama-3.1-8B'
   os.environ['CALIB_DATASET_PATH'] = '/vemlp-demo-models/datasets-llama-awq/'
   os.environ['QUANT_MODEL_PATH'] = '/vemlp-demo-models/model-quant-awq'
   
   model_path = os.getenv('BASE_MODEL_PATH')
   dataset_path = os.getenv('CALIB_DATASET_PATH')
   quant_path = os.getenv('QUANT_MODEL_PATH')
   
   tokenizer = AutoTokenizer.from_pretrained(model_path)
   model = AutoAWQForCausalLM.from_pretrained(model_path, device_map="auto", safetensors=True)
   
   data = load_dataset(dataset_path, split="train")
   dataset = [text for text in data["text"] if text.strip() != '' and len(text.split(' ')) > 20]
   
   #Set quantization hyperparameters
   quant_config = { "zero_point": True, "q_group_size": 128, "w_bit": 4, "version": "GEMM" }
   model.quantize(tokenizer, quant_config=quant_config, calib_data=dataset)
   
   model.save_quantized(quant_path, safetensors=True, shard_size="4GB")
   tokenizer.save_pretrained(quant_path)
   EOF
   
   pip install autoawq==0.2.6
   python3 awq-quant.py
   ```
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee6d50dfd2bb4e4f995648d8a604cebd~tplv-goo7wpa0wc-image.image) </span>


3. Allocate resources

   1. Select the appropriate resources, and the best practice is to use one xni3c machine.

   2. Mount TOS and CFS. Note: The path of TOS Mount on the development machine is inconsistent with the path of Mount in custom tasks. When filling in the model path in the environment variables, make sure it is the path of Mount in custom tasks.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a54878ce00e34e4e8ed9f450b04db7db~tplv-goo7wpa0wc-image.image) </span>


<span id="方式二：命令行"></span>
## Method 2: Command Line


1. Execute the following command in Terminal to edit awq\-quant.py. Change the cloud disk access path in the Dev boxes to the access path in custom tasks.


```bash
  import os
  from awq import AutoAWQForCausalLM
  from transformers import AutoTokenizer
  from datasets import load_dataset

  #Configure the model and dataset address
  os.environ['BASE_MODEL_PATH'] = '/data/model-llama/Meta-Llama-3.1-8B'
  os.environ['CALIB_DATASET_PATH'] = '/data/datasets-llama-quant/'
  os.environ['QUANT_MODEL_PATH'] = '/data/model-quant-awq'

  model_path = os.getenv('BASE_MODEL_PATH')
   dataset_path = os.getenv('CALIB_DATASET_PATH')
   quant_path = os.getenv('QUANT_MODEL_PATH')

   #Load base model and tokenizer
   tokenizer = AutoTokenizer.from_pretrained(model_path)
   model = AutoAWQForCausalLM.from_pretrained(model_path, device_map="auto", safetensors=True)

   Load the calibration dataset and prepare the data for calibration.
   data = load_dataset(dataset_path, split="train")
   dataset = [text for text in data["text"] if text.strip() != '' and len(text.split(' ')) > 20]

   #Set the hyperparameters of AWQ quantization. At present, AutoAWQ only supports 4bit quantization, and the w_bit needs to be set to 4.
   quant_config = { "zero_point": True, "q_group_size": 128, "w_bit": 4, "version": "GEMM" }
   model.quantize(tokenizer, quant_config=quant_config, calib_data=dataset)

   model.save_quantized(quant_path, safetensors=True, shard_size="4GB")
   tokenizer.save_pretrained(quant_path)
```



2. Create a **quantization\-task.yaml** file for performing quantization custom tasks by executing the following command in Terminal.


```bash
cd /vemlp-demo-models/
touch quantization-task.yaml
```



3. Edit the YAML file submitted by the quantification task.


```bash
TaskName:  "Quant-Meta-Llama-3-1-8B-Instruct-AWQ-INT4"
Description:  "Use AWQ to quantize Meta-Llama-3.1-8B-Instruct in INT4 format"
Entrypoint: |
    cd  /data && bash ./awq-quant.sh
Tags: []
Envs: []

ResourceQueueID:  "q-**************"            #Please replace it with your own ResourceQueueID.
Framework:  "PyTorchDDP"
TaskRoleSpecs:                                  #Please replace it with your own TaskRoleSpecs
        - RoleName:  "worker"
            RoleReplicas: 1
            Flavor:  "custom"
            ResourceSpec:
                    Family:  "ml.xni3c"
                    CPU: 15.000
                    Memory: 70.000
                    GPUNum: 1
            
ActiveDeadlineSeconds: 3600
EnableTensorBoard: False

Storages:                                        #Please replace it with your own Storages
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
volc ml_task submit --conf=/vemlp-demo-models/awq-quantization-task.yaml
```



5. Please refer to the above for the comparison of the quantitative model before and after.
