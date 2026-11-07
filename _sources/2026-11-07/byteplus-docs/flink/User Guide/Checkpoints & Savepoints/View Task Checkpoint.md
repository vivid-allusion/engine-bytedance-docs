---
title: "View Task Checkpoint"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/View_Task_Checkpoint"
---

If your Flink job has Checkpoint configuration enabled, it will automatically create Checkpoints based on parameters such as Checkpoint interval and Checkpoint timeout once it is running properly. You can view the list of Checkpoints on the Flink UI.

<span id="8aba393e"></span>
## View Checkpoint


1. Log in to the [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, then click on the project block to enter the project.

4. In the project's left navigation bar, select **Task Operations \> Compute Task Management**.

5. On the task list page, click the **Actions** column’s **Flink UI** button for the target task.

   The browser will automatically open the Web UI page, where you can view the details of the task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5169f319be984fc49d2db9e739ce7a1c~tplv-goo7wpa0wc-image.image) </span>

6. In the **Jobs \> Running Jobs** section of the Flink UI, click on the job name.

7. In the **Checkpoints \> History** section of the job details, view the list of Checkpoints.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d58b05c4852c4c71a0bb6e25b4756277~tplv-goo7wpa0wc-image.image) </span>
