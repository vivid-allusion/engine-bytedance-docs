---
title: "Feature Overview"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Feature_Overview"
---

<span id="资源组"></span>
# Resource Group

The machine learning platform provides [resource groups] for purchasing and managing resources. Users (usually operation and maintenance engineers or personnel responsible for resource purchasing and management) can purchase resources (such as 10 Tesla\-A100 servers) in a cost\-effective manner through **Subscription** , and pool this part of the resources into several queues. Workloads that handle different businesses in different queues can be used by users at any time before the resource group expires at no additional cost.


* Resource group permissions: Only users with resource group administrator privileges can perform actions such as create, modify, renew, unsubscribe, and create queues for resource groups.


<span id="队列"></span>
# Queue

A queue defines a quota of resources (CPU, memory, GPU, etc.) that users can use to create workloads.


* Support both prepaid and postpaid charging models.

* Queue permissions: The queue administrator (Admin, the queue creator defaults to the queue administrator) supports user management, allocation, resource transfer and other actions on the queue. General users can only use queues to run workloads.


<span id="实例"></span>
# Example

The basic unit of computing resources on a machine learning platform. An instance contains a certain number of CPUs, memory, and GPUs, which can be compared to a virtual machine. Training tasks or online services need to run on an instance, and the instance will consume the total amount of resources of a queue. Different instances consume different amounts of resources. See [instance specifications and pricing ](https://docs.byteplus.com/en/docs/mlp/Instance_Specifications_and_Pricing)for details.

<span id="镜像仓库"></span>
# Mirror warehouse

Training and deploying models requires not only hardware computing resources, but also Docker images as a running environment that encapsulates the software dependencies required for the program to run. The [Image Warehouse] of the machine learning platform provides users with a large number of [preset images ](https://docs.byteplus.com/en/docs/mlp/Preset_mirror_list). When the preset images cannot meet the needs, users can choose to migrate their own images to the machine learning platform, or build custom images in the machine learning platform. For detailed actions, please refer to


* Image: A special file system that contains the programs, libraries, resources, configuration, etc. required by the container to run, which is equivalent to encapsulating the software running environment.

* Dockerfile: A text file used to build an image that contains instructions, a list of dependencies, and some important instructions for building the image.


<span id="开发机"></span>
# Developer computer

[Developer computer] is a module for online compilation, debugging code and model development provided by the machine learning platform for developers. The developer computer supports online development using WebIDE or remote development via SSH connection to the developer computer, and also provides persistent cloud storage services and shared file systems for storing data in development. When the development machine is shut down to release the computing power, the user's previous actions, downloaded data and configuration environment will be retained, and the user will continue to use it after the next boot. See [create developer computer ](https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes)for details.

<span id="自定义训练"></span>
# Custom training

The [Custom Training] module of the machine learning platform provides users with a flexible and easy\-to\-use machine learning training environment. Preset [TensorFlowPS](https://docs.byteplus.com/docs/mlp/76491#tensorflowps), [PyTorchDDP](https://docs.byteplus.com/docs/mlp/76491#pytorchddp), [BytePS](https://docs.byteplus.com/docs/mlp/76491#byteps), [MPI](https://docs.byteplus.com/docs/mlp/76491#mpi)a variety of distributed training framework, users do not need to care about the underlying machine scheduling and operation and maintenance, upload code and fill in the right amount of parameters can quickly [initiate distributed training tasks ](https://docs.byteplus.com/en/docs/mlp/Initiate_stand-alone_distributed_training_tasks).

&nbsp;

<span id="在线服务"></span>
# Online service

After users have trained the model, they need to deploy it as an online service before it can be used to solve real\-world business problems. The [Online Services] module of the machine learning platform enablesof models and provides complete Monitoring and logging. Users can not only fully grasp the health status of the service, but also conduct detailed and in\-depth troubleshooting of problems through functions such as logs and WebShell.

<span id="sdk-命令行-openapi"></span>
# SDK/Command Line/OpenAPI

In addition to the console pages, the machine learning platform also encapsulates and OpenAPI, making it easy for developers to complete machine learning business or integrate machine learning platform functions into downstream business systems without the console.
