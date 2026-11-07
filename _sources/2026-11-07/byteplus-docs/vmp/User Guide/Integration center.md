---
title: "Integration center"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/integration-center"
---

Vital Managed Service for Prometheus (VMP) supports quick cloud service integration through the integration center. This topic describes the primary features and common operations of the integration center.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<span id=".5LuA5LmI5piv6ZuG5oiQ5Lit5b-D"></span>
### What is the integration center

The integration center is provided by VMP for cloud service integration. In the integration center, you can create integration tasks and configure collector hosting and service discovery to quickly integrate cloud services such as ECS into VMP.

The integration center mainly provides the following features:


* Provides a list of services that support integration to help you quickly add integration objects.

* Supports custom service discovery to automatically discover target objects. It allows you to specify parameters such as collection interval, timeout, metric URI path, and port number.

* Allows you to edit, view, and delete integration tasks, and view the target list.


<span id=".5Yib5bu66ZuG5oiQ5Lu75Yqh"></span>
## Create an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation panel, click **Integration Center \> Component**.

4. Click the cloud service for integration and click **Create Integration Task**. Configure the integration task to achieve cloud service integration.


<span id=".5p-l55yL6ZuG5oiQ5Lu75Yqh"></span>
## View the integration task

After you configure an integration task, you can view the details of the integration task.


1. In the left navigation panel, click **Integration Center \> Integration Task**.

2. In the **task list**, click the name of the target task to view the configurations of the integration task.


<span id=".5YGc55So6ZuG5oiQ5Lu75Yqh"></span>
## Suspend an integration task

You can suspend an integration task if you do not need it temporarily.


1. In the left navigation panel, click **Integration Center** \> **Integration Task**.

2. In the **task list**, find the target task. Click **Suspend task** in the **Actions** column to disable the integration task.


<span id="TUNofirJ"></span>
## Start an integration task


1. You can restart an integration task that has been disabled.

2. In the left navigation panel, click **Integration Center** \> **Integration Task**.

3. In the **task list**, find the target task. In the **Actions** column, click **Start task** to start the integration task.


<span id=".57yW6L6R6ZuG5oiQ5Lu75Yqh"></span>
## Edit an integration task

After you configure an integration task and the task runs as expected, you can modify the configurations of the integration task.


1. In the left navigation panel, click **Integration Center** \> **Integration Task**.

2. In the **task list**, find the target task. Click **Edit** in the **Actions** column to edit the integration task.


<span id=".5Yig6Zmk6ZuG5oiQ5Lu75Yqh"></span>
## Delete an integration task

If you do not need to monitor a specific monitoring target, you can delete the corresponding integration task.


1. In the left navigation panel, click **Integration Center** \> **Integration Task**.

2. In the **task list**, find the target task. Click **Delete** in the **Actions** column, and click Delete in the message that appears to delete the integration task.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you delete the integration job, the corresponding VMP workspace will not be deleted at the same time.</div>
