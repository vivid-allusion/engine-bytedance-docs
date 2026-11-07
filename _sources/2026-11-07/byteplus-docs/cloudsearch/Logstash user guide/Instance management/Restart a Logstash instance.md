---
title: "Restart a Logstash instance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Restart_a_Logstash_instance"
---

This article describes how to manually restart a Logstash instance or node in the Cloud Search console.

<span id="ykKqzPul"></span>
## Prerequisites

A Logstash instance has been created and is in the **Running** state. For specific steps, refer to [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

<span id="qaPmJ0tf"></span>
## Operation steps


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the upper\-left corner of the top menu bar, select the project and region where the Logstash instance is located.

3. In the left\-side navigation pane, select **Data Processing** \> **Logstash**.

4. On the Logstash Instances page, click **Restart** in the **Actions** column for the target Logstash instance.

5. In the dialog box that appears, set the following parameters and click **OK**.

   
   |**Parameter** |**Note** |
   |---|---|
   |Action type |Select to restart an **instance** or a **node** based on your business requirements. |
   |Select nodes |When **Action type** is set to **Node**, select the nodes to restart as required. |
   |Restart mode |Select **Restart** or **Force restart** as required.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Select <strong>Restart</strong> to restart nodes one by one. Select <strong>Force restart</strong> to restart all nodes at the same time.</div><br> |
   |Set concurrency |When **Action type** is set to **instance** and **Restart mode** is set to **Forced restart**, you can set the concurrency percentage. |
   

6. Click **OK**. The Logstash instance or node starts to restart, and **Restarting.**  is displayed in the **Status** column.
