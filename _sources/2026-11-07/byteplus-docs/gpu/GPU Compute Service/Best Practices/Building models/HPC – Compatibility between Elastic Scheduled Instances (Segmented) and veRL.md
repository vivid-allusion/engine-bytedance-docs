---
title: "HPC – Compatibility between Elastic Scheduled Instances (Segmented) and veRL"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/HPC__veRL_adapted_for_Elastic_Scheduled_Instances_Segmented"
---

This topic describes how to resolve the conflict between computing resource cost and performance stability in deep learning training tasks, achieving an optimal balance between cost saving and stability.

<span id="9EbmlMDq"></span>
## Background

In deep learning training tasks, compute resources usually account for the largest proportion of costs. The Elastic Scheduled Instances\-Segmented type offered by the platform reduces the cost by more than 60% compared with regular pay\-as\-you\-go instances. However, they are unstable and may be reclaimed at any time due to market price fluctuations or resource shortages, which undoubtedly makes the training work troublesome:


* Training interruption: When a running training task is forcibly stopped, the current task fails, and the consumed compute resources are wasted.

* Checkpoint loss: If a running training task is interrupted and the training checkpoints (snapshots of training progress) are not saved timely, the training must be restarted from the beginning. This further increases computing cost and time cost.


To resolve the above issues, the new feature [MR#2192](https://github.com/volcengine/verl/pull/2192?utm_source=chatgpt.com) has been added to the [verl](https://github.com/volcengine/verl) framework. When an ESI\-Segmented instance is about to expire or to be reclaimed, the system automatically triggers the action of saving the checkpoint. This ensures that the training task can be recovered in a secure manner. This feature, in addition to the characteristics of advance duration locking in ESI\-Segmented, helps you achieve the optimal balance between cost saving and stability.

<span id="oTfu6yNT"></span>
## Capability overview

<span id="MjYag6c4"></span>
### Capabilities achieved via veRL\-ESI integration


* Core function: should_save_ckpt_esi

   * Determine whether the instance is about to expire.

   * Forcibly save the checkpoint within the redundant time window before the instance expires.

* Parameter configuration

   * The default value of esi_redundant_time is 120 seconds.

   * The default value of save_ckpt_duration is 60 seconds and is an estimated saving duration.


<span id="Ouuc6f84"></span>
### Trigger logic

When the saving requirement is met or the ESI is approaching its expiration time, a checkpoint saving action is forcibly executed.

T<sub>expiration</sub> \- T<sub>now</sub> ≤ T<sub>max_steps</sub> + T<sub>save</sub> + T<sub>redundant</sub>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">T<sub>expiration</sub>: The expiration timestamp of the instance.</div>


* <div data-tips="true" data-tips-type="default">T<sub>now</sub>: Current time.</div>


* <div data-tips="true" data-tips-type="default">T<sub>max_steps</sub>: Maximum duration of a single training step (dynamically estimated).</div>


* <div data-tips="true" data-tips-type="default">T<sub>save</sub>: The duration required to save a checkpoint (default: 60 seconds).</div>


* <div data-tips="true" data-tips-type="default">T<sub>redundant</sub>: Redundant time (configuration item esi_redundant_time. Default value: 120 seconds).</div>



Assumption:


* An instance will expire in 200 seconds.

* The maximum duration for a single training step is 80 seconds.

* It is expected to take 60 seconds to save the checkpoint.

* Redundant time configured: 120 seconds.


Then calculate:

80 + 60 + 120 = 260 \> 200

This indicates that the remaining time is insufficient, and the action of early checkpoint saving will be triggered.

<span id="qVFEzyL9"></span>
## Deployment guidelines

<span id="hdtXpnYz"></span>
### Step 1: Purchase an ESI\-Segmented instance

Purchase an ecs.hpcpni3ln.45xlarge instance by referring to Elastic Scheduled Instances\-Segmented.

<span id="XPCtTGJZ"></span>
### Step 2: Obtain the instance release time


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to install volcengine\-python\-sdk.

   ```Shell
   pip install volcengine-python-sdk
   ```
   

3. Upload the following ecs_scheduled_instance_auto_release_time.py file and install.sh file to the instance. [How to upload files to an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview)

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97789ab370b5249896c17252bb1d5236.sh" name="ecs_scheduled_instance_auto_release_time.py..sh">ecs_scheduled_instance_auto_release_time.py..sh</Attachment>
   

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7462b87ad155d4661d15497540da1407.sh" name="install.sh">install.sh</Attachment>
   

4. Add the execute permission and run.

   ```Bash
   chmod +x install.sh
   ./install.sh
   ```
   


<span id="VaozlpV4"></span>
### Step 3: Start a training task


1. Run the following command to enter the training container.

   ```Shell
   docker exec -it ecs-esi-container bash
   ```
   

2. Check whether the instance expiration timestamp is embedded.

   ```Bash
   echo $MLP_CURRENT_CAPACITY_BLOCK_EXPIRATION_TIMESTAMP
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa00ee4735e8f42493557c1429dfbf27.png) </span>

3. Start a training task.

   * Method 1: Run the built\-in demo.

      Go to the /root/verl\-esi directory and execute the `bash examples/grpo_trainer/run_qwen2-7b.sh` command.

   * Method 2: Customize startup script.

      ```Shell
      set -x
      
      python3 -m verl.trainer.main_ppo \
          algorithm.adv_estimator=grpo \
          data.train_files=$HOME/data/gsm8k/train.parquet \
          data.val_files=$HOME/data/gsm8k/test.parquet \
          data.train_batch_size=1024 \
          data.max_prompt_length=512 \
          data.max_response_length=1024 \
          data.filter_overlong_prompts=True \
          data.truncation='error' \
          actor_rollout_ref.model.path=/data1/llm/Qwen2-7B-Instruct \
          actor_rollout_ref.actor.optim.lr=1e-6 \
          actor_rollout_ref.model.use_remove_padding=True \
          actor_rollout_ref.actor.ppo_mini_batch_size=256 \
          actor_rollout_ref.actor.ppo_micro_batch_size_per_gpu=40 \
          actor_rollout_ref.actor.use_kl_loss=True \
          actor_rollout_ref.actor.kl_loss_coef=0.001 \
          actor_rollout_ref.actor.kl_loss_type=low_var_kl \
          actor_rollout_ref.actor.entropy_coeff=0 \
          actor_rollout_ref.model.enable_gradient_checkpointing=True \
          actor_rollout_ref.actor.fsdp_config.param_offload=False \
          actor_rollout_ref.actor.fsdp_config.optimizer_offload=False \
          actor_rollout_ref.rollout.log_prob_micro_batch_size_per_gpu=40 \
          actor_rollout_ref.rollout.tensor_model_parallel_size=2 \
          actor_rollout_ref.rollout.name=vllm \
          actor_rollout_ref.rollout.gpu_memory_utilization=0.6 \
          actor_rollout_ref.rollout.n=5 \
          actor_rollout_ref.ref.log_prob_micro_batch_size_per_gpu=40 \
          actor_rollout_ref.ref.fsdp_config.param_offload=True \
          algorithm.use_kl_in_reward=False \
          trainer.critic_warmup=0 \
          trainer.logger='["console","swanlab"]' \
          trainer.project_name='verl_grpo_example_gsm8k' \
          trainer.experiment_name='qwen2_7b_function_rm' \
          trainer.n_gpus_per_node=8 \
          trainer.nnodes=1 \
          trainer.save_freq=20 \
          trainer.test_freq=5 \
          trainer.total_epochs=15 $@
      ```
      


<span id="UUsyZR6K"></span>
### Step 4: Verify the checkpoint upon expiration of the reserved duration

At each step of the simulation, you will see the following log output:

```Bash
[DEBUG] should_save_ckpt_esi - Input params: max_steps_duration=193.8472616119543, save_ckpt_duration=60, redundant_time=0
[DEBUG] should_save_ckpt_esi - Environment variables: MLP timestamp=1757853000, AWS timestamp=None
[DEBUG] should_save_ckpt_esi - VEMLP platform: remaining_time=273525.75s
[DEBUG] should_save_ckpt_esi - VEMLP: Should save checkpoint? False
```


When `Should save checkpoint == True`, you can dump the model ckpt in the `checkpoints/${trainer.project_name}/${trainer.experiment_name}` directory.

<span id="cdPb5Rdv"></span>
## Engineering recommendations and key points for optimization


* **Measure saving duration (T_save)** : Perform a real save_checkpoint() test once, record the duration and update save_ckpt_duration. The saving duration depends on checkpoint size, disk I/O, and network mounting latency.

* **Set the T_max_steps policy**: It is recommended to use a sliding window (such as the recent 100 steps). Use the maximum value or the 95th/99th percentile. This avoids underestimating the peak value when the average is solely relied on.

* **Redundant time esi_redundant_time**: It is recommended to set it to a value greater than or equal to the upper limit of network or system jitter (for example, 1 to 30 minutes). For critical training, this value can be increased as appropriate.

* **Saving policy**: When I/O cost is manageable, reducing the size of each checkpoint (by saving more frequently with smaller checkpoints) can help you decrease retraining loss after a failure, but will increase I/O overhead. Therefore, you need to strike a balance between cost and recovery speed.


<span id="0WPu77J8"></span>
## Troubleshooting FAQs


* **Failed to obtain information of the scheduled instance/the auto_release_at field is empty**: Check and confirm that the instance is an ESI\-type instance, or check whether the permission or credentials contain the DescribeScheduledInstances permission.

* **Failed to parse time format**: Observe the format of the time string returned by the API, and use dateutil.parser.parse() for compatible parsing if needed.

* **Saving timed out or failed**: Check disk space, target path permission, and network mounting (NFS/S3) latency. Increase save_ckpt_duration and retry.

* **Environment variable not injected into container**: Check and confirm that it has been passed in with "docker run \-e", or that the container entry script has the variable exported.
