---
title: "EMR Serverless Custom Job usage instructions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_Custom_Job_User_guide"
---

EMR Serverless Custom Job provides an out\-of\-the\-box, fully managed job service. Users can submit jobs in a form similar to a K8S job on EMR Serverless, supporting the following features:


* No need to manage the underlying cluster operations; out\-of\-the\-box, with options for Pay\-As\-You\-Go or Subscription.

* Supports custom images, allowing you to use images from your own image repository.

* Supports customizing the number of job replicas, retry policies, and other parameters.

* Supports attaching auxiliary network interfaces, enabling network connectivity with resources in your specified VPC.

* Supports mounting TOS paths to the job, allowing seamless access to TOS using local path access within the job.


<span id="db291bd4"></span>
# prerequisites


1. Enable the EMR Serverless Spark service.

2. Upload custom images to your account's image repository.

3. Ensure the image repository feature is allowlisted. If not, please contact Volcano Engine staff.


<span id="510516d6"></span>
# Job submission

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Job: A Job in EMR Serverless is a collection of Tasks.</div>


* <div data-tips="true" data-tips-type="tip">Task: In a Job, each replica is called a Task.</div>



EMR Serverless Custom Job supports submission via SQL, allowing jobs to be submitted in DataLeap or the EMR Serverless SQL editor. This example demonstrates submitting via SQL to actually start a Python job:


1. Open the EMR Serverless console and create a job.

2. Enter the following command and click Run to submit an EMR Serverless Custom Job.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following example allows you to submit a custom Python job and run it with three replicas.   </div>
   

   ```SQL
   set serverless.custom.job.image = <您的镜像地址>;
   set serverless.custom.job.entrypoint = ["python", "<script_path>"];
   set serverless.custom.job.replicas = 3;
   ```
   

3. The Python code is as follows:

   ```Python
   print('你好')
   ```
   

4. The query log will display the job instance ID and job status.

   You can go to the job instance list in the parent directory, search for the job by instance ID, and view the log information (currently, only the task log with index 0 among multiple replicas is displayed).


<span id="6e12ccaf"></span>
# Detailed parameter list

<span id="3bd2d94d"></span>
## Core submission parameters


|Parameter name |Parameter description |Example |
|---|---|---|
|serverless.custom.job.image |Job image address. Enter the image address from your image repository. |image\-repo\-cn\-beijing.cr.volces.com/emr\-serverless/job:v1.0 |
|serverless.custom.job.entrypoint |Job startup command. Users need to configure it in JSON array format. |["python", "tos/redis_test.py"] or ["sh", "\-c", "python /home/root/a.py"] |
|serverless.custom.job.args |Job startup parameters. Users need to configure them in JSON array format. |["\-\-url_list", "/home/root/img2dataset/sbu\-captions\-all.json", "\-\-out_folder", "/home/root/img2dataset/result/sbu\-captions"] |
|serverless.custom.job.replicas |Number of job replicas. The default is 1. |3 |


<span id="0dfc2fde"></span>
## Custom job resource usage


|Parameter name |Parameter description |Example |
|---|---|---|
|serverless.custom.job.task.cores |CPU for each task |4 |
|serverless.custom.job.task.memory |Memory for each task |4Gi |


<span id="db705ef8"></span>
## Mount TOS

The following table is the updated version


|Parameter name |Parameter description |Example |
|---|---|---|
|serverless.tos.volumes |* Specify the TOS mount configuration. Both FSX and S3FS mount types are supported. The following parameters must be configured:<br><br>   * type: Mount type,<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">type, supports setting to fsx or s3fs.      </div><br>      <br><br>   * tosPath: TOS path,<br><br>   * mountPath: Mount path,<br><br>   * readOnly: Read\-only or not,<br><br>   * ak/sk: AK/SK for accessing TOS.<br><br>* Configuration must be provided by the user in JSON array format.<br><br>* For detailed parameter information, see:[ ](https://www.volcengine.com/docs/6491/2212809?lang=zh)[Mount TOS](https://docs.byteplus.com/en/docs/E-MapReduce/Mount_TOS). |[{"type": "fsx", "tosPath": "tos://test\-1/tos", "mountPath": "/home/root/", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"}] |


<span id="b020b0a7"></span>
## Attach auxiliary network interfaces across VPCs to access resources in the user's VPC


|Parameter name |Parameter description |Example |
|---|---|---|
|serverless.cross.vpc.access.enabled |Enable cross\-VPC |true |
|serverless.cross.vpc.vpc.id |VPC ID of the resource to be accessed |vpc\-xxx |
|serverless.cross.vpc.subnet.ids |Subnet ID(s) used to access resources in the VPC. Multiple selections are supported, separated by commas |subnet\-aa,subnet\-bb |
|serverless.cross.vpc.security.group.id |Security group id used to access resources in the VPC |sg\-xxxx |


<span id="d8237856"></span>
## GPU support


|Parameter name |Parameter description |Example |
|---|---|---|
|las.cluster.type |Node type. To enable GPU, you need to set it to run with vci. |* vci<br><br>* vke |
|serverless.custom.job.gpu.enabled |Enable GPU support |true |
|serverless.custom.job.task.gpus |Number of GPU cards for each task |1 |


