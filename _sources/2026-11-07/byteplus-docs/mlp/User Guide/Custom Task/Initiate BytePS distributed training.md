---
title: "Initiate BytePS distributed training"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Initiate_BytePS_distributed_training"
---

BytePS is a self\-developed distributed training communication framework that is currently open\-sourced on [GitHub ](https://github.com/bytedance/byteps). The main features are as follows:


* It also supports three computing frameworks: TF, PyTorch, and MXNet.

* High performance: For communication\-intensive tasks, the performance significantly exceeds that of Horovod and PyTorch DDP under equivalent conditions.

* The current implementation scenarios include large\-scale training such as BERT and GAN.


<span id="基本流程"></span>
# basic flow


1. When the user creates a training task in the [Custom Training] module, select the instance to be configured as `BytePS`, configure various training roles on demand and submit the task form to enter the task Create link. There are several training roles as follows:

* Server: Manages the storage and updating of parameters.

* Workers: Perform training tasks.

* Scheduler: Responsible for communication between server and worker.

2. After the task is submitted, the Machine Learning Platform will Create the corresponding instance for the user and inject relevant environment variables into all instances, and learn the information of the cluster and the training role corresponding to the current instance through the environment variables user code, so as to complete the corresponding role's own task until the end of training.

   * Before training, the platform waits for the network to be clear between all instances.

   * During the training process, if any instance fails (the exit code is not `0`), the training task fails.

   * If all instances are trained (exit code is `0`), the training task is successful.


<span id="调用方式"></span>
# call method

The platform injects environment variables that may be used in training code or entry commands for users, and combines the environment variables Start training task with the `bpslaunch`Start command officially provided by BytePS.

**environment variables**


* DMLC_PS_ROOT_URI: The domain name for scheduler0.

* DMLC_PS_ROOT_PORT: Port of scheduler.

* DMLC_NUM_SERVER: The number of server instances.

* DMLC_NUM_WORKER: Number of worker instances.

* DMLC_ROLE: the role type of the instance.

* DMLC_WORKER_ID: worker number.


If you need to use the common environment variables of the [Custom Training] module, please refer to the [List of common environment variables](https://docs.byteplus.com/docs/mlp/List_of_common_environment_variables).

Start BytePS distributed training tasks with the following command:

```Plain
bpslaunch python <Absolute path of code file>
```


<span id="示例代码"></span>
# sample code

Detailed sample code can be found on [GitHub ](https://github.com/volcengine/ml-platform-sdk-python).
