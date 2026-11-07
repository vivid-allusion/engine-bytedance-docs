---
title: "Task resource specifications configuration"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Task_resource_specifications_configuration"
---

For resource consumption tasks that use compute power from the public resource pool, the default maximum build resource specification is 1C2G. To meet the needs of different business scenarios, the pipeline allows users to flexibly configure build resource specifications at the task level. This article introduces how to configure the build resource specifications for a task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Manual checkpoint</strong>, <strong>Kubernetes image upgrade</strong>, <strong>Kubernetes batch release</strong>, and <strong>application deployment</strong> are not resource\-intensive tasks and do not require configuring build resource specifications.</div>


* <div data-tips="true" data-tips-type="tip">Existing pipeline tasks can run normally when they have not been edited. If you re\-edit, you will need to manually select the resource specifications used by the task again.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The pipeline has been created, and tasks have been configured for the pipeline. For detailed instructions, see [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines) and [Process orchestration](https://docs.byteplus.com/en/docs/cp/Process_orchestration).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. On the pipeline's **Process orchestration** tab, click the target task card.

2. On the edit task page, scroll to the bottom of the **Advanced settings \> Resource limits** section.

3. Select the CPU and memory limits used by the public resource pool for the current task.

   Provides computing resource specifications with CPU\-to\-memory ratios of 1:2, 1:4, and 1:8, with a default minimum configuration of 1 CPU and 2 GB memory. The unit price varies depending on the resource specification. For details, see [Pipeline runtime duration billing details](https://docs.byteplus.com/en/docs/cp/Pipeline_run_duration).

4. After the configuration is complete, click **OK** to save the current task.

5. Click **Save** to save the pipeline configuration.
