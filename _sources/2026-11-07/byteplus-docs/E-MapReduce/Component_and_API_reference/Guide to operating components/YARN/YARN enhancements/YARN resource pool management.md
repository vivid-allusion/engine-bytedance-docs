---
title: "YARN resource pool management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/YARN_resource_pool_management"
---

The Volcano Engine E\-MapReduce (EMR) console supports visual management of Node Labels (that is, resource pools) for YARN cluster queues, and allows you to allocate Node Label resources to different queues, including Node Label resource settings, queue capacity settings, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is an enhanced capability of the YARN component in EMR\*\*, and all configurations can be achieved by manually modifying the YARN configuration file.\*\*</div>


<span id="f7636316"></span>
## Prerequisites


1. Only supports creating one sub\-level for YARN queues, for example: root.level1.

2. Only supports the YARN Capacity Scheduler.


<span id="8ddf204b"></span>
## Usage instructions

<span id="56108247"></span>
### Enable resource pool management


1. In the **Service Management \> YARN \> Service Operations** dropdown, select the **Enable Node\-Label** option.

2. After selecting, you can configure queues to run on resource groups composed of specified instance sets.


<span id="6f23c2e0"></span>
### Create a resource pool


1. Click the **Service Management \> YARN \> Create Resource Pool** button to open the resource pool creation page.

2. Enter the resource pool label.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Resource pool tags are equivalent to Node\-Label names.</div>



3. Associate queues

   1. The system lists all current leaf queues. Selecting a queue will direct the queue's submitted resources to the corresponding resource pool.

   2. Selecting the resource percentage for a queue specifies the minimum percentage of the resource pool that the queue must use.

   3. Selecting the maximum resource percentage for a queue is optional. If not specified, the queue can only use the corresponding resource pool up to the minimum percentage. If specified, it indicates the maximum percentage of the resource pool that the queue can use when resources are available.

4. Resource pool node groups

   1. The system lists all instances under the CORE and TASK node groups. Any instance can be selected to form a resource pool.

   2. An instance can only be selected in one resource pool.


<span id="544be659"></span>
### Manage resource pools


1. Resource pool list

   1. Associated resource pools will display resource summary, instance details, associated queues, and other information in the list.

   2. Editing resource pools is allowed, including modifying queue parameters or instance associations.

   3. Deleting resource pools is allowed. The resource pool and its corresponding relationships will be deleted.

2. Default resource pool

   1. After resource pool management is enabled, resources that are not assigned to any resource pool will be displayed in a fixed Default resource pool, which cannot be edited.
