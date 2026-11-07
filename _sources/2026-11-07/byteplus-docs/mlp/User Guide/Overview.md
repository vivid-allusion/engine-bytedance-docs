---
title: "Overview"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Overview2"
---

Through the [Feature Overview](https://docs.byteplus.com/docs/mlp/Feature_Overview), users have a preliminary understanding of each module, and the user guide contains a detailed introduction to the use of important functions and limitations in each module. When a user encounters a problem in a functional module, they can seek a solution in the module section corresponding to the user guide. The main content of each module guide is introduced below.

<span id="资源组"></span>
# Resource Group


* Create Resource Group: Prepaid [Create (purchased) resource groups ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing)are required to use cost\-effective compute resources.

* Resource group management:

   * Management of permissions: As long as the user with `MLPlatformAdminAccess`and `BillingCenterFullAccess`(formerly `Bill FullAccess`) permissions is the resource group administrator, all resource group operations can be carried out.

   * Resource management: When the resource group is insufficient and the Duration expires, you can choose to expand or renew. Please unsubscribe the resource group in time when the resource group is no longer used. For specific operations, please refer [to Renewal/Rematch/Unsubscribe for Resource Groups](https://docs.byteplus.com/en/docs/mlp/ResourceGroup).

* Create the queue:

   * Management of permissions: Queues support the addition and deletion of users, and configure the queue permissions of each user (queue administrator or ordinary personnel)/the upper limit of personal resource usage. For specific operations, please refer to [the users in the management queue](https://docs.byteplus.com/en/docs/mlp/Manage_users_in_a_queue).

   * Resource management: If the queue has insufficient resources, you can choose to expand, and if there are too many resources, you can choose to shrink or transfer resources to other queues in the same availability area under the same resource group. For specific operations, please refer to [Queue Allocation/Transfer Resources](https://docs.byteplus.com/en/docs/mlp/Allocate-transfer_resources_to_the_queue).

* Instance Specification List and Pricing: Running a task requires selecting a specific instance. The [instance specification and pricing ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing)list lists the resource instances currently supported on the Machine Learning Platform and the corresponding unit price.


<span id="镜像仓库"></span>
# Container Registry


* Preset mirror list: The platform provides a large number of common CUDA basic mirrors, deep learning training/inference mirrors, see the [Preset mirror list](https://docs.byteplus.com/docs/mlp/Preset_mirror_list)for details.

* Build custom mirrors: When the preset mirror does not meet the user request, you can transfer other Container Registry mirrors to the Machine Learning Platform, or build custom mirrors based on existing mirrors/Dockerfiles.


<span id="开发机"></span>
# Dev boxes


* Create Dev boxes: In the early stage of modeling, the training code needs to be developed and debugged. Please refer to [Create Dev boxes ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes)to complete the Create of Dev boxes.

* Use Dev boxes: Support connecting to the Dev boxes container from local SSH, and also support using the computing power of Dev boxes in the WebIDE cloud integrated development environment pre\-installed by the platform for development and debugging. For details, see [Connect Dev boxes](https://docs.byteplus.com/en/docs/mlp/Remote_connection_to_Dev_boxes_via_SSH).


<span id="自定义训练"></span>
# Custom training


* General process of submitting training tasks: When the user needs to perform large\-scale training after developing the code, he can refer to the operation steps explained in [initiating stand-alone/distributed training tasks](https://docs.byteplus.com/en/docs/mlp/Initiate_stand-alone_distributed_training_tasks), and freely choose the console or command line to submit the training task. Refer to the method described in [Viewing TensorBoard Logs ](https://docs.byteplus.com/en/docs/mlp/View_TensorBoard_logs)to view the TensorBoard training log.

* Notes on submitting distributed tasks: The Machine Learning Platform presets a variety of distributed training methods, each of which has several specific environment variables or Start methods. For details, please refer to [initiate TensorFlowPS distributed training](https://docs.byteplus.com/en/docs/mlp/Initiate_TensorFlowPS_distributed_training), [initiate PyTorchDDP distributed training ](https://docs.byteplus.com/en/docs/mlp/Initiate_PyTorchDDP_distributed_training), [initiate MPI distributed training ](https://docs.byteplus.com/en/docs/mlp/Initiate_MPI_distributed_training), and [Initiate BytePS distributed training](https://docs.byteplus.com/docs/mlp/Initiate_BytePS_distributed_training).

* Accelerating Distributed Training with RDMA Networks: The Machine Learning Platform allows users to purchase high\-performance GPU instances that support RDMA to improve the training efficiency of large models. For details, please refer to [Accelerated training through RDMA networks](https://docs.byteplus.com/docs/mlp/Accelerated_training_through_RDMA_networks).


<span id="工作流"></span>
# Pipeline


* The pipeline module supports organizing multiple relatively independent [custom training](https://www.volcengine.com/docs/6459/79925#%E8%87%AA%E5%AE%9A%E4%B9%89%E8%AE%AD%E7%BB%83) (see [Overview](https://docs.byteplus.com/docs/mlp/Overview2)) into a pipeline. By running the pipeline, one\-click to open and advance, the final operation result is obtained.

* Through the pipeline, users can realize the whole process of machine learning orchestration, connecting the process from data processing, model training, model evaluation, model registration to service release.


<span id="在线服务"></span>
# Inference Services


* Deploy and invoke services: When the model training is completed and needs to be deployed as an API for invocation, please refer to [How to call inference services (new)](https://docs.byteplus.com/docs/mlp/Howtocallinferenceservices_new). When you want to know the health of the service during the operation of the service, please refer to [View the status/monitoring/logs of the service (new)](https://docs.byteplus.com/docs/mlp/View_the_status_monitoring_logs_of_the_service_new) for methods of viewing status, monitoring, and logging.

* Service management: According to the real\-time status of the service, users can choose to perform operations such as capacity expansion and reduction or upgrade model on the number of service instances on demand, and all changes to the service will form a change record. For details, please refer to [Service changes and change records](https://docs.byteplus.com/docs/mlp/Service_changes_and_change_records). When a service is no longer in use and needs to be deleted, refer to the method operation in the [Delete service](https://docs.byteplus.com/docs/mlp/Delete_service).
