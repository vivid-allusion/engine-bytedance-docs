---
title: "Managing workflows"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-workflows"
---

The Workflow page is your central dashboard for monitoring statistics, reviewing execution logs, and managing the lifecycle of all your automated workflows.

<span id="23ba80c6"></span>
# Prerequisites

You have already created at least one workflow. For instructions, see [Creating workflows](https://docs.byteplus.com/docs/sealsuite/creating-workflows).

<span id="349fb151"></span>
# **Viewing Workflow Statistics**


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Enterprise Settings** \> **Workflow**.

3. The **Workflow** page provides a high\-level overview and a detailed list of your workflows.

   * **Dashboard Analytics:** 

      The top of the page displays key statistics, including the total number of enabled workflows, total processed objects, and total tasks triggered. A donut chart visualizes the status distribution of all workflow runs.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2576f3fc5f442519eda22505dc30d5c~tplv-goo7wpa0wc-image.image) </span>

   * **Workflow List and Filters:** 

      Use the filters to find specific workflows by **Template Type**, **Status** (Enabled/Disabled), **Name**, or **Date**. The list displays key information for each workflow, and you can use the toggle switch in the **Action** column to enable or disable them.


<span id="2d0cb517"></span>
# **Viewing workflow details**


1. Log in to the Admin Console.

2. Go to **Enterprise Settings** \> **Workflow**.

3. Click the name of a workflow in the list to open its details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f427b8fe206f4b7cbb0acfd96eb1da5d~tplv-goo7wpa0wc-image.image) </span>

4. The details page contains two main tabs:

   * **Basic Information**

      This tab provides a summary of the workflow's configuration.

      
      |**Section** |**Field** |**Description** |
      |---|---|---|
      |**Basic Information** |Workflow name |The name of the workflow. |
      ||Total run |The total number of times this workflow has been executed. |
      ||Last run time |The timestamp of the most recent execution. |
      ||Next run time |For scheduled workflows, this shows the next planned execution time. |
      ||Last modified by |The administrator who last edited the workflow. |
      ||Scope |The users, devices, or conditions this workflow applies to. |
      ||Description |The workflow's description. |
      ||Trigger event |The event that initiates the workflow. |
      |**Task Configuration** |/ |A summary of the automated tasks configured within this workflow. |
      

   * **Run History Tab:** 

      This tab provides a detailed log of every time the workflow has been executed.

      1. Filter the history by **Start Time**, **End Time**, **Request ID**, or **Status**.

      2. Review the list, which shows the start/end times, status, and a summary of the tasks performed.

      3. In the **Action** column for a specific run, you can:

         * Click **View Tasks** to see a detailed breakdown of each step in that execution.

         * Click **Cancel** to stop a workflow that is currently in progress.


<span id="28d88cc5"></span>
# **Editing and deleting a workflow**


1. Log in to the Admin Console.

2. Go to **Enterprise Settings** \> **Workflow**.

3. Click the name of the workflow you want to manage.

4. From the top\-right corner of the details page, you can:

   * **Delete:**  Permanently remove the workflow.

   * **Edit:**  Modify the workflow's configuration.

   * **Enable/Disable:**  Use the toggle switch to activate or deactivate the workflow.


<span id="755dcd60"></span>
# **Managing individual tasks in a workflow run**


1. Log in to the Admin Console.

2. Navigate to the **Processing History** tab for a specific workflow.

3. Find the workflow you want to inspect and click **View Tasks** in its row.

4. On the task details page, you can:

   * Review the status and details of each individual task.

   * Pause or restart specific tasks if needed for troubleshooting.
