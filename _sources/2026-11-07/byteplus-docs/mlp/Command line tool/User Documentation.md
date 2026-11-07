---
title: "User Documentation"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/72394"
---

The Machine Learning Platform provides a command\-line tool for users to manage training tasks on the platform from any machine with network connectivity.

<span id="63166154"></span>
# Installation

```Plain
sh -c "$(curl -fsSL https://ml-platform-public-examples-cn-beijing.tos-cn-beijing.volces.com/cli-binary/install.sh)"  && export PATH=$HOME/.volc/bin:$PATH
```


After installation, ensure that the `$HOME/.volc/bin` directory is in your `$PATH`.

<span id="ec367e44"></span>
# Commands

<span id="988e2a45"></span>
## configure

Before using the command\-line tool, you must configure user identity credentials including AK, SK, and Region.

Users can use `volc configure` to interactively configure relevant parameters.


* The region list is as follows:

   * North China 2 (Beijing): cn\-beijing.

   * East China 2 (Shanghai): cn\-shanghai.

   * South China 1 (Guangzhou): cn\-guangzhou.

   * North China 3（Beijing 2）：cn\-beijing2。

   * Southeastern Asia (Johor)：ap\-southeast\-1。


```Plain
volc configure
volc access key [********4M2Q]: █
volc secret access key [********TQ==]:█
volc region [cn-beijing]:█
```


After setup is complete, check whether the two files `$HOME/.volc/config` and `$HOME/.volc/credentials` exist.

```Plain
# View the config file
ls $HOME/.volc/
config credentials
```


<span id="5ceb2a36"></span>
## version

View the version of the current command\-line tool.

<span id="79ef95ad"></span>
## upgrade

Update the command\-line tool.

<span id="dade119e"></span>
## help

View the help information of the command\-line tool, which includes the usage of each command.

<span id="06c55334"></span>
## ml_task

A collection of commands for the [Custom Training] module of the machine learning platform.

<span id="1b794c65"></span>
### submit

Initiate a custom training task via local code.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Configuration file for the training task. |Supported |
|\-\-task_name |\-n |Name of the training task. |Not supported |
|\-\-description |\-d |Description of the training task. |Not supported |
|\-\-user_code_path |\-\-cp |User's code path; configuring this parameter will override the value in conf. If it is a directory and ends with '/', upload all contents in the directory to the remote directory; if it is a directory and does not end with '/', upload the directory and all its contents to the remote directory |Not supported |
|\-\-entrypoint |\-e |Specify the entry command for the training task; if it contains spaces, use quotation marks. After configuring this parameter, the Entrypoint configuration value in the conf file will be overwritten. |Not supported |
|\-\-args |\-a |Specify the command arguments (args) for the training task; if they contain spaces, use quotation marks. Supports using multiple at once; multiple values will be combined into one, separated by spaces. After configuring this parameter, the Args configuration value in the conf file will be overwritten. |Not supported |
|\-\-image |\-i |Image URL. After configuring this parameter, it will override the value in conf. In the corresponding details page of the Image Center, find the specified image version to get the image URL. |Not supported |
|\-\-resource_group_id |\-g |Resource Group ID. After configuring this parameter, it will override ResourceGroupID in conf. On the list page of the Resource Group module in the console, hover the mouse over the name of the specified resource group to view the Resource Group ID. This configuration value will be deprecated subsequently. |Not supported |
|\-\-resource_queue_id |\-q |Resource Queue ID. After configuring this parameter, it will override the ResourceQueueID in conf. On the Queue Module List page of the console, hover the mouse over the name of the specified queue to view the Queue ID. |Not supported |
|\-\-resource_queue_name |\-queue_name |Resource Queue Name. After configuring this parameter, it will override the command line parameter `--resource_queue_id`. On the Queue Module List page of the console, you can view the name of the specified queue. |Not supported |
|\-\-framework |\-f |Training framework. Supported options include `TensorFlowPS`, `PyTorchDDP`, `MXNet`, `BytePS`, `MPI`, `Custom`. Configuring this parameter will override the value in conf. |Not supported |
|\-\-local_diff | |Whether to only upload incremental code files to speed up the task submission process. Supported options include `on`, `off`. If this parameter is not configured, the default is `on`. |Not supported |
|\-\-copy\-links |\-L |When uploading code encounters a soft link, the actual file content will be uploaded instead of the soft link. If the soft link points to a directory, the entire pointed directory will be uploaded. This option is disabled by default. If required or if there are soft links pointing to absolute paths in the uploaded code, this option can be used. |Not supported |
|\-\-links | |When uploading code encounters a soft link, the soft link will be uploaded directly. It is necessary to ensure that the same link relationship exists in the container; otherwise, an error will be reported. This option is disabled by default. If required, this option can be used. |Not supported |
|\-\-access_type | |Specify the visibility scope of the training task. Supported options include `Public`, `Queue`, and `Private`, which respectively indicate visible within the main account, visible to members within the queue, and visible only to the creator. Only the `Queue` option can be used with the `--access_users` parameter or `AccessUsers` field to set visibility for members within the queue and specified sub\-accounts. |Not supported |
|\-\-access_users | |Specify the visible users of the training task. If the user does not set the visibility scope or visible users, the default visibility scope is visible to members within the queue. |Not supported |
|\-\-preemptible | |Specify that this task is preemptible. Preemptible tasks can use idle resources lent by each queue, reducing queuing time to some extent. When non\-preemptible tasks in each queue start queuing, preemptible tasks may be stopped by the system, copied, and re\-queued. (default value: false) |Not supported |
|\-\-priority | |Specify the priority of the training task. The full priority range is 1~9 (the higher the value, the higher the priority). When submitting a task, only some levels are available for selection; the remaining levels are for queue administrators. After submission, the platform will try to schedule tasks in the order of priority from high to low and creation time from earliest to latest. The final scheduling order is determined based on actual resource conditions (ensuring that with sufficient resources and the same priority, tasks submitted first are scheduled first). Queue administrators are allowed to adjust the priority while the task is queuing. If not specified, the default priority configured in the queue is used. |Not supported |
|\-\-output | |Supports displaying command output in a specific format; currently only supports Json. |Not supported |
|\-\-set | |Used to override the value of a parameter in the configuration file, but its priority is lower than other flags mentioned above. Supports specifying values for multiple parameters simultaneously in the form of `--set Entrypoint=\"sleep 5s\" --set Priority=4`. |Not supported |



