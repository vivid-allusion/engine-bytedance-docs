---
title: "Limitations"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Limitations"
---

Certain unintended operations during your use of the AI Data Lake Service LAS (hereafter referred to as LAS) may cause some functions to become unavailable. To avoid such issues, please read this document carefully and familiarize yourself with the following limitations.

1. When accessing the LAS console, use **Google Chrome 36.0 or later**. For the best console experience, Google Chrome 100.0 or later is recommended.

2. Once the LAS product is activated, it cannot be deactivated. However, you will not incur additional fees unless you purchase new resources or execute tasks.

3. Do not perform the following actions to avoid making some product functions unavailable.

|High\-risk operations |Possible outcomes |Recommendations |
|---|---|---|
|Manually deleting the image associated with a "running development machine / task" in the image repository |1. The task being executed will fail immediately;<br><br>2. The development machine will encounter errors when restarting or starting up |It is strictly prohibited to manually delete the associated image of running resources. To clean up images, first confirm that the corresponding development machine / task has stopped. |
|Manually deleting the listener / backend service group configured for a "running development machine" in the load balancing configuration |The development machine cannot log in via SSH |Avoid modifying the load balancing configuration of a running development machine. To make adjustments, first stop the development machine service. |
|Directly pulling a public image larger than 10 GB when starting a development machine / executing a task |The development machine startup times out, and task execution initialization fails |First upload large images to the BytePlus official image repository, then pull the image from the repository to start resources to improve stability |
|When saving a development machine as an image, the data stored on the cloud disk exceeds 30 GB |1. The time required to save the image increases significantly;<br><br>2. Saving may fail (such as due to timeout or resource limitations) |Routinely store unnecessary files (such as logs and temporary data) in shared storage, and retain only the core data required for the image to control cloud disk usage. |
|Perform deletion or downgrade operations on queues that have 'running jobs' or 'development machines in operation' |1. Result calculation for running jobs or workflows may be abnormal;<br><br>2. Periodically scheduled jobs or workflows may fail to trigger;<br><br>3. The development machine may suddenly be interrupted or malfunction |1. Before deletion or downgrade, stop all running jobs and development machines in the queue;<br><br>2. Confirm that periodically scheduled tasks are paused, then adjust the queue |
|Delete job or workflow definitions that have 'running instances' |1. Running tasks may become unresponsive or terminate abnormally;<br><br>2. Historical execution results cannot be queried (associated records are lost after the definition is deleted) |Wait until all instances have completed execution before deleting the job or workflow definition; for urgent cleanup, terminate running instances and back up the results first |
|Delete TOS, vePFS, or NAS storage resources bound to tasks or development machines |Tasks or development machines cannot access storage data, resulting in execution interruption or errors |1. Bound storage resources must be managed in sync with the lifecycle of tasks or development machines; confirm that resources are unbound before deletion;<br><br>2. Avoid directly deleting storage resources that are in use |
|When using the A10 GPU model, use the storage mounting feature |When performing TOS mounting and Vepfs mounting, trunk ENI may be missing |It is not recommended to use the storage mounting feature on this model |
|When the number of data partitions is extremely large (for example, more than ten thousand), reading a large number of partitions in a single operation |The server enforces request limits and directly rejects the read operation |SQL queries must include partition conditions (such as filtering by time or region), read data in batches, and reduce server load |
|Directly modify the TOS bucket policy associated with the LAS dataset in the TOS console |The permissions of the associated LAS dataset become invalid, making it impossible to read or write data |To adjust the TOS bucket policy, first confirm that the bucket is not associated with any LAS dataset; if already associated, unbind the dataset before modifying the policy |
|If you directly delete or damage the original files under the path corresponding to the LAS dataset in the TOS console, |This will result in the loss of dataset data. It will be impossible to query or use the data (the data cannot be recovered). |It is strictly prohibited to directly access, modify, or delete files in the TOS file path corresponding to the dataset. To clean up data, use the dataset management feature in the LAS console to avoid accidental deletion. |