<span id="e0ea444a"></span>
## Others


|Parameter name |Parameter description |Example |
|---|---|---|
|serverless.custom.job.working.dir |Default working directory for the task. The default is /home/root |/home/root/test |
|serverless.custom.job.restart.policy |Restart policy after task exit. The following policies are supported:<br><br><br>* Always: Always restart, even if the Task exits normally<br><br>* OnFailure: Restart only on failure<br><br>* Never: Never restart<br><br><br>The default is Never |OnFailure |
|serverless.custom.job.max.retry |Maximum number of task retries. If this number is exceeded, the job is marked as failed. The default is 3 times. |* 3: If the Task fails after 3 retries, the Job is marked as failed<br><br>* \-1: Task retries indefinitely |
|serverless.custom.job.env |Set environment variables for CustomJob, configured in JSON array format. |["zzw=123", "wyj=123123123"] |


<span id="4d264ba5"></span>
## Supported environment variables


|Environment variable name |Environment variable description |Example |
|---|---|---|
|VC_TASK_INDEX |Current task index |1 |
|VC_TASK_NUM |Total number of replicas for the current job |10 |


<span id="030f1f6f"></span>
# Best practices

<span id="86cee9d4"></span>
## Use TOS to host code

EMR Serverless Custom Job supports mounting TOS paths. You can host your code in a folder on TOS, then use the mount TOS method to read and write code without rebuilding the image. The steps are as follows:


* Create a TOS path and upload the code. In this example, the code is uploaded to the tos://test\-1/tos path:

* Submit Job for EMR Serverless Custom Job and set:

   * serverless.tos.volumes: mount the tos folder to the target dir

   * serverless.custom.job.entrypoint=["python", "tos/redis_test.py"], set the startup command to run the Python script, script path: tos/redis_test.py, corresponding to the tos://test\-1/tos/redis_test.py file

      The complete code is as follows:

   ```SQL
   set serverless.custom.job.image=emr-vke-qa-cn-beijing.cr.volces.com/emr/custom-job:python3.10-redis;
   set serverless.custom.job.entrypoint=["python", "tos/redis_test.py"];
   set serverless.emr.access.key=xx;
   set serverless.emr.secret.key=xxx;
   set serverless.tos.volumes=[{"type": "fsx", "tosPath": "tos://test-1/tos", "mountPath": "/home/root/", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"}];
   ```
   


<span id="fd69ef6f"></span>
## Use multiple replicas to accelerate img2dataset downloads

EMR Serverless Custom Job supports multiple replicas, and the current number of replicas and the task's replica index can be obtained from environment variables.

img2dataset is a tool for batch downloading images. In practical applications, you can manually shard the data file containing URLs and use the multi\-replica mechanism of Custom Job to execute in parallel, thereby accelerating downloads. The steps are as follows:

Taking the official example https://github.com/rom1504/img2dataset/blob/main/dataset_examples/SBUcaptions.md, process a small portion of URLs in the SBU Captions dataset:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, EMR Serverless CustomJob cannot access the public network. If the URL needs to be downloaded via the public network, please use the auxiliary network card mounting feature.</div>



* Preparations:

   * Place the URL JSON list to be downloaded on TOS; here, the path is tos://test\-1/img2dataset/sbu\-captions\-all.json.

* Code implementation:

   * Read the URL list, perform a hash modulo operation on the URLs, and determine whether a URL can be processed by the current task.

   * Download using img2dataset and write to the local path.

   ```Python
   import argparse
   import json
   import logging
   import os
   
   import img2dataset
   from fsspec.implementations.local import LocalFileSystem
   
   
   def download(url_list, output_folder):
       logging.info(f"start task, input url dir: {url_list}, output dir: {output_folder}")
       img2dataset.download(
           processes_count=16,
           thread_count=64,
           retries=0,
           timeout=10,
           url_list=url_list,
           image_size=256,
           resize_only_if_bigger=True,
           output_folder=output_folder,
           output_format="webdataset",
           input_format="json",
           url_col="image_urls"
       )
   
   
   if __name__ == "__main__":
       parser = argparse.ArgumentParser()
       parser.add_argument("--url_list", default="/home/root/img2dataset/sbu-captions-all.json")
       parser.add_argument("--out_folder", default="/home/root/img2dataset/result/sbu-captions")
       args = parser.parse_args()
       task_index = os.getenv("VC_TASK_INDEX", 1)
       task_num = os.getenv("VC_TASK_NUM", 1)
       logging.info(f"current task num: {task_num}, index: {task_index}")
   
       task_list = []
       # assign task
       fs = LocalFileSystem()
       with fs.open(args.url_list, 'r') as f:
           local_dict = json.loads(f.readline())
       for url in local_dict['image_urls']:
           if hash(url) % int(task_num) == int(task_index):
               task_list.append(url)
   
       # start task
       logging.info(f"index: {task_index}, len url: {len(task_list)}")
       url_path = f'url-{task_index}.json'
       with fs.open(url_path, 'w') as f:
           json_dict = {'image_urls': task_list}
           f.write(json.dumps(json_dict))
           f.close()
   
       download(url_path, args.out_folder)
   ```
   

