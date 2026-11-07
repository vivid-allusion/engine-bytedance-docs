---
title: "Developing code with WebIDE"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Developing_code_with_WebIDE"
---

WebIDE is an online integrated development environment provided by the Machine Learning Platform. The new version of WebIDE comes with a built\-in VSCode\-Python plugin, Tensorboard, and Jupyter Notebook for a better online development experience. The following describes some of the tools commonly used in WebIDE, such as the Volc CLI and the Rclone CLI.

<span id="使用-volc-命令行工具提交分布式训练任务"></span>
# Submit distributed training tasks using the Volc command\-line tool

The Machine Learning Platform provides command\-line tools for users to manage training tasks on the platform on any machine with a smooth network.

<span id="volc-配置"></span>
## Volc configuration


1. Use `volc configure`on the command line to configure the relevant parameters below.


```Plain
volc configure
volc access key [********4M2Q]:          //Enter the AK of this account
volc secret access key [********TQ==]:   //Enter the SK of this account
volc region [cn-beijing]:                //Enter the area（cn-beijing、cn-shanghai、cn-guangzhou）
```



2. After the setup is complete, please check the existence of `$HOME/.volc/config`and `$HOME/.volc/credentials`.


```Plain
# view config file
ls $HOME/.volc/
config      credentials
```



* 


<span id="如何使用-volc-提交自定义任务"></span>
## How to submit custom tasks with Volc


* Initiate custom training through a configuration file.


```Plain
volc ml_task submit -c config.yaml
```



* 


<span id="config配置"></span>
## Config configuration

```yaml
# Task name
TaskName: my-dev-task

# Task description [Optional]
Description: ""

# Tags [Optional]
Tags: 
  - tag-a
  - tag-b

# Entry command
Entrypoint: python3 /path/to/demo_project/torch_tensorboard.py

# Local code path
# If it is a directory ending with '/', all contents under the directory will be uploaded to RemoteMountCodePath
# If it is a directory not ending with '/', the directory itself and all contents under it will be uploaded to RemoteMountCodePath
UserCodePath: ./demo_project/

# Code mount path in container
RemoteMountCodePath: "/path/to/demo_project/"

# Image URL used for training
ImageUrl: "cr-cn-beijing.volces.com/ml_platform/pytorch:1.7"

# Image credential [Optional]
# When ImageUrl is a private repository other than BytePlus, the repository username and token must be provided to pull the image
ImageCredential:    
  RegistryUsername: "replace with your RegistryUsername"
  RegistryToken: "replace with your RegistryToken"

# Instance configuration
# Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom
Framework: "Custom"

# Instance configuration
TaskRoleSpecs:  
  - RoleName: "worker"               # Role name  
    RoleReplicas: 2                  # Number of roles  
    Flavor: "ml.c1ie.xlarge"         # Instance type

# Resource queue name [Optional]
# Use public queue if not specified
ResourceQueueName: "replace with your ResourceQueueName"

# Environment variables [Optional]
# If you want to view logs other than stdout, please write the log into a file ending with .log and place it in the path specified by environment variable MLP_LOG_PATH
Envs:  
  - Name: "ENV_A"
    Value: "value"
  - Name: "ENV_B"
    Value: "value"

# Maximum running time; tasks exceeding this time will be automatically canceled. Set to 0 to disable this feature [Optional]
ActiveDeadlineSeconds: 432000

# Instance retention time after completion or failure; must not exceed the maximum task running time [Optional]
DelayExitTimeSeconds: 120

# Enable TensorBoard [Optional]
# Please write TensorBoard logs to this path: os.getenv("TENSORBOARD_LOG_PATH", "/tensorboard_logs/")
EnableTensorBoard: true

# Memory ratio required by the cache service of the TOS data disk (0~1) [Optional]
SidecarMemoryRatio: "replace with your ratio"   

# Shared file system mounts [Optional]
# The shared file system provides persistent storage; its data will not be lost when workloads stop or encounter errors. Up to 10 data disks can be mounted.
Storages:  
  - Type: "Tos"                               # Mount TOS data disk  
    MountPath: "replace with your path"       # Mount directory in container  
    Bucket: "replace with your bucket"        # TOS bucket to be mounted  
    Prefix: "replace with your prefix"        # Directory path under the TOS bucket [Optional]  

  - Type: "Vepfs"                             # Mount File Storage PFS data disk  
    MountPath: "replace with your path"       # Mount directory in container  

  - Type: "Nas"                               # Mount NAS data disk  
    MountPath: "replace with your path"       # Mount directory in container  
    NasAddr: "replace with your NAS address"  # Mount point address of NAS instance
```


<span id="rclone"></span>
# Rclone

Rclone is a powerful command\-line tool that supports interfacing with multiple cloud storage systems and can be used to perform operations such as data upload, download, synchronization, and management. WebIDE has built\-in Rclone tools that can be used with only manual configuration.

<span id="初始化配置"></span>
## Initialization configuration


1. Edit `the~/.config/rclone/rclone.conf`file.

2. In access_key_id and secret_access_key, respectively, enter the corresponding AK and SK of the account.


&nbsp;

<span id="操作指南"></span>
## Operation guide

The following will introduce common operation commands of TOS, such as viewing directories, uploading files, and viewing directory sizes. For more information, see the [Rclone command](https://rclone.org/commands/).

<span id="查看桶或目录"></span>
### View bucket or directory


1. View all bucket lists under the current account.


```Plain
rclone lsd volces-tos: //volces-tos is the name of the configured remote connection.
```



2. View a list of first\-level folders in a bucket.


```Plain
rclone lsd volces-tos:bucket-demo //bucket-demo is the name of the bucket
```


<span id="上传本地文件"></span>
### Upload local file


1. The source data can be copied to the destination by using the rclone copy command.


```Plain
rclone copy source:sourcepath dest:destpath
```



2. Copy all the files in the local folder `testdir`to the `bucket-demo`bucket and place them in the bucket root directory to execute the following command.


```Plain
rclone copy testdir volces-tos:bucket-demo
```



3. Copy the local folder `testdir`to the `bucket-demo`bucket and let `testdir`be the first\-level directory in the bucket.


```Plain
rclone copy testdir volces-tos:bucket-demo/testdir
```


<span id="同步本地目录"></span>
### Sync local directory


1. Use the `rclone sync`command when you need to synchronize incremental data to the target (including new and modified files)


```Plain
rclone sync source:path dest:path [flags]
```



2. If you need to make the data in the testdir folder in the bucket exactly the same as the local folder testdir, execute the following command


```Plain
rclone sync testdir volces-tos:bucket-demo/testdir
```


<span id="查看目录大小"></span>
### View directory size


1. If you need to count the number and total capacity of files in a bucket or directory, execute the `rclone size`command.


```Plain
rclone size remote:path [flags]
```



2. For example, if you need to count the total number and size of files in the `bucket-demo`bucket, execute the following command.


```Plain
rclone size volces-tos:bucket-demo
```



3. For example, if you need to count the total number and size of the testdir folder in the bucket\-demo`testdir folder in the bucket-demo`bucket, execute the following command.


```Plain
rclone size volces-tos:bucket-demo/testdir
```


<span id="文件对比校验"></span>
### File comparison verification


1. If you need to compare data between source and destination, execute the `rclone check`command.


```Plain
rclone check source:path dest:path [flags]
```


Optional parameters are as follows:


* `--Size-only`: Compare only file sizes.

* `--Download`: Download remote files and compare them.
