---
title: "Node Failure Notification and Load Migration Guide"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Node_Fault_Notification_and_Load_Migration_Guide"
---

After a node fails, load evacuation will be completed within 48 hours. After evacuation is completed, we will immediately repair the node where the load is located.

To provide you with a better service experience, you need to complete the evacuation of development machines or custom tasks within 48 hours as much as possible to ensure your running tasks are not lost. Thank you for your cooperation!

<span id="邮件通知"></span>
# Email Notification

When your load is detected on a node that needs to be taken offline, we will notify you via email of the names and IDs of the involved development machines or custom tasks to help you complete the evacuation quickly. .

<span id="操作指南"></span>
# Action Guide

<span id="重启正在运行中的开发机"></span>
### Restart running development machines


1. After receiving the email notification, enter the main page of the machine learning platform, and via the left navigation bar, access 「Training & Inference」 \- 「Development Machine」

2. The email notification sent to you contains the name and ID of the development machine that needs to be turned off Based on this, you can search by name or ID on the right side of 「All」 or 「Created by Me」 to find the development machine that needs to be turned off

3. Click the 「Shut Down」 button in the Actions column After the development machine is turned off, click 「Start Up」 and your task will be automatically scheduled to run on a normal node


<span id="复制自定义任务"></span>
### Copy Custom Task


1. Enter the main page of the machine learning platform, and via the left navigation bar, access 「Training & Inference」 \- 「Custom Task」

2. The email notification sent to you contains the name and ID of the custom task that needs to be turned off Based on this, you can search by name or ID on the right side of 「All」 or 「Created by Me」 to find the custom task that needs to be turned off

3. Click the 「Stop」 button in 「···」 of the Actions column Click the "Copy" button, and your task will be automatically scheduled to run on a normal node.


<span id="迁移推理服务"></span>
### Migrate Inference Service

Under normal circumstances, when a machine fails, the online service will migrate automatically: create a new instance and delete the old instance running on the faulty machine. Only when the quota in the queue is insufficient, new instances cannot be created due to quota restrictions, and you need to manually clean up the queue quota and migrate instances.


1. The email notification sent to you contains the name and ID of the inference service that needs to be migrated. Based on this, you can search by name or ID on the right side of "All" or "Created by Me" to find the corresponding inference service.

2. In the "Actions" column of the "Instance List", click "Migrate", and your task will be automatically scheduled to run on a normal node.