* Submit Job. The complete code is as follows:

   ```Python
   set serverless.custom.job.image=emr-vke-qa-cn-beijing.cr.volces.com/emr/custom-job:python3.10-img;
   set serverless.custom.job.entrypoint=["python", "tos/image2dataset_test.py", "--url_list", "/home/root/img2dataset/sbu-captions-all.json", "--out_folder", "/home/root/img2dataset/result/sbu-captions"];
   set serverless.emr.access.key=xx;
   set serverless.emr.secret.key=xx;
   set serverless.tos.volumes=[
    {"type": "fsx", "tosPath": "tos://test-1/tos", "mountPath": "/home/root/tos", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"},
    {"type": "fsx", "tosPath": "tos://test-1/img2dataset", "mountPath": "/home/root/img2dataset", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"}
   ];
   set serverless.custom.job.replicas = 2;
   ```
   


<span id="2a516f7d"></span>
## Read and write Redis in the tenant VPC

The network environment in which EMR Serverless Custom Job runs is the EMR managed environment, which by default is not connected to the VPC network under your account. To enable network connectivity, set the parameters and use the auxiliary network interface attachment method to establish the connection.

As an example of reading and writing your fully managed Redis in your VPC:


* Preparation:

   * Enable redis

   * Write Python code

      ```Python
      import redis
      
      # Establish a connection to the Redis server
      r = redis.Redis(host='redis-cnlf68vdfvox694ma.redis.ivolces.com', port=6379, db=0, password='11111111')
      
      # Write data
      r.set('my_key', 'Hello, Redis!')
      
      # Read data
      value = r.get('my_key')
      print(value.decode('utf-8'))  # Print the retrieved value
      
      # You can also use hash tables for read and write operations
      r.hset('my_hash', 'field1', 'value1')
      print(r.hget('my_hash', 'field1').decode('utf-8'))
      
      # Close the connection
      r.close()
      ```
      

   * Set additional VPC\-related parameters in the Job. You need to specify your VPC ID, subnet ID (multiple subnets supported), and security group ID under the VPC

      ```SQL
      set serverless.cross.vpc.access.enabled = true;
      set serverless.cross.vpc.vpc.id = vpc-rs09o6sxx;
      set serverless.cross.vpc.subnet.ids = subnet-13fxx,subnet-14fxx;
      set serverless.cross.vpc.security.group.id = sg-rsxx;
      ```
      

* The result is successfully written after execution.


<span id="5117cb20"></span>
## Submit Job using Dataleap

EMR Serverless CustomJob supports submission using Dataleap. You can create an EMR Serverless Spark SQL task on Dataleap.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/187e2f605b394c68b45f46349ef68e95~tplv-goo7wpa0wc-image.image" width="2424px" /></div>


And submit jobs via SQL:

This was originally an image. Since parameter updates are needed, it has been changed to a code block. The content from the original image was copied and the parameters were modified.

```SQL
set serverless.custom.job.image=emr-vke-qa-cn-beijing.cr.volces.com/emr/custom-job:python3.10-img;
set serverless.emr.access.key=xx;
set serverless.emr.secret.key=xx;
set serverless.custom.job.entrypoint=［"python"，"tos/custom_job.py"];
set serverless.tos.volumes=[{"type": "fsx", "tosPath": "tos://test-1/tos", "mountPath": "/home/root/", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"}];

set serverless.cross.vpc.access.enabled=true; 
set serverless.cross.vpc.id=<vpc_id>; 
set serverless.cross.vpc.subnet.ids=subnet-mimeqvc0gtmo5smt1ayqtfwh; 
set serverless.cross.vpc.security.group.id=sg-miy0rjg55am85smt1bvecy88;
```


In the debug logs, you can find the job instance ID of EMR Serverless, and view the logs in the EMR Serverless console using the instance ID.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4eb054088c7467bbd132de2f57242e0~tplv-goo7wpa0wc-image.image" width="1838px" /></div>


<span id="f56cfe9f"></span>
## Use GPU

EMR Serverless CustomJob supports Pay\-As\-You\-Go GPUs. You can enable GPU support through parameters.

The complete case is as follows:

```SQL
set serverless.custom.job.image=emr-vke-qa-cn-beijing.cr.volces.com/emr/custom-job:python312;
set serverless.custom.job.entrypoint=["python", "tos/custom_job.py"];
set serverless.emr.access.key=xx;
set serverless.emr.secret.key=xx;
set serverless.tos.volumes=[{"type": "fsx", "tosPath": "tos://test-1/tos", "mountPath": "/home/root/", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"}];

set las.cluster.type = vke;
set serverless.custom.job.gpu.enabled = true;
set serverless.custom.job.node.selector = gpu-pool;
```


After running, you can see that the job has GPU mounted by default.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49d34851c63347f9b8c5c36b67522778~tplv-goo7wpa0wc-image.image" width="2030px" /></div>
