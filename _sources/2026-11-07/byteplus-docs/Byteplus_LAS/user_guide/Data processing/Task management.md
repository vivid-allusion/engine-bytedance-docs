---
title: "Task management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Task_manage"
---

LAS task management provides developers with flexible, stable, and high\-performance data processing task management capabilities. It supports multiple algorithm frameworks, enables distributed processing of large\-scale data processing tasks, reduces customer costs, and improves development efficiency.

<span id="90451d16"></span>
# Prerequisites


* You already have a complete executable image available through a development machine or other means.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your image is in the BytePlus image repository, please note that your repository must be a standard edition instance.   </div>
   

* You have created the queue resources required for task execution. For instructions on creating queues, see [Queue management](https://docs.byteplus.com/docs/Byteplus_LAS/queue_manage).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To use GPU resources, please note that you need to select GPU when creating the queue.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When using a custom image, tasks currently do not support running on dedicated queues (that is, EMR Serverless queues).   </div>
   

* To create and run Python tasks, first upload the job files to a TOS bucket in the same region as LAS. This allows you to select them directly when creating tasks.


<span id="f8fb7c16"></span>
# Create a task

<span id="57c694c4"></span>
## Configure basic information


1. Log in to **LAS Console**, select the target region and project, and in the left navigation bar, choose **Data Processing ＞ Task Management** to enter the task management page.

2. Click  **＋Create Task** to go to the **Create Task** page and configure the relevant parameters.

   1. Configure basic information.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49429f1cf0ef4685894b3a814856bb58~tplv-goo7wpa0wc-image.image) </span>

      
      |Configuration items |Note |
      |---|---|
      |Name |* Length: 1–100 characters<br><br>* Only Chinese characters, uppercase and lowercase letters, or numbers can be used as the initial character<br><br>* Only hyphens “\-” and underscores “＿” are supported; special characters are not allowed |
      |Description |Description information, length: 0–200 characters |
      |Task type |Supports Daft, Spark, and Python task types.<br><br><br>* Daft: Distributed tasks, suitable for efficiently processing AI multimodal data and similar scenarios<br><br>* Python: Supports direct execution of Python scripts and related dependencies, suitable for lightweight data processing scenarios.<br><br>* Spark: Suitable for traditional big data scenarios such as batch and stream processing of massive data, SQL analysis, and more. |
      


<span id="4bef95e5"></span>
## Configure environment information

<span id="b9f22b0a"></span>
### Daft/Python tasks

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0a5de3aad034bbfa5b22f159eafed2b~tplv-goo7wpa0wc-image.image) </span>


|Configuration items |Note |
|---|---|
|Image type & image |Supports images from built\-in images, custom images, BytePlus image repository, and accessible image URLs.<br><br><br>* Built\-in images: Official built\-in images such as Daft, Ray, and Spark provided by LAS.<br><br>* Custom images: Supports deploying and launching development machines with custom images built on the LAS platform.<br><br>* BytePlus images: Supports selecting images that have been uploaded to the BytePlus image repository.<br><br>* Image URL: Supports setting images via URLs from self\-hosted image repositories that are accessible from the public network. When configuring in this way, you can perform a connectivity test after setting the image URL to ensure that the corresponding image can be retrieved normally during subsequent development machine deployment. |
|Entry command |Configure the job startup command. |
|Python job parameters<br><br>(Python tasks require configuration) |Configure the job parameters for Python jobs. The supported data types for Python job parameters are: String, Float, Boolean, JSON, List, and Flag. You can configure the corresponding job parameters according to the configuration examples shown in the interface to ensure the data format of the job parameters is correct.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0f73fe3171141bf9c32b8d7bacb3f45~tplv-goo7wpa0wc-image.image) </span> |
|Environment variables |Environment variables are entered in the Key:Value format. Supports adding environment variables line by line in KV mode or adding them collectively in text format. After setting environment variables in the development machine, you can directly reference the corresponding variables in subsequent tasks.<br><br>For example, if you set the variable name and value in the environment variables as `APP_ENV:PRODUCTION`, you can retrieve it in the job as follows: `import os; var = os.getenv("APP_ENV")`. Here, `var` will be assigned the value "`PRODUCTION`". |
|dataset mount |* Dataset name: If you have already created the data required for subsequent tasks as a LAS dataset, you can also mount the dataset to the development machine here. During subsequent development tasks, you can directly read data based on the mounted dataset.<br><br>* Mount path: Indicates the path where the dataset is mounted to DSW, for example `/mnt/data`. In your code, you can access this path to retrieve the dataset.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Mount paths for multiple datasets must not be duplicated.</div><br> |
|Mount storage path |Supports mounting TOS, and NAS file systems for storing data that needs to be accessed or for persisting files generated during development. For detailed information about storage mounting, see [Storage mounting instructions](https://docs.byteplus.com/docs/Byteplus_LAS/92505). |


<span id="d12c6d82"></span>
### Spark tasks

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d88e2ca2122c47e7a1c26f3e375d1340~tplv-goo7wpa0wc-image.image) </span>


