---
title: "View the batch operation task list"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/View-batch-operation-task-list"
---

When uploading, downloading, copying, or deleting objects in bulk, a list of successful and failed tasks is generated after completion. The default storage folder is the `defaultOutputDir` parameter in the configuration file. This article introduces the file formats generated under the folder.

<span id="文件格式"></span>
## File format

```Plain
${command}_${succeed|failed}_${task_id}_YYYYMMDDHHmmSS.txt

# For example:
# cp_succeed_d77636b8-c414-423f-8d9c-2a29e61c5ff7_20220527162239.txt represents the task list of a successful cp command executed at 16:22:39 on May 27, 2022. The task_id is a UUID generated for each batch operation, which in this example is d77636b8-c414-423f-8d9c-2a29e61c5ff7.
```
