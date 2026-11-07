---
title: "Jobs, development machines, and tasks FAQ"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/jobs_faq"
---

<span id="b638110b"></span>
# Task configuration

<span id="15a696ff"></span>
## From development machine to task management

<span id="10422523"></span>
### The script that works on the development machine fails to connect to the ray client when running in task management

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1d30c30adca4b19b4d5fae8b596f8d3~tplv-goo7wpa0wc-image.image" width="2550px" /></div>


A few lines of code need to be added to the Python script:

```YAML
import ray

ray.init(dashboard_host="0.0.0.0")
daft.context.set_runner_ray("ray://127.0.0.1:10001")
```


<span id="fbdfb2eb"></span>
### The script that passes testing on the development machine fails to start in task management, and the head health check fails


* The user\-installed daft/ray framework overwrites the framework provided by the built\-in LAS image, resulting in missing LAS components when starting the task.

* Use the built\-in image or install the specified version of the Daft framework.


<span id="a7f78967"></span>
### The script that passes testing on the development machine accesses a public TOS address via code, but reports "TOS address connection timeout" in task management


* The task is configured with cross\-VPC parameters, so network requests are routed through the bound VPC by default, which cannot access the public network

* Enable and bind NAT outbound access for this VPC


<span id="64b1e07d"></span>
## Workflow configuration

<span id="8064c58a"></span>
### How can task instances started by a workflow coordinate with other task instances in the same workflow?


* When starting a workflow instance, you can specify global environment variables. Each task instance can coordinate using these environment variables, for example, by using the same TOS folder to transfer data.

* In addition, the following environment variables can be obtained in the task instance pod:

   * LAS_TASK_ID=t\-xxx (task template ID)

   * LAS_TASK_INSTANCE_ID=ti\-xxx (task instance ID)

   * LAS_TASK_WORKFLOW_TEMPLATE_ID=wf\-tpl\-xxx (workflow template ID)

   * LAS_TASK_WORKFLOW_INSTANCE_ID=wf\-tpl\-xxx\-xxx (workflow instance ID)

   * LAS_TASK_WORKFLOW_INSTANCE_TIMESTAMP_MS=1779872124749 (workflow instance start timestamp)


<span id="e8341fe2"></span>
### How to set different environment variables for different nodes when starting a workflow?


* Only one set of global environment variables can be set when starting a workflow; individual settings are not supported

* Scripts for different nodes can focus on different key values, so only the relevant key values are read

* For cases where multiple nodes in the same workflow use the same task template, the script can first read KeyName, then use the value of KeyName as the key to read the environment variable. This is equivalent to an extra mapping step, allowing different KeyNames to be set for different nodes.


<span id="a2126c46"></span>
# Task execution

<span id="ffe40be8"></span>
## Daft tasks

<span id="231a3a3a"></span>
### Daft\-type tasks hang at the end of execution


* The task execution log is normal, but the task hangs at the end without exiting

* The reason is that some tasks are assigned to the head node, so an additional line needs to be added to the startup script.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4adc6c9bfea24b5a9e09240882b176cc~tplv-goo7wpa0wc-image.image" width="1488px" />   </div>
   


<span id="21fd7167"></span>
### Error when running Daft tasks: "Missing ray..."


* You need to use the built\-in Daft/Ray image, or a custom image created based on either of these images.

* If a custom base image must be used, the appropriate versions of Daft, Ray, and other dependencies need to be installed.


<span id="8b78113b"></span>
## Python tasks

<span id="562d0ea8"></span>
### Error when running Python tasks: "StartTaskInstance..."


* The reason is that the entry command contains a statement like: `cd /aa/bb && python cc.py --xx`

* The entry command for Python tasks can only be a single command; multiple commands are not supported.

* This can be optimized to: `python /aa/bb/cc.py --xx`

* For complex commands

   1. You can set the entry command to `sh -c`, and then enter a complex command line in the "Python job parameters": `cd /../ && ...` `&& ...`

   2. You can write the commands in a script file, mount it to a directory using tos, and start it with a single entry command: `python /test/test.py`


<span id="24287cc5"></span>
## Spark tasks

<span id="7479af8c"></span>
### When running serverless Spark jobs, users are prompted that they do not have operation permissions.

```java
2024-05-08 15:16:59-ERROR: analysis.AnalysisException: Permission denied: user [1025770] does not have privilege in:
[Resource{resourceScope='TABLE', catalogName='hive', schemaName='test_lf', tableName='table_20240507'}], action:[SELECT]
```


Reason: The user does not have permission for the object.

Solution: Go to LAS \- Permission Management and grant the user permission for the corresponding object.

For more details: [Permission management](https://docs.byteplus.com/docs/Byteplus_LAS/Permission_Management)

<span id="a6826e10"></span>
## General component issues

<span id="1a5c711a"></span>
### No execution logs when running tasks


* If the task execution time is too short (<5s), the log may not be saved. For testing, you can print something and then sleep for a while.

* When using `print()` to print logs, logs may not be collected because the buffer is not flushed in time. You can flush manually or use a log library (which flushes automatically).


<span id="5d6f591f"></span>
### Task cannot start due to basic component issues, such as image pull failure.


* From ECS monitoring, you can see that the vdb write bandwidth is saturated (180MB/s), causing basic system functions to be blocked.

* The reason is that the customer writes a large amount of data to the default path "/tmp/...", which is on the system disk, resulting in the system being unable to function properly.

* Solution: The user should write data to the `/data/...` directory, which has a dedicated data disk. If the data disk speed or capacity is insufficient, contact SRE to replace the data disk.


<span id="a39f7126"></span>
# Queue resource issues

<span id="153a3c58"></span>
### After the task starts, the submission log reports "Insufficient ... eni" (insufficient network interfaces).


* The ENI (Elastic Network Interface) resources in the queue are limited. The following resources may occupy ENIs:

   * Each head/worker occupies one.

   * When mounting vepfs/nas, the fsx agent occupies one on each node.

* In general, you can adjust the number of workers to avoid excessive ENI consumption.


<span id="83fa0eeb"></span>
### Error occurred during compute queue task execution: "ValueError: Job with submission_id las\-0aqk9jhz\-4mm2t already exists. Please use a different submission_id."


* An earlier error has already occurred, and the error is caused by SubmitPod automatically retrying. Check the previous logs for the actual error log.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f696636e0f941d0ac660a22d11a4b85~tplv-goo7wpa0wc-image.image" width="2978px" />   </div>
   


<span id="f481a93a"></span>
### Submitting a Daft task to the EmrServerless public queue and requesting 64 CPUs causes the task to hang.


* The maximum specification for the public queue host is 64 CPUs, but some resources may be occupied, so it is generally recommended to set the task maximum to 32 CUs.


<span id="701fbee2"></span>
# Logs and component UI

<span id="2c076977"></span>
### During task instance processing, logs can be viewed in DaftUI. After execution is complete, logs cannot be viewed in RayUI.


* If a custom image lacks necessary dependencies, logs cannot be collected. The custom image must meet the following requirements:

   1. The `python` command must point to `python3.x` by default.

   2. Ensure that the required packages for log collection are installed: `pip install tos, requests`


<span id="524e41f9"></span>
### The Ray Core Overview section on the RayUI page does not display any content.


* If the number of tasks exceeds a certain threshold (approximately 3,000), the specific task details cannot be displayed.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/873c74aea25a4a62903c46e136e0f988~tplv-goo7wpa0wc-image.image" width="1664px" />   </div>
