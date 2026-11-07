---
title: "Process orchestration"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Process_orchestration"
---

Process orchestration is used to define the execution order and specific content of each stage, task, and step in the pipeline. Process orchestration enables you to organically connect components such as testing, build, deployment, and process control, and define your automated delivery process. This article provides an introduction to process orchestration.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

A pipeline is divided into three levels: stage, task, and step. Stages run serially. Within the same stage, tasks support serial or parallel execution. Steps within the same task run serially.


* **Stage**: A set of tasks executed sequentially within a pipeline; stages are executed in series.

* **Task**: The specific actions that need to be completed within a stage; tasks can be executed either serially or in parallel. Code Pipeline currently includes the following categories of predefined tasks: testing, building, deployment, command execution, image build and push, process control, and more.

* **Step**: The specific step that needs to be completed within a task, executed sequentially. Steps are the core capability at the lowest level of a pipeline, and every pipeline is composed of steps that are arranged and combined.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The pipeline has been created. For specific operations, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Go to the process orchestration tab of the pipeline.

   1. Log in [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter the current workspace.

   4. Select **Pipeline** in the left navigation bar to enter the pipeline page.

   5. In the pipeline list, select the target pipeline and click  **`...`**   **\> edit**, go to the Process orchestration tab of the current pipeline.

2. Perform process orchestration on the pipeline as needed.

3. After completing the orchestration, click **Save** to save the pipeline configuration.
