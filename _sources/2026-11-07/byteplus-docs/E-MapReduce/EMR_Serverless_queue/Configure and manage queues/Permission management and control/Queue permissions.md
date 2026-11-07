---
title: "Queue permissions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Queue_permissions"
---

<span id="ba5800d2"></span>
## Permission overview

Queue permissions are used to restrict the permissions of different users on different queues. Currently, two roles are supported: Developer and Admin. The primary account has Admin permissions by default, and queue permissions for sub\-accounts must be granted. Currently, sub\-accounts cannot request permissions; permissions must be proactively granted by the account.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Admin users can enable <strong>Default grant usage permissions</strong> for the queue. After enabling, all users will have Developer permissions for this queue. For specific operations, please refer to: <a href="https://docs.byteplus.com/docs/E-MapReduce/Queue_permissions#101aa536">Default grant usage permissions</a>.</div>


* <div data-tips="true" data-tips-type="tip">When a user is granted permissions multiple times on a queue, the highest\-level permission is applied.</div>



<span id="bb7cc1d9"></span>
## Add permissions


1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the top menu bar, select the region and resource group according to your needs.

3. On the **Serverless** \> **Resource queue** page, click Permission management in the upper right corner.

4. On the **Queue permissions** page, click **Grant permissions** in the upper right corner. In the pop\-up window, search for and select users or user groups and roles, then click **Grant** to assign the corresponding role for the current queue to the specified users or user groups.


<span id="46f2cd6f"></span>
## Edit permissions


1. On the Queue permission page, select the relevant user, and click the **Edit** button in the operation column to edit the current permission record.


<span id="786ed498"></span>
## Delete permissions


1. On the **Queue permissions** page, select the relevant user, and click the **Delete** button in the operation column to delete the current permission record.


<span id="101aa536"></span>
## Default grant usage permissions

On the **Resource queue** page, select the queue you want to operate on, then click ⦁⦁⦁\> Enable\-Grant default permisison in sequence. After enabling, all users (including those who have not been granted permissions) will have Developer permissions for this queue.

<span id="6f9140ec"></span>
## Permission details

The details of queue permissions are as follows:


|Permission points ||Role ||
|---|---|---|---|
|**Permission name** |**Note** |**Admin** |**Developer** |
|GetQueue |Allows retrieving the status and configuration of a queue |✔️ |✔️ |
|UpdateQueue |Allows modifying the status and configuration of a queue, meaning the user can change the CPU and memory configuration of the queue, as well as enable or stop the queue |✔️ | |
|ExecuteOnQueue |Allows submitting jobs in the queue |✔️ |✔️ |
|MonitorQueue |Allows viewing current and past queries executed on the queue, as well as usage statistics for the queue |✔️ |✔️ |
|ListJob |Allow viewing all tasks in this queue |✔️ |✔️ |
|KillJob |Allow killing or deleting tasks in this queue |✔️ | |
|ModifyJob |Allow editing tasks in this queue |✔️ | |
|DeleteQueue |Allow deleting this queue |✔️ | |
|All |Allow full control over a queue, including the ability to grant permissions for it |✔️ | |