* conf file example (can be obtained via get for existing online task config)

   * **SidecarMemoryRatio**: The proportion of memory that the file caching service can use when mounting a TOS data disk.

      * **The larger the data size and read\-write concurrency of the mounted TOS bucket, the larger this ratio needs to be configured**.

      * When this parameter is not filled in the conf file, the system will automatically allocate memory based on the currently selected instance specification and the number of mounted TOS. The allocated memory size (GiB) = `(0.15 * number of CPU cores + 3) * number of TOS data disks`.

      * **If this parameter is filled in, it is recommended that SidecarMemoryRatio \* instance specification memory is not less than** **`4GiB`** **; otherwise, it may easily cause TOS data disk mount failure or user container exceptions**.

   * NasAddr: When mounting a NAS data disk, you need to fill in the mount point address of the NAS file system, which can be viewed in the [File Storage NAS console](https://console.byteplus.com/filenas).

   * ImageUrl: Image address, which can be obtained by selecting the image to use in the 【Image Center】 of the machine learning platform, entering the details page, and copying it from the 【Version List】.

   * ResourceQueueID: Submit tasks to the specified queue.Flavor: Instance specification required for submitting tasks. For details, see [Instance Specifications and Pricing](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing).


```Plain
# Task name
TaskName: "tf_random_mono_repo_ecs"
# Task description
Description: ""
# Entry point command
Entrypoint: echo 'hello' & echo "world" && sleep 1d
# Entry point command parameters, which are concatenated by the platform after the entry point command
Args: ""
# Tags
Tags: [tag1,tag2]
# Local code path. If it is a directory and ends with '/', all contents in the directory are uploaded to RemoteMountCodePath. If it is a directory and does not end with '/', the directory and all contents in the directory are uploaded to RemoteMountCodePath.
UserCodePath: ./project_xxx/src
# Code mount path in the container
RemoteMountCodePath: "/xxx_path/project_xxx/src/"
# Environment variables
Envs:
- Name: "env1"
Value: "value1"
- Name: "env2"
Value: "value2"
IsPrivate: false # Whether to set an environment variable to be visible only to the creator in the details page
# Image URL address
ImageUrl: "replace with your ImageUrl"
# When ImageUrl is a private repository image, you need to fill in the repository username and key to pull the image
ImageCredential:
RegistryUsername: "replace with your RegistryUsername"
RegistryToken: "replace with your RegistryToken"
# The ID of the resource group to which it belongs. If it is empty, the public resource group is used by default. If it is not empty, it is changed to the ID of the user's private resource group. The latest version of volc will gradually abandon support for this field
# ResourceGroupID: "replace with your ResourceGroupID"
# Queue ID, use the public queue when it is empty
ResourceQueueID: "replace with your ResourceQueueId"
# Queue name, priority is higher than ResourceQueueID
ResourceQueueName: "replace with your ResourceQueueName"
# Training framework, supports TensorFlowPS / PyTorchDDP / MPI / BytePS / Custom
Framework: "Custom"
# Instance configuration, including role name (RoleName), number of roles (RoleReplicas) and specific instance specifications (Flavor)
TaskRoleSpecs:
- RoleName: "worker"
RoleReplicas: 1
Flavor: "ml.c1e.xlarge"
GpuRate: 0.1 # Optional. When you need to split the GPU, please fill in the split ratio. The value range is (0, 1). Different models of GPUs have different split points. For example, ml.g1v.2xlarge (Tesla-V100) can be split into 8 parts. When GpuRate is filled in 0.1, it will be rounded up to 1/8 card.
# Maximum running time
ActiveDeadlineSeconds: 432000
# Instance retention time
DelayExitTimeSeconds: 0
# Visible range, supports Public / Queue / Private
AccessType: "Public"
# Visible users
AccessUsers:
- "xxx"
Preemptible: false # Optional, configure whether the task is preemptible, non-preemptible by default
Priority: 4 # Optional, configure the task priority (the larger the number, the higher the priority), only supports configuration of some gears (default is 2, 4, 6). If not configured, the default priority of the custom task in the queue shall prevail
# Automatic retry
RetryOptions:
EnableRetry: false # Whether to enable automatic retry, closed by default
MaxRetryTimes: 5 # Maximum number of retries
IntervalSeconds: 120 # Retry interval = time when the new task is submitted - time when the last task is terminated
PolicySets: # Trigger conditions for automatic retry, support Failed (task failure), InstanceReclaimed (idle resource recovery)
- "Failed"
# Task diagnosis strategy
DiagOptions:
- Name: "EnvironmentalDiagnosis"
Enable: false
- Name: "PythonDetection"
Enable: true
PythonDetectionInterval: 3600
- Name: "LogDetection"
Enable: true
LogDetectionInterval: 1800
# Task vpc settings
PrivateNetwork:
VpcId: "xxx"
SubnetId: ""
SecurityGroupIds:
- ""
# Custom indicator collection port
CustomServices:
- ListenPort: xxx
Type: "Metrics"
Path: "/metrics"
# Whether to enable TensorBoard
EnableTensorBoard: true
# Fill in after enabling TensorBoard, write logs to NAS or vePFS, need to be enabled
TensorBoardStorage:
Type: "Nas/Vepfs" # Required, TensorBoard Log writing storage instance type, can be Nas or Vepfs
NasId: "replace with your NAS Id" #NAS instance Id, fill in when Type is Nas, and select at least one of NasAddr
NasAddr: "replace with your NAS Addr" #NAS instance mount point address, fill in when Type is Nas, and select at least one of NasId
SubPath: "replace with NAS sub path" #Required, the storage instance subdirectory where TensorBoard logs are written, when Type is vePFS, you need to have the mount permission of the subdirectory
#Mount the data disk to the training container
SidecarMemoryRatio: "replace with your ratio" #The memory ratio required for the cache service of the TOS data disk
Storages:
- Type: "Tos" #Mount the cfs data disk
MountPath: "replace with your path" #The mount directory in the container
Bucket: "replace with your bucket" # TOS Bucket to be mounted
Prefix: "replace with your prefix" # Directory path under TOS Bucket to be mounted
FsName: "replace with your FsName" # Change to the name of the CLoudFS instance to be mounted
MetaCacheCapacity: "replace with cache number" # The number of cached TOS file metadata. The larger the cache, the better the performance, but there is additional memory consumption
MetaCacheExpiryMinutes: "replace with cache expired time" # Cache metadata expiration time (min). It will be re-cached after expiration. If you don't want to refresh, you can set it to -1
- Type: "Sfcs" # Mount TOS data disk
MountPath: "replace with your path" # Mount directory in the container
Bucket: "replace with your bucket" # TOS Bucket to be mounted
Prefix: "replace with your prefix" # Directory path under TOS Bucket to be mounted
- Type: "Vepfs" # Mount vePFS data disk
MountPath: "replace with your path" # Mount directory in the container
SubPath: "replace with vePFS sub path" # vePFS subdirectory with mount permission, can be ignored when mounting vePFS root directory
ReadOnly: true # Mount vePFS subdirectory with mount permission in read-only mode, can be ignored when mounting in read-write mode
- Type: "Nas" # Mount NAS data disk
MountPath: "replace with your path" # Mount directory in the container
NasId: "replace with your Nas Id" # NAS instance Id, at least one of NasAddr
NasAddr: "replace with your NAS address" # NAS instance mount point address, at least one of NasId
```



* `--entrypoint` Usage:


```Plain
--entrypoint=./start.sh
--entrypoint="python main.py"
--entrypoint='python main.py'
```



* `--args` Usage: (The following four forms have the same effect)


```Plain
--args=--aaa=1 --args=--bbb=2 --args=--ccc=3
--args="--aaa=1 --bbb=2 --ccc=3"
--args='--aaa=1 --bbb=2 --ccc=3'
--args='--aaa=1 --bbb=2' --args=--ccc=3
```



* `--copy-links` Detailed usage:

   * \-\-copy\-links is generally used in file upload scenarios, such as code uploads and model uploads, and is disabled by default.

   * When this parameter is turned on, the actual file corresponding to the soft link will be uploaded instead of the soft link file.

   * It is recommended to turn it on in the following two situations:

      1. The soft link uses an absolute path.

      2. The file pointed to by the soft link is outside the directory to be uploaded.

* `--links` detailed usage:

   * \-\-links is generally used in file upload scenarios, such as code uploads, and is disabled by default.

   * When this parameter is turned on, the soft link will be uploaded directly.

   * It is recommended to turn it on in the following situation: There are files in the directory to be uploaded that point to outside code_path, and the linked files exist in the container (for example, links pointing to files in the TOS mount path).


<span id="a36c87da"></span>
### upload

Training code can be uploaded when creating a task. It also supports uploading training code in advance via the `upload` command. When specifying this code during task creation, it will not be uploaded repeatedly, thus accelerating the task creation speed.


|Parameter |Description |Required |
|---|---|---|
|\-\-local_code_path |User's code path. |Supported |
|\-\-tos_end_point |TOS access domain name. Currently, the list of domain names supported by TOS is available in [TOS-Region and Access Domain Name](https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint). |Not supported |
|\-\-region |Region. Supports `cn-beijing`, `cn-shanghai`, `cn-guangzhou`. |Supported |
|\-\-timeout |Upload timeout period (unit: seconds). |Not supported |
|\-\-local_diff |Whether to only upload incremental code files to speed up the task submission process. Supported options include `on`, `off`. If this parameter is not configured, the default is `on`. |Not supported |
|\-\-copy\-links |When uploading code encounters a soft link, upload the actual file content instead of the soft link. If the symbolic link points to a directory, the entire pointed directory will be uploaded. This option is not enabled by default. You can use it if needed or if there are symbolic links pointing to absolute paths in the uploaded code. |Not supported |
|\-\-links |When uploading code encounters a symbolic link, the symbolic link will be uploaded directly. Need to ensure the same link relationship exists in the container; otherwise, an error will occur. This option is not enabled by default. You can use it if needed. |Not supported |


<span id="1f05f487"></span>
### list

Get the list of training tasks, which by default lists tasks that are `queuing`, `deploying`, `running`, and `stopping`. While obtaining the task list, specific shortcut key instructions will be displayed, and shortcut keys can be used to perform corresponding actions.


* Shortcut keys:

   * [Enter]: View details.

   * [j / k]: Select up/down.

   * [q]: Exit to the previous level.

   * [e]: Export current task configuration.

   * [r]: Refresh task/task instance.

   * 【d】: download task code.

* Task status:

   * Initialized: being created.

   * Queue: being queued.

   * Staging: being deployed.

   * Running: running.

   * Killing: being stopped.

   * Success: completed.

   * Failed: failed.

   * Killed: stopped.

   * Exception: Exception.



|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-status |\-s |Filter specific task lists by status; multiple statuses are separated by `,` |Not supported |
|\-\-name |\-n |Filter specific task lists by task name ID |Not supported |
|\-\-profile |\-p |User credential configuration. View the currently configured credential list via `cat $HOME/.volc/credentials` |Not supported |
|\-\-output | |Specify the output data display format. Currently only supports `json` After using this parameter, the output no longer provides an interactive method |Not supported |
|\-\-format | |Specify the list of fields to output The format is `--format=FieldName[=outputFieldName]`. You can use `--format=FieldName=outputFieldName` to specify the output field name, or use `--format=FieldName` to use the default `FieldName` as the output field. |Not supported |
|\-\-helpformat | |List the supported fields. |Not supported |


<span id="f3545ada"></span>
### get

View training task details.


|Parameter |Description |Required |
|---|---|---|
|\-\-id |ID of the training task. It can be viewed via the `volc ml_task list` command, such as `t-20211216120106-vx7d4`. |Supported |
|\-\-profile |User credential configuration. View the list of currently configured credentials via `cat $HOME/.volc/credentials` |Not supported |
|\-\-output |Specify the output data display format. Currently only supports `json` After using this parameter, the output no longer provides an interactive method |Not supported |
|\-\-format |Specify the list of fields to output The format is `--format=FieldName[=outputFieldName]`. You can use `--format=FieldName=outputFieldName` to specify the output field name, or use `--format=FieldName` to take the default `FieldName` as the output field. |Not supported |
|\-\-helpformat |List the supported fields. |Not supported |


<span id="60541c36"></span>
### cancel

Cancel submitted training tasks.


|Parameter |Description |Required |
|---|---|---|
|\-\-id |The ID of the training task. It can be viewed via the `volc ml_task list` command, for example `t-20211216120106-vx7d4`. |Supported |


<span id="6adee06b"></span>
### logs

Get logs of training task instances.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-task |\-t |Training task ID, which can be viewed via the `volc ml_task list` command, e.g., `t-20211216120106-vx7d4`. |Supported |
|\-\-instance |\-i |The ID of an instance under a training task, which can be viewed via the `volc ml_task list` command, such as `worker_0`. |Supported |
|\-\-content |\-c |Search keyword, supports Lucene syntax. For example, `--content error` will return log entries containing the `error` field. |Not supported |
|\-\-reverse |\-r |Whether to view logs in reverse order. Not turned on by default. |Not supported |
|\-\-lines |\-l |Number of log lines obtained, default is `500`. |Not supported |
|\-f | |Continuously scroll and update logs. |Not supported |
|\-\-profile |\-p |User credential configuration, view the currently configured credential list via `cat $HOME/.volc/credentials` |Not supported |



&nbsp;

* 


<span id="9ad1cf9f"></span>
### export

Export the configuration file and code of the specified task; if only the task ID is filled in, export the task configuration by default.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-task |\-t |ID of the training task, which can be viewed via the `volc ml_task list` command, such as `t-20211216120106-vx7d4`. |Supported |
|\-\-config | |Export the task configuration to the current path. |Not supported |
|\-\-code | |Download the task code to the current path. |Not supported |


<span id="48b5d1db"></span>
### instance

Commands related to training task instances.

<span id="447f2a44"></span>
#### list


* Shortcut key:

   * 【Enter】: View details.

   * 【j / k】: Select up/down.

   * 【q】: Exit to the previous level.

   * 【r】: Refresh task instance.



|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |\-i |The ID of the training task, which can be viewed via the `volc ml_task list` command, such as `t-20211216120106-vx7d4`. |Supported |
|\-\-profile |\-p |User credential configuration. View the currently configured credential list via `cat $HOME/.volc/credentials`. |Not supported |
|\-\-output | |Specify the output data display format. Currently only `json` is supported. After using this parameter, the output no longer provides an interactive method. |Not supported |
|\-\-format | |Specify the list of fields to output. The format is `--format=FieldName[=outputFieldName]`. You can specify the output field name using `--format=FieldName=outputFieldName`, or use the default `FieldName` as the output field via `--format=FieldName`. |Not supported |
|\-\-helpformat | |List the supported fields. |Not supported |


<span id="8c423da6"></span>
## ml_model

Collection of commands for the machine learning platform's 【Model Repository】 module.

<span id="449d23f7"></span>
### register / create

Create a new model or register a new model version.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Model ID. When not empty, register a new model version under the corresponding Model ID. Can be viewed via the `volc ml_model list` command, such as `m-20220519204748-qnfvj`. |Not supported |
|\-\-name |\-n |Model name. When the \-\-id parameter is specified, this parameter is ignored. |Not supported |
|\-\-description |\-d |Model description. |Not supported |
|\-\-version\-description |\-\-vd |Description of the model version. |Not supported |
|\-\-format |\-\-fm |Model format. Optional values: `SavedModel`, `GraphDef`, `TorchScript`, `TensorRT`, `ONNX`, `CaffeModel`, `NetDef`, `MXNetParams`, `Scikit_Learn`, `XGBoost`, `LightGBM`, `MATX`, `Custom`. |Supported |
|\-\-framework |\-\-fw |Model framework, format::. Example: `TensorFlow:2.0`. Optional values for framework name: `TensorFlow`, `PyTorch`, `TensorRT`, `ONNX`, `Caffe`, `Caffe2`, `MXNet`, `Scikit_Learn`, `XGBoost`, `LightGBM`, `MATX`, `Custom`. |Supported |
|\-\-path |None |Model storage path, which can be a local directory or a path on TOS. For TOS paths, the format is: `tos://bucket/prefix/`. |Supported |
|\-\-source |\-s |Model source. Optional values: `Local`,`TOS`, `AutoML`, `Perf`. |Supported |
|\-\-category |\-c |Model category, optional values: `TextClassification`, `TabularClassification`, `TabularRegression`, `ImageClassification`. |Not supported |
|\-\-dataset |\-\-ds |Dataset ID used for training the model. On the dataset module list page of the console, hover the mouse over the name of the specified dataset to view the dataset ID. |Not supported |
|\-\-base\-version\-id |\-\-bv |The original model ID that the converted model is based on. When \-\-source is not `Perf`, this parameter will be ignored. |Not supported |
|\-\-source\-id |\-\-sid |The model's source ID. For example, the ID of the training task that generates the model, or the ID of the model conversion task. |Not supported |
|\-\-tags |\-t |Model tag list. Separated by commas, each tag format: <标签名\>:<标签值\>. |Not supported |
|\-\-profile |\-p |User credential configuration: view the list of currently configured credentials via `cat $HOME/.volc/credentials`. |Not supported |
|\-\-copy\-links |\-L |When uploading code with a soft link, upload the actual file content instead of the soft link. If the soft link points to a directory, the entire target directory will be uploaded. This option is not enabled by default. It can be used if needed or if there are soft links pointing to absolute paths in the uploaded code. |Not supported |


Tensor configuration file, example:

```Plain
Inputs:
  - TensorName: "Conv1_input"
    DType: "INT32"
    Shape:
    - -1
    - 28
    - 28
Outputs:
  - TensorName: "Softmax"
    DType: "INT32"
    Shape:
    - -1
    - 10
```


Use CLI to create a new model from a local model package, example:

```Plain
volc ml_model create --name="demo-model" --description="demo model" --version-description="local upload" --format="SavedModel" --framework="TensorFlow:2.0" --path="./tmp" --source="Local" --tensor-config=""./docs/examples/model_tensor_config_example.yaml""
```


Use CLI to register the model package stored in TOS as a new model version, example:

```Plain
volc ml_model register --id=m-20220124172610-48psg --version-description="tos register" --format="SavedModel" --framework="TensorFlow:2.0" --path="tos://model-beijing/tf-model/1/" --source="TOS" --tensor-config="./docs/examples/model_tensor_config_example.yaml" --tags="hd:T4,precision:float"
```


<span id="d8e25b40"></span>
### list

Display a list of models or model versions.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Filter models by model ID. |Not supported |
|\-\-name |None |Filter models by model name. |Not supported |
|\-\-offset |\-o |The starting offset position of the model list. Default is 0. |Not supported |
|\-\-limit |\-l |Number of models per page in the model list. Default is 10. |Not supported |
|\-\-sort\-by |None |Which field to sort by. Optional values: `ModelName`, `CreateTime`. Default is `CreateTime`. |Not supported |
|\-\-sort\-order |None |Sort order. Optional values: `Ascend`, `Descend`. Default is `Descend`. |Not supported |
|\-\-profile |\-p |User credential configuration: view the list of currently configured credentials via `cat $HOME/.volc/credentials` |Not supported |


Use CLI to get a list of models, example:

```Plain
volc  ml_model list
```


<span id="4c7d5d76"></span>
### show / get

Get model or model version information.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Model ID. Can be viewed via the `volc ml_model list` command, such as `m-20220519204748-qnfvj`. |Supported |
|\-\-version |\-v |Model version number. |Not supported |
|\-\-profile |\-p |User credential configuration; view the list of currently configured credentials via `cat $HOME/.volc/credentials`. |Not supported |


Use CLI to get model details, example:

```Plain
volc ml_model show --id=m-20220119194754-rrdwf
```


Use CLI to get model version details, example:

```Plain
volc ml_model show --id=m-20220119194754-rrdwf --version="V1.0"
```


<span id="56ff7a95"></span>
### update

Update the model or model version.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Model ID. Can be viewed via the `volc ml_model list` command, such as `m-20220519204748-qnfvj`. |Supported |
|\-\-version |\-v |Model version number. |Not supported |
|\-\-name |\-n |Modified model name. If the \-\-version parameter is specified, this field is ignored. |Not supported |
|\-\-description |\-d |The description of the modified model or model version. If the \-\-version parameter is specified, this field represents the description of the model version; otherwise, it represents the description of the model. |Not supported |
|\-\-tensor\-config |\-\-tc |The modified model Tensor configuration file. YAML format. |Not supported |
|\-\-profile |\-p |User credential configuration, view the list of currently configured credentials via `cat $HOME/.volc/credentials`. |Not supported |


Use CLI to update model description, example:

```Plain
volc ml_model update --id="m-20211208174903-d2snv" --v="V1.0" --description="test cli update"
```


Use CLI to update model Tensor configuration, example:

```Plain
volc ml_model update --id=m-20220124172610-48psg --version="V1.0" --tensor-config="./docs/examples/model_tensor_config_example.yaml"
```


<span id="0f9cb82e"></span>
### download

Download the model.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Model ID. Can be viewed via the `volc ml_model list` command, such as `m-20220519204748-qnfvj`. |Supported |
|\-\-version |\-v |Model version number. |Supported |
|\-\-path |\-v |Path to save the downloaded model locally. Download to the current directory by default. |Not supported |
|\-\-profile |\-p |User credential configuration: view the list of currently configured credentials via `cat $HOME/.volc/credentials` |Not supported |


Use CLI to download the model, example:

```Plain
volc ml_model download --id=m-20220124172610-48psg --version="V2.0" --path="./tmp"
```


<span id="42d87deb"></span>
### delete

Delete the model or model version.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Model ID Can be viewed via the `volc ml_model list` command, such as `m-20220519204748-qnfvj` |Supported |
|\-\-version |\-v |Model version number |Not supported |
|\-\-profile |\-p |User credential configuration. View the list of currently configured credentials via `cat $HOME/.volc/credentials` |Not supported |


Use CLI to delete the model version, example:

```Plain
volc ml_model delete --id="m-20220124172610-48psg" --version="V3.0"
```


Use CLI to delete the model, example:

```Plain
volc ml_model delete --id="m-20220124172610-48psg"
```


&nbsp;

<span id="d419c65d"></span>
## ml_service Multi\-role Multi\-deployment

For the 【Inference Service】 module of the machine learning platform, a collection of commands for multi\-role multi\-deployment.

> Multi\-role multi\-deployment requires whitelist activation to use; contact your account manager to submit a configuration application.


<span id="f9278e16"></span>
### create

Create an inference service. Basically the same as the creation of a single deployment, only the parameters differ.

**Command example**

```Shell
mlp ml_service create -c demo-service.yaml
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Parameter configuration file; configuration file parameters have lower priority than command line parameters. |Supported |
|\-\-name |\-n |Inference service name. |Not supported |
|\-\-description |\-d |Inference service description. |Not supported |


**Configuration File Example** (demo\-service.yaml)

```Shell
# demo-service.yaml

ServiceName: "example-service"
Description: "This is an example service"
Envs:
  - Name: "ENV_VAR_1"
    Value: "value1"
  - Name: "ENV_VAR_2"
    Value: "value2"
Ports:
  - ListenPort: "8080"
    ExposePort: 8083
    Type: "HTTP"
    Path: "/metrics"
InstanceNetwork:
  VpcId: "vpc-mj8yet2n01z45smt1b9k2s2n"
  SubnetId: "subnet-rrq5bxpv2hogv0x57cwyj46"
  SecurityGroupIds:
    - "sg-mj8yeyzqc7wg5smt1aokt1np"
```


<span id="7ac57e61"></span>
### stop

Stop the inference service; actions are consistent with single deployment.

**Command Example**

```Shell
mlp ml_service stop --id={service_id}
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference Service ID. |Supported |


<span id="de265711"></span>
### update

Update the inference service; actions are consistent with single deployment.

**Command Example**

```Shell
mlp ml_service update --id={service_id} --description={description} --model={model_id} --model-version={model_version} --image={image} --flavor={flavor} --conf service.yaml
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Parameter configuration file. Configuration file parameters have lower priority than command line parameters. |Supported |


**Configuration File Example** (update_servicev2.yaml)

```Shell
ServiceId: "s-20241202111417-x4nqr"
Ports:
  - ListenPort: "8081"
    ExposePort: 8081
    Type: "HTTP"
InstanceNetwork:
  VpcId: "vpc-mjjnre6mf5s05smt1bfjeqfd"
Network:
  Type: "CLB"
  InstanceId: "clb-13flabqoc14hs3n6nu4lg1dip"
  EnableEip: false
```


<span id="3fc36c65"></span>
### start

Start the inference service.

**Command Example**

```Shell
mlp ml_service start --id={service_id}
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service ID. |Supported |


<span id="cf83f863"></span>
### delete

Delete the inference service.

**Command Example**

```Shell
mlp ml_service delete --id={service_id} 
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service ID. |Supported |


<span id="fa697fae"></span>
### get

Get details of the specified inference service.

**Command Example**

```Shell
mlp ml_service get --id={service_id}
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service ID. |Supported |


<span id="ecb36e58"></span>
### list

List all inference services.

**Command Example**

```Shell
mlp ml_service list
```


<span id="16456941"></span>
### export (export service)

On the `get` or `list` page, enter `e` to export the service configuration as a YAML file.

<span id="b88d35b2"></span>
### rollback

Roll back the inference service version; not available in multi\-deployment and multi\-role scenarios.

**Command Example**

```Shell
mlp ml_service rollback --id={service_id} --version={version}
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service ID. |Supported |
|\-\-version |None |Target version number. |Supported |


<span id="053da30b"></span>
### scale

<span id="9a1cca96"></span>
#### Multiple Deployment Scenarios

**Note**: in multiple deployment scenarios, you cannot directly expand via service ID; you must specify the deployment ID.

**Error Example**

```Shell
mlp ml_service scale --id={service_id} --replicas={replicas}
```


**Normal Example**

```Shell
mlp ml_service scale --id={service_id} --did={deployment_id} --replicas={replicas}
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference Service ID. |Supported |
|\-\-did |None |Inference Deployment ID. |Supported |
|\-\-replicas |\-r |Target replica count. |Supported |


<span id="15c2e406"></span>
#### Multiple Roles and Multiple Deployment Scenarios

**Command Example**

```Shell
mlp ml_service scale --id={service_id} --did={deployment_id} --rid={role_id} --replicas={deployment_replicas}
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference Service ID. |Supported |
|\-\-did |None |Inference Deployment ID. |Supported |
|\-\-rid |None |Role ID. |Supported |
|\-\-replicas |\-r |Target number of replicas. |Supported |


<span id="19f61853"></span>
### create deployment

<span id="28cc9bce"></span>
#### Multiple Deployment Scenarios

Create an inference deployment.

**Command Example**

```Shell
mlp ml_service create deployment -c demo-deployment.yaml
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Parameter configuration file (lower priority than command line parameters). |Supported |
|\-\-name |\-n |Inference deployment name. |Not supported |
|\-\-description |\-d |Inference deployment description. |Not supported |
|\-\-model |None |Model ID. |Not supported |
|\-\-model\-version |None |Model version. |Not supported |
|\-\-image |\-i |Image address. |Not supported |
|\-\-queue |\-q |Queue ID. |Not supported |
|\-\-flavor |\-f |Instance specification. |Not supported |
|\-\-replicas |\-r |Number of instances. |Not supported |


**Configuration File Example** (demo\-deployment.yaml)

```YAML
ServiceId: "s-20241107200608-rskct"
DeploymentName: "example-service"
Description: "This is an example service"
Envs:
  - Name: "ENV_VAR_1"
    Value: "value1"
  - Name: "ENV_VAR_2"
    Value: "value2"
ModelID: "m-20240108160951-krnxz"
ModelVersion: "v1.0"
ImageUrl: "vemlp-cn-beijing.cr.volces.com/preset-images/python:3.9"
ResourceQueueID: "q-20241102222303-cdsqj"
Replicas: 3
FlavorID: "ml.g1ve.2xlarge"
Command: "sleep inf"
ReadinessProbe:
  Type: "http"
  Path: "/health"
  Port: 8080
  TimeoutSeconds: 5
ReadinessProbeV2:
  TCPSocket:
    Port: 8080
  InitialDelaySeconds: 1
  TimeoutSeconds: 1
  PeriodSeconds: 10
  SuccessThreshold: 1
  FailureThreshold: 3
  Enabled: true
StartupProbe:
  Exec:
    Command: "sleep 1"
  InitialDelaySeconds: 1
  TimeoutSeconds: 1
  PeriodSeconds: 10
  SuccessThreshold: 1
  FailureThreshold: 3
  Enabled: true
LivenessProbe:
  HTTPGet:
    Path: "/"
    Port: 8080
    Scheme: "HTTP"
  InitialDelaySeconds: 1
  TimeoutSeconds: 1
  PeriodSeconds: 10
  SuccessThreshold: 1
  FailureThreshold: 3
  Enabled: true
Autoscaler:
  Enabled: false
RollingUpdate:
  MaxUnavailable: 20
  MaxSurge: 1
Ports:
  - ListenPort: "8080"
    ExposePort: 8080
    Type: "HTTP"
InstanceNetwork:
  SubnetId: "subnet-mj8yfuk853i85smt1b0x58mk"
  SecurityGroupIds:
    - "sg-mj8yeyzqc7wg5smt1aokt1np"
```


<span id="378bc108"></span>
#### Multiple Roles and Multiple Deployments Scenario

Create a multiple\-role inference deployment.

**Command Example**

```Shell
mlp ml_service create deployment -c demo-deployment.yaml
```


**Parameter Description** (same as multi\-deployment scenario)


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Parameter configuration file (with lower priority than command\-line parameters). |Supported |
|\-\-name |\-n |Inference deployment name. |Not supported |
|\-\-description |\-d |Inference deployment description. |Not supported |
|\-\-model |None |Model ID. |Not supported |
|\-\-model\-version |None |Model version. |Not supported |
|\-\-image |\-i |Image address. |Not supported |
|\-\-queue |\-q |Queue ID. |Not supported |
|\-\-flavor |\-f |Instance specification. |Not supported |
|\-\-replicas |\-r |Instance count. |Not supported |


**Configuration File Example** (multi\-role demo\-deployment.yaml)

```YAML
ServiceId: "s-20250221154219-xmtmw"
DeploymentName: "example-service"
Description: "This is an example service"
ResourceQueueID: "q-20250107103716-bzqc7"
Priority: 4
Network:
  SubnetId: "subnet-213es3xwbqi9svn3c9tgmazh"
  SecurityGroupIds:
    - "sg-213z10qdxbshsvn3cakseayl"
Listener:
  Scheduler: "wrr"
AcceptTraffic: true
Preemptible: false
MultiRoles:
  - Name: "prefill"
    ImageUrl: "vemlp-cn-beijing2.cr.volces.com/preset-private-images/xllm:r1"
    Command: "sleep inf"
    Envs:
      - Name: "SPLITWISE_PREFILL_LENGTH_THRESHOLD"
        Value: "256"
      - Name: "XLLM_MODEL_SLOT_BLOCK_SIZE"
        Value: "256"
      - Name: "XLLM_MODEL_NUM_BLOCKS"
        Value: "100"
      - Name: "XLLM_SCHEDULER_MAX_SCHEDULE_BATCH_SIZE"
        Value: "128"
      - Name: "MODEL_PATH"
        Value: "/testphi3/models/vemlp-deepseek-r1-enc/vemlp-deepseek-r1-enc"
      - Name: "XLLM_PARALLEL_PP_SIZE"
        Value: "1"
      - Name: "XLLM_PARALLEL_LOCAL_WORLD_SIZE"
        Value: "8"
      - Name: "XLLM_MODEL_MP_SIZE"
        Value: "8"
      - Name: "XLLM_PARALLEL_TP_SIZE"
        Value: "8"
    FlavorID: "ml.hpcpni3l.48xlarge"
    Replicas: 1
    ShardNum: 1
    RollingUpdate:
      MaxUnavailable: 20
      MaxSurge: 1
    InstanceNetwork:
      SubnetId: "subnet-213es3xwbqi9svn3c9tgmazh"
      SecurityGroupIds:
        - "sg-213z10qdxbshsvn3cakseayl"
    GracefulShutdownPeriod: 10
    Ports:
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/"
        Source: "Service"
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/metrics"
        Source: "Service"
    LivenessProbe:
      HTTPGet:
        Path: "/"
        Port: 8080
        Scheme: "HTTP"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Autoscaler:
      Enabled: false
    ReadinessProbeV2:
      TCPSocket:
        Port: 8080
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    StartupProbe:
      Exec:
        Command: "sleep 1"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Expose: false
  - Name: "decode"
    ImageUrl: "vemlp-cn-beijing2.cr.volces.com/preset-private-images/xllm:r1"
    Envs:
      - Name: "SPLITWISE_PREFILL_LENGTH_THRESHOLD"
        Value: "256"
      - Name: "XLLM_MODEL_SLOT_BLOCK_SIZE"
        Value: "256"
      - Name: "XLLM_MODEL_NUM_BLOCKS"
        Value: "100"
      - Name: "XLLM_SCHEDULER_MAX_SCHEDULE_BATCH_SIZE"
        Value: "128"
      - Name: "MODEL_PATH"
        Value: "/testphi3/models/vemlp-deepseek-r1-enc/vemlp-deepseek-r1-enc"
      - Name: "XLLM_PARALLEL_PP_SIZE"
        Value: "1"
      - Name: "XLLM_PARALLEL_LOCAL_WORLD_SIZE"
        Value: "8"
      - Name: "XLLM_MODEL_MP_SIZE"
        Value: "8"
      - Name: "XLLM_PARALLEL_TP_SIZE"
        Value: "8"
    FlavorID: "ml.hpcpni3l.48xlarge"
    Replicas: 1
    ShardNum: 1
    RollingUpdate:
      MaxUnavailable: 20
      MaxSurge: 1
    InstanceNetwork:
      SubnetId: "subnet-213es3xwbqi9svn3c9tgmazh"
      SecurityGroupIds:
        - "sg-213z10qdxbshsvn3cakseayl"
    GracefulShutdownPeriod: 10
    Ports:
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/"
        Source: "Service"
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/metrics"
        Source: "Service"
    LivenessProbe:
      HTTPGet:
        Path: "/"
        Port: 8080
        Scheme: "HTTP"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Autoscaler:
      Enabled: false
    ReadinessProbeV2:
      TCPSocket:
        Port: 8080
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    StartupProbe:
      Exec:
        Command: "sleep 1"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Expose: false
```


<span id="a037d138"></span>
### delete deployment

Delete the specified inference deployment.

**Command Example**

```Shell
mlp ml_service delete --id={service_id} --did={deployment_id}

# 示例
mlp ml_service delete --id="s-20241107200608-rskct" --did="s-20241107200608-rskct-h8hrh"
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference Service ID. |Supported |
|\-\-did |None |Inference Deployment ID. |Supported |


<span id="af425e86"></span>
### start deployment

Start the specified inference deployment.

**Command Example**

```Shell
mlp ml_service start --id={service_id} --did={deployment_id}

# 示例
mlp ml_service start --id="s-20241107200608-rskct" --did="s-20241107200608-rskct-h8hrh"
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service ID. |Supported |
|\-\-did |None |Inference deployment ID. |Supported |


<span id="0693640e"></span>
### stop deployment

Stop the specified inference deployment.

**Command Example**

```Shell
mlp ml_service stop --id={service_id} --did={deployment_id}

# 示例
mlp ml_service stop --id="s-20241107200608-rskct" --did="s-20241107200608-rskct-h8hrh"
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service ID. |Supported |
|\-\-did |None |Inference deployment ID. |Supported |


<span id="5ba47507"></span>
### get deployment

<span id="4f4a03de"></span>
#### get

Get details of the specified inference deployment.

**Command Example**

```Shell
mlp ml_service get --did={deployment_id}

# 示例
mlp ml_service get --id="s-20241107200608-rskct" --did="s-20241107200608-rskct-h8hrh"
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service ID. |Supported |
|\-\-did |None |Inference Deployment ID. |Supported |


<span id="3baf47ea"></span>
#### list

List the deployment versions under the specified service (Interaction process: `mlp ml_service list --id={id}` then enter `v`).

**Command Example**

```Shell
mlp ml_service list deployment version --did={deployment_id}
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference Service ID. |Supported |


<span id="4f668476"></span>
#### export

Export the deployment configuration as a YAML file.

<span id="1a1af825"></span>
### update deployment

<span id="b1e3ee32"></span>
#### Multiple Deployment Scenarios

Update the inference deployment configuration.

**Command Example**

```Shell
mlp ml_service update deployment --id={service_id} --description={description} --model={model_id} --model-version={model_version} --image={image} --flavor={flavor} --conf deployment.yaml
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Parameter configuration file (priority is lower than command line parameters). |Supported |
|\-\-model |None |Model ID. |Not supported |
|\-\-model\-version |None |Model version. |Not supported |
|\-\-image |\-i |Image address. |Not supported |
|\-\-queue |\-q |Queue ID. |Not supported |
|\-\-flavor |\-f |Instance specification. |Not supported |


**Configuration File Example** (updatedeployment.yaml)

```Shell
ServiceId: "s-20241107200608-rskct"
DeploymentId: "s-20241107200608-rskct-bxjzq"
Envs:
  - Name: "ENV_VAR_1"
    Value: "value3"
  - Name: "ENV_VAR_2"
    Value: "value2"
ModelID: "m-20240108160951-krnxz"
ModelVersion: "v1.0"
ImageUrl: "vemlp-cn-beijing.cr.volces.com/preset-images/python:3.9"
ResourceQueueID: "q-20241102222303-cdsqj"
Replicas: 3
FlavorID: "ml.g1ve.2xlarge"
Command: "sleep inf"
ReadinessProbe:
  Type: "http"
  Path: "/health"
  Port: 8080
  TimeoutSeconds: 5
Autoscaler:
  Enabled: false
RollingUpdate:
  MaxUnavailable: 20
  MaxSurge: 1
Ports:
  - ListenPort: "8080"
    ExposePort: 8080
    Type: "HTTP"
InstanceNetwork:
  SubnetId: "subnet-mj8yfuk853i85smt1b0x58mk"
  SecurityGroupIds:
    - "sg-mj8yeyzqc7wg5smt1aokt1np"
```


<span id="cce979e8"></span>
#### Multi\-role and Multi\-deployment Scenarios

Update the multi\-role inference deployment configuration.

**Command Example**

```Shell
mlp ml_service update --id="{service_id}" deployment --conf multi_role_deployment.yaml
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Parameter configuration file (with lower priority than command\-line parameters). |Supported |
|\-\-model |None |Model ID. |Not supported |
|\-\-model\-version |None |Model version. |Not supported |
|\-\-image |\-i |Image address. |Not supported |
|\-\-queue |\-q |Queue ID. |Not supported |
|\-\-flavor |\-f |Instance specification. |Not supported |
|\-\-replicas |\-r |Replica count. |Not supported |


**Configuration File Example** (multi_role_deployment.yaml)

```Shell
ServiceId: "s-20250221154219-xmtmw"
DeploymentId: "s-20250221154219-xmtmw-mr-xq7v7"
DeploymentName: "example-service"
Description: "This is an example service"
ResourceQueueID: "q-20250107103716-bzqc7"
Priority: 4
Network:
  SubnetId: "subnet-213es3xwbqi9svn3c9tgmazh"
  SecurityGroupIds:
    - "sg-213z10qdxbshsvn3cakseayl"
Listener:
  Scheduler: "wrr"
AcceptTraffic: true
Preemptible: false
MultiRoles:
  - Name: "prefill"
    Id: "s-20250221154219-xmtmw-mr-r4rhb-prefill"
    ImageUrl: "vemlp-cn-beijing2.cr.volces.com/preset-private-images/xllm:r1"
    Command: "sleep inf"
    Envs:
      - Name: "SPLITWISE_PREFILL_LENGTH_THRESHOLD"
        Value: "256"
      - Name: "XLLM_MODEL_SLOT_BLOCK_SIZE"
        Value: "256"
      - Name: "XLLM_MODEL_NUM_BLOCKS"
        Value: "100"
      - Name: "XLLM_SCHEDULER_MAX_SCHEDULE_BATCH_SIZE"
        Value: "128"
      - Name: "MODEL_PATH"
        Value: "/testphi3/models/vemlp-deepseek-r1-enc/vemlp-deepseek-r1-enc"
      - Name: "XLLM_PARALLEL_PP_SIZE"
        Value: "1"
      - Name: "XLLM_PARALLEL_LOCAL_WORLD_SIZE"
        Value: "8"
      - Name: "XLLM_MODEL_MP_SIZE"
        Value: "8"
      - Name: "XLLM_PARALLEL_TP_SIZE"
        Value: "8"
      - Name: "fromcli"
        Value: "fromcli"
    FlavorID: "ml.hpcpni3l.48xlarge"
    Replicas: 1
    ShardNum: 1
    RollingUpdate:
      MaxUnavailable: 20
      MaxSurge: 1
    InstanceNetwork:
      SubnetId: "subnet-213es3xwbqi9svn3c9tgmazh"
      SecurityGroupIds:
        - "sg-213z10qdxbshsvn3cakseayl"
    GracefulShutdownPeriod: 10
    Ports:
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/"
        Source: "Service"
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/metrics"
        Source: "Service"
    LivenessProbe:
      HTTPGet:
        Path: "/"
        Port: 8080
        Scheme: "HTTP"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Autoscaler:
      Enabled: false
    ReadinessProbeV2:
      TCPSocket:
        Port: 8080
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    StartupProbe:
      Exec:
        Command: "sleep 1"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Expose: false
  - Name: "decode"
    Id: "s-20250221154219-xmtmw-mr-r4rhb-decode"
    ImageUrl: "vemlp-cn-beijing2.cr.volces.com/preset-private-images/xllm:r1"
    Envs:
      - Name: "SPLITWISE_PREFILL_LENGTH_THRESHOLD"
        Value: "256"
      - Name: "XLLM_MODEL_SLOT_BLOCK_SIZE"
        Value: "256"
      - Name: "XLLM_MODEL_NUM_BLOCKS"
        Value: "100"
      - Name: "XLLM_SCHEDULER_MAX_SCHEDULE_BATCH_SIZE"
        Value: "128"
      - Name: "MODEL_PATH"
        Value: "/testphi3/models/vemlp-deepseek-r1-enc/vemlp-deepseek-r1-enc"
      - Name: "XLLM_PARALLEL_PP_SIZE"
        Value: "1"
      - Name: "XLLM_PARALLEL_LOCAL_WORLD_SIZE"
        Value: "8"
      - Name: "XLLM_MODEL_MP_SIZE"
        Value: "8"
      - Name: "XLLM_PARALLEL_TP_SIZE"
        Value: "8"
      - Name: "fromcli"
        Value: "fromcli"
    FlavorID: "ml.hpcpni3l.48xlarge"
    Replicas: 1
    ShardNum: 1
    RollingUpdate:
      MaxUnavailable: 20
      MaxSurge: 1
    InstanceNetwork:
      SubnetId: "subnet-213es3xwbqi9svn3c9tgmazh"
      SecurityGroupIds:
        - "sg-213z10qdxbshsvn3cakseayl"
    GracefulShutdownPeriod: 10
    Ports:
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/"
        Source: "Service"
      - ListenPort: "8080"
        ExposePort: 8080
        Type: "HTTP"
        Path: "/metrics"
        Source: "Service"
    LivenessProbe:
      HTTPGet:
        Path: "/"
        Port: 8080
        Scheme: "HTTP"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Autoscaler:
      Enabled: false
    ReadinessProbeV2:
      TCPSocket:
        Port: 8080
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    StartupProbe:
      Exec:
        Command: "sleep 1"
      InitialDelaySeconds: 1
      TimeoutSeconds: 1
      PeriodSeconds: 10
      SuccessThreshold: 1
      FailureThreshold: 3
      Enabled: true
    Expose: false
```


<span id="10ccbf32"></span>
### rollback deployment

Roll back the specified inference deployment version.

**Command Example**

```Shell
mlp ml_service rollback --id={service_id} --did={deployment_id} --version={version}

# 示例
mlp ml_service rollback --id="s-20241107200608-rskct" --did="s-20241107200608-rskct-h8hrh" --version="100010065"
```


**Description**


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference Service ID. |Supported |
|\-\-did |None |Inference Deployment ID. |Supported |
|\-\-version |None |Deployment Version ID. |Supported |


<span id="273446d5"></span>
## ml_service Single Deployment

For the collection of commands for single deployment of the [Inference Service] module in the machine learning platform.

<span id="8c1bb20a"></span>
### create

Create an inference service.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-conf |\-c |Parameter configuration file; the priority of configuration file parameters is lower than command line parameters. |Supported |
|\-\-name |\-n |Inference service name. |Not supported |
|\-\-description |\-d |Inference service description. |Not supported |
|\-\-model |None |Model ID. |Not supported |
|\-\-model\-version |None |Model version. |Not supported |
|\-\-image |\-i |Image address. |Not supported |
|\-\-queue |\-q |Queue Id. |Not supported |
|\-\-flavor |\-f |Instance specification. |Not supported |
|\-\-replicas |\-r |Instance count. |Not supported |


Configuration file example:

```Plain
# Inference service name
ServiceName: "test_service"
# Inference service description
Description: "this is a description for test_service"

# Image Url address
ImageUrl: "replace with your ImageUrl"
# When ImageUrl is a private repository image, you need to fill in the repository username and key to pull the image
ImageCredential:
RegistryUsername: "replace with your RegistryUsername"
RegistryToken: "replace with your RegistryToken"
# Model id
ModelID: "m-xxxxxxxx"
# Model version
ModelVersion: "V1.0"
# Service entry command, the preset inference image has a default entry command
Command: "replace with your command"
# Environment variables
Envs:
- Name: "env1"
Value: "value1"
- Name: "env2"
Value: "value2"
# Port configuration, up to 5, ListenPort and ExposePort value range 1-65535, type value range HTTP, RPC, Metrics, Others
# The preset inference image has a default port configuration
Ports:
- ListenPort: "2222" # Listening port, value range 1-65535
ExposePort: "2222" # Calling port, value range 1-65535
Type: "HTTP" # Port usage, value range HTTP, RPC, Metrics, Others
- ListenPort: "2223"
ExposePort: "2223"
Type: "RPC"
# Health check
ReadinessProbe:
Enabled: true # Whether to enable health check true | false
Command: "replace with your command" # Health check command
InitialDelaySeconds: 120 # Waiting time for the first check
PeriodSeconds: 30 # Check interval
FailureThreshold: 3 # Maximum number of failures

# Queue ID
ResourceQueueID: "replace with your ResourceQueueID"
# Compute specification
Flavor: "ml.c1ie.large"
# Number of instances
Replicas: 1
# Automatic expansion
Autoscaler:
Enable: true # Whether to enable automatic expansion and contraction true or false, Crons and MetricsAutoscaler must be selected
Crons: # Scheduled automatic expansion and contraction
- Schedule: "1 * * * *" # Cron statement, such as: 1 * * * *, represents 1 execution per minute
Target: 2 # Target number of instances
MetricsAutoscaler: # Metrics automatic expansion and contraction
Metrics:
- Name: cpu # Metric name, optional cpu, memory, gpu
TargetPercentage: 50 # Metric utilization
MinReplicas: 1 # Minimum number of instances
MaxReplicas: 2 # Maximum number of instances
# Mount configuration of shared file system. This part of the configuration is exactly the same as Storages in conf of ml_task submit command
Storages:
- Type: "Tos"
MountPath: "replace with your path"
Bucket: "replace with your bucket"
Prefix: "replace with your prefix"
MetaCacheCapacity: "replace with cache number"
MetaCacheExpiryMsec: "replace with cache expired time"
- Type: "Vepfs"
MountPath: "replace with your path"
SubPath: "replace with vePFS sub path"
- Type: "Nas"
MountPath: "replace with your path"
NasId: "replace with your Nas Id"
NasAddr: "replace with your NAS address"

# Before configuration, you need to configure the Ports field first, otherwise the configuration will be invalid
NetWork:
VpcId: vpc-xxxxxxxxxx # Private network ID (vpc-id)
SubnetId: subnet-xxxxxxxxxx # Subnet ID (subnet-id) under private network
EnableEip: true # Whether to enable public network access true or false
EipId: eip-xxxxxxxxxx # Public network IP id
```


<span id="6b6be71a"></span>
### update

Update the inference service. If the update items include health check, auto\-scaling, rolling update, and access configuration, a YAML configuration file must be submitted.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service id. |Supported |
|\-\-conf |\-c |Parameter configuration file; configuration file parameters have lower priority than command line parameters. |Not supported |
|\-\-description |\-d |Inference service change description. |Not supported |
|\-\-model |None |Model ID. |Not supported |
|\-\-model\-version |None |Model version. |Not supported |
|\-\-image |\-i |Image address. |Not supported |
|\-\-flavor |\-f |Instance specification. |Not supported |


Updated service configuration file example:


* The fields supported by the updated service configuration file are a subset of the fields for creating the service configuration file. The following are the specific fields supported for update.


```Plain
# Change description
Description: "describe what you changed"

# Image Url address
ImageUrl: "replace with your ImageUrl"
# When ImageUrl is a private repository image, you need to fill in the repository username and key to pull the image
ImageCredential:
RegistryUsername: "replace with your RegistryUsername"
RegistryToken: "replace with your RegistryToken"
# Model id
ModelID: "m-xxxxxxxx"
# Model version
ModelVersion: "V1.0"
# Entry command
Command: "replace with your command"

# Environment variables
Envs:
- Name: "env1"
Value: "value1"
- Name: "env2"
Value: "value2"
# Port configuration
Ports:
- ListenPort: "2222" # Listening port, value range 1-65535
ExposePort: "2222" # Call port, value range 1-65535
Type: "HTTP" # Port usage, value range HTTP, RPC, Metrics, Others
- ListenPort: "2223"
ExposePort: "2223"
Type: "RPC"
# Health check
ReadinessProbe:
Enabled: true # Whether to enable health check true | false
Command: "your health check command" # Health check command
InitialDelaySeconds: 120 # Waiting time for the first check
PeriodSeconds: 30 # Check interval
FailureThreshold: 3 # Maximum number of failures

# Computing specifications
Flavor: "ml.g1ie.large"
# Shared file system mount configuration
Storages:
- Type: "Tos"
MountPath: "replace with your path"
Bucket: "replace with your bucket"
Prefix: "replace with your prefix"
MetaCacheCapacity: "replace with cache number"
MetaCacheExpiryMsec: "replace with cache expired time"
- Type: "Vepfs"
MountPath: "replace with your path"
SubPath: "replace with vePFS sub path"
- Type: "Nas"
MountPath: "replace with your path"
NasId: "replace with your Nas Id"
NasAddr: "replace with your NAS address"

# Access configuration
NetWork:
VpcId: vpc-xxxxxxxxxx # Private network ID (vpc-id)
SubnetId: subnet-xxxxxxxxxx # Subnet ID under private network (subnet-id)
EnableEip: true # Whether to enable public network access true or false
EipId: eip-xxxxxxxxxx # Public network IP id
```


<span id="79fecbc3"></span>
### list

List all inference services.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-status |None |List services with status as status; optional values for status are Deploying, Running, Abnormal, Stopping, None. |Not supported |
|\-\-name |\-c |Filter services whose names contain 'name'. |Not supported |


<span id="47716c0c"></span>
### get

View inference service details.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service Id. |Supported |


<span id="28628a82"></span>
### delete

Delete inference service.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service Id. |Supported |
|\-\-delete\-eip |\-d |Whether to delete the public IP associated with the service. |Not supported |


<span id="e5eda61f"></span>
### start

Start inference service.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service Id. |Supported |


<span id="f1f5bb42"></span>
### stop

Stop inference service.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference Service Id. |Supported |


<span id="a044196c"></span>
### rollback

Roll back the inference service to the specified version.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service Id. |Supported |
|\-\-version |v |Service version number. First list services using the list command, select a service, and press the v key to query the corresponding change records, which include the version number for each change. |Supported |


<span id="2e4991bd"></span>
### scale

Inference service scaling.


|Parameter |Abbreviation |Description |Required |
|---|---|---|---|
|\-\-id |None |Inference service Id. |Supported |
|\-\-replicas |\-r |Number of inference service instances. |Supported |


<span id="42866211"></span>
# Automatic prompt

For Bash and Zsh shell users, the autocomplete script will be automatically installed. Zsh requires installing oh\-my\-zsh. If you find the automatic prompt does not meet expectations, you can refer to the following method to reinstall.

<span id="c431e5a8"></span>
## Bash

```Plain
mkdir autocomplete
curl -o autocomplete/bash_autocomplete https://ml-platform-public-examples-cn-beijing.tos-cn-beijing.volces.com/autocomplete/bash_autocomplete

sudo cp ./autocomplete/bash_autocomplete /etc/bash_completion.d/volc
. /etc/bash_completion.d/volc
```


<span id="13ed3fed"></span>
## Zsh

```Plain
mkdir autocomplete
curl -o autocomplete/zsh_autocomplete https://ml-platform-public-examples-cn-beijing.tos-cn-beijing.volces.com/autocomplete/zsh_autocomplete

# Method 1: Add the following configuration to the .zshrc file
PROG=volc
_CLI_ZSH_AUTOCOMPLETE_HACK=1
source path/to/autocomplete/zsh_autocomplete (autocomplete absolute path required)

# Method 2: Install the oh-my-zsh plugin
cp ./autocomplete/zsh_autocomplete $ZSH/custom/plugins/volc/volc.plugin.zsh
# Edit .zshrc and add volc to the plugins configuration as follows:
plugins=(
git
volc
tmux
zsh-autosuggestions
zsh-syntax-highlighting
)
```
