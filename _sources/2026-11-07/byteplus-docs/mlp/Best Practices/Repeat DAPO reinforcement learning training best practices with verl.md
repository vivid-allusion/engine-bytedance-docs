---
title: "Repeat DAPO reinforcement learning training best practices with verl"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Repeat_DAPO_reinforcement_learning_training_best_practices_with_verl"
---

<span id="49365cef"></span>
# **brief introduction**

[DAPO ](https://github.com/BytedTsinghua-SIA/DAPO)proposed the decoupled clipping and dynamic sampling strategy optimization (DAPO) algorithm to make this research public, with the aim of providing practical tools for scalable reinforcement learning to a wider range of researchers and society, so that more people can benefit from this technological advancement. Applying DAPO to the Qwen 2.5\-32B base model outperformed the previous state\-of\-the\-art DeepSeek\-R1\-Zero\-Qwen\-32B model in the AIME 2024 evaluation, achieving 50% accuracy with a 50% reduction in training steps.

[Verl ](https://github.com/volcengine/verl)is a BytePlus reinforcement learning library for large language models (LLMs) that is flexible, efficient, and suitable for production environments.


* Flexible and easy to use: Multiple reinforcement learning algorithms can be easily extended through a hybrid programming model.

* Fast: Integrate existing advanced LLM training and inference frameworks for high generation and training throughput, efficient actor model sharding, and reduced memory redundancy and communication overhead.

* Open\-source ecosystem: Modular APIs enable seamless integration with existing LLM frameworks such as PyTorch FSDP, Megatron\-LM, and vLLM; support for flexible device mapping to deploy models on different GPU combinations; and integration with HuggingFace models. It has been open\-sourced through GitHub and is widely followed by developers.


In this tutorial, you will learn how to use DAPO reinforcement learning for verl\-based training on the BytePlus Machine Learning Platform (mlp).

<span id="bfe0f2a3"></span>
## **goal**


* Understand the fundamentals of DAPO reinforcement learning

* Learn how to use verl for model reinforcement learning

* Use verl for DAPO reinforcement learning training on the Machine Learning Platform custom tasks module.


<span id="3aa9526c"></span>
## **Components** This article will use the following components:


* BytePlus Machine Learning Platform

* [Verl ](https://github.com/volcengine/verl)reinforcement learning training framework

* PFS


<span id="f69f39fb"></span>
# **Environment preparation**

Before starting the task, you need to configure volc cli or volc python sdk, if you don't know your AK/SK, you can get the key pair of your current identity through [Identity and Access Management - API access key ](https://console.byteplus.com/iam/keymanage).

<span id="9cf2ad08"></span>
## **Development Preparation**

To Create Dev boxes in the Machine Learning Platform, select the queue computing resource configuration, access configuration, and mount shared file system, and then Create.


* The user needs to use the mirror URL in the mirror entrance: and modify the URL according to your region, for example:

   * Asia Pacific (Johor): [vemlp-ap-southeast-1.cr.volces.com/preset-images/verl: dapo-v0.0.1](https://docs.byteplus.com/en/docs/186/vemlp-ap-southeast-1.cr.volces.com/preset-images/verl:)

   * This article is about mounting PFS to the `/file_system`directory, which can be adjusted according to your specific situation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6f8ab593a2e4bffab92d32f049bc581~tplv-goo7wpa0wc-image.image) </span>

Log in to the Machine Learning Platform Dev boxes WebIDE, open the end point, create a new Jupyter Notebook interactive development environment, and select the appropriate Python environment

```JSON
# Check the current Python environment path; it's recommended to use `/usr/bin/python`
which python
```


<span id="5e7c4458"></span>
## **Environment variables configuration**

<span id="45f42f12"></span>
### **Volc cli Configure**

volc cli is a command line tool for Machine Learning Platform, which can conveniently perform task submission, task management and other operations in the way of command line. The preset mirror already has the volc command line tool installed for the upgrade operation.

```JSON
# Upgrade volc CLI
! volc upgrade
# Check volc CLI version
! volc v
```


The environment dependencies required for volc cli and jupyter notebooks can be configured by the following operations

If you don't know your AK/SK, you can get the key pair of your current identity through the [API Access Key ](https://console.byteplus.com/iam/keymanage).

```Bash
# BytePlus authentication configuration (replace with your AK/SK)
VOLC_ACCESS_KEY_ID = 'xx'
VOLC_SECRET_ACCESS_KEY = 'yy=='

# By default, use the region where the Dev box is located
import os
VOLC_REGION = os.environ['MLP_REGION']

# Set all environment variables at once (Jupyter magic command)
%set_env VOLC_ACCESS_KEY_ID={VOLC_ACCESS_KEY_ID}
%set_env VOLC_SECRET_ACCESS_KEY={VOLC_SECRET_ACCESS_KEY}
%set_env VOLC_REGION={VOLC_REGION}

# Configure BytePlus CLI (automatically reads the set environment variables)
! volc configure --ak $VOLC_ACCESS_KEY_ID --sk $VOLC_SECRET_ACCESS_KEY --region $VOLC_REGION

# Validate configuration files (optional)
! echo "volc config:" && cat ${HOME}/.volc/config
! echo "volc credentials:" && cat ${HOME}/.volc/credentials
```


<span id="cfb5c61e"></span>
### **Mirror configuration**

All tasks submitted by this document are configured here, and the mirror information used will use the mirror of the region where you boot by default. If you have other needs, please replace it with your region to get a better experience.

```Bash
# Generate image URL based on the current region
image_url = f'vemlp-{VOLC_REGION}.cr.volces.com/preset-images/verl:dapo-v0.0.1'
print(f'image: {image_url}')
```


<span id="2e1fe4fc"></span>
# **DAPO**

<span id="a41616c1"></span>
## **Algorithm introduction**

The decoupling clipping and dynamic sampling strategy optimization (DAPO) algorithm, which includes the following key techniques. Detailed analysis and insights can be found in DAPO's [technical reports ](https://dapo-sia.github.io/static/pdf/dapo_paper.pdf).


* **Clip\-Higher** : It increases the diversity of the system and avoids entropy collapse. DAPO observed entropy collapse in preliminary experiments. DAPO increases the upper clipping range of the importance sampling ratio in the policy layer loss to mitigate this problem.

* **Dynamic Sampling** : It improves training efficiency and stability. DAPO developed a strategy to perform dynamic sampling and filter out groups of hints with accuracy equal to 1 and 0, thus maintaining the same number of hints with valid layers across batches.

* **Token\-level Policy Gradient Loss** : This is crucial in long\-chain reinforcement learning (long\-CoT RL) scenarios.

* **Overlong Reward Shaping** : It reduces reward noise and stabilizes training.


<span id="5d13285a"></span>
## **Dataset**


* Training dataset: [DAPO-Math-17k](https://huggingface.co/datasets/BytedTsinghua-SIA/DAPO-Math-17k)

* Validation dataset: [AIME-2024](https://huggingface.co/datasets/BytedTsinghua-SIA/AIME-2024)


<span id="c584bc81"></span>
## **validator**


* DAPO uses a simple but robust **rule\-based validator that** relies on string normalization and matching.


<span id="f10b00ca"></span>
# **DAPO reinforcement learning process**

<span id="fcfabad9"></span>
## **Tosutil configuration (requires manual configuration)** 

This step can be skipped if you do not use platform\-preset datasets and models.

[Tosutil ](https://docs.byteplus.com/en/docs/tos/overview)is a command line tool for accessing and managing BytePlus Torch Object Storage (TOS). Through this command\-line tool, you can perform batch data processing between local and TOS to handle common business scenarios such as local small and medium\-sized data on the cloud, cloud\-based small and medium\-sized data download, and automated script task integration. Machine Learning Platform Dev boxes come pre\-installed tosutil

```Bash
! tosutil version
```


You can configure the environment dependencies required by tosutil by the following operations, and declare the shared storage directory, so that subsequent submission tasks can use the same storage configuration. This article takes the mount of PFS to the `/file_system`directory as an example

```Bash
! tosutil config -i $VOLC_ACCESS_KEY_ID -k $VOLC_SECRET_ACCESS_KEY -e tos-$VOLC_REGION.ivolces.com -re $VOLC_REGION

root_path = '/file_system'
model_path = f'{root_path}/models'
dataset_path = f'{root_path}/datasets'
checkpoint_path = f'{root_path}/ckpt'

model_name = 'Qwen/Qwen2.5-32B'
train_dataset_name = 'BytedTsinghua-SIA/DAPO-Math-17k'
test_dataset_name = 'BytedTsinghua-SIA/AIME-2024'

# If the shared storage uses TOS, you need to declare your TOS prefix
tos_prefix = "your_bucket_name/prefix"
```


<span id="95822ea7"></span>
## **Data Preparation**

BytePlus provides TOS Torch Object Storage preset datasets for user\-friendly self\-replication and accelerated experimentation.

```Shell
import os

# `cp` requires the -r flag; otherwise, directories will not be downloaded.
# If the transfer is slow, you can adjust the `-j` and `-p` concurrency parameters based on the number of CPUs on the Dev box.
! tosutil cp tos://preset-datasets-{VOLC_REGION}/{train_dataset_name}/ {dataset_path}/{os.path.dirname(train_dataset_name)} -r -u -j=32 -p=4 -nfj=16
! tosutil cp tos://preset-datasets-{VOLC_REGION}/{test_dataset_name}/ {dataset_path}/{os.path.dirname(test_dataset_name)} -r -u -j=32 -p=4 -nfj=16

## TOS mount does not support full POSIX semantics; you can directly upload to TOS
# ! tosutil cp tos://preset-datasets-{VOLC_REGION}/{train_dataset_name}/ tos://{tos_prefix}/{os.path.dirname(train_dataset_name)} -r -u -j=32 -p=4 -nfj=16
# ! tosutil cp tos://preset-datasets-{VOLC_REGION}/{test_dataset_name}/ tos://{tos_prefix}/{os.path.dirname(test_dataset_name)} -r -u -j=32 -p=4 -nfj=16

## Refresh the directory to sync contents from TOS to the cache file system
# ! cfs-cli ls {dataset_path}/{train_dataset_name}
# ! cfs-cli ls {dataset_path}/{test_dataset_name}
```


<span id="8f65dcec"></span>
## **Machine Learning Platform Preset Model Download** BytePlus provides TOS Torch Object Storage preset model weight file, which is convenient for customers to copy and speed up experiments. Take the Qwen/Qwen 2.5\-32B model as an example.

```Shell
import os

# `cp` requires the -r flag; otherwise, directories will not be downloaded.
# If the transfer is slow, you can adjust the `-j` and `-p` concurrency parameters based on the number of CPUs on the Dev box.
! tosutil cp tos://preset-models-{VOLC_REGION}/{model_name}/ {model_path}/{os.path.dirname(model_name)} -r -u -j=32 -p=4 -nfj=16

## TOS mount does not support full POSIX semantics; you can directly upload to TOS
# ! tosutil cp tos://preset-datasets-{VOLC_REGION}/{model_name}/ tos://{model_path}/{os.path.dirname(model_name)} -r -u -j=32 -p=4 -nfj=16

## Refresh the directory to sync contents from TOS to the cache file system
# ! cfs-cli ls {model_path}/{os.path.dirname(model_name)}
```


<span id="34d8a6f8"></span>
## **Use verl to initiate DAPO reinforcement learning training tasks**

Verl supports GRPO reinforcement learning training of Qwen32B models in the form of Ray multi\-node tasks. This paper uses the gsm8k dataset to demonstrate the process of reinforcement learning fine\-tuning the model by taking the distributed training of the Qwen32B model on two Hopper nodes as an example.

<span id="11bdd827"></span>
### **Run environment settings**

You can get the relevant running configuration in the following ways


* Visit [File storage PFS ](https://console.byteplus.com/pfs/region:pfs+ap-southeast-1/overview?)for configuration information about vepfs.

* Access [queue management ](https://console.byteplus.com/ml-platform/region:ml-platform+ap-southeast-1/resourceQueue?Category=General&current=1&fields=%7B%22Role%22%3A%22General%22%7D&pageSize=10)to get the queue ID

* Visit [Instance Specifications and Pricing](https://docs.byteplus.com/docs/mlp/Instance_Specifications_and_Pricing) for the specifications you wish to use

* Please ensure that the notebook Mount configuration is exactly the same as the following file system configuration


```Python
# Resource configuration
queue = 'q-2025xxxx-1234'            # Queue ID
flavor = 'ml.hpcpni3ln.45xlarge'     # H20 is used as an example here
replicas = 16

# File system configuration
storage_type = "Vepfs"  
mount_path = "/file_system"          # File storage PFS mount path
vepfs_id = "vepfs-xxxx"              # File storage PFS ID
```


<span id="d0b4f2e8"></span>
### **Set training parameters**

for more detailed instructions see [DAPO Readme](https://github.com/volcengine/verl/blob/aa2d8c0f0fa48cb1f190e52bef55ed766eeaffe6/recipe/dapo/README.md)

```Python
import os

# DAPO

## Clip-Higher
## - clip_ratio_low and clip_ratio_high specify ε_low and ε_high in the DAPO objective.
clip_ratio_low = 0.2
clip_ratio_high = 0.28

## Dynamic Sampling (with Group Filtering)
## - The trainer will repeatedly sample using gen_batch_size until enough qualified groups are found for train_batch_size, 
##   or the limit specified by max_num_gen_batches is reached.
train_batch_size = 512
gen_batch_size = train_prompt_bsz * 3

enable_filter_groups = True   # Set to True to filter out all groups with the same output metric values. 
                              # For example, for accuracy (acc), groups where all outputs are 1 or 0 will be filtered.
filter_groups_metric = "acc"  # Options: score / seq_reward / seq_final_reward / ...
max_num_gen_batches = 10      # Non-positive values mean no upper limit

## Token-level Policy Gradient 
## - Setting use_token_level_loss to True means policy gradient loss will be calculated on all tokens across all sequences in the batch.
use_token_level_loss = True

## Overlong Reward Shaping
## - max_response_length - overlong_buffer_len defines the expected length. 
##   Tokens beyond that length will be penalized, controlled by overlong_penalty_factor.
enable_overlong_buffer = True
overlong_buffer_len = 1024 * 4
overlong_penalty_factor = 1.0
max_prompt_length = 1024 * 2
max_response_length = 1024 * 20

# Others

## Disable KL (Kullback-Leibler Divergence)
kl_coef = 0.0
kl_loss_coef = 0.0

## Performance Related Parameters
gen_tp = 4
sp_size = 8
use_dynamic_bsz = True
actor_ppo_max_token_len = max_prompt_length + max_response_length
infer_ppo_max_token_len = max_prompt_length + max_response_length
offload = True

## Train
train_prompt_mini_bsz = 32

## Validation
val_top_k = -1                # 0 for HF rollout, -1 for vLLM rollout
n_resp_per_prompt = 16

## Tracking
use_tracking = True
project_name = "DAPO"                 # BytePlus Machine Learning Platform experiment tracking - Project name, required if use_tracking=True
experiment_name = "DAPO-Qwen2.5-32B"  # BytePlus Machine Learning Platform experiment tracking - Experiment name, required if use_tracking=True
```


<span id="9e9e9372"></span>
### **Submit tasks**

First configure the start parameter of custom tasks and submit custom tasks through the volc cli command line tool. Using the Ray framework for distributed training, execute the following command to create a demo\-grpo\-train\-task .yaml task configuration file:

```Python
import yaml
def build_envs():
    envs = [
        {"Name": "TORCH_NCCL_AVOID_RECORD_STREAMS", "Value": "1", "IsPrivate": False},
        {"Name": "VLLM_ATTENTION_BACKEND", "Value": "XFORMERS", "IsPrivate": False},
        {"Name": "VLLM_USE_V1", "Value": "1", "IsPrivate": False},
        {"Name": "VERL_PPO_LOGGING_LEVEL", "Value": "DEBUG", "IsPrivate": False},
    ]
    if use_tracking:
        envs.extend(
            [
                {"Name": "VOLC_ACCESS_KEY_ID", "Value": VOLC_ACCESS_KEY_ID, "IsPrivate": False},
                {"Name": "VOLC_SECRET_ACCESS_KEY", "Value": VOLC_SECRET_ACCESS_KEY, "IsPrivate": True},
                {"Name": "MLP_TRACKING_REGION", "Value": "ap-southeast-1", "IsPrivate": False}, #  {"Name": "MLP_TRACKING_PROJECT_NAME", "Value": project_name, "IsPrivate": False},
            ]
        )
    return envs
def build_entrypoint():
    return f'''python3 -m verl.trainer.main_ppo \
    data.train_files="{dataset_path}/{train_dataset_name}/verl/dapo-math-17k.parquet" \
    data.val_files="{dataset_path}/{test_dataset_name}/verl/aime-2024.parquet" \
    data.prompt_key=prompt \
    data.truncation='left' \
    data.max_prompt_length={max_prompt_length} \
    data.max_response_length={max_response_length} \
    data.gen_batch_size={gen_batch_size} \
    data.train_batch_size={train_batch_size} \
    actor_rollout_ref.rollout.n={n_resp_per_prompt} \
    algorithm.adv_estimator=grpo \
    algorithm.kl_ctrl.kl_coef={kl_coef} \
    actor_rollout_ref.actor.kl_loss_coef={kl_loss_coef} \
    actor_rollout_ref.actor.clip_ratio_low={clip_ratio_low} \
    actor_rollout_ref.actor.clip_ratio_high={clip_ratio_high} \
    algorithm.filter_groups.enable={enable_filter_groups} \
    algorithm.filter_groups.max_num_gen_batches={max_num_gen_batches} \
    algorithm.filter_groups.metric={filter_groups_metric} \
    actor_rollout_ref.model.use_remove_padding=True \
    actor_rollout_ref.actor.use_dynamic_bsz={use_dynamic_bsz} \
    actor_rollout_ref.ref.log_prob_use_dynamic_bsz={use_dynamic_bsz} \
    actor_rollout_ref.rollout.log_prob_use_dynamic_bsz={use_dynamic_bsz} \
    actor_rollout_ref.actor.ppo_max_token_len_per_gpu={actor_ppo_max_token_len} \
    actor_rollout_ref.ref.log_prob_max_token_len_per_gpu={infer_ppo_max_token_len} \
    actor_rollout_ref.rollout.log_prob_max_token_len_per_gpu={infer_ppo_max_token_len} \
    actor_rollout_ref.model.path="{model_path}/{model_name}" \
    +actor_rollout_ref.model.override_config.attention_dropout=0. \
    +actor_rollout_ref.model.override_config.embd_pdrop=0. \
    +actor_rollout_ref.model.override_config.resid_pdrop=0. \
    actor_rollout_ref.model.enable_gradient_checkpointing=True \
    actor_rollout_ref.actor.optim.lr=1e-6 \
    actor_rollout_ref.actor.optim.lr_warmup_steps=10 \
    actor_rollout_ref.actor.optim.weight_decay=0.1 \
    actor_rollout_ref.actor.ppo_mini_batch_size={train_prompt_mini_bsz} \
    actor_rollout_ref.actor.fsdp_config.param_offload={offload} \
    actor_rollout_ref.actor.fsdp_config.optimizer_offload={offload} \
    actor_rollout_ref.actor.entropy_coeff=0 \
    actor_rollout_ref.actor.grad_clip=1.0 \
    actor_rollout_ref.actor.use_token_level_loss={use_token_level_loss} \
    actor_rollout_ref.actor.ulysses_sequence_parallel_size={sp_size} \
    actor_rollout_ref.rollout.gpu_memory_utilization=0.80 \
    actor_rollout_ref.rollout.tensor_model_parallel_size={gen_tp} \
    actor_rollout_ref.rollout.enable_chunked_prefill=True \
    actor_rollout_ref.rollout.max_num_batched_tokens={max_prompt_length + max_response_length} \
    actor_rollout_ref.rollout.val_kwargs.top_k="{val_top_k}" \
    actor_rollout_ref.rollout.val_kwargs.top_p=1.0 \
    actor_rollout_ref.rollout.val_kwargs.temperature=1.0 \
    actor_rollout_ref.rollout.val_kwargs.n=1 \
    actor_rollout_ref.rollout.val_kwargs.do_sample=True \
    actor_rollout_ref.ref.fsdp_config.param_offload={offload} \
    actor_rollout_ref.ref.ulysses_sequence_parallel_size={sp_size} \
    actor_rollout_ref.actor.fsdp_config.fsdp_size=-1 \
    custom_reward_function.overlong_buffer.enable={enable_overlong_buffer} \
    custom_reward_function.overlong_buffer.len={overlong_buffer_len} \
    custom_reward_function.overlong_buffer.penalty_factor={overlong_penalty_factor} \
    trainer.logger=['console','vemlp_wandb'] \
    trainer.project_name="{project_name}" \
    trainer.experiment_name="{experiment_name}" \
    trainer.n_gpus_per_node=8 \
    trainer.nnodes="{replicas}" \
    +trainer.val_before_train=True \
    trainer.test_freq=5 \
    trainer.save_freq=5 \
    trainer.total_epochs=1 \
    trainer.default_local_dir="{checkpoint_path}/{project_name}/{experiment_name}" \
    trainer.resume_mode=auto'''# define config content task_config = {
    "TaskName": "DAPO",
    "Description": "Use Ray and verl to reproduce DAPO",
    "Entrypoint": build_entrypoint(),
    "Envs": build_envs(),
    "ResourceQueueID": queue,             #replace_with_your_ResourceQueueID    "Framework": "Ray",
    "TaskRoleSpecs": [                           #replace_with_your_TaskRoleSpecs        {
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
    #replace_with_your_Storages    "Storages": [                              
        {
          "MountPath": mount_path,
          "Type": storage_type,
          "VepfsId": vepfs_id,
        }
    ],
    "ImageUrl": image_url,                   #replace_with_you_image_url    "RetryOptions": {
        "EnableRetry": False,
        "MaxRetryTimes": 5,
        "IntervalSeconds": 120,
        "PolicySets": [],
    },
}
# write config into DAPO.yaml
import datetime
verl_grpo_config_yaml = f'DAPO-{datetime.datetime.now().strftime("%Y%m%d_%H%M%S")}.yaml'
with open(verl_grpo_config_yaml, "w") as file:
    yaml.dump(task_config, file, default_flow_style=False)
print(f"{verl_grpo_config_yaml} is generated")
! volc ml_task submit --conf {verl_grpo_config_yaml}
```


Query the job status with the volc command line tool:

```Python
! volc ml_task get --id t-20241021145150-qc49r --output json --format Status
```


<span id="5094eb46"></span>
#### **Observe the execution status of the job through the Ray Dashboard**

After initiating the training task, you can view the detailed task execution status and log in the Ray Dashboard:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6a503950fcc4adcb53725ba76c555b3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3245b01c8f5473a8d89e7a8e5e870ee~tplv-goo7wpa0wc-image.image) </span>For details, please refer to: [Submit distributed tasks using the RAY Compute Engine](https://docs.byteplus.com/docs/mlp/Submit_distributed_tasks_using_the_RAY_Compute_Engine)
