---
title: "Scheduled trigger"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Scheduled_trigger"
---

Code Pipeline supports configuration of scheduled trigger rules at the minute level, enabling pipelines to be triggered periodically. A pipeline supports configuring multiple scheduled triggers. This article explains how to configure scheduled trigger rules.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The pipeline has been created. For detailed steps, see [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Use any of the following methods to access the add trigger panel.

   * Edit a pipeline

      1. In the pipeline list, select the target pipeline, and click  **`...`**   **\> Edit** to enter the process orchestration tab of the current pipeline.

      2. In the code source & trigger panel, click **Add \> Scheduled trigger**.

   * Trigger quick access

      1. In the pipeline list, click the name of the target pipeline to go to its Run History tab.

      2. Click **trigger** to switch to the trigger tab.

      3. Click **Add trigger \> Scheduled trigger**.

2. Configure scheduled trigger rules

   
   |Configuration Item |Descriptions |
   |---|---|
   |Trigger name |Name of the custom scheduled trigger. Scheduled trigger names must be unique within the same pipeline. |
   |Configuration method |Supports two configuration methods: **form configuration** and **Crontab configuration**.<br><br><br>* Form configuration: Please select cycle time and trigger time using the visual configuration method.<br><br>* Crontab configuration: Configure using expressions. For configuration instructions, see the [official documentation](https://crontab.guru/).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Crontab expressions use UTC+8 time zone by default.</div><br> |
   |Dynamic Parameter |An optional configuration. Dynamic Parameters are used to configure the actual value of dynamic variables when a trigger initiates pipeline execution. If no configuration is provided, dynamic variables will use the default value.<br><br>Scenario example: The same pipeline is used to perform image build task(s), so that image versions produced from different branches can be distinguished. For example, when the main branch is triggered manually, the output image version is `prod-$(DATETIME)`; when the test branch is triggered on a schedule, the output image version is `test-$(DATETIME)`.<br><br>First, add the dynamic variable `image` with the default value `prod`. Then, use the dynamic variable `$(parameters.image)-$(DATETIME)` for the version of the built image. Finally, set the runtime value of `image` to `test` here, and select the test branch as the runtime branch. This enables the output image version to be `test-$(DATETIME)` when the test branch is triggered on a schedule. |
   |Notes |Enter remarks for the current trigger. This field can be left blank. |
   |Runtime branch |When a pipeline has a code source, you can configure the code branch to use at runtime.<br><br><br>* Turn on: Allows you to select the code branch used for scheduled pipeline triggers. If you want to use a non\-default branch for scheduled triggers, configure this parameter. For example, on the same pipeline, the default branch of the code source is the main branch. However, if you want to schedule the development branch to be triggered at a fixed time every Monday, and the test branch to be triggered at a fixed time every Wednesday, you can achieve this by configuring this parameter.<br><br>* Turn off: When the pipeline is triggered on a schedule, the default branch specified in the code source configuration will be used. |
   

3. Click **OK** to complete the scheduled trigger configuration.

4. If you enter through the edit pipeline entry, click **Save** in the lower right corner to save the pipeline configuration.
