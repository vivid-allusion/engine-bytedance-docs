---
title: "Start Tasks using Savepoints"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Start_Tasks_using_Savepoints"
---

When your task already has a savepoint, you can use it directly to restore (start) a task.

<span id="9cee5b00"></span>
## Start tasks using a designated savepoint

Existing Savepoints can be used in the **designated savepoint startup** method. For instructions on how to restore tasks using savepoints, please see start job.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b367c6651b44458bce96a3f0c46df8f~tplv-goo7wpa0wc-image.image) </span>

<span id="7f53c94f"></span>
## Start tasks using the latest status

Existing Checkpoints or Savepoints can be used in the **starting** **from the latest state** method. For instructions on how to restore tasks using savepoints, please see start job.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/375c6d63718e4ecda27674b73ab94c03~tplv-goo7wpa0wc-image.image) </span>
