---
title: "Manage pipelines"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Manage_pipelines"
---

This topic describes how to manage pipelines, including stopping, editing, copying, and deleting pipelines.

<span id="TrdtwLZd"></span>
## Prerequisites


* A Logstash instance has been created and is in the **Running** state. For more information, refer to [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

* A pipeline has been created in the Logstash instance. For more information, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline).


<span id="w3KFXQBv"></span>
## Edit a pipeline


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation pane, select **Data Processing** \> **Logstash**.

3. On the Logstash Instances page, click the name of the target instance to go to the **Basic Information** tab.

4. In the left navigation pane, select the **Pipeline Management** tab.

5. In the **actions** column for the target pipeline, click **edit**.

6. In the **Edit Pipeline** panel, modify the pipeline configuration, and then click **Save and Deploy**.


<span id="w5zYwUG4"></span>
## Copy a pipeline


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation pane, select **Data Processing** \> **Logstash**.

3. On the Logstash Instances page, click the name of the target instance to go to the **Basic Information** tab.

4. In the left navigation pane, select the **Pipeline Management** tab.

5. In the **actions** column for the target pipeline, select  **...**  \> **Copy**.

6. In the **Copy Pipeline** panel, modify the pipeline configuration as needed, and then click **Save** or **Save and Deploy**.


<span id="HxX8AmgS"></span>
## Stop a pipeline

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The pipeline to be stopped is deployed and in the <strong>Running</strong> state.</div>



1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation pane, select **Data Processing** \> **Logstash**.

3. On the Logstash Instances page, click the name of the target instance to go to the **Basic Information** tab.

4. On the left, select the **Pipeline Management** tab.

5. In the **Actions** column of the target pipeline, click **Stop**.

6. In the Stop Pipeline dialog box, click **Confirm**.


<span id="X00543Id"></span>
## Delete a pipeline

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The pipeline cannot be recovered after it is deleted, and running pipelines will be interrupted. Confirm the action.</div>



1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation pane, select **Data Processing** \> **Logstash**.

3. In the Logstash Instances list, click the name of the target instance to go to the **Basic Information** tab.

4. On the left, select the **Pipeline Management** tab.

5. In the **Actions** column for the target pipeline, select  **...**  \> **Delete**.

6. In the Delete Pipeline dialog box, confirm the pipeline information and click **Confirm**.
