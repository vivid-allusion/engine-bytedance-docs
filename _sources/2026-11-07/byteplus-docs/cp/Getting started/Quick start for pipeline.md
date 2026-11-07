---
title: "Quick start for pipeline"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Pipeline_quick_start"
---

Code Pipeline achieves continuous integration, continuous validation, continuous build, and continuous deployment of business code through pipelines. This article walks you through the basic pipeline workflow and helps you quickly get started with continuous delivery.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

The process and core functions of the pipeline are shown in the following figure.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65bel5L2c5Yy6"></span>
### Step 1: Create a workspace

Create a workspace, that is, an independent R&D project space. After the workspace is created successfully, you can create code sources and pipelines within it. For detailed instructions, see [create workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).

<span id=".5q2l6aqk5LqM77ya5Yib5bu65Luj56CB5rqQ"></span>
### Step 2: Integrate code source

The pipeline requires access to services such as artifact repositories and code sources. You can register these services with the service connections in Code Pipeline in advance to facilitate unified management in the future. For detailed actions, see [Integrate code source](https://docs.byteplus.com/en/docs/cp/Integrate_code_source).

<span id=".5q2l6aqk5LiJ77ya5Yib5bu65rWB5rC057q_"></span>
### Step 3: Create a pipeline

Create a one\-stop delivery pipeline that aligns with R&D and operations practices, orchestrate the pipeline process, and configure the pipeline with code source, trigger, variables, Cache directory, and Notification reminders. For detailed instructions, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<span id=".5q2l6aqk5Zub77ya6L-Q6KGM5rWB5rC057q_"></span>
### Step 4: Run the pipeline

Running the pipeline enables continuous integration, testing, and deployment.


* To manually run a pipeline, see [Run a pipeline](https://docs.byteplus.com/en/docs/cp/Run_a_pipeline).

* For automatic pipeline triggering, see [trigger](https://docs.byteplus.com/en/docs/cp/Trigger).


<span id=".5pON5L2c57uT5p6c"></span>
## Action results

After the pipeline has finished running, the console will display detailed results for the pipeline, including the results for each stage, task, and step, the run logs, artifacts, task configuration information, and more. For details, see [View run details](https://docs.byteplus.com/en/docs/cp/View_run_details).
