---
title: "Ray tasks run on GPUs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_tasks_run_on_GPUs"
---

Ray supports running tasks on GPUs, which is very useful for applications that require significant computational resources, such as deep learning. This article describes the steps for running Ray GPU tasks on Volcano Engine Container Service (VKE).

<span id="_1-前提条件"></span>
## 1. Prerequisites


* The VKE cluster is running properly.

* At least one node in the VKE cluster is configured with an NVIDIA GPU and has the appropriate drivers installed.

* Deploy the Ray service in the EMR on VKE product.


<span id="_2-选择ray镜像"></span>
## 2. Select Ray image

When deploying the RayCluster component in the EMR on VKE product, the image used does not include CUDA dependencies.

EMR provides Ray images with CUDA dependencies, which also include TensorFlow and PyTorch dependencies. See [Ray image list](https://docs.byteplus.com/docs/E-MapReduce/109430) for relevant images.

<span id="_3-pod中配置gpu资源"></span>
## 3. Configure GPU resources in Pod

The EMR management platform provides installation and deployment of RayCluster, allowing you to specify the Ray image and the number of GPUs via a YAML file. For the RayJob method, you can also use a YAML file. The following is an example YAML file:

```yaml
groupName: gpu-group
replicas: 0
minReplicas: 0
maxReplicas: 5
...
template:
    spec:
     ...
     containers:
      - name: ray-node
        image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-cu11.8.0-py3.9-ubuntu20.04-1.2.0
        ...
        resources:
         nvidia.com/gpu: 1 # Optional, included just for documentation.
         cpu: 3
         memory: 50Gi
        limits:
         nvidia.com/gpu: 1 # Required to use GPU.
         cpu: 3
         memory: 50Gi
         ...
```


In the example, `nvidia.com/gpu` indicates that Nvidia GPUs can be used. This can be configured in the `headGroupSpec` and `workerGroupSpecs` sections of the RayCluster YAML. At the same time, the Ray Autoscaler feature also enables elasticity for GPUs.

<span id="_4-ray作业中使用gpu资源"></span>
## 4. **Use GPU resources in Ray jobs**

Once a Ray pod with GPU access is deployed, you can execute tasks and actors that request GPUs. For example, use `@ray.remote(num_gpus=1)` to annotate an actor that requires 1 GPU:

```python
import ray

ray.init()

@ray.remote(num_gpus=1)
class GPUActor:
    def say_hello(self):
        print("I live in a pod with GPU access.")

# Request actor placement.
gpu_actors = [GPUActor.remote() for _ in range(2)]
# The following command will block until two Ray pods with GPU access are scaled
# up and the actors are placed.
ray.get([actor.say_hello.remote() for actor in gpu_actors])

# scale up GPU resources.
ray.autoscaler.sdk.request_resources(bundles=[{"GPU": 1}] * 2)

ray.autoscaler.sdk.request_resources(bundles=[])
```


In the example, `@ray.remote(num_gpus=1)` indicates that the actor requires one GPU.

<span id="_5-使用示例"></span>
## 5. Usage example

```python
"""Example of a custom gym environment and model. Run this for a demo.

This example shows:
  - using a custom environment
  - using a custom model
  - using Tune for grid search

You can visualize experiment results in ~/ray_results using TensorBoard.
"""
import argparse

import ray
from ray import air, tune
from ray.rllib.examples.env.gpu_requiring_env import GPURequiringEnv
from ray.rllib.utils.framework import try_import_tf, try_import_torch
from ray.rllib.utils.test_utils import check_learning_achieved
from ray.tune.registry import get_trainable_cls
from pyarrow import fs

tf1, tf, tfv = try_import_tf()
torch, nn = try_import_torch()

parser = argparse.ArgumentParser()
parser.add_argument(
    "--run", type=str, default="PPO", help="The RLlib-registered algorithm to use."
)
parser.add_argument(
    "--framework",
    choices=["tf", "tf2", "torch"],
    default="torch",
    help="The DL framework specifier.",
)
parser.add_argument("--num-gpus", type=float, default=0.5)
parser.add_argument("--num-workers", type=int, default=1)
parser.add_argument("--num-gpus-per-worker", type=float, default=0.0)
parser.add_argument("--num-envs-per-worker", type=int, default=1)
parser.add_argument(
    "--as-test",
    action="store_true",
    help="Whether this script should be run as a test: --stop-reward must "
    "be achieved within --stop-timesteps AND --stop-iters.",
)
parser.add_argument(
    "--stop-iters", type=int, default=50, help="Number of iterations to train."
)
parser.add_argument(
    "--stop-timesteps", type=int, default=100000, help="Number of timesteps to train."
)
parser.add_argument(
    "--stop-reward", type=float, default=180.0, help="Reward at which we stop training."
)

if __name__ == "__main__":
    args = parser.parse_args()
    ray.init()

    # These configs have been tested on a p2.8xlarge machine (8 GPUs, 16 CPUs),
    # where ray was started using only one of these GPUs:
    # $ ray start --num-gpus=1 --head

    # Note: A strange error could occur when using tf:
    #       "NotImplementedError: Cannot convert a symbolic Tensor
    #       (default_policy/cond/strided_slice:0) to a numpy array."
    #       In rllib/utils/exploration/random.py.
    #       Fix: Install numpy version 1.19.5.

    # Tested arg combinations (4 tune trials will be setup; see
    # tune.grid_search over 4 learning rates below):
    # - num_gpus=0.5 (2 tune trials should run in parallel).
    # - num_gpus=0.3 (3 tune trials should run in parallel).
    # - num_gpus=0.25 (4 tune trials should run in parallel)
    # - num_gpus=0.2 + num_gpus_per_worker=0.1 (1 worker) -> 0.3
    #   -> 3 tune trials should run in parallel.
    # - num_gpus=0.2 + num_gpus_per_worker=0.1 (2 workers) -> 0.4
    #   -> 2 tune trials should run in parallel.
    # - num_gpus=0.4 + num_gpus_per_worker=0.1 (2 workers) -> 0.6
    #   -> 1 tune trial should run in parallel.

    config = (
        get_trainable_cls(args.run)
        .get_default_config()
        # Setup the test env as one that requires a GPU, iff
        # num_gpus_per_worker > 0.
        .environment(
            GPURequiringEnv if args.num_gpus_per_worker > 0.0 else "CartPole-v1"
        )
        .framework(args.framework)
        .resources(
            # How many GPUs does the local worker (driver) need? For most algos,
            # this is where the learning updates happen.
            # Set this to > 1 for multi-GPU learning.
            num_gpus=args.num_gpus,
            # How many GPUs does each RolloutWorker (`num_workers`) need?
            num_gpus_per_worker=args.num_gpus_per_worker,
        )
        # How many RolloutWorkers (each with n environment copies:
        # `num_envs_per_worker`)?
        .rollouts(
            num_rollout_workers=args.num_workers,
            # This setting should not really matter as it does not affect the
            # number of GPUs reserved for each worker.
            num_envs_per_worker=args.num_envs_per_worker,
        )
        # 4 tune trials altogether.
        .training(lr=tune.grid_search([0.005, 0.003, 0.001, 0.0001]))
    )

    stop = {
        "training_iteration": args.stop_iters,
        "timesteps_total": args.stop_timesteps,
        "episode_reward_mean": args.stop_reward,
    }

    # Note: The above GPU settings should also work in case you are not
    # running via ``Tuner.fit()``, but instead do:

    # >> from ray.rllib.algorithms.ppo import PPO
    # >> algo = PPO(config=config)
    # >> for _ in range(10):
    # >>     results = algo.train()
    # >>     print(results)

    s3 = fs.S3FileSystem(access_key='xxx', secret_key='xxx',endpoint_override='xxx', force_virtual_addressing=True)

    results = tune.Tuner(
        args.run, param_space=config.to_dict(), run_config=air.RunConfig(stop=stop, storage_path="ceshi-dts/ray-store", storage_filesystem = s3)
    ).fit()

    if args.as_test:
        check_learning_achieved(results, args.stop_reward)
    ray.shutdown()
```


In the example, a torch model is trained using a GPU, and intermediate data generated during the job execution is stored in the TOS object storage. Therefore, you need to provide the actual access_key, secret_key, and endpoint_override parameters.

You can view GPU resource usage in the Ray dashboard.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a6edaf1296323cac1f5580f16de222a1.png) </span>
