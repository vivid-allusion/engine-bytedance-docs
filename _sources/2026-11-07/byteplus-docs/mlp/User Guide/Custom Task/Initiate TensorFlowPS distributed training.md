---
title: "Initiate TensorFlowPS distributed training"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Initiate_TensorFlowPS_distributed_training"
---

TensorFlow supports parameter server training on multiple machines. Under this ps\-worker architecture, some instances are designated as worker processes and some instances are designated as parameter servers. In each round of training, ps distributes the latest model parameters to workers. After the worker completes the calculation, the layer is sent back to ps. After ps updates the parameters, it enters the next round of training until the training is completed.

<span id="基本流程"></span>
# basic flow


1. When the user creates a training task in the [Custom Training] module, select the instance configuration as `TensorFlow PS`, configure various training roles on demand and submit the task form to enter the task creation process. There are several training roles as follows:

   * Ps: A parameter server that manages parameter storage and updates. The number of instances must be \> = 1.

   * Worker: The process of performing a training task. Without a chief, the number of instances of worker must be \> = 1.

   * Chief: Equivalent to worker0, responsible for saving checkpoints or logs in addition to performing training tasks. In the absence of a worker, the number of instances of chief must be \> = 1.

   * Evaluator: Perform evaluation tasks. Configure the number of instances as needed.

2. After the task is submitted, the Machine Learning Platform will create a corresponding instance for the user and inject relevant environment variables into all instances, and learn the information of the cluster and the training role corresponding to the current instance through the environment variables user code, thus completing the corresponding role's own task until the end of training.

   * Before training, the platform waits for the network to be clear between all instances.

   * During the training process, if any instance fails (the exit code is not `0`), the training task fails.

   * If all instances are trained (exit code is `0`), the training task is successful.


<span id="tf-config"></span>
# TF_CONFIG

`TF_CONFIG`It is the most critical environment variable in TensorFlow distributed training. The platform is configured according to the user's instance and populates the cluster information to `TF_CONFIG`according to the specifications of the open source community. Here is a specific example:

```Plain
{
    "cluster": {
        "chief": [              // List of chief instances
            "chief0-host:port",
            "chief1-host:port"
            // ...
        ],
        "evaluator": [         // List of evaluator instances
            "evaluator0-host:port",
            "evaluator1-host:port",
            // ...
        ],
        "ps": [                // List of ps instances
            "ps0-host:port",
            "ps1-host:port",
            // ...
        ],
        "worker": [            // List of worker instances
            "worker0-host:port",
            "worker1-host:port",
            // ...
        ]
    },
    "environment": "cloud",
    "task": {
        "index": 0,           // Role number
        "type": "chief"       // Affiliated role 
    }
}
```


Each instance knows the number of chief/worker/ps/evaluator and the corresponding address of the entire distributed set according to the cluster field in the TF_CONFIG ,`cluster field in the TF_CONFIG`, and knows the role and number of the current instance from the `task`field. In this example, the role of the current instance is chief, and checkpoints and logs need to be saved in addition to being a worker process.

If you need to use the common environment variables of the [Custom Training] module, please refer to the [List of common environment variables](https://docs.byteplus.com/docs/mlp/List_of_common_environment_variables)[ ](https://www.volcengine.com/docs/6459/75329).

<span id="示例代码"></span>
# sample code

Detailed sample code can be found on [GitHub ](https://github.com/volcengine/ml-platform-sdk-python).
