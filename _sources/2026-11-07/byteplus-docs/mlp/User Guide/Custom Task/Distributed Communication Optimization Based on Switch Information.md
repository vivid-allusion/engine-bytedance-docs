---
title: "Distributed Communication Optimization Based on Switch Information"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Distributed_Communication_Optimization_Based_on_Switch_Information"
---

Common large model training methods include data parallelism/model parallelism/pipeline parallelism, etc. Different parallel methods actually group the instances participating in the training. The communication frequency (traffic) between instances in the same group is much higher than the communication frequency (traffic) between instances in the same group, so the instances in the same group should be dispatched to the more friendly nodes of the network as much as possible during task scheduling. This article describes how to reduce the frequency of cross\-switch communication under large\-scale training.

<span id="在训练任务中注入交换机信息"></span>
# Inject switch information into the training task

The Machine Learning Platform will inject some environment variables into the corresponding container when the task is created, and these environment variables record the information of the switch.


* MLP_RACK_TOPO_FILE: The path of the switch information file in the container, the default path is `/ml_platform/rack_topo`, the example is as follows:

   ```Plain
   # ${MLP_TASK_INSTANCE_ID}          ${MLP_PRIMARY_HOST}    ${MLP_WORKER_RACK_SW_ID}
   t-20230615154118-9mlks-worker-0    10.252.133.193         febd30c7302dda1fae1399fe0266930f
   t-20230615154118-9mlks-worker-1    10.252.132.1           febd30c7302dda1fae1399fe0266930f
   ...
   ```
   

* MLP_ ${MLP_ROLE} _RACK_SW_ID: the switch hash_id of the node where the current task instance is located, which will only be injected into the HPC container.

* MLP_ ${MLP_ROLE} _RACK_RANK_INDEX: PyTorchDDP and MPI framework tasks will inject worker index environment variables sorted by switch hash_id, while ensuring that worker0 has index = 0. This environment variable can be used in training to specify node_rank to reduce the frequency of cross\-switch communication in scenarios such as allreduce.

   * The tasks of the MPI framework will be sorted according to the switch hash_id, and in addition to the original /root/mpi_hostfile, an additional hostfile file will be generated, the path is `/root/mpi_rack_hostfile`, and the worker_0 is guaranteed to be in the first place. In addition, the platform will inject environment variables MLP_MPI_RACK_HOSTS in the same format as [Initiate MPI distributed training](https://docs.byteplus.com/docs/mlp/Initiate_MPI_distributed_training), but the order of the IPs is sorted by switching hash_id.


<span id="启动脚本示例"></span>
# Startup script example

Below is an example of a PyTorchDDP startup (note that `NODE_RANK`is specified as `MLP_WORKER_RACK_RANK_INDEX`). For MPI users, you can start the task directly through the `/root/mpi_rack_hostfile`without additional environment variables configuration.

```Plain
export GPUS_PER_NODE=${MLP_WORKER_GPU:-1}
export NNODES=${MLP_WORKER_NUM:-1}
export NODE_RANK=${MLP_WORKER_RACK_RANK_INDEX:-0}
export PORT=${MLP_WORKER_0_PORT:-1234}
export MASTER_ADDR=${MLP_WORKER_0_HOST:-127.0.0.1}
export MASTER_PORT=${MLP_WORKER_0_PORT:-1234}
DISTRIBUTED_ARGS="--nproc_per_node $GPUS_PER_NODE --nnodes $NNODES --node_rank $NODE_RANK --master_addr $MASTER_ADDR --master_port $MASTER_PORT"
python -m torch.distributed.launch $DISTRIBUTED_ARGS <Path to the startup script>
```
