---
title: "Initiate MPI distributed training"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Initiate_MPI_distributed_training"
---

MPI is a parallel programming technique based on information transfer. The Machine Learning Platform allows users to initiate distributed training tasks for MPI, and also supports common MPI\-based training frameworks such as Horovod and DeepSpeed. This article uses the above two frameworks as examples to introduce how to initiate distributed training tasks on a Machine Learning Platform.

<span id="基本流程"></span>
# basic flow


1. When the user creates a training task in the [Custom Training] module, select the instance configuration as `MPI`, configure various training roles on demand and submit the task form to enter the task creation process. The MPI contains only the worker role used to train the model, where the worker numbered `0`(worker0) is responsible for executing entry commands (other workers do not execute entry commands) and the task of saving checkpoints or logs.

2. After the task is submitted, the Machine Learning Platform will create a corresponding instance for the user and inject relevant environment variables into all instances, and learn the information of the cluster and the training role corresponding to the current instance through the environment variables user code, thus completing the corresponding role's own task until the end of training.

   * Before training, the platform waits for the network to be clear between all instances.

   * During the training process, if any instance fails (the exit code is not `0`), the training task fails.

   * Worker0 training is completed (exit code is `0`), the training task is successful.


<span id="调用方式"></span>
# call method

The platform injects users with environment variables that may be used in training code or entry commands, and starts training tasks by combining environment variables with the startup commands ( `horovodrun`and `deepspeed`) provided by Horovod and DeepSpeed respectively.

**environment variables**


* MLP_WORKER_NUM: the number of workers.

* MLP_WORKER_GPU: The number of GPUs a single woker contains.

* MLP_MPI_HOSTS: the domain name of each training instance and the number of processes on a single instance.

   * When selecting a CPU instance specification: MLP_MPI_HOSTS = worker0:1, worker1:1,..., i.e. 1 training process per worker.

   * When selecting the GPU instance specification: MLP_MPI_HOSTS = worker0: MLP_WORKER_GPU, worker1: MLP_WORKER_GPU,..., i.e. the number of training processes on each worker corresponds to the number of GPUs.

* MLP_MPI_RACK_HOSTS: Similar to MLP_MPI_HOSTS, but the IP of each worker is sorted by switch hash_id.

* MLP_MPI_HOSTFILE: The hostfile address required by the MPI task. Hostfile functions similarly to MLP_MPI_HOSTS, recording the IP of each worker and the corresponding number of training processes on the worker.

   * The policy of allocating training processes per worker is consistent with MLP_MPI_HOSTS (there is only one training process on a worker instance of the CPU, and the number of training processes on a GPU instance is equal to the number of GPUs contained in that instance).

   * Hostfile example: Represents a total of 2 workers, each containing 2 training processes.

   ```Plain
   172.22.128.95 slots=2
   172.22.128.94 slots=2
   ```
   

* MLP_MPI_NP: The total number of training sessions.

   * When selecting a CPU instance specification: MLP_MPI_NP = MLP_WORKER_NUM.

   * When selecting a GPU instance specification: MLP_MPI_NP = MLP_WORKER_NUM \* MLP_WORKER_GPU.


If you need to use the common environment variables of the [Custom Training] module, please refer to the [List of common environment variables](https://docs.byteplus.com/docs/mlp/List_of_common_environment_variables)[ ](https://www.volcengine.com/docs/6459/75329).

**Key parameters**


* Np: The value corresponding to the MLP_MPI_NP.

* H: The value corresponding to the MLP_MPI_HOSTS.

* Hostfile: Value corresponding to MLP_MPI_HOSTFILE.


Start the Horovod and DeepSpeed distributed training tasks with the following commands:


* Horovod can choose to start tasks with `-H`or `-hostfile`.

   ```Plain
   horovodrun -np $MLP_MPI_NP -H $MLP_MPI_HOSTS python <Absolute path of the code file>
   horovodrun -np $MLP_MPI_NP -hostfile $MLP_MPI_HOSTFILE python <Absolute path of the code file>
   ```
   

* DeepSpeed only supports starting tasks with `--hostfile`.

   Single machine task:

   ```Plain
   deepspeed --hostfile=$MLP_MPI_HOSTFILE <Absolute path of the code file>
   ```
   

   Multi\-mission:

   ```Plain
   deepspeed --hostfile $MLP_MPI_HOSTFILE --master_addr ${MLP_WORKER_0_HOST} --force_multi
   ```
   


&nbsp;

<span id="示例代码"></span>
# sample code

Detailed sample code can be found on [GitHub ](https://github.com/volcengine/ml-platform-sdk-python).