|Configuration items |Note |
|---|---|
|Image type & images |Supports images from built\-in images, custom images, BytePlus image repository, and accessible image URLs.<br><br><br>* Built\-in images: Official built\-in images such as Daft, Ray, and Spark provided by LAS.<br><br>* Custom images: Supports deploying and launching development machines using custom images built on the LAS platform.<br><br>* BytePlus images: Supports selecting images that have been uploaded to the BytePlus image repository.<br><br>* Image URL: Supports setting images via URLs from self\-hosted image repositories that are accessible over the public internet. When configuring in this way, you can perform a connectivity test after setting the image URL to ensure that the corresponding image can be retrieved normally during subsequent development machine deployment. |
|Python/Jar files |Job files uploaded to TOS buckets in the same region. |
|Main Class |The main class for running SparkJar jobs. |
|Main task file |The primary Jar resource for SparkJar jobs. You can upload the resource to TOS and then specify the TOS path here. |
|Dependency Jar |In addition to the main task file, SparkJar jobs also support adding dependency Jar files, which will be added to the job classpath during execution. Similarly, you can upload resources to TOS and specify the path here. |
|Depends on python resources |Job files uploaded to TOS buckets in the same region as the current Serverless queue. |
|Depends on file resource |Dependency files for SparkJar jobs, which users can access via API in the task code. |
|Spark Conf |Spark job parameters, allowing you to specify resources used by the Spark job and more. |
|Main parameters (Main Conf) |Parameters required when running the main class of a SparkJar job. |
|dataset mount |* Dataset name: If you have already created the data required for subsequent tasks as a LAS dataset, you can mount the dataset to the development machine here. For subsequent development tasks, you can directly read data based on the mounted dataset.<br><br>* **Mount path**: Indicates the path where the dataset is mounted to DSW, for example `/mnt/data`. In your code, you can retrieve the dataset from this path.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Mount paths for multiple datasets must not be duplicated.</div><br> |
|Mount storage path |Supports mounting TOS, and NAS file systems for storing data that needs to be accessed or for persisting files generated during development. For detailed information about storage mounting, see [Storage mounting instructions](https://docs.byteplus.com/docs/Byteplus_LAS/92505). |


<span id="f387341d"></span>
## Advanced settings


|Configuration items |Note |
|---|---|
|Task timed out |Configure the switch to determine whether to set a task timeout period.<br><br><br>* Off: Indicates that no timeout is set.<br><br>* On: You must set a task timeout period. If the actual runtime of a subsequent task exceeds the specified duration, the corresponding task will be automatically canceled. |
|Scheduling |Configure whether subsequent tasks require periodic scheduling. When enabled, tasks can be automatically executed according to the scheduling policy.<br><br><br>* Effective time: Specifies the activation time point for the periodic task scheduling policy.<br><br>* Scheduling policy & interval: You can configure the time granularity and interval for periodic scheduling. Supported time granularities include minute, hour, day, week, and month.<br><br>* Allow concurrency: Allowed by default. If concurrency is not allowed, and the previous task has not finished during periodic scheduling, the current scheduling will be skipped.<br><br>* Resources & runtime parameters: When configuring subsequent periodic scheduling tasks, specify which queue resources the task will run on, and use the configured runtime parameters to occupy the corresponding queue resources. |
|Network connection |* When enabled, the selected resource queue can be connected to the target VPC network. To access services in a VPC environment, you need to turn on the switch and configure VPC\-related information (select VPC, subnet, and security group).<br><br>   For example, to mount a vePFS file system as a storage path, turn on the switch and select the VPC network where the file system is located.<br><br>* PrivateZone switch: After enabling the PrivateZone feature, you can use DNS resolution rules within the VPC. This setting is effective only when the task is submitted to a dedicated queue. |


<span id="4529130e"></span>
# Execute tasks

<span id="db477104"></span>
## Manual execution

After the task is created, you can manually trigger task execution as needed.


1. On the task list page, click the "Execute" button next to the corresponding task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4da4e978e1864d999ca7409d6d82d6f2~tplv-goo7wpa0wc-image.image) </span>

2. Follow the prompts on the interface to configure the resources and runtime parameters for this task execution.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3acb899a9ee344ec8382cf54139a5db8~tplv-goo7wpa0wc-image.image) </span>

3. After configuration is complete, click the "Execute" button in the lower right corner of the page to start executing the current task.


<span id="844e7f6c"></span>
## Automatic execution of periodic tasks

For periodic tasks, you can wait for the task to execute automatically according to the configured scheduling policy.

<span id="32ac2049"></span>
## Orchestrate workflows

You can also orchestrate multiple tasks based on workflows. After organizing multiple tasks in the form of a workflow, running the workflow will trigger the submission and execution of multiple tasks within the workflow. For details, see [Workflow](https://docs.byteplus.com/docs/Byteplus_LAS/92504).

<span id="c199c95f"></span>
# View task instances (execution results and logs)

Each time a task is triggered and executed, a task instance is generated on the “Task instances” page. You can view the execution results, logs, and monitoring information provided by Daft UI in the task instance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47e4487497e046099661e161a9e8513b~tplv-goo7wpa0wc-image.image) </span>


* You can view all task instances on the task instance page and filter them by instance ID, associated task, executor, and other criteria.

* For task instances that fail to run, you can hover your mouse over the instance status to view a brief prompt of the failure reason, or click “Log” to view detailed runtime log information and troubleshoot the cause of the failure.

* For manually triggered task instances, you can also click “Retry” to trigger the instance execution again. After retrying, you need to reset the task's resource and other parameters and trigger execution, which will generate a new task instance.

* For Daft tasks, you can click “Daft UI” to enter Daft's web interface and view more Daft details.


<span id="59da2ab2"></span>
# Edit/copy/delete tasks

After a task is successfully created, you can view all created tasks on the task list page and perform operations such as editing, copying, and deleting on existing tasks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04555411b1144cccbf5031d2b6613e56~tplv-goo7wpa0wc-image.image) </span>
