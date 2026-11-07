---
title: "RayJob jobs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/RayJob_jobs"
---

To meet user requirements for multimodal data processing with Ray, EMR Serverless supports the submission and execution of Ray jobs. Ready to use out of the box, with no additional cluster management required.

<span id="155fc65a"></span>
# Prerequisites


* An EMR Serverless queue has been created, and you have Developer/Admin permissions for the queue. For operation details, see: [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue), [Queue permissions](https://docs.byteplus.com/docs/E-MapReduce/Queue_permissions).

* A compute group has been created. Currently, only general compute groups and Ray compute groups are supported. For operation details, see [Create and manage compute groups](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups).

* The job files have been uploaded to the TOS bucket in the same region as the current Serverless queue.


<span id="55424499"></span>
# Submit Job

<span id="ef2bad31"></span>
## **Submit Job: via console**


1. Log in to the EMR Serverless console, click Job center \> Job management in the left navigation bar, then click the "Create job" button in the upper right corner of the job management page to enter the job creation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7c6b3ca8f50408099947bf93322a75c~tplv-goo7wpa0wc-image.image) </span>

   You can also click "Create job" in the upper right corner of the Serverless queue/compute group page to jump to the job creation page.

2. Configure job parameters on the job creation page.

   1. Configure basic job information and resource configuration.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76c840ef724249eda70af80060fe155b~tplv-goo7wpa0wc-image.image) </span>

      * Customize the job name and select RayJob as the job type.

      * Select the queue resource where the job will run.

   2. Configure the job environment.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68dc15c298f4435b8b829dc500b4d8e8~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Configuration description |
      |---|---|
      |Task master file |Select the main file uploaded to the TOS bucket in the same region as the current Serverless queue. |
      |Entry command |The entry command for RayJob submission is usually `python xxx.py`.<br><br>If there are parameters, add them to the command. |
      

   3. Advanced configuration.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5df971ebd0742c29548ac379a66c298~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |Configuration description |
      |---|---|
      |GCS High Availability |When submitting a RayJob, you can use a toggle on the page to choose whether to enable GCS high availability.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To learn more about GCS high availability, see <a href="https://docs.ray.io/en/latest/ray-core/fault_tolerance/gcs.html">GCS Fault Tolerance</a> for more information.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When submitting a RayJob through a RayCluster compute group, the compute group's GCS high availability configuration is automatically inherited. No additional configuration is required.</div><br><br><br><br>If enabled, you need to fill in the following parameters:<br><br><br>* RedisURL: Specify the Redis instance used for GCS backup. After creating an instance in the Redis console, obtain the private domain name/port of the target instance from the instance list page.<br><br>* Password: Specify the Redis instance password and set the password for the default account of the corresponding instance. |
      |Internet connection |Configure whether to enable network connectivity. If enabled, you must set the corresponding VPC, subnet, and security group.<br><br>After configuration is complete, during subsequent job execution, Ray head/worker nodes can use the VPC configured here to access services or resources within the enterprise VPC network. |
      |Custom parameters |Add custom job parameters based on the actual job situation. |
      |Storage path mount |Set the storage paths that may need to be mounted for the current job. For details, see [Overview of storage mounting](https://docs.byteplus.com/docs/E-MapReduce/Overview_of_storage_mounting). |
      

3. After editing the job, click the Create and run button in the lower right corner to submit the job.

   You can also just create the job, and manually trigger the task to run later from the job list page.


<span id="c30d55b5"></span>
## **Submit Job:**  via SDK

For detailed operations, refer to: [Serverless Ray usage guide](https://docs.byteplus.com/docs/undefined/69d872d5b2b492054482fcae).

<span id="3121acf1"></span>
# View/run/delete jobs

After a job is created, you can view all created jobs on the job list page, manually trigger a job to run, or edit, modify, and delete jobs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1941ed94ade4f4cbbd2cde209b34c06~tplv-goo7wpa0wc-image.image) </span>

<span id="95c33735"></span>
# View and diagnose job instances

After submitting a job, you can also view the details of all submitted job run instances on the Job center \> Job instance page, including run status, job type, resource details, submitter, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ff2963cba543d1a50fb25d9508db7e~tplv-goo7wpa0wc-image.image) </span>


* At the top of the page, you can quickly filter job instances by scope, submitter, and other criteria to view the details of the job instances.

