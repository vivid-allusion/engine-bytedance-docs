---
title: "Selectors"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Selectors"
---

Preset pipeline **Selectors** task supports determining the subsequent path of the pipeline through manual decision\-making, enhancing the pipeline's decision orchestration capabilities. This article introduces how to use selectors in the pipeline.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

**Selectors must be used in conjunction with downstream tasks in the same stage**. A downstream task is executed when its execution conditions match the manual decision options in Selectors; if they do not match, the task is not executed. This example uses selectors and two command execution tasks to describe the usage process.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

Selectors and the downstream task to be selected must be in the same stage; otherwise, the selection will not take effect.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Configure **Selectors** task.

   1. When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Task template selection **Flow control \> Selectors**.

   2. Configure the Selectors task as required. After completing the configuration, click Confirm.

      
      |Configuration Item |Descriptions |
      |---|---|
      |Task name |The default is Selectors, and custom task names are supported. |
      |Upstream task |Display the names of upstream serial tasks for the current task. Displayed as "none" when there is no upstream task.`-`. |
      |Operator |Select the decision maker for manual decision\-making. When settings include multiple decision makers, decisions can be made by any one of them. |
      |Options |Settings for selector options Support adding multiple items Option values are displayed as button names in the pipeline run details for decision makers to select.<br><br>Caution: Bind each option value one\-to\-one with the execution conditions of downstream tasks. |
      |Timeout duration |Set the automatic timeout period for Selectors task. The Selectors task automatically fails if its runtime duration exceeds the timeout period. |
      |Task output |This preset task has no output artifacts. |
      |Advanced settings |Webhook notification: Supports pushing task\-level notifications through two methods, Webhook and Lark bot, helping you stay informed about task updates. |
      

2. Configure the downstream tasks of Selectors within the same stage. After configuration is complete, click **confirm**.

   In Step 1, the Selectors configuration contains two options, so two downstream tasks need to be added. This article adds two command execution tasks and binds them one\-to\-one to the option values of selectors.

   * Add command execution 1 with `echo hello function 1` as the execution content. Then, in **Advanced settings \> Selector conditions**, select **feature 1**, and bind this task to the selector's **feature 1**.

   * Add command execution 2 with the execution content `echo hello function 2`, then in **Advanced settings \> Selector conditions**, select **feature 2**, and bind this task to the selector's **feature 2**.

3. Click **Save** to save the pipeline.


<span id=".6L-Q6KGM6K-05piO"></span>
## Operation description

When the pipeline reaches the Selectors task, it enters a waiting state, waiting for the decision\-maker to decide the execution path of the Selectors.


* Select **Feature 1**, the pipeline will execute **Execute Command 1**.

* If you select **feature 2**, the pipeline will execute **command execution 2**.

* If you select **Reject**, the pipeline will terminate execution, and the pipeline status will be failed.


As shown in the figure below, this example selects **feature 2**, the pipeline executes **command execution 2**, and successfully prints `hello function 2`.
