---
title: "GPU/CPU Flexible Use Guide"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/GPU-CPU_Flexible_Use_Guide"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function is a grant whitelist access function, and rollback is not supported after grant whitelist access (cancel grant whitelist access), please apply for use on demand.</div>


<span id="功能概述"></span>
# Feature Overview

The new platform supports the flexible matching function of GPU and CPU specifications, which aims to open up the flexibility of resource selection and improve the utilization of CPU/memory resources on the GPU server.

<span id="功能限制"></span>
# Functional limitations

Dev boxes/custom tasks/inference services all support GPU/CPU flexible matching function.

<span id="快速开始"></span>
# Quick start

<span id="页面交互"></span>
## Page interaction


> * Dev boxes Path: [Dev boxes] \- [Create Dev boxes] \- [Environment Configuration \- Computing Resources]

> * Custom tasks path: [custom tasks] \- [create custom tasks] \- [resource configuration \- instance configuration]

> * Inference services path: [Inference services] \- [Create services] \- [Resource configuration \- Computing resources]


The following are the steps in custom tasks:


1. Click custom tasks \- create custom tasks and select resource configuration \- instance configuration. The selection of GPU servers and CPU servers is supported in the instance configuration. The following resource configuration methods are supported when using a GPU server:

   1. Select the CPU server, the GPU specification is grey out, and only the corresponding CPU/memory resources can be selected.

   2. Select the GPU server, the number of GPU cards can be selected from 0 to 8 (depending on the upper limit of the GPU quota in the queue), and the corresponding CPU/memory resources can be selected according to the number of cards selected by the GPU.

      1. Due to this resource allocation method, it is easy to cause GPU resource fragmentation. Therefore, when selecting a GPU machine without allocating GPU resources (selecting card 0), it is recommended to enable the "Use idle resources" feature. At this point, CPU tasks that cause fragmentation may be preempted by GPU tasks to improve GPU utilization.

   3. The optional GPU and CPU specs are capped on the queue quota, meaning that if there are no GPU resources in the queue, the GPU specs option is not visible at this time.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4875d5726cf14407b85fefa961d2fc46~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1c54a275eaa47c7982175a3bd4cda6a~tplv-goo7wpa0wc-image.image) </span>


<span id="命令行"></span>
## Command line


* In the volc cli ml_task related commands to add support for flexible matching mode specified resources.

   * The custom tasks yaml definition extends the structure of the specified resource.

      * Submit custom tasks in a non\-flexible matching way, and the format will not be changed.

         ```yaml
         # self define e.g text_classification
         Task Name: "Tasks submitted in a non-flexible ratio method"
         # description for this task
         Description: ""
         # entry point command
         Entrypoint: "sleep infinity"
         Tags: []
         # the code path you want to upload locally
         User Code Path: ""
         # remote path mount in training container
         Remote Mount Code Path: ""
         # user define env var
         Envs: []
         # queue created under Resource Group, empty as default queue
         Resource Queue ID: "q-xxxxxxxxxx"
         # distributed framework, support: TensorFlow PS, PyTorch DDP, Horovod, BytePS
         Framework: "Custom"
         Task Role Specs:
           - Role Name: "worker"
             Role Replicas: 1
             Flavor: "ml.c2i.large"
         Active Deadline Seconds: 864000
         # enable tensor board or not
         Enable TensorBoard: false
         # storages
         Storages: []
         Image URL: "vemlp-ap-southeast-1.cr.volces.com/preset-images/python:3.10"
         Cache Type: "Cloudfs"
         # user define retry options
         Retry Options:
           Enable Retry: true
           Max Retry Times: 5
           Interval Seconds: 120
           Policy Sets:
             - "Failed"
         ```
         

      * After enabling the flexible matching method to submit custom tasks, the specified resource format is extended accordingly.

         ```yaml
         # self define e.g text_classification
         Task Name: "GPU/CPU tasks submitted in a flexible ratio method"
         # description for this task
         Description: ""
         # entry point command
         Entrypoint: "sleep inf"
         Tags: []
         # the code path you want to upload locally
         User Code Path: ""
         # remote path mount in training container
         Remote Mount Code Path: ""
         # user define env var
         Envs: []
         # queue created under Resource Group, empty as default queue
         Resource Queue ID: "q-xxxxxxxxxx"
         # distributed framework, support: TensorFlow PS, PyTorch DDP, Horovod, BytePS
         Framework: "TensorFlow PS"
         Task Role Specs:
           - Role Name: "worker"
             Role Replicas: 1
             # When submitting a GPU task using the flexible ratio method, fill in the following parameters. Comment them out when submitting a CPU task.
             Flavor: "custom"
             Resource Spec:
               Family: "ml.hpcpni2l"
               CPU: 105.000
               Memory: 1875.000
               GPU Num: 8
             # When submitting a CPU task using the flexible ratio method, fill in the following parameters. Comment them out when submitting a GPU task.
             Flavor: "custom"
             Resource Spec:
               CPU: 2.000
               Memory: 8.000
         
         Active Deadline Seconds: 864000
         # enable tensor board or not
         Enable TensorBoard: false
         # storages
         Storages: []
         Image URL: "vemlp-ap-southeast-1.cr.volces.com/preset-images/python:3.10"
         Cache Type: "Cloudfs"
         # user define retry options
         Retry Options:
           Enable Retry: false
           Max Retry Times: 5
           Interval Seconds: 120
           Policy Sets: []
         ```
         

   * **Submit subcommand**

      * The CLI side will pre\-check the filled CPU/memory, allowing only the CPU/memory combination visible to the user when submitting tasks on the front end of the platform.

      * Do not allow **non\-flexible matching users who have been whitelisted** to submit using the **flexible matching method** , and an error will be intercepted when submitting.

         * Allow **flexible matching users who have been whitelisted** to submit the **non\-flexible matching method** before use, and after submission, it will be automatically converted to the corresponding flexible matching method according to the Flavor specified in the original method.

   * **Export subcommand**

      * Supports the export of tasks that specify resources in the "Flexible Matching Mode".


<span id="已知问题"></span>
# known issues


1. After granting whitelist access, the newly submitted load (only likely to be submitted by cli) will be smaller than the original.

2. After granting whitelist access, there may be some incompatibility when users use the original yaml file to submit tasks in the mixed queue. It is recommended to use a new task submission method.

3. Due to the statistical problem that the queue has applied for quotas, the Quota of the existing queue will become smaller.

   * During this period, there may be an existing queue over\-Quota.

   * Existing queued tasks may have Quota but queued (users can resubmit this task in the new flexible matching method).

   * Because the stock queue Quota becomes smaller, there may be a stock load that does not necessarily mention this queue.
