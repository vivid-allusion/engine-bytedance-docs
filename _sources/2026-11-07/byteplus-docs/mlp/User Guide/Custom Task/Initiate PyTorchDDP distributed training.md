---
title: "Initiate PyTorchDDP distributed training"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Initiate_PyTorchDDP_distributed_training"
---

PyTorch DistributedDataParallel (DDP) is a distributed training method for data parallelism. Create multiple processes through DDP for model training, do process communication through ring\-all\-reduce method, complete layer exchange and parameter update.

<span id="基本流程"></span>
# basic flow


1. When the user creates a training task in the [Custom Training] module, select the instance configuration as `PyTorch DDP`, configure various training roles on demand and submit the task form to enter the task creation process. The PyTorch DDP includes only the worker role for training the model, where the worker numbered `0`(worker0) additionally takes on the task of saving checkpoints or logs.

2. After the task is submitted, the Machine Learning Platform will create a corresponding instance for the user and inject relevant environment variables into all instances, and learn the information of the cluster and the training role corresponding to the current instance through the environment variables user code, thus completing the corresponding role's own task until the end of training.

   * Before training, the platform waits for the network to be clear between all instances.

   * During the training process, if any instance fails (the exit code is not `0`), the training task fails.

   * If all instances are trained (exit code is `0`), the training task is successful.


<span id="调用方式"></span>
# call method

The platform injects the environment variables that may be used in the training code or entry command for the user, and starts the training task through the `torch.distributed.launch`startup command provided by the PyTorch official combined with the environment variables.

**environment variables**


* MLP_WORKER_0_HOST: address of worker0 (worker with RANK = 0).

* MLP_WORKER_0_PORT: port for worker0 (worker with RANK = 0).

* MLP_ROLE_INDEX: the number of the training instance (machine), the values of the environment variables are different in different instances.

* MLP_WORKER_NUM: Number of training instances.

* MLP_WORKER_GPU: The number of GPUs a single woker contains.


If you need to use the common environment variables of the [Custom Training] module, please refer to the [List of common environment variables](https://docs.byteplus.com/docs/mlp/List_of_common_environment_variables)[ ](https://www.volcengine.com/docs/6459/75329).

**Key parameters**


* nproc_per_node: The number of processes running on a single instance (machine), usually the number of GPUs per machine when using GPUs.

* Nnodes: Values MLP_WORKER_NUM environment variables.

* node_rank: the values MLP_ROLE_INDEX environment variables.

* master_addr: the values MLP_WORKER_0_HOST environment variables.

* master_port: the values MLP_WORKER_0_PORT environment variables.


Start the DDP distributed training task with the following command:

```Plain
python -m torch.distributed.launch --nproc_per_node <Number of processes on a single instance> --master_addr $MLP_WORKER_0_HOST --node_rank $MLP_ROLE_INDEX --master_port $MLP_WORKER_0_PORT --nnodes $MLP_WORKER_NUM <Absolute path of the code file>
# When selecting the CPU instance specification, if nproc_per_node = 1, it means that only one training process is executed on each instance.
python -m torch.distributed.launch --nproc_per_node 1 --master_addr $MLP_WORKER_0_HOST --node_rank $MLP_ROLE_INDEX --master_port $MLP_WORKER_0_PORT --nnodes $MLP_WORKER_NUM <Absolute path of the code file>
# When selecting the GPU instance specification, configure the number of training processes on each instance to be the same as the number of GPUs through environment variables.
python -m torch.distributed.launch --nproc_per_node $MLP_WORKER_GPU --master_addr $MLP_WORKER_0_HOST --node_rank $MLP_ROLE_INDEX --master_port $MLP_WORKER_0_PORT --nnodes $MLP_WORKER_NUM <Absolute path of the code file>
```
