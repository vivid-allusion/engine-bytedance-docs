---
title: "Create and manage compute groups"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Create_and_manage_compute_groups"
---

<span id="9159c642"></span>
# Context

After the queue is created, a Default general compute group is automatically created for you. You can also plan and create custom compute groups based on subsequent job requirements. The following introduces the specific types of compute groups and their resource allocation methods.


|Compute group types |Note |Resource allocation method of compute groups |
|---|---|---|
|General compute group \- Default |The default compute group is automatically created for the queue. |The compute resources of the Default general compute group are dynamic. Its available resources are the remaining available resources in the queue after custom compute groups are created. |
|Custom compute group |Supports creating various types of custom compute groups, including general compute groups, SparkSQL Warehouse, PrestoSQL Warehouse, and more. |In custom compute groups:<br><br><br>* Custom general compute group: The resources of the compute group are allocated using a "logical allocation" method. That is, after a custom general compute group is created, resources in the queue are not directly isolated and allocated to the corresponding custom general compute group. Instead, resources are allocated only when jobs are running in this compute group.<br><br>* Other types of custom compute: After other types of custom compute groups are created, resources in the queue are isolated and allocated to the corresponding compute group based on the resource allocation configuration results of the compute group. |


From the above, it can be concluded:


* The actual available resources in the queue are the resources of the Default compute group. If you create a new compute group, resources will be allocated from the Default compute group.

* During the creation of a compute group, if a job happens to be running in the Default compute group and occupies some of its resources, the resources intended for the new compute group may be temporarily occupied. In this case, the 'resource preemption policy' configured when creating the new compute group will be used to handle resources temporarily occupied by jobs running in the Default compute group.


<span id="a4e28919"></span>
# Prerequisites


* The dedicated EMR Serverless queue has been created. For details, see [Create a queue](https://docs.byteplus.com/docs/E-MapReduce/Create_a_queue).

* You have permissions for the corresponding queue (at least Developer permissions). If you do not have operation permissions for the corresponding queue, contact the queue administrator to add permissions for you.


<span id="e1a470ed"></span>
# Create compute groups

<span id="7c8421fa"></span>
## Entry point for creation


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home), select the region in the upper left corner, and in the left navigation bar, select Resources\>**Serverless**. On the Serverless page, select the queue for which you want to create a general compute group and enter the queue details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/013a7f2a6f644aa09993e921bf35a6d5~tplv-goo7wpa0wc-image.image) </span>

