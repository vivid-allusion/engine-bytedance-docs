---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/tensorflow_basic_usage"
---

After successfully submitting the first Primus training task in [Quickstart](https://docs.byteplus.com/docs/E-MapReduce/109533), you can now try using Primus to run distributed TensorFlow training tasks! This section demonstrates three different TensorFlow distributed strategies in order: Single Node, MultiWorkerMirrored, and ParameterServer.

<span id="_1-准备工作"></span>
# 1 Preparation

Since TensorFlow training requires training data and a Python environment, you need to carry out additional preparation here!

```bash
# Change to yarn user
$ su --shell=/bin/bash - yarn

# Create the workspace
$ mkdir ~/primus-playground
$ cd ~/primus-playground
$ cp -r /usr/lib/emr/current/tensorflow_on_yarn/examples .

# Build the Python virtual environment
$ cd examples/shared/venv 
$ ./build.sh

# Prepare the workspace on HDFS and the datasets
$ cd ~/primus-playground/
$ hdfs dfs -mkdir mnist
$ hdfs dfs -mkdir mnist/models
$ hdfs dfs -put examples/shared/mnist/data mnist
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">In the tutorial, the required Python packages are installed using pip to create the Python virtual environment, so the cluster's master node needs to be bound to a public IP address. To create a Python virtual environment on the local machine due to various factors, refer to: <a href="https://docs.byteplus.com/docs/E-MapReduce/109528">Advanced usage</a>.</div>


2. <div data-tips="true" data-tips-type="warning">At the same time, the EMR DataScience cluster already has the tensorflow and tensorflow\-io Python packages installed. Therefore, if future training does not require other Python packages, the step of creating a Python virtual environment can be skipped.</div>


3. <div data-tips="true" data-tips-type="warning">The domain name conventions for nodes may differ between EMR versions, so the “emr\-master\-1\-1” in the sample code of this section can be adjusted accordingly by referring to EMR’s <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a>.</div>



<span id="_2-开始训练！"></span>
# 2 Start training!

Once all preparation is complete, you can start distributed TensorFlow training!

<span id="_2-1-single-node"></span>
## [2.1 Single Node](https://www.tensorflow.org/tutorials/quickstart/beginner)

First, you can review the Primus training configuration. From the configuration, you can see that compared to Hello Primus, more training resources are specified, including the Primus virtual environment and training script, as well as more complex training commands!

```json
{
  "name": "primus_tensorflow_single",
  "files": [ 
    "examples/shared/venv/venv.tar.gz", // Python virtual environent
    "examples/tensorflow-single"        // Path to training script folder
  ],
  "role": [
    {
      "roleName": "main",
      "num": 1, // Single-node training
      "vcores": 1,
      "memoryMb": 512,
      "jvmMemoryMb": 512,
      "command": "./tensorflow-single/main.sh venv.tar.gz", // Training command
      "successPercent": 100,
      "failover": {
        "commonFailoverPolicy": {
          "commonFailover": {
            "maxFailureTimes": 10,
            "maxFailurePolicy": "FAIL_ATTEMPT"
          }
        }
      }
    }
  ]
}
```


Submit the training using primus\-submit!

```bash
# Submit Primus application
$ cd ~/primus-playground
$ primus-submit --primus_conf examples/tensorflow-single/primus_config.json
...
22/03/03 18:36:47 INFO impl.YarnClientImpl: Submitted application <YARN-APPLICATION-ID>
22/03/03 18:36:47 INFO client.YarnSubmitCmdRunner: Tracking URL: http://emr-master-1-1:8088/proxy/<YARN-APPLICATION-ID>/
22/03/03 18:36:57 INFO client.YarnSubmitCmdRunner: Training successfully started. Scheduling took 10010 ms.
22/03/03 18:38:18 INFO client.YarnSubmitCmdRunner: State: FINISHED  Progress: 100.0%
22/03/03 18:38:18 INFO client.YarnSubmitCmdRunner: Application <YARN-APPLICATION-ID> finished with state FINISHED at 2022-03-03 18:38
22/03/03 18:38:18 INFO client.YarnSubmitCmdRunner: Final Application Status: SUCCEEDED
...

# Observe YARN logs
$ yarn logs --applicationId <YARN-APPLICATION-ID> | grep -E "Epoch|FIN"
...
+ echo FIN
Epoch 1/5
Epoch 2/5
Epoch 3/5
Epoch 4/5
Epoch 5/5
FIN
...
```


Finally, since this example outputs the model to HDFS, you can use a Python script to test the model's performance!

```bash
$ cd ~/primus-playground/examples/tensorflow-single
 
$ export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/jre/lib/amd64/server/
$ export HADOOP_HDFS_HOME=/usr/lib/emr/current/hadoop
$ export CLASSPATH=$(hadoop classpath --glob)

$ python3.9 evaluate.py \
  --mnist hdfs://emr-master-1-1:8020/user/yarn/mnist/data \
  --model hdfs://emr-master-1-1:8020/user/yarn/mnist/models/model-single
...
Model accuracy: [0.29252758622169495, 0.9218999743461609]
...
```


<span id="_2-2-multi-worker-mirrored"></span>
## [2.2 Multi Worker Mirrored](https://www.tensorflow.org/api_docs/python/tf/distribute/experimental/MultiWorkerMirroredStrategy)

Before submitting the Primus training task, you can review the Primus training configuration. You can quickly see that the Primus training configuration for Multi Worker Mirrored training is very similar to that for Single Node training. The main difference is that Multi Worker Mirrored training requires multiple nodes to complete, so in the Primus training configuration, the number of nodes for "num" is set to 2.

```json
{
  "name": "primus_tensorflow_multiworkermirrored",
  "maxAppAttempts": 1,
  "files": [
    "examples/shared/venv/venv.tar.gz",
    "examples/tensorflow-multiworkermirrored"
  ],
  "role": [
    {
      "roleName": "worker",
      "num": 2, // Multi-node training
      "vcores": 1,
      "memoryMb": 512,
      "jvmMemoryMb": 512,
      "command": "./tensorflow-multiworkermirrored/main.sh venv.tar.gz",
      "successPercent": 100,
      "failover": {
        "hybridDeploymentFailoverPolicy": {
          "commonFailover": {
            "maxFailureTimes": 10,
            "maxFailurePolicy": "FAIL_ATTEMPT"
          }
        }
      }
    }
  ]
}
```


Submit the training using primus\-submit!

```plaintext
# Submit Primus application
$ cd ~/primus-playground
$ primus-submit --primus_conf examples/tensorflow-multiworkermirrored/primus_config.json
...
22/03/03 18:42:53 INFO impl.YarnClientImpl: Submitted application <YARN-APPLICATION-ID>
22/03/03 18:42:53 INFO client.YarnSubmitCmdRunner: Tracking URL: http://emr-master-1-1:8088/proxy/<YARN-APPLICATION-ID>/
22/03/03 18:43:03 INFO client.YarnSubmitCmdRunner: Training successfully started. Scheduling took 10014 ms.
22/03/03 18:44:34 INFO client.YarnSubmitCmdRunner: State: FINISHED  Progress: 100.0%
22/03/03 18:44:34 INFO client.YarnSubmitCmdRunner: Application <YARN-APPLICATION-ID> finished with state FINISHED at 2022-03-03 18:44
22/03/03 18:44:34 INFO client.YarnSubmitCmdRunner: Final Application Status: SUCCEEDED
...

# Observe YARN logs
$ yarn logs --applicationId <YARN-APPLICATION-ID> | grep -E "Epoch|FIN"
...
+ echo FIN
Epoch 1/3
Epoch 2/3
Epoch 3/3
FIN
+ echo FIN
Epoch 1/3
Epoch 2/3
Epoch 3/3
FIN
...
```


Similarly, since this example outputs the model to HDFS, you can also use a Python script to test the model's performance!

```bash
$ cd ~/primus-playground/examples/tensorflow-multiworkermirrored
 
$ export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/jre/lib/amd64/server/
$ export HADOOP_HDFS_HOME=/usr/lib/emr/current/hadoop
$ export CLASSPATH=$(hadoop classpath --glob)

$ python3.9 evaluate.py \
  --mnist hdfs://emr-master-1-1:8020/user/yarn/mnist/data \
  --model hdfs://emr-master-1-1:8020/user/yarn/mnist/models/model-multiworkermirrored
...
Model accuracy: [2.0982000827789307, 0.5758000016212463]
...
```


<span id="_2-3-parameter-server"></span>
## [2.3 Parameter Server](https://www.tensorflow.org/tutorials/distribute/parameter_server_training)

Again, start by reviewing the Primus training configuration. Compared to the Primus training configuration for Single Node, the configuration required for Parameter Server is much larger.

However, the main differences are only two parts: more roles, and the exit conditions for the PS and Worker roles are set to 0%. In the TensorFlow Parameter Server distributed strategy, these two roles are persistent, so the training processes do not exit automatically.

```json
{
  "name": "primus_tensorflow_parameterserver",
  "maxAppAttempts": 1,
  "files": [
    "examples/basics/shared/venv/venv.tar.gz",
    "examples/basics/tensorflow-parameterserver/main.sh", 
    "examples/basics/tensorflow-parameterserver/chief.py",
    "examples/basics/tensorflow-parameterserver/ps.py",
    "examples/basics/tensorflow-parameterserver/worker.py"
  ],
  "role": [ // More roles!
    {
      "roleName": "chief",
      "num": 1,
      "vcores": 1,
      "memoryMb": 512,
      "jvmMemoryMb": 512,
      "command": "./main.sh venv.tar.gz chief.py",
      "successPercent": 100,
      "failover": {
        "commonFailoverPolicy": {
          "maxFailureTimes": 1,
          "maxFailurePolicy": "FAIL_ATTEMPT"
        }
      }
    },
    {
      "roleName": "ps",
      "num": 1,
      "vcores": 1,
      "memoryMb": 512,
      "jvmMemoryMb": 512,
      "command": "./main.sh venv.tar.gz ps.py",
      "successPercent": 0, // The Parameter Server in TensorFlow strategy is persistent, so there is no need to wait for this process to complete
      "failover": {
        "commonFailoverPolicy": {
          "maxFailureTimes": 1,
          "maxFailurePolicy": "FAIL_ATTEMPT"
        }
      }
    },
    {
      "roleName": "worker",
      "num": 1,
      "vcores": 1,
      "memoryMb": 512,
      "jvmMemoryMb": 512,
      "command": "./main.sh venv.tar.gz worker.py",
      "successPercent": 0, // Same as Parameter Server
      "failover": {
        "commonFailoverPolicy": {
          "maxFailureTimes": 1,
          "maxFailurePolicy": "FAIL_ATTEMPT"
        }
      }
    }
  ]
}
```


Submit the training using primus\-submit!

```bash
# Submit Primus application
$ cd ~/primus-playground
$ primus-submit --primus_conf examples/tensorflow-parameterserver/primus_config.json
...
22/03/03 18:58:39 INFO impl.YarnClientImpl: Submitted application <YARN-APPLICATION-ID>
22/03/03 18:58:39 INFO client.YarnSubmitCmdRunner: Tracking URL: http://emr-master-1-1:8088/proxy/<YARN-APPLICATION-ID>/
22/03/03 18:58:49 INFO client.YarnSubmitCmdRunner: Training successfully started. Scheduling took 10010 ms.
22/03/03 19:00:23 INFO client.YarnSubmitCmdRunner: State: FINISHED  Progress: 100.0%
22/03/03 19:00:23 INFO client.YarnSubmitCmdRunner: Application <YARN-APPLICATION-ID> finished with state FINISHED at 2022-03-03 19:00
22/03/03 19:00:23 INFO client.YarnSubmitCmdRunner: Final Application Status: SUCCEEDED
...

# Observe YARN logs
$ yarn logs --applicationId <YARN-APPLICATION-ID> | grep -E "Epoch|FIN"
...
+ echo FIN
Epoch 1/5
Epoch 2/5
Epoch 3/5
Epoch 4/5
Epoch 5/5
FIN
...
```
