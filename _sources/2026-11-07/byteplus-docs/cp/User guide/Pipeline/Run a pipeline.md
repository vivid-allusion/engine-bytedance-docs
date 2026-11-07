---
title: "Run a pipeline"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Run_a_pipeline"
---

Code Pipeline supports [code source trigger](https://docs.byteplus.com/en/docs/cp/Trigger_from_code_source), [scheduled trigger](https://docs.byteplus.com/en/docs/cp/Scheduled_trigger), [webhook trigger](https://docs.byteplus.com/en/docs/cp/General_webhook_trigger), and manual trigger. You can select the appropriate method to trigger the pipeline based on your specific use case. This article introduces the procedure for manually triggering pipeline execution.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* You can run a pipeline by specifying a branch, tag, or commit ID. Please select as needed.

* Termination is supported at any time during pipeline execution. After termination, currently running tasks are canceled immediately, and tasks that have not started will not be executed.

* After a task in the pipeline fails to run, the pipeline stops running. Supports retrying from failed tasks; preceding tasks that have already run successfully will not be executed again, which improves pipeline efficiency.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The pipeline has been created. For specific operations, refer to [Create a Pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. Select **workspace** in the left navigation bar.

3. Click the name of the target workspace to enter that workspace.

4. Select **pipeline** in the left navigation bar to enter the **pipeline** page.

5. Select the target pipeline, click **Run**, and the **Run Pipeline** dialog box appears.

6. Enter the following parameters as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |code source |Display the code source used by this pipeline.<br><br>Further configuration of the pipeline code retrieval method is required. The pipeline supports retrieving code by branch, tag, or commit ID. Please select as needed.<br><br><br>* **Branch**: A branch consists of a series of commits. Pulling code by branch is the most common method. If you want to pull code from a specific branch, select or enter the branch name.<br><br>* **Tag**: A tag points to a specific commit and is commonly used to mark a particular version. For example, to pull the code for version V2.0, you can select or enter V2.0.<br><br>* **Commit ID**: A Commit ID is the ID of a specific commit. If you want to pull code based on a specific Commit ID, please enter the Commit ID. |
   |Variable |If your pipeline has dynamic variables configured, you can set their runtime values here. |
   |Operation description |Add remarks for this run; this field can be left blank. |
   

7. Click **confirm**. The pipeline starts running, and the system navigates to the details page of the current pipeline.

   * The page updates the running status in real time.

   * When multiple tasks are running, the page displays the current progress in real time.

   * After a successful run, you can view outputs, run logs, and other related content. For more information, refer to [view run details](https://docs.byteplus.com/en/docs/cp/View_run_details).

8. (Optional) Terminate pipeline execution

   1. On the pipeline details page, click **Terminate**. A confirmation dialog appears.

   2. After confirming the pipeline information, click **Confirm** to terminate the pipeline.

9. Optional retry on failure

   1. On the pipeline details page, select the task card for a failed run, click **Retry**, and a confirmation dialog appears.

   2. Click **confirm**, the pipeline starts executing from the current failed task.
