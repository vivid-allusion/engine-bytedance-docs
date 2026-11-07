---
title: "Create pipelines using YAML"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_pipeline_via_YAML"
---

Continuous Delivery supports creating pipelines using the YAML method. This article introduces the top\-level structure of pipeline YAML, as well as the meaning, usage, and value specifications of each parameter, helping you define the pipeline's source, stage, task, step, and reusable component in a one\-off, code\-based manner, and manage pipelines through version control.

<span id="RbaJzTte"></span>
## Background

Pipeline as Code converts pipelines visually orchestrated in the console into structured YAML files, supporting review, audit, gray\-scale reuse, and cross\-project migration.


* **code source (sources)** : Declare the pipeline trigger source and materials, defining the pipeline's source and trigger method.

* **stage (stages)** : Sequentially define key delivery gates, such as build, test, deploy, and other process nodes.

* **task (tasks)** : A collection of tasks within a single stage that can be executed in parallel or serially, defining the work to be performed in the same stage.

* **step (steps)** : The minimum execution unit within a task, defining the specific execution process for each work item.

* **component (component)** : Atomic capability encapsulation that can be reused across pipelines; business steps can be standardized by referencing components.


<span id="Dd2wPDKc"></span>
## Prerequisites

The service connection has been created. For action details, see [code source integration](https://docs.byteplus.com/en/docs/cp/Integrate_code_source).

<span id="RKofkO4l"></span>
## Procedure

<span id="3BzRuftg"></span>
### Step 1: Enter the YAML editing entry


1. Log in to the [Continuous Delivery console ](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace**. On the workspace page, click the target workspace name to enter the current workspace.

3. Click **Create pipeline \> YAML editing**.

4. Click **Confirm** to enter the YAML configuration page for the current pipeline.


<span id="o362FmMt"></span>
### Step 2: Write the pipeline

According to the YAML syntax section, sequentially complete source, stages, tasks, steps, and the optional component. For detailed description, see [YAML syntax](https://docs.byteplus.com/en/docs/cp/YAML_syntax).

A minimum runnable pipeline YAML skeleton example is as follows:

```YAML
version: 2.0.0
agentPool: public/prod-v2-public
sources:
  - name: service-connection-demo
    type: Gitee
    url: https://gitee.com/volc-code-pipeline/demo.git
    branch: master
    credential:
      type: serviceConnection
      serviceConnectionId: <your-service-connection-id>
stages:
  - stage: build
    displayName: build
    tasks:
      - task: cmd-exec
        displayName: command execution
        steps:
          - step: exec-cmd
            displayName: command execution
            component: exec@1.0.0
            inputs:
              shell: BASH
              cmd: echo hello
        resourcesPolicy: all
        timeout: 2h
        resources:
          limits:
            cpu: 1C
            memory: 2Gi
```


<span id="cwiY6hfb"></span>
### Step 3: Validation and save


1. Click **Validation** at the lower right of the editor. Continuous Delivery will perform YAML syntax, schema, and reference integrity validation.

2. After validation passes, click **Save** to finish creation.
