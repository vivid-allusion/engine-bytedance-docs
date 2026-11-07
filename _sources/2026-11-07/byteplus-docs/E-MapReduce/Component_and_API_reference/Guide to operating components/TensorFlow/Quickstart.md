---
title: "Quickstart"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/tensorflow_quickstart"
---

This article will demonstrate how to use Primus and submit a sample Hello Primus task.

After successfully running Primus Hello, you can go to [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109529) to further learn how Primus collaborates with TensorFlow to perform a distributed model training task.

<span id="_1-准备工作"></span>
# 1 Preparation

If this is your first time using an EMR DataScience cluster, some preparation is required first!

Since the following examples are all operated by the Yarn user, you must configure HDFS read and write permissions for the Yarn user. This part of the configuration can be completed using the Ranger component in EMR. For detailed steps, refer to the screenshots below.

<span id="_1-1-进入-ranger-ui"></span>
## 1.1 Access the Ranger UI


1. To access the cluster, you need to bind an elastic public IP to the ECS instance. For public network operations, see [Bind Public IP](https://www.volcengine.com/docs/6401/68687), and for other details, see [Access link](https://docs.byteplus.com/docs/E-MapReduce/105434).

2. In **Quickly configure service ports**, you need to add the source address and corresponding port to the allowlist before you can continue accessing.

3. The username and password required for access can be obtained from the service parameters of **Ranger Service**.


<span id="_1-2-配置hdfs-的读写权限"></span>
## 1.2 Configure HDFS read and write permissions


1. Click the **HDFS** folder and then the **default_hadoop** configuration entry:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61808996f942eb67e28af9426ba642d3.png) </span>


2. In the operation column where **Policy Name** is **all\-path**, click the **Edit** button to enter the permission configuration entry:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ce71937838b2794e1ca869b1cb8f6d5f.png) </span>


3. Add Yarn in the user selection field:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba209a69b13a21b583952ee0787c36a0.png) </span>


4. Click the save button to complete the permission configuration.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_680034187f00e84d57e3dfc74ffb91c9.png) </span>

<span id="_2-hello-primus"></span>
# 2 Hello Primus!

After completing the preparation, before we submit our first Primus task, let us first take a look at the Primus training configuration for the Hello Primus task. At this point, you may also notice that Hello Primus is a lazy task, because each role takes a secret nap of 900 seconds between saying Hello and Goodbye!

```plain
{
  "name": "primus_basic_hello", // 任务名称
  "maxAppAttempts": 1,          // 重试次数
  "role": [                     // 角色定义
    {
      "roleName": "chief",                   // 角色名称
      "num": 1,                              // 数量
      "vcores": 1,                           // CPU 配置
      "memoryMb": 1024,                      // Mem 配置
      "jvmMemoryMb": 1024,                   // Java Mem 配置
      "command": "env && echo 'Hello from Chief' && sleep 900 && echo 'Goodbye from Chief'", // 训练指令
      "successPercent": 100,                 // 角色退出条件 (100% 需要训练进程自行退出，目前仅支援 100 跟 0)
      "failover": {                          // 角色失败处理
        "commonFailoverPolicy": {
          "maxFailureTimes": 1,              // 失败重试
          "maxFailurePolicy": "FAIL_ATTEMPT" // 角色失败时，失败这次 YARN Attempt 
        }
      }
    },
    {
      "roleName": "ps",
      "num": 1,
      "vcores": 1,
      "memoryMb": 1024,
      "jvmMemoryMb": 1024,
      "command": "env && echo 'Hello from PS' && sleep 900 && echo 'Goodbye from PS'",
      "successPercent": 100,
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
      "memoryMb": 1024,
      "jvmMemoryMb": 1024,
      "command": "env && echo 'Hello from worker' && sleep 900 && echo 'Goodbye from worker'",
      "successPercent": 100,
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


Now we can finally submit our first Primus training task!

```plain
# Change to yarn user
$ su --shell=/bin/bash - yarn

# Move to primus directory
$ cd /usr/lib/emr/current/tensorflow_on_yarn/

# Submit primus-hello!
$ primus-submit --primus_conf examples/hello/primus_config.json
...
22/03/03 18:36:47 INFO impl.YarnClientImpl: Submitted application <YARN-APPLICATION-ID>
22/03/03 18:36:47 INFO client.YarnSubmitCmdRunner: Tracking URL: http://emr-master-1:8088/proxy/<YARN-APPLICATION-ID>/
22/03/03 18:36:57 INFO client.YarnSubmitCmdRunner: Training successfully started. Scheduling took 10010 ms.
22/03/03 18:38:18 INFO client.YarnSubmitCmdRunner: State: FINISHED  Progress: 100.0%
22/03/03 18:38:18 INFO client.YarnSubmitCmdRunner: Application <YARN-APPLICATION-ID> finished with state FINISHED at 2022-03-03 18:38
22/03/03 18:38:18 INFO client.YarnSubmitCmdRunner: Final Application Status: SUCCEEDED
...

# Verify the results (Can check in another terminal before the completion of the Primus application)
$ yarn logs --applicationId <YARN-APPLICATION-ID> | grep -i hello
...
Hello from Chief
Hello from PS
Hello from worker
...
```


Since the Primus training task is a standard YARN task, you can observe the Primus training task in the YARN UI!

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d08b1d263c7d215a8df0fe4346661397.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_50513d5a963ff411bfb85dfb300cde13.png) </span>
