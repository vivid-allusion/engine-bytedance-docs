---
title: "Automate Tasks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/automate-tasks"
---

Automated tasks are tasks that are automatically triggered at regular intervals. Through this function, you can set a specified time to automatically trigger script tasks, agent tasks, or intent planning engine tasks, and support the configuring webhook channels to receive task execution results. Upgrade the reactive agent to active execution. This article describes how to use the Automated Tasks feature.

# New task

1. Log into the Marketing Agent console and, at the top of the left navigation bar, select **Marketing Interactive Assistant**.

2. In the left navigation bar of the Marketing Interactive Assistant, select **Automate Tasks** \> **Task List**.

3. At the top right of the task list, select **Create manually**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c6a2461df7e47db82d83942f72d22b5~tplv-goo7wpa0wc-image.image)

4. Go to the **New Automation Task** page and complete the following configuration:

   * **Basic information**

      * Task name: Required, custom name, identifies the current task.

      * Description: Optional, you can fill in the specific description of the task.

      * Enable: The switch is used to control whether to enable or disable the current task, and the default is on.

   * **Scheduling strategy**

      * Scheduling Type Select **Interval:**  You need to configure the number of seconds in the interval to trigger the task according to the period of the number of seconds in the interval.

      * Scheduling type Select **Cron:**  You need to configure the Cron expression to trigger the task according to the Cron expression cycle.

      * Scheduling type selection **One\-time:**  You need to configure a specific execution time, and the task will be triggered after the arrival time.

   * **Task content**

      * Task Type Select **Script Task:**  You need to configure the script (lifecycle hook) to build the actions to be performed at each stage of the task lifecycle by modifying the default Python code.

      * Task type Select **agent task:**  You need to select the agent in turn, and write the message or instruction input to the agent after triggering the task.

      * Task Type Select **Intent Planning Engine:**  You need to select the intent planning engine in turn, and write the message or instruction input to the intent planning engine after triggering the task.

      * When the task type is an **agent task** or **intent planning engine** , you can choose to configure the channel to receive the task execution results through the webhook channel. For how to configure channels, see [configure channels](https://docs.byteplus.com/docs/dataagent/124543#ec1dad7d).

   * **Advanced Options**

      * Timeout seconds: Set the task timeout, the default is 600 seconds.

5. (Optional) Only if the task type is a script task, you can click **practice run** in the upper right corner of the page to debug the results of the script run.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a64a8d8838cc4cf2a6eae1d5ab3bcdef~tplv-goo7wpa0wc-image.image)

6. After confirming that the content is correct, click **Save** in the upper right corner of the page.

   After the task is saved, it can be viewed in the task list.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b926c67980e54f71a00a8a076f779654~tplv-goo7wpa0wc-image.image)

# Execute a task

Manually execute in the left navigation bar **Automation Tasks** \> **Task List**.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05ad2daad6894d938ca32ac7e2df113d~tplv-goo7wpa0wc-image.image)

After manual execution, you can view the execution log in the left navigation bar **Automation Tasks** \> **Execution Log**.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3df6a4ddf62d4211a6a32a839b6cb348~tplv-goo7wpa0wc-image.image)

# Task management operation instructions

In the left navigation bar **Automation Tasks** \> **Task List** , support viewing, editing, copying, enabling, disabling and deleting tasks.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9edc812194f40418ecf49e1f2af2814~tplv-goo7wpa0wc-image.image)

|**Operation** |**Description** |
|---|---|
|View |Click **View** in a task **operation** column to jump to the task details page to view the task specific configuration information. |
|Edit |Click **Edit** in a task **operation** column to modify the task configuration.<br><br>> **注意**<br><br><br>> Only disable task support for editing configuration items.<br> |
|Copy |Click **Copy** in a task **operation** column to quickly copy a new task, and modify existing configuration items during replication is supported. |
|Enable/disable |* Click **Enable** in the **Deactivated** task **Operation** column to enable the task.<br><br>* In the **Enabled** status task **Operation** column, click **Deactivate** to deactivate the task. |
|Delete |Tasks can be deleted by clicking **Delete** in the Tasks **Operation** column that are no longer needed.<br><br>> **注意**<br><br><br><br>* > Only deactivating tasks supports deletion.<br><br><br>* > Once the task is deleted, it cannot be restored. Please proceed with caution.<br> |

# View execution history

1. Log into the Marketing Agent console and, at the top of the left navigation bar, select **Marketing Interactive Assistant**.

2. In the left navigation bar of the Marketing Interaction Assistant, select **Automated Tasks** \> **Execution Log**.

3. On the **Execution Logs** page, view the execution logs of various tasks.

   * At the top of the page, support for setting task ID, status, time period filter criteria for filtering tasks.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/996eeb9cc91e40c088b17e272836e90a~tplv-goo7wpa0wc-image.image)

   * In the task list, display the task's ID, name, status, start and end time, time elapsed, and number of retries.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c07d522656e45d79148462571d30e45~tplv-goo7wpa0wc-image.image)

4. Click **Details** in a task operation column to view detailed data on the execution of the task, including information such as run ID, task ID, task name, trigger type, log, and output data.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/900c0cb813014320888da2b908729e2a~tplv-goo7wpa0wc-image.image)

# Configure channels

You can configure a three\-way webhook channel, and when the task type is **an agent task** or an **intent planning engine**, you can optionally configure the channel to receive task execution results through the webhook channel.

1. Log into the Marketing Agent console and, at the top of the left navigation bar, select **Marketing Interactive Assistant**.

2. In the left navigation bar of the Marketing Interactive Assistant, select **Automated Tasks** \> **Channel Configuration**.

3. In the upper right corner of the **channel configuration** page, click **New Configuration**.

4. On the New Channel Configuration page, complete the following configuration.

   |**Configuration item** |**Description** |
   |---|---|
   |Basic information |* Configuration name: Required, custom name, identifies the current channel.<br><br>* Description: Optional, a detailed description of the current channel.<br><br>* Enable: The switch is used to control whether the current channel is enabled or disabled, and the default is on. |
   |Webhook Settings |Fill in the HTTP webhook URL, required. |
   |Request settings |* URL Parameters: Optional, click  **+ Add Parameters** to add URL parameters. String values support `{{answer}}`placeholders, which are replaced at runtime with agent replies.<br><br>* Headers: Optional, request header parameters, click  **+ Add Header** to add header parameters.<br><br>* Request body: Optional, custom request body parameters. Only POST/PUT/PATCH is valid. Supports `{{answer}}`placeholders, replaced by agent reply at runtime.<br><br>* Timeout: in seconds, default is 5. |
