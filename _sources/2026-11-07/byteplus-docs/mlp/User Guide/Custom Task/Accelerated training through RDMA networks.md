---
title: "Accelerated training through RDMA networks"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Accelerated_training_through_RDMA_networks"
---

Remote Direct Memory Access (RDMA) is a new generation of network transmission technology, which was born mainly to solve the delay of server\-side data processing in network transmission. In large\-scale distributed training tasks, high throughput and low latency network communication can be obtained by using RDMA technology, which improves training efficiency. This article will introduce how to perform distributed training on high\-performance GPU instances based on RDMA on the Machine Learning Platform.

<span id="相关概念"></span>
# related concepts


* [Instance Specifications and Pricing](https://docs.byteplus.com/docs/mlp/Instance_Specifications_and_Pricing)


<span id="使用前提"></span>
# premise of use


* Have access to \> = 1 dedicated resource group.

* The queue contains at least 2 **high\-performance GPU instances** that support RDMA.

* Refer to [Verify that the mirror supports RDMA.](https://docs.byteplus.com/docs/mlp/Verify_that_the_mirror_supports_RDMA) to verify that the relevant configuration of RDMA in the image is complete.


<span id="操作步骤"></span>
# Procedure


1. The basic steps for creating a training task are detailed in [Initiate stand-alone/distributed training tasks](https://docs.byteplus.com/docs/mlp/Initiate_stand-alone_distributed_training_tasks)[ ](https://www.volcengine.com/docs/6459/72350).

2. Complete a small amount of code modification according to the training framework selected by the user and its underlying communication framework to enable the RDMA feature.

   * **Using NCCL as a communication framework**

      * Applicable distributed training frameworks:

         * TensorFlowPS, the basic training process is detailed in[ ](https://www.volcengine.com/docs/6459/75221)[Initiate TensorFlowPS distributed training](https://docs.byteplus.com/docs/mlp/Initiate_TensorFlowPS_distributed_training).

         * PyTorchDDP actually supports PyTorchDDP/Megatron, etc. The basic training process is detailed in [Initiate PyTorchDDP distributed training](https://docs.byteplus.com/docs/mlp/Initiate_PyTorchDDP_distributed_training)[ ](https://www.volcengine.com/docs/6459/75222).

         * MPI, actual support for Horovod/DeepSpeed, etc. The basic training process is detailed in [Initiate MPI distributed training](https://docs.byteplus.com/docs/mlp/Initiate_MPI_distributed_training)[ ](https://www.volcengine.com/docs/6459/75223).

      * The platform will preset the following environment variables, please refer to [the environment variables description of NCCL ](https://docs.nvidia.com/deeplearning/nccl/user-guide/docs/env.html).

         ```Plain
         # If the default values of the following three variables do not meet your requirements, you can override the corresponding values before starting the training script.
         NCCL_DEBUG=${NCCL_DEBUG:-INFO}
         NCCL_IB_TIMEOUT=${NCCL_IB_TIMEOUT:-23}
         NCCL_IB_RETRY_CNT=${NCCL_IB_RETRY_CNT:-7}
         # It is recommended that users directly use the default values for the following variables and do not modify them manually.
         NCCL_IB_HCA=<Automatically injected by the platform based on the instance specification>
         NCCL_IB_DISABLE=0 
         NCCL_IB_GID_INDEX=<Automatically injected by the platform based on the instance specification>
         NCCL_SOCKET_IFNAME=<The default VPC network card injected by the platform>
         NCCL_IB_PCI_RELAXED_ORDERING=1 
         NCCL_TOPO_FILE=<Automatically injected by the platform based on the instance specification>
         ```
         

   * **A communication optimization framework developed by Volcano**

      * Applicable distributed training frameworks:

         * BytePS

         * veGiantModel

      * Inject the following environment variables before the training script starts, as detailed in [the environment variables description of BytePS ](https://github.com/bytedance/byteps/blob/master/docs/env.md).

         ```Plain
         export DMLC_ENABLE_RDMA=1
         export DMLC_INTERFACE=eth0
         ```
         

3. When configuring a resource group, select a proprietary resource group that contains a high\-performance GPU (e.g. ml.hpcg1v.21xlarge, ml.hpcg1ve.21xlarge, ml.hpcpni2.28xlarge), and configure the corresponding instance specification as an instance of a high\-performance GPU.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1251efec55c041feafa2b6bf76f0d85c~tplv-goo7wpa0wc-image.image) </span>


4. After submitting the task configuration, wait for the task state to reach `the running`, and then the training task uses RDMA for distributed training.

5. Support for viewing RDMA\-related monitoring metrics during training.