* For jobs that failed to run, you can click "Log" to view detailed job run logs and locate the cause of the failure; you can also use the "AI diagnosis" feature to perform intelligent job diagnosis.


<span id="7ca81722"></span>
# Reference: Custom parameters supported by RayJob


|Category |Parameter name |Default value |Description |Configuration example/format |
|---|---|---|---|---|
|Image and startup |serverless.ray.entrypoint.cmd |None |Command to start the Ray job. |`python test.py` |
|Image and startup |serverless.ray.entrypoint.bundle.path |None |TOS address for job code or dependencies. |`tos://some-bucket/demo.zip` |
|Image and startup |serverless.customized.image.enabled |false |Whether to enable custom images.<br><br><br>* true: Indicates pulling images from the customer's image repository<br><br>* false: Use images from the platform image repository |true |
|Image and startup |serverless.ray.image |None |Image address in use |`emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-ray/ray:******-233` |
|Basic configuration |serverless.ray.cluster.name |None |Ray cluster name | |
|Basic configuration |serverless.ray.runtime.env.json |None |Runtime environment variables, JSON format |```JSON```<br>```{"pip":["requests==2.26.0","pendulum==2.1.2","s3fs"],"env_vars":{"counter_name":"test_counter"}}```<br> |
|Basic configuration |serverless.ray.head.pod.env |None |Environment variable configuration for the Head Pod. |```JSON```<br>```[{"name":"ENV_K1","value":"ENV_V1"}]```<br> |
|Basic configuration |serverless.ray.worker.pod.env |None |Environment variable configuration for the Worker Pod. |```JSON```<br>```[{"name":"ENV_K1","value":"ENV_V1"}]```<br> |
|Scheduling and deployment |serverless.ray.autoscaler.options.idle.timeout.seconds |60 |Worker idle auto\-release time (seconds) |None |
|Scheduling and deployment |serverless.ray.enable.autoscaling |false |Whether to enable auto\-scaling for Workers |None |
|Scheduling and deployment |serverless.ray.autoscaler.options.cpu |500m |CPU configuration for each Worker in auto\-scaling. Must be set to a value greater than 0. |None |
|Scheduling and deployment |serverless.ray.autoscaler.options.memory |512Mi |The memory configuration for each Worker in auto scaling must be set to an integer greater than 0. |None |
|Network and access |serverless.cross.vpc.access.enabled |None |Whether to enable cross\-VPC access |None |
|Network and access |serverless.cross.vpc.accountId |None |Target account ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.vpc.id |None |Target VPC ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.subnet.ids |None |Target subnet ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.security.group.id |None |Security group ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.dns.resolve.enabled |false |Whether to enable DNS resolution for cross\-VPC |None |
|Resource configuration |serverless.ray.head.cpu |1 |The CPU quota for the Head node must be set to an integer greater than 0. |None |
|Resource configuration |serverless.ray.head.memory |2Gi |The memory quota for the Head node must be set to an integer greater than 0, and the configuration parameter value must include the Unit. |None |
|Resource configuration |serverless.ray.head.gpu.amount |0 |The number of GPUs for the Head node must be set to an integer greater than 0. |None |
|Resource configuration |serverless.ray.head.gpu.vendor |nvidia.com |The GPU vendor for the Head node (such as NVIDIA) |None |
|Resource configuration |serverless.ray.worker.cpu |1 |The CPU quota for the Worker node must be set to an integer greater than 0. |None |
|Resource configuration |serverless.ray.worker.memory |2Gi |The memory quota for the Worker node must be set to an integer greater than 0, and the configuration parameter value must include the Unit. |None |
|Resource configuration |serverless.ray.worker.gpu.amount |0 |The number of GPUs for the Worker node must be set to an integer greater than 0. |None |
|Resource configuration |serverless.ray.worker.gpu.vendor |nvidia.com |The GPU vendor for the Worker node |None |
|Resource configuration |serverless.ray.worker.replicas |1 |The number of Worker replicas in fixed mode |None |
|Resource configuration |serverless.ray.worker.min.replicas |None |The minimum number of Worker replicas for auto scaling must be set to an integer greater than 0. |None |
|Resource configuration |serverless.ray.worker.max.replicas |None |The maximum number of Worker replicas for auto scaling must be set to an integer greater than 0. |None |
|Resource configuration |serverless.ray.start.params.head.num.cpus |None |The number of CPU cores reserved when starting the Head node |None |
