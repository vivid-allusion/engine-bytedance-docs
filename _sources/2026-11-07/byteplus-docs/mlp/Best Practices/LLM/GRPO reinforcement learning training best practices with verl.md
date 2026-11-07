---
title: "GRPO reinforcement learning training best practices with verl"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/GRPO_reinforcement_learning_training_best_practices_with_verl"
---

<span id="简介"></span>
# brief introduction

[DeepSeek-R1-Zero ](https://huggingface.co/deepseek-ai/DeepSeek-R1-Zero)uses the GRPO algorithm for reinforcement learning (Reforcing Learning, RL) training to explore the potential of large language models to develop inference capabilities without supervised data. In the training process, it does not rely on supervised fine\-tuning at all, and guides the model to learn through a fixed\-rule reward function. The model develops the ability to self\-reflect, self\-validate, and grow a Chain of Thought (COT).

[veRL ](https://github.com/volcengine/verl)is a BytePlus reinforcement learning library for large language models (LLM) that is flexible, efficient, and suitable for production environments.


* Flexible and easy to use: Multiple reinforcement learning algorithms can be easily extended through a hybrid programming model.

* Fast: Integrate existing advanced LLM training and inference frameworks for high generation and training throughput, efficient actor model sharding, and reduced memory redundancy and communication overhead.

* Open\-source ecosystem: Modular APIs enable seamless integration with existing LLM frameworks such as PyTorch FSDP, Megatron\-LM, and vLLM; support for flexible device mapping to deploy models on different GPU combinations; and integration with HuggingFace models. It has been open\-sourced through gitHub and has attracted wide attention from developers.


In this tutorial, you will learn how to use veRL for GRPO reinforcement learning training on the BytePlus Machine Learning Platform (veMLP).

<span id="目标"></span>
## goal


* Understand the fundamentals of GRPO reinforcement learning

* Learn about model reinforcement learning using veRL

* Use veRL for GRPO reinforcement learning training on the Machine Learning Platform custom tasks module.


<span id="组件"></span>
## component

This article will use the following components:


* BytePlus Machine Learning Platform

* [veRL ](https://github.com/volcengine/verl)reinforcement learning training framework

* vePFS


<span id="环境准备"></span>
# Environmental preparation

Before starting the task, you need to configure volc cli or volc python sdk, if you don't know your AK/SK, you can get the key pair of your current identity through https://console.byteplus.com/iam/keymanage[ ](https://console.volcengine.com/iam/keymanage/).

<span id="开发准备"></span>
## development readiness

Create Dev boxes in the Machine Learning Platform, select the queue computing resource configuration, access configuration, and mount shared file system.


* The user needs to use the mirror URL in the mirror entrance: and modify the URL according to your region, for example:

   * North China 2: `vemlp-cn-beijing.cr.volces.com/preset-images/verl-grpo: 0.0.1`

   * East China 2: `vemlp-cn-shanghai.cr.volces.com/preset-images/verl-grpo: 0.0.1`

* This article is about mounting PFS to the `/file_system`directory, which can be adjusted according to your specific situation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/967dd0d6f0f744838e59e8fcf8bc92f7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a69133e11304efb986040fea8f967c4~tplv-goo7wpa0wc-image.image) </span>

Log in to the Machine Learning Platform Dev boxes WebIDE, open the end point, create a new Jupyter Notebook interactive development environment, and select the appropriate Python environment

`#To view the current python environment path, it is recommended to choose '~//miniconda3/bin/python' which python`

<span id="环境变量配置"></span>
## Environment variables configuration

<span id="volc-cli-配置"></span>
### Volc cli configuration

Volc CLI is a command line tool for Machine Learning Platform, which can conveniently perform task submission, task management and other operations in the form of command line. The preset mirror already has the volc command line tool installed for the upgrade operation.

`#Upgrade volc cli! Volc upgrade #Check out the volc cli version! volc v`

The environment dependencies required for volc cli and jupyter notebooks can be configured by the following operations

If you don't know your AK/SK, you can get the key pair of your current identity through the [API access key ](https://console.byteplus.com/iam/keymanage).

```Bash
#BytePlus authentication configuration (replace with your AK/SK)
VOLC_ACCESS_KEY_ID = '**' 
VOLC_SECRET_ACCESS_KEY = '==' #Default to use the region where the Dev boxes are located
import os 
VOLC_REGION=os.environ['MLP_REGION'] 
#Set all environment variables at once (Jupyter magic command)
%set_env VOLC_ACCESS_KEY_ID={VOLC_ACCESS_KEY_ID} 
%set_env VOLC_SECRET_ACCESS_KEY={VOLC_SECRET_ACCESS_KEY} 
%set_env VOLC_REGION={VOLC_REGION} 
#Configure the Volcano command line tool (automatically reads set environment variables)
! volc configure --ak $VOLC_ACCESS_KEY_ID --sk $VOLC_SECRET_ACCESS_KEY --region $VOLC_REGION 
#Verify the configuration file (optional)
! echo "volc config:" && cat ${HOME}/.volc/config 
! echo "volc credentials:" && cat ${HOME}/.volc/credentials
```


<span id="镜像配置"></span>
### Mirror Configuration

Configure all the tasks submitted by this document here, and the mirror information used will use the mirror of the region where you boot by default. If you have other needs, please change it to your region for a better experience.

```Bash
#Generate mirror address based on current region
image_url = f'vemlp-{VOLC_REGION}.cr.volces.com/preset-images/verl-grpo:0.0.1' 
print(f'image: {image_url}')
```


<span id="grpo-强化学习原理"></span>
# GRPO reinforcement learning principle

The basic concept of GRPO is as follows:


|Role |concept |
|---|---|
|Actor model |Strategy model, the goal we want to optimize. The policy model switches back and forth between training and inference, and during the inference phase (RollOut), a random batch of prompts is selected and responses are iteratively generated (token generation sequentially one by one). In the training phase, training updates will be performed according to the loss function based on the responses and rewards generated by a batch of prompts. |
|Reference model |The reference model is used to constrain the policy model to prevent it from deviating significantly from the original model. Removing this penalty term could cause the model to generate garbled text during optimization to fool the reward model into offering a high reward value. The reference model is only inference and not updated, and only inference once for a batch of prompts. |
|Reward func |The reward function, which only verifies the correctness and format of the results, scores the output of the policy model. |


The core of GRPO is to optimize policies through relative rewards within groups, rather than relying on the traditional critic model. Specifically:


* For each input problem, the model generates a set of possible outputs.

* These outputs are not evaluated individually, but are scored by comparison with each other, i.e. by calculating the performance of each output relative to the average within the group to determine its advantage.

* This approach eliminates the need for independent evaluators, making the training process more efficient.


GRPO is particularly suitable for tasks that require complex problem solving and long inference chains, such as mathematical inference, code generation, etc

<span id="grpo-强化学习微调流程"></span>
# GRPO reinforcement learning fine tuning process

<span id="tosutil-配置（需要手动配置）"></span>
## Tosutil configuration (requires manual configuration)

You can skip this step if you don't use the platform\-preset datasets and models.

[Tosutil ](https://docs.byteplus.com/en/docs/tos/overview)is a command line tool for accessing and managing BytePlus Torch Object Storage (TOS). With this command\-line tool, you can perform batch data processing between local and TOS to handle common business scenarios such as local small and medium\-sized data on the cloud, cloud\-based small and medium\-sized data download, and automated script task integration. Machine Learning Platform Dev boxes come pre\-installed tosutil

```Bash
! tosutil version
```


You can configure the environment dependencies required by tosutil through the following operations, and declare the shared storage directory, so that subsequent submission tasks can use the same storage configuration. This article takes the mount of PFS to the `/file_system`directory as an example

```Bash
! tosutil config -i $VOLC_ACCESS_KEY_ID -k $VOLC_SECRET_ACCESS_KEY -e tos-$VOLC_REGION.ivolces.com -re $VOLC_REGION 
root_path = '/file_system' 
model_path = f'{root_path}/models' 
model_name = 'Qwen/Qwen2.5-32B-Instruct'
```


<span id="数据准备"></span>
## Data preparation

At present, we have preset the gsm8k and countdown datasets in the mirror, which you can use directly. The example processing steps for the dataset are as follows:


* GSM8K dataset:


```Bash
cd /root/code/verl/examples/data_preprocess/ python3 gsm8k.py --local_dir /root/code/data/gsm8k
```



* Countdown dataset:


```Bash
cd /root/code/TinyZero mkdir -p /root/code/TinyZero/data/countdown python examples/data_preprocess/countdown.py --template_type=qwen-instruct --local_dir=/root/code/TinyZero/data/countdown
```


<span id="机器学习平台预置模型下载"></span>
## Machine Learning Platform Preset Model Download

BytePlus provides TOS Torch Object Storage preset model weight file, which is convenient for customers to copy and accelerate experiments. Take the Qwen/Qwen 2.5\-32B\-Instruct model as an example.

```Bash
import os 
#cp needs to have the -r parameter, otherwise the directory will not be downloaded; the transmission speed is slow, you can adjust the -j -p concurrency parameter according to the number of CPUs in the Dev boxes
! tosutil cp tos://preset-models-{VOLC_REGION}/{model_name}/ {model_path}/{os.path.dirname(model_name)} -r -u -j=32 -p=4 -nfj=16
```


<span id="使用-verl-发起-grpo-强化学习训练任务"></span>
## Initiate a GRPO reinforcement learning training task using veRL

veRL supports GRPO reinforcement learning for Qwen32B models in the form of Ray multi\-node tasks. This paper uses the gsm8k dataset to demonstrate the process of reinforcement learning fine\-tuning the model by taking the distributed training of the Qwen32B model on two Hopper nodes as an example.

<span id="运行环境设置"></span>
### operating environment settings

You can obtain the relevant running configuration in the following ways


* Visit [File storage PFS ](https://console.byteplus.com/pfs/region:pfs+ap-southeast-1/instance?)for configuration information about vepfs.

* Access [queue management ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/resourceQueue?Category=General&current=1&fields=%7B%22Role%22%3A%22General%22%7D&pageSize=10)to get the queue ID

* Visit [instance specifications and pricing ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing)for the specifications you wish to use

* Please ensure that the notebook Mount configuration is exactly the same as the following file system configuration


```Bash
#resource allocation
queue='q-xx-gp9gt' 
#queue id
flavor='ml.hpcpni3ln.45xlarge' replicas=2 
#File system configuration
mount_path = "/file_system" #vepfs Mount Path
storage_type = "Vepfs"   
vepfs_id = "vepfs-xxx" #vepfs id experiment_name = "qwen2_3b_function_rm" #wandb experiment name
```


<span id="设置训练参数"></span>
### Set training parameters

At present, we have preset some tuned parameters, and you can further customize the hyperparameters. The relevant configuration is in the `/root/code/verl/examples/grpo_trainer/train_mlp.sh`file. For more information on the meaning of parameters and for training tuning, refer to the official tuning guide [perf_tunning ](https://verl.readthedocs.io/en/latest/perf/perf_tuning.html)of verl.

<span id="提交任务"></span>
### submit task

First configure the Start parameter of custom tasks and submit custom tasks through the volc cli command line tool. Using the Ray framework for distributed training, execute the following command to create a demo\-grpo\-train\-task .yaml task configuration file:

```Bash
import yaml

#Define the configuration content
task_config = {
    "TaskName": "ray-verl-grpo-Qwen-32B",
    "Description": "Use Ray and verl rl Qwen-32B model",
    "Entrypoint": f'''export MODEL_PATH={model_path}/{model_name}
                    export experiment_name={experiment_name} 
                    export NUM_NODE={replicas}
                    cd /root/code/verl
                    bash examples/grpo_trainer/train_mlp.sh ''',
    "Tags": [],
    "Envs": [],
    "ResourceQueueID": queue,             #replace_with_your_ResourceQueueID
    "Framework": "Ray",
    "TaskRoleSpecs": [                           #replace_with_your_TaskRoleSpecs
        {
            "RoleName": "head",
            "RoleReplicas": 1,
            "Flavor": flavor,
        },
        {
            "RoleName": "worker",
            "RoleReplicas": replicas - 1,
            "Flavor": flavor,
        }
    ],
    "ActiveDeadlineSeconds": 864000,
    "EnableTensorBoard": False,
     #replace_with_your_Storages
    "Storages": [                              
        {
          "MountPath": mount_path,
          "Type": storage_type,
          "VepfsId": vepfs_id,
        }
    ],
    "ImageUrl": image_url,                   #replace_with_you_image_url
    "RetryOptions": {
        "EnableRetry": False,
        "MaxRetryTimes": 5,
        "IntervalSeconds": 120,
        "PolicySets": [],
    },
}

#Write the configuration to the ray-verl-grpo.yaml file
import datetime
verl_grpo_config_yaml = f'ray-verl-grpo-{datetime.datetime.now().strftime("%Y%m%d_%H%M%S")}.yaml'
with open(verl_grpo_config_yaml, "w") as file:
    yaml.dump(task_config, file, default_flow_style=False)

print(f"{verl_grpo_config_yaml} 文件已生成")

! volc ml_task submit --conf {verl_grpo_config_yaml}

```


Query job status via volc command line tool

```Bash
! volc ml_task get --id t-20241021145150-qc49r --output json --format Status
```


<span id="通过-ray-dashboard-观察作业的执行状态"></span>
#### Observe job execution status through Ray Dashboard

After initiating the training task, you can view the detailed task running status and log in the Ray Dashboard.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21d19e962b6c4063a39074f484bab0db~tplv-goo7wpa0wc-image.image) </span>

For details, please refer to: [Submit distributed tasks using the RAY Compute Engine](https://docs.byteplus.com/docs/mlp/Submit_distributed_tasks_using_the_RAY_Compute_Engine)

<span id="训练性能对比参考"></span>
### Training Performance Comparison Reference

Using the Hopper model, the performance parameters of training on different basic models of Qwen are compared as follows:


|Base model |Equipment specifications |number of cards |ppo_mini_batch_size |micro_batch_size |Time (s)/step |Memory utilization (max) |MFU |
|---|---|---|---|---|---|---|---|
|Qwen/Qwen2.5\-32B |ml.hpcpni3l (H20) |2\*8 |256 |Dynamic batch\-size |478.5 |97% |0.6495 |
|Qwen/Qwen2.5\-32B |ml.hpcpni3l (H20) |2\*8 |256 |8 |547.7 |85% |0.5131 |
|Qwen/Qwen2.5\-14B |ml.hpcpni3l (H20) |2\*8 |256 |8 |338.4 |80% |0.50428 |
|Qwen/Qwen2.5\-1.5B |ml.hpcpni3l (H20) |2\*8 |256 |8 |66.0 |65% |0.35187 |
|Qwen/Qwen2.5\-32B |ml.hpcpni3l (H20) |8 |256 |8 |985.9 |99% |0.5341 |
|Qwen/Qwen2.5\-14B |ml.hpcpni3l (H20) |8 |256 |8 |445.3 |88% |0.51396 |
|Qwen/Qwen2.5\-7B |ml.hpcpni3l (H20) |8 |256 |8 |222.1 |86% |0.67174 |
|Qwen/Qwen2.5\-1.5B |ml.hpcpni3l (H20) |8 |256 |8 |101.9 |67% |0.38671 |


The performance comparison between the H20 model and the A800 model is as follows:


|Base model |Equipment specifications |number of cards |ppo_mini_batch_size |micro_batch_size |Time (s)/step |Memory utilization (max) |MFU |
|---|---|---|---|---|---|---|---|
|Qwen/Qwen2.5\-32B |ml.hpcpni3l (H20) |2\*8 |256 |Dynamic batch\-size |478.5 |97% |0.6495 |
|Qwen/Qwen2.5\-32B |ml.hpcpni2l(A800) |2\*8 |256 |Dynamic batch\-size |389.3 |99% |0.47 |
|Qwen/Qwen2.5\-32B |ml.hpcpni3l (H20) |2\*8 |256 |8 |547.7 |85% |0.5131 |
|Qwen/Qwen2.5\-32B |ml.hpcpni2l(A800) |2\*8 |256 |8 |431.5 |89% |0.34 |


The training process of different models under different steps is compared as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_694b758c3cc393b6903f22de59d12469.jpg) </span>

<span id="使用-tinyzero-项目复现-deepseek-r1-zero-的效果"></span>
## Repeat the effects of DeepSeek R1 Zero with the TinyZero project

[TinyZero ](https://github.com/Jiayi-Pan/TinyZero)is an open source project based on veRL. It replicates the effect of DeepSeek\-R1\-Zero in countdown and multiplication tasks. Through GRPO reinforcement learning training, it uses a rule\-based rewards function, and focuses on verifying the correctness and format of the results. After a certain step of training, the Qwen 3B basic model can develop self\-verification and search capabilities on its own.

We can replicate this effect in the Machine Learning Platform. Here are the specific steps.

<span id="设置训练参数"></span>
### Set training parameters

```Bash
#resource allocation
queue='q-xx-gp9gt' #queue id
flavor='ml.hpcpni3ln.45xlarge'

#File system configuration
mount_path = "/file_system" #vepfs Mount Path
storage_type = "Vepfs"  
vepfs_id = "vepfs-xxx" # vepfs id

experiment_name="qwen2_3b_function_rm" #wandb experiment name

```


Execute the following command to create a demo\-tinyzero\-train\-task task profile:

```Bash
import yaml

#Define the configuration content
task_config = {
    "TaskName": "grpo-deepseek-r1-zero-reproduction",
    "Description": "Use grpo reproduction deepseek-r1-zero base on tinyzero ",
    "Entrypoint": f'''export MODEL_PATH={model_path}/{model_name}
                    export experiment_name={experiment_name} 
                    cd /root/code/TinyZero
                    bash scripts/train_mlp.sh''',
    "Tags": [],
    "Envs": [],
    "ResourceQueueID": queue, #replace_with_your_ResourceQueueID
    "Framework": "Ray",
    "TaskRoleSpecs": [                           #replace_with_your_TaskRoleSpecs
        {
            "RoleName": "head",
            "RoleReplicas": 1,
            "Flavor": "ml.hpcpni3ln.45xlarge",
        }
    ],
    "ActiveDeadlineSeconds": 864000,
    "EnableTensorBoard": False,
     #replace_with_your_Storages
    "Storages": [                              
        {
          "MountPath": mount_path,
          "Type": storage_type,
          "VepfsId": vepfs_id,
        }
    ],
    "ImageUrl": image_url,
    "RetryOptions": {
        "EnableRetry": False,
        "MaxRetryTimes": 5,
        "IntervalSeconds": 120,
        "PolicySets": [],
    },
}

#Write the configuration to the ray-verl-grpo.yaml file
import datetime
tinyzero_config_yaml = f'tinyzero-{datetime.datetime.now().strftime("%Y%m%d_%H%M%S")}.yaml'
with open(tinyzero_config_yaml, "w") as file:
    yaml.dump(task_config, file, default_flow_style=False)

print(f"{tinyzero_config_yaml} 文件已生成")

! volc ml_task submit --conf {verl_grpo_config_yaml}
```


<span id="复现结果示例"></span>
#### Example of reproducing results

After certain steps, the model developed the ability to reflect and self\-validate.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91f93da0361ba051b28e4b0b0e009563.jpg) </span>

The evolution of the critic/score/mean metrics during training is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b41e3d87deae566ceea47ec864d3d33.jpg) </span>