2. In the left navigation bar of the queue details page, select Compute group\*\*,\*\* and on the compute group page, click Create a compute group in the upper right corner of the page, then select the type of compute group you want to create:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3eff42195274e18a4035497478fdaea~tplv-goo7wpa0wc-image.image) </span>

   
   |Compute group types |Applicable task scenarios and features |
   |---|---|
   |General compute group |Supports execution of various jobs, including Spark, Spark Jar, Ray Job, and more. Supports configuration of both resident (MIN) capacity and maximum (MAX) capacity. MIN capacity is exclusively reserved and mutually isolated to ensure job operation. When the compute group's MAX capacity exceeds its MIN capacity and job requests exceed the MIN value, it can utilize the idle capacity from other general groups (MAX\-MIN), enabling more refined and flexible resource allocation. This allows adaptation to a wide range of offline production workloads and foundational services. |
   |SparkSQL Warehouse |Specialized for efficient execution of Spark SQL jobs. For tasks such as SparkSQL, the Spark SQL Warehouse compute group reduces task execution latency by preheating resources, enabling tasks to start within seconds. This is especially suitable for ad\-hoc query tasks that require rapid response. |
   |PrestoSQL Warehouse |Specialized for efficient execution of Presto SQL jobs. Designed for interactive analytics and ad\-hoc queries, creating a Presto SQL Warehouse compute group reserves resident resources for PrestoSQL tasks, providing a low\-latency data exploration experience. |
   |Ray Cluster |Specialized for efficient execution of Ray Job. Supports large\-scale heterogeneous compute scheduling and serves as the foundation for distributed AI training and data processing. |
   |Ray Serve |Suitable for deploying models to perform inference tasks. Provides production\-grade model inference services, supporting high inference traffic and joint deployment of multiple models. |
   |Hive/MapReduce |Specialized for efficient execution of Hive and MapReduce jobs.<br><br>Hive/MapReduce compute groups are an allowlist feature. To use this feature, you can [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to apply for activation. |
   

3. Configure compute group parameters according to the selected compute group type. For detailed parameter descriptions, see the section **Configure compute group parameters** below.


<span id="db2066eb"></span>
## Configure compute group parameters: general compute group


1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91dddf6f154f40a982ebaf49f0fa9bfb~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Compute group name &Notes |Customize the compute group name and remarks to facilitate subsequent identification of the corresponding compute group.<br><br>For example, specify the business purpose or department ownership of the compute group in the note. |
   

2. Configure compute group capacity. Based on the allocatable resources of the current queue, assign the dedicated 'resident capacity' and flexible 'maximum capacity' to the current compute group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b6b7d4dc96345a4bb20da909522622f~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Permanent (MIN) capacity |Exclusive resources for the current compute group. After configuration, the corresponding capacity of resources will be isolated from the queue as dedicated resources for the current computing group, serving as the minimum resources required for subsequent tasks running on this computing group. |
   |Maximum (MAX) capacity |The maximum number of resources after automatic elastic scaling. When the number of tasks on the computing group increases, EMR Serverless automatically scales up the computing group resources for you. Once the tasks are completed, the scaled resources are automatically released. Currently, the supported options for the maximum capacity after scaling are:<br><br><br>* Queue maximum: The maximum resource capacity after scaling is equal to the maximum capacity of the entire queue.<br><br>* Custom: Customize the maximum resource capacity after scaling, which cannot exceed the current queue's maximum resource capacity. |
   

3. Compute group configuration.

   
   |**Parameters** |**Configuration instructions** |
   |---|---|
   |Concurrency cap |Set the concurrency limit for tasks in the computing group. |
   |EngineRuntime |Select the Spark compute engine environment. You can choose the Spark version and the corresponding Java Runtime or Bolt Runtime.<br><br><br>* Java Runtime: Standard Java runtime.<br><br>* Bolt Runtime: BytePlusProprietary native kernel acceleration engine that can improve the execution speed of Spark, Presto, and other jobs. For detailed information, see .<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The EngineRuntime parameter priority for general compute groups is lower than that for Spark jobs. The EngineRuntime parameters configured when submitting a job take precedence.</div><br> |
   |Metadata |Set which metadata service is used for data processing by jobs in the current computing group. |
   |VPC & HMS connection<br><br>(Configuration required for external HMS) |If the metadata of the computing group is of the 'external HMS' type, you must also configure the network information (VPC, subnet, security group) for connecting to the external HMS and the corresponding HMS connection address.<br><br><br>* Network for connecting to external HMS: Set the VPC network information (VPC, subnet, security group) that is connected to the network where the HMS service resides.<br><br>* HMS connection address: Format is `thrift://<HMS IP/Domain>:<HMS Port>`<br><br><br>After completing the configuration, you can click 'Test Link' to test the network connectivity. |
   

4. Other configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3992df1151e14c0c89bbe866327fab2e~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Storage path mount |Add a storage mount to the current compute group.<br><br><br>* Currently, you can mount vePFS, NAS, and TOS to the compute group.<br><br>* Before mounting vePFS or NAS, you need to complete the relevant storage network configuration. For details, see [Overview of storage mounting](https://docs.byteplus.com/docs/E-MapReduce/Overview_of_storage_mounting). |
   


<span id="e00edcc4"></span>
## Configure computing group parameters: SparkSQL Warehouse


1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91dddf6f154f40a982ebaf49f0fa9bfb~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Compute group name & Remarks |Customize the compute group name and remarks to facilitate subsequent identification of the corresponding compute group.<br><br>For example, specify the business purpose or department ownership of the compute group in the note. |
   

2. Configure computing group capacity. Allocate resource quotas for Driver and Worker nodes in the current computing group based on the allocatable resources of the current queue.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7fa8a2855da45a884fce283d4ce40b8~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Driver specifications |Set the available resource specifications for the Driver node. The number of drivers is set to 1 by default and cannot be modified. |
   |Worker (resident) & Worker (on\-demand) specification |Set the resource specification available to each Worker node; and set the number of resident Worker nodes and on\-demand Worker nodes. The resource specification for resident Worker nodes and on\-demand Worker nodes is the same. Among them:<br><br><br>* Resident Worker nodes: The number of workers that are immediately started and always retained after the compute group is launched. Suitable for latency\-sensitive tasks, as there is no need to wait for resource allocation.<br><br>* On\-demand Worker nodes: The number of nodes that can be automatically scaled elastically. When the workload on the compute group increases, EMR Serverless will automatically scale out Worker nodes for you, and automatically release them after the tasks are completed. |
   

3. Computing group configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c04d51f755d47f9add379255c7a560b~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Resource delivery strategy |If the resources of the Default compute group are occupied by other jobs and there are not enough idle resources available, select an appropriate delivery strategy. The following options are currently supported:<br><br><br>* Wait: Wait for the task to finish and release resources. You can set a waiting time of up to 30 minutes.<br><br>* Preempt: Immediately end the task and release resources. This may cause other tasks to fail.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating a compute group, the resources allocated to the compute group are actually distributed from the Default compute group. Resources may be temporarily unavailable due to being occupied by other compute groups. For details, see the <a href="https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups#9159c642">Context</a> section above.</div><br> |
   |Wait timeout<br><br>(Configuration required for "Wait" type) |When the "Resource delivery strategy" is set to "Wait", you need to configure the timeout for waiting. Unit: "minutes". |
   |Priority |Set the resource allocation priority for the current computing group. The value range is 0–10. The higher the value, the higher the priority. When the queue is fully loaded, high\-priority computing groups will be allocated resources earlier than low\-priority computing groups or jobs. |
   |Scheduling policy |Corresponds to the open\-source parameter `spark.scheduler.mode`, supporting:<br><br><br>* FAIR: Fair scheduling<br><br>* FIFO: First in, first out |
   |Concurrency cap |Set the concurrency limit for computing group tasks. |
   |EngineRuntime |Select the Spark compute engine environment. You can choose the Spark version and the corresponding Java Runtime or Bolt Runtime.<br><br><br>* Java Runtime: Standard Java runtime.<br><br>* Bolt Runtime: BytePlusProprietary native kernel acceleration engine that can improve the execution speed of Spark, Presto, and other jobs. For detailed information, see .<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The EngineRuntime parameter priority for SparkSQL Warehouse compute groups is higher than that for SQL jobs. If a job submitted to a SparkSQL Warehouse compute group is configured with EngineRuntime parameters, the compute group parameters take precedence.</div><br> |
   |Metadata |Set the metadata type for the current computing group. |
   |VPC & HMS connection<br><br>(Configuration required for external HMS) |If the metadata of the computing group is of the 'external HMS' type, you must also configure the network information (VPC, subnet, security group) for connecting to the external HMS and the corresponding HMS connection address.<br><br><br>* Network for connecting to external HMS: Set the VPC network information (VPC, subnet, security group) that is connected to the network where the HMS service resides.<br><br>* HMS connection address: Format is `thrift://<HMS IP/Domain>:<HMS Port>`<br><br><br>After completing the configuration, you can click 'Test Link' to test the network connectivity. |
   |Independent Shuffle Service |After enabling, you can configure the already created EMR Serverless RSS service for the compute group to achieve better shuffle performance and load isolation.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the queue has Independent Shuffle Service enabled, existing Spark compute groups follow the queue Independent Shuffle Service configuration, and you can also modify the Independent Shuffle Service configuration on the compute group details page.</div><br> |
   

4. Custom configuration. You can configure additional resource settings here as custom parameters as needed. The configuration format is key\-value, and multiple parameters are separated by line breaks. For supported parameters, see [available properties](https://archive.apache.org/dist/spark/docs/3.5.1/configuration.html#available-properties).


<span id="6a6ad3a9"></span>
## Configure computing group parameters: PrestoSQL Warehouse

<span id="9d302b02"></span>
### Basic configuration items


1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91dddf6f154f40a982ebaf49f0fa9bfb~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Compute group name & Remarks |Customize the compute group name and remarks to facilitate subsequent identification of the corresponding compute group.<br><br>For example, specify the business purpose or department ownership of the compute group in the note. |
   

2. Configure computing group capacity. Allocate resource quotas for Coordinator and Worker nodes in the current computing group based on the allocatable resources of the current queue.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58864e95b14e4515900236d7f7e85e1c~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Coordinator specifications |Set the available resource specifications for Coordinator nodes. The number of Coordinator nodes defaults to 1 and cannot be modified. |
   |Worker (resident) & Worker (on\-demand) specification |Set the resource specification available to each Worker node; and set the number of resident Worker nodes and on\-demand Worker nodes. The resource specification for resident Worker nodes and on\-demand Worker nodes is the same. Among them:<br><br><br>* Resident Worker nodes: The number of workers that are immediately started and always retained after the compute group is launched. Suitable for latency\-sensitive tasks, as there is no need to wait for resource allocation.<br><br>* On\-demand Worker nodes: The number of nodes that can be automatically scaled elastically. When the workload on the compute group increases, EMR Serverless will automatically scale out Worker nodes for you, and automatically release them after the tasks are completed. |
   

3. Compute group configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51aa72c13fc8463bb6c585c2cf4b4b0f~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Resource delivery strategy |If the resources of the Default compute group are occupied by other jobs and there are not enough idle resources available, please select an appropriate delivery strategy. Currently, the following options are supported:<br><br><br>* Wait: Wait for the task to finish and release resources. You can set a waiting time of up to 30 minutes.<br><br>* Preempt: Immediately end the task and release resources. This may cause other tasks to fail.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating a compute group, the resources allocated to the compute group are actually distributed from the Default compute group. Resources may be temporarily unavailable due to being occupied by other compute groups. For details, see the <a href="https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups#9159c642">Context</a> section above.</div><br> |
   |Wait timeout<br><br>(Configuration required for "Wait" type) |When the "Resource delivery strategy" is set to "Wait", you need to configure the timeout for waiting. Unit: "minutes". |
   |Priority |Set the resource allocation priority for the current computing group. The value range is 0–10. The higher the value, the higher the priority. When the queue is fully loaded, high\-priority computing groups will be allocated resources earlier than low\-priority computing groups or jobs. |
   |Concurrency cap |Set the concurrency limit for computing group tasks. |
   |Runtime |Set the execution engine for computing group tasks. Supports selection of the open\-source 'Java Runtime' engine or the proprietary 'Bolt acceleration' engine. |
   |Metadata |Set the metadata type for the current computing group. |
   |VPC & HMS connection<br><br>(Configuration required for external HMS) |If the metadata of the computing group is of the 'external HMS' type, you must also configure the network information (VPC, subnet, security group) for connecting to the external HMS and the corresponding HMS connection address.<br><br><br>* Network for connecting to external HMS: Set the VPC network information (VPC, subnet, security group) that is connected to the network where the HMS service resides.<br><br>* HMS connection address: Format is `thrift://<HMS IP/Domain>:<HMS Port>`<br><br><br>After completing the configuration, you can click 'Test Link' to test the network connectivity. |
   |Resource Group Parameter Configuration |To use a custom Resource Group configuration file, upload the file to TOS in the same region. Here, select or enter the TOS path for the Resource Group configuration file. The corresponding configuration file will be referenced during subsequent task resource allocation, and resources will be allocated based on the settings in the configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you also configure a concurrency limit in the Resource Group settings, the configuration here will take effect, and the concurrency limit set on the page above will not be applied.</div><br> |
   


<span id="fd77a029"></span>
### Custom parameter configuration

The Presto computing group supports custom parameter configuration, including custom catalogs, access control, and more. The following provides guidance for configuring these two custom parameters.


1. After creating the PrestoSQL Warehouse computing group as described above, click "Parameter configuration" on the computing group details page. On the parameter configuration page, click "Add Catalog parameter" to start configuring custom parameters.

2. Configure custom catalogs.

   1. For parameter configuration methods, refer to: https://prestodb.io/docs/0.283/connector.html.

   2. After creation, you can click Edit to modify custom catalog information, **no need to restart the computing group**. (Due to cache time, **configuration changes take effect in about 1 minute**.)

   3. Click the Delete button to remove this catalog.

3. Configure access control to enable custom permission control.

   1. For parameter configuration methods, refer to: https://prestodb.io/docs/0.283/security/built\-in\-system\-access\-control.html

   2. After completing rule definition, you can click the Edit button to modify rules. After modification, **no need to restart the computing group**, and the configuration takes effect within 5 minutes.

   3. Disable permission control: You can also edit Access\-control\-rule, delete all content, and Save. Afterwards, **restart the computing group to take effect**. Permission control is disabled by deleting the configuration result.


<span id="7f5c8871"></span>
## Configure computing group parameters: Ray Cluster

<span id="764f1d7d"></span>
### Basic configuration items


1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91dddf6f154f40a982ebaf49f0fa9bfb~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Compute group name & Remarks |Customize the compute group name and remarks to facilitate subsequent identification of the corresponding compute group.<br><br>For example, specify the business purpose or department ownership of the compute group in the note. |
   

2. Configure computing group capacity.

   1. (Optional) If your queue contains GPU resources, you can select the GPU resource group in the resource type dropdown of the capacity configuration. Once selected, allocate GPU and CPU resources in the resource allocation table below.

   2. Allocate resource quotas for Head and Worker nodes in the current compute group based on the available resources in the current queue.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9dbd94a45315473fad6d2d7ab5660258~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameters |Note |
      |---|---|
      |Head specification |Set the resource specification available to the Head node. The number of Head nodes is fixed at 1. |
      |Worker |Set the resource specification available to each Worker node; and set the number of resident Worker nodes and on\-demand Worker nodes. The resource specification for resident Worker nodes and on\-demand Worker nodes is the same. Among them:<br><br><br>* Resident Worker nodes: The number of workers that are immediately started and always retained after the compute group is launched. Suitable for latency\-sensitive tasks, as there is no need to wait for resource allocation.<br><br>* On\-demand Worker nodes: The number of nodes that can be automatically scaled elastically. When the workload on the compute group increases, EMR Serverless will automatically scale out Worker nodes for you, and automatically release them after the tasks are completed. |
      

3. Environment configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/271bb83e297d412ea230d39b5bfdbf0b~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Mirror image &Mirror address |Select the image environment for task execution. Currently, you can choose either the official base image provided to you or a custom image that has been uploaded to the image repository. |
   |environment variables |Environment variables are entered in `key-value` format. For example, if you enter `APP_ENV` in the left input box of each row and `PRODUCTION` in the right input box, you can retrieve it in your job as follows: `import os; var = os.getenv("APP_ENV")`. Here, `var` will be assigned the value `"PRODUCTION"`. |
   

4. Advanced configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/260719b4df2a461ab31a67ea24dd0eb1~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Resource delivery strategy |If the resources of the Default compute group are occupied by other jobs and there are not enough idle resources available, please select an appropriate delivery strategy. Currently, the following options are supported:<br><br><br>* Wait: Wait for the task to finish and release resources. You can set a waiting time of up to 30 minutes.<br><br>* Preempt: Immediately end the task and release resources. This may cause other tasks to fail.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating a new compute group, the resources allocated to the compute group are actually allocated from the Default compute group. There may be cases where resources are temporarily occupied. For details, see the <a href="https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups#9159c642">Context</a> section above.</div><br> |
   |Wait timeout<br><br>(Configuration required for "Wait" type) |When the "Resource delivery strategy" is set to "Wait", you need to configure the timeout for waiting. Unit: "minutes". |
   |Priority |Set the resource allocation priority for the current computing group. The value range is 0–10. The higher the value, the higher the priority. When the queue is fully loaded, high\-priority computing groups will be allocated resources earlier than low\-priority computing groups or jobs. |
   |GCS High Availability & Redis URL & Password |You can choose whether to enable the GCS high availability switch as needed.<br><br><br>* It is recommended to enable the GCS high availability switch. Once enabled, subsequent tasks can leverage GCS's fault tolerance mechanism to ensure task fault tolerance. For details, see [GCS high availability help documentation](https://docs.ray.io/en/latest/cluster/kubernetes/user-guides/kuberay-gcs-ft.html).<br><br>* The high availability capability of GCS relies on a highly available Redis service at the underlying layer. Therefore, after enabling the GCS high availability switch, you must also configure the connection URL and password for the corresponding Redis cluster. |
   |Internet connection |To access services related to your private network in a job, configure the subnet and security group information for the target network. |
   |access configuration |Configure whether to enable the access configuration switch. After enabling, you must configure the inbound access address of the Ray cluster Head node (the VPC and public IP for accessing the cluster). Once configuration is complete, you can connect to the cluster using the fixed access address you configured, and the cluster access address will not change when the compute group restarts.<br><br><br>* Private network, subnet, security group: After enabling the access configuration switch, you must set the VPC network, subnet, and security group for accessing the cluster.<br><br>* Public IP: You can enable the public IP switch as needed and bind a public IP to enable public network connectivity. Enabling public network access poses security risks. Please proceed with caution. |
   |storage path mount |Add a storage mount to the current compute group.<br><br><br>* Currently, you can mount vePFS, NAS, and TOS to the compute group.<br><br>* Before mounting vePFS or NAS, you must complete the relevant storage network configuration. For details, see [Overview of storage mounting](https://docs.byteplus.com/docs/E-MapReduce/Overview_of_storage_mounting). |
   

5. Custom configuration. You can configure additional resources here as custom parameters as needed. The configuration format is key\-value, and multiple parameters are separated by line breaks.


<span id="0c6ca393"></span>
### Custom parameter configuration

Ray Cluster and Ray Serve compute groups support custom parameter configuration. After creating the compute group as described above, click "Parameter Configuration" on the compute group details page, then click "Edit" on the parameter configuration page to start configuring custom parameters.

The supported custom parameter list is as follows.


|Category |Parameter name |Default value |Description |Configuration example/format |
|---|---|---|---|---|
|Image and startup |serverless.ray.entrypoint.cmd |None |Command to start the Ray job. |`python test.py` |
|Image and startup |serverless.ray.entrypoint.bundle.path |None |TOS address for the job code or dependency package. |`tos://some-bucket/demo.zip` |
|Image and startup |serverless.customized.image.enabled |false |Whether to enable custom image.<br><br><br>* true: Indicates pulling the image from the customer's image repository<br><br>* false: Use the platform image repository image |true |
|Image and startup |serverless.ray.image |None |Image address used |`emr-serverless-online-cn-beijing.cr.volces.com/emr-serverless-ray/ray:******-233` |
|Basic configuration |serverless.ray.cluster.name |None |Ray cluster name | |
|Basic configuration |serverless.ray.runtime.env.json |None |Runtime environment variables, JSON format |```JSON```<br>```{"pip":["requests==2.26.0","pendulum==2.1.2","s3fs"],"env_vars":{"counter_name":"test_counter"}}```<br> |
|Basic configuration |serverless.ray.head.pod.env |None |Head Pod environment variable configuration. |```JSON```<br>```[{"name":"ENV_K1","value":"ENV_V1"}]```<br> |
|Basic configuration |serverless.ray.worker.pod.env |None |Worker Pod environment variable configuration. |```JSON```<br>```[{"name":"ENV_K1","value":"ENV_V1"}]```<br> |
|Scheduling and deployment |serverless.ray.autoscaler.options.idle.timeout.seconds |60 |Worker idle auto\-release time (seconds) |None |
|Scheduling and deployment |serverless.ray.enable.autoscaling |false |Whether to enable Worker auto\-scaling |None |
|Scheduling and deployment |serverless.ray.autoscaler.options.cpu |500m |CPU configuration for each Worker in auto\-scaling. Must be set to an integer greater than 0. |None |
|Scheduling and deployment |serverless.ray.autoscaler.options.memory |512Mi |Memory configuration for each Worker in auto\-scaling. Must be set to an integer greater than 0. |None |
|Network and access |serverless.cross.vpc.access.enabled |None |Enable cross\-VPC access |None |
|Network and access |serverless.cross.vpc.accountId |None |Target account ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.vpc.id |None |Target VPC ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.subnet.ids |None |Target subnet ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.security.group.id |None |Security group ID for cross\-VPC |None |
|Network and access |serverless.cross.vpc.dns.resolve.enabled |false |Enable DNS resolution for cross\-VPC |None |
|Shared memory |serverless.shm.enabled |true |Whether to enable shared memory |None |
|Shared memory |serverless.shm.size |None |Set the shared memory size |```Plain```<br>```serverless.shm.size=4Gi```<br> |


<span id="a940228e"></span>
## Configure compute group parameters: Ray Serve

<span id="87133bca"></span>
### Basic configuration items


1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91dddf6f154f40a982ebaf49f0fa9bfb~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Ray service name &Remarks |Customize the Ray service name and note information to facilitate subsequent identification of the corresponding compute group.<br><br>For example, specify the business purpose or department ownership of the compute group in the note. |
   

2. Configure compute group capacity. Allocate resource quotas for Head and Worker nodes in the current compute group based on the available resources in the current queue.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c125a3f31fae4284a1bc54861d5ff77d~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Head specification |Set the resource specification available to the Head node. The number of Head nodes is fixed at 1. If your queue includes GPU resources, you also need to set the number of GPUs for the Head node. |
   |Worker (resident) & Worker (on\-demand) specification |Set the resource specification available to each Worker node; and set the number of resident Worker nodes and on\-demand Worker nodes. The resource specification for resident Worker nodes and on\-demand Worker nodes is the same. Among them:<br><br><br>* Resident Worker nodes: The number of workers that are immediately started and always retained after the compute group is launched. Suitable for latency\-sensitive tasks, as there is no need to wait for resource allocation.<br><br>* On\-demand Worker nodes: The number of nodes that can be automatically scaled elastically. When the workload on the compute group increases, EMR Serverless will automatically scale out Worker nodes for you, and automatically release them after the tasks are completed. |
   

3. Environment configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/271bb83e297d412ea230d39b5bfdbf0b~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Mirror image &Mirror address |Select the image environment for task execution. Currently, you can choose either the official base image provided to you or a custom image that has been uploaded to the image repository. |
   |environment variables |Environment variables are entered in `key-value` format. For example, if you enter `APP_ENV` in the left input box of each row and `PRODUCTION` in the right input box, you can retrieve it in your job as follows: `import os; var = os.getenv("APP_ENV")`. Here, `var` will be assigned the value `"PRODUCTION"`. |
   

4. RayServe network VPC access configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/046e21365c8c451b84a98e1453d62bfd~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |VPC & Subnet &Security group |Select a VPC network and configure the corresponding subnet and security group for generating the Ray Serve inference address later. |
   

5. Advanced configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/876f6e15e3b54a719fcc9bf82fa49fce~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Resource delivery strategy |If the resources of the Default compute group are occupied by other jobs and there are not enough idle resources available, please select an appropriate delivery strategy. Currently, the following options are supported:<br><br><br>* Wait: Wait for the task to finish and release resources. You can set a waiting time of up to 30 minutes.<br><br>* Preempt: Immediately end the task and release resources. This may cause other tasks to fail.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating a new compute group, the resources allocated to the compute group are actually allocated from the Default compute group. There may be cases where resources are temporarily occupied. For details, see the <a href="https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups#9159c642">Context</a> section above.</div><br> |
   |Wait timeout<br><br>(Configuration required for "Wait" type) |When the "Resource delivery strategy" is set to "Wait", you need to configure the timeout for waiting. Unit: "minutes". |
   |Priority |Set the resource allocation priority for the current computing group. The value range is 0–10. The higher the value, the higher the priority. When the queue is fully loaded, high\-priority computing groups will be allocated resources earlier than low\-priority computing groups or jobs. |
   |GCS High Availability & Redis URL & Password |You can choose whether to enable the GCS high availability switch as needed.<br><br><br>* It is recommended to enable the GCS high availability switch. After enabling, tasks can benefit from the fault tolerance mechanism provided by GCS. For details, see [GCS High Availability Help Documentation](https://docs.ray.io/en/latest/cluster/kubernetes/user-guides/kuberay-gcs-ft.html).<br><br>* The high availability capability of GCS relies on a highly available Redis service at the underlying layer. Therefore, after enabling the GCS high availability switch, you must also configure the connection URL and password for the corresponding Redis cluster. |
   |Internet connection |To access services related to your private network in a job, configure the subnet and security group information for the target network. |
   |storage path mount |Add a storage mount to the current compute group.<br><br><br>* Currently, you can mount vePFS, NAS, and TOS to the compute group.<br><br>* Before mounting vePFS or NAS, you must first complete the relevant storage network configuration. For details, see [Overview of storage mounting](https://docs.byteplus.com/docs/E-MapReduce/Overview_of_storage_mounting). |
   

6. Ray Serve configuration & custom configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0152a7e353dc4f5988bf30a1922b480e~tplv-goo7wpa0wc-image.image) </span>

   * You can apply the configuration results from the Ray Serve YAML file here. It is recommended to use the `serve build` tool to automatically generate the YAML configuration results, then configure the generated content here. For details about the YAML file and the `serve build` tool, see [Serve Config Files](https://docs.ray.io/en/latest/serve/production-guide/config.html).

   * You can configure additional resources here as custom parameters as needed. The configuration format is key\-value, and multiple parameters are separated by line breaks.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the Ray Serve scenario, you need to mount the model to the EMR serverless queue. You can either integrate the model directly into a custom image and select the corresponding custom image in the Ray Serve image configuration above, or upload the model to TOS, configure the model storage path here in key\-value format, and use the corresponding path as the model invocation path when you Submit Job later.      </div>
      

<span id="08d7bb03"></span>
### Custom parameter configuration

Same as Ray Cluster. For details, see [Custom parameter configuration](https://docs.byteplus.com/docs/E-MapReduce/Create_and_manage_compute_groups#0c6ca393) above.

<span id="2295f25c"></span>
## Configure compute group parameters: Hive/MapReduce

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Hive/MapReduce compute group is an allowlist feature. To use this feature, you can <a href="https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D">submit a ticket</a> to apply for activation.</div>



1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b0744f722d94fc4a629ce24dac76a4c~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Compute group name &Notes |Customize the compute group name and remarks to facilitate subsequent identification of the corresponding compute group.<br><br>For example, specify the business purpose or department ownership of the compute group in the note. |
   

2. Compute group capacity configuration. Hive/MapReduce compute groups do not support elastic scaling.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85a4b3a2c8c54833b000a617c05f5234~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Resource Manager (Resident) |Fixed reserved resources for the YARN Resource Manager, responsible for resource scheduling and task allocation for the entire compute group. The Resource Manager must remain resident to ensure service availability. |
   |Node Manager (Resident) |Fixed reserved resources for the YARN Node Manager, which runs on each compute node, reports resource status, and executes task containers. The Node Manager must remain resident to ensure service availability. |
   |Operational resources (resident) |A fixed resource pool allocated for actual Hive/MapReduce job execution. Jobs draw resources from this pool during execution. |
   

3. Advanced compute group configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f0fe8ef60f94c9f85badb1bbe444864~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Note |
   |---|---|
   |Resource delivery strategy |When Default compute group resources are insufficient, new Hive/MapReduce compute group tasks are queued to wait or preempt resources.<br><br><br>* Wait: New tasks wait for other tasks to finish and release resources. This does not affect other running tasks. The maximum wait time can be set to 120 minutes.<br><br>* Preempt: Tasks are immediately terminated to release resources, which may cause other tasks to fail. |
   |Wait timeout |This takes effect when the **Wait** strategy is selected. If resources are not obtained within the specified time, the task fails. The maximum wait time can be set to 120 minutes. |
   |Priority |Set the resource allocation priority for the current computing group. The value range is 0–10. The higher the value, the higher the priority. When the queue is fully loaded, high\-priority computing groups will be allocated resources earlier than low\-priority computing groups or jobs. |
   |Metadata |The metadata management service (Metadata Service) currently connected to the compute group supports managing table information for storage\-compute separated Hive based on TOS using the LAS Catalog. This is only effective for the current compute group. |
   


<span id="fcc1151c"></span>
# Modify and manage compute groups

<span id="26ffde63"></span>
## View compute group list

After completing compute group creation

you can subsequently view all compute groups in the compute group page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a15a503409ee453fae7ba18d7ca6768b~tplv-goo7wpa0wc-image.image) </span>


* You can view the current status of compute groups on the compute group list page. Typically, compute groups with the status "Running" are available compute groups, while those with the status "Starting" are compute groups in the process of being created.

* Hover your mouse over the chart in the "Current CPU usage/Current GPU allocation" column to view the CPU/GPU resource allocation for the corresponding compute group.

* You can also view basic information such as the creator and runtime.


<span id="9e4fd8bc"></span>
## View and modify compute group configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Editing the compute group may cause jobs running in the compute group to fail. Please proceed with caution.</div>



1. On the compute group list page, click the name of the corresponding compute group to enter the compute group details page.

2. You can modify the compute group's compute resource configuration, metadata, network configuration, and more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b3f8ead36b041daaafe59e03acf8895~tplv-goo7wpa0wc-image.image) </span>

   The range of parameters that can be modified varies for different types of compute groups. Details are as follows.

   
   |Compute group types |Note |
   |---|---|
   |General compute group (default) |* Compute group configuration:<br><br>   * You can modify the concurrency limit of the compute group.<br><br>   * Modify the EngineRuntime compute engine environment for the compute group.<br><br>* Metadata and network connection:<br><br>   * Supports changing the metadata type and VPC information for network connections.<br><br>* Other configuration:<br><br>   * Supports modifying the storage mount configuration. |
   |General compute group (custom) |* Basic information:<br><br>   * Description of the compute group.<br><br>* Capacity configuration:<br><br>   * Resident capacity: GPU allocation and card count, CU allocation.<br><br>   * Maximum capacity: You can modify the allocation method for maximum capacity. When customizing maximum capacity, you can modify GPU allocation and card count, and CU allocation.<br><br>* Compute group configuration:<br><br>   * You can modify the concurrency limit of the compute group.<br><br>   * Modify the EngineRuntime engine for the compute group.<br><br>* Metadata and network connection:<br><br>   * Supports changing the metadata type and VPC information for network connections.<br><br>* Other configuration:<br><br>   * Supports modifying the storage mount configuration. |
   |SparkSQL |* Basic information:<br><br>   * Description of the compute group.<br><br>* Capacity configuration:<br><br>   * Specifications for Driver nodes and Worker nodes.<br><br>   * Number of resident Worker nodes and on\-demand Worker nodes.<br><br>* Compute group configuration:<br><br>   * Supports changing the resource delivery policy of the compute group.<br><br>   * You can modify the concurrency limit of the compute group.<br><br>   * Modify the EngineRuntime engine for the compute group.<br><br>   * Modify the priority of the computing group.<br><br>* Custom configuration:<br><br>   * Supports modifying the configuration results of custom parameters.<br><br>* Metadata and network connection:<br><br>   * Supports changing the metadata type and VPC information for network connections.<br><br>* Other configuration:<br><br>   * Supports modifying the Independent Shuffle Serviceconfiguration. The compute group Independent Shuffle Serviceconfiguration takes precedence over the queue configuration. |
   |PrestoSQL |* Basic information:<br><br>   * Description of the compute group.<br><br>* Capacity configuration:<br><br>   * Specifications for Coordinator nodes and Worker nodes.<br><br>   * Number of resident Worker nodes.<br><br>* Compute group configuration:<br><br>   * Supports changing the resource delivery policy of the compute group.<br><br>   * Modify the Runtime engine of the compute group.<br><br>   * Modify the priority of the computing group.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Modifying the compute group's concurrency, metadata, and network connection configuration is not supported.</div><br> |
   |Ray Cluster |* Basic information:<br><br>   * Description of the compute group.<br><br>* Capacity configuration:<br><br>   * GPU and CU allocation for Head nodes and Worker nodes.<br><br>   * Number of resident Worker nodes and on\-demand Worker nodes.<br><br>* Compute group configuration:<br><br>   * Modify the configuration for the GCS high availability switch.<br><br>   * Supports changing the resource delivery policy of the compute group.<br><br>   * Modify the priority of the computing group.<br><br>* Other configuration:<br><br>   * Supports modifying the storage mount configuration.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Modifying the compute group's image and custom configuration is not supported.</div><br> |
   |Ray serve |* Basic information:<br><br>   * Description of the compute group.<br><br>* Capacity configuration:<br><br>   * GPU and CU allocation for Head nodes and Worker nodes.<br><br>   * Number of resident Worker nodes and on\-demand Worker nodes.<br><br>* Compute group configuration:<br><br>   * Modify the configuration for the GCS high availability switch.<br><br>   * Supports changing the resource delivery policy of the compute group.<br><br>   * Modify the priority of the computing group.<br><br>* Other configuration:<br><br>   * Supports modifying the storage mount configuration. |
   |Hive/MapReduce |* Basic information:<br><br>   * Description of the compute group.<br><br>* Capacity configuration:<br><br>   * Compute resources, including the CU amount for Node Manager (resident) and job resources (resident).<br><br>* Compute group configuration:<br><br>   * Modify the resource delivery policy.<br><br>   * Modify the wait timeout period.<br><br>   * Modify the priority of the computing group. |
   

3. On the compute group details page, click "Parameter configuration" in the left navigation to enter the parameter configuration page, where you can also modify the parameter configuration results for the compute group.


<span id="b5eff0c6"></span>
## Start, stop, and delete compute groups

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9e74d58995f4c3084ee518c6bdda19f~tplv-goo7wpa0wc-image.image) </span>


* You can stop running compute groups from the operations column of the compute group. After stopping, the resources of this compute group will be reallocated to the Default compute group.

* For compute groups that have been stopped, you can also restart them. After restarting, the resources will be reallocated to the corresponding compute group.

* For compute groups that are no longer in use, you can directly delete the compute group.


<span id="e5216c76"></span>
## Access the web UI

On some compute group details pages, you can jump to the UI page entry of the corresponding engine. For example, with Spark UI, you can conveniently jump to the UI page via the UI page entry.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27a6a2e85c9c43348bf4ad8ad1622449~tplv-goo7wpa0wc-image.image) </span>

The currently supported compute group types include: PrestoSQL, SparkSQL, and Ray Cluster.

<span id="9cce647e"></span>
# Compute group monitoring

On the left navigation bar of the corresponding compute group details page, click "Monitoring" to view details of common monitoring metrics for the compute group, such as CPU and memory usage. You can also flexibly set different data monitoring time ranges.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f60e6f4f2a948adb998e54534251c5a~tplv-goo7wpa0wc-image.image) </span>

<span id="cc9e79c8"></span>
# related operations

<span id="7faa93e2"></span>
## Create a job


1. After the compute group for the queue is created, you can start creating and running related jobs based on the compute group type. The common operation entry points are as follows.

   
   |General entry for creating jobs in the queue |Create jobs from the compute group list page |Create jobs from the compute group details page |
   |---|---|---|
   |Click "Create Job" in the upper right corner of the queue details page to access the job submission entry.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16a2bb45059e4b1b85fb6e531ddc6285~tplv-goo7wpa0wc-image.image) </span><br><br>On this page, you can edit jobs and set the job development type, the compute group to use, and other options. |You can also access the job creation page from the compute group list page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67d7980235ed499290d24b17790d43d7~tplv-goo7wpa0wc-image.image) </span> |You can also access the job creation page from the compute group details page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cb7da2782fc49c1927494af97e9e231~tplv-goo7wpa0wc-image.image) </span> |
   

2. For details about job creation, see [Create and submit jobs](https://docs.byteplus.com/docs/E-MapReduce/118293).


<span id="ccb39830"></span>
## Job instance management

After a job is running, you can view the status, runtime, and other details of job instances running in the current compute group on the job instance management page in the compute group details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d61d489c00c44bff8b0333573c248caa~tplv-goo7wpa0wc-image.image) </span>


* You can click the corresponding job instance to further view job instance details, submission logs, and other job instance runtime information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f24640028d99443199014f40fcb9c542~tplv-goo7wpa0wc-image.image) </span>


<span id="9cea7940"></span>
## SQL editor


1. After the compute group for the queue is created, you can start creating and running related jobs based on the compute group type. The common operation entry points are as follows.

   
   |General entry for creating jobs in the queue |Access from the compute group details page |
   |---|---|
   |Click "SQL Editor" in the upper right corner of the queue details page to access the SQL Editor.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72727e861201405c8aa26f7dd8fca79f~tplv-goo7wpa0wc-image.image) </span><br><br>On this page, you can edit jobs and set the job development type, the compute group to use, and other options. |You can also access the job creation page from the compute group details page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/607be4b1eece43898683811c08c97443~tplv-goo7wpa0wc-image.image) </span> |
