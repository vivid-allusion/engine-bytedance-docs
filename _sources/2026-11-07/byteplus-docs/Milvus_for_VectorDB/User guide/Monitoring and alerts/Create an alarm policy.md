---
title: "Create an alarm policy"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_alarm_policy"
---

Milvus for VectorDB integrates with Cloud Monitor, allowing you to manage alarm rules by using Cloud Monitor. This topic describes how to create an alarm policy in the Milvus console.

<span id="SRkgpNIL"></span>
## Precautions

Only Dedicated and Serverless instances support creating alarm policies.

<span id="jVXgRgID"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. On the top navigation bar, select the target project and region.

3. Click **Alarm management** in the left navigation pane.

4. At the top of the page, click the **Alarm policy** tab.

5. On the **Alarm policy** page, select **Dedicated** or **Serverless** as needed, then click **Create alarm policy** to open the **Create alarm policy** page in Cloud Monitor. For more information about how to create an alarm policy, see [Create an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When you configure alarm objects on the Create alarm strategy page, select <strong>Milvus for VectorDB</strong> for Resource type.</div>


* <div data-tips="true" data-tips-type="default">Performance and Data monitoring metrics support creating alarm policies at the instance dimension, while Resource monitoring metrics support creating alarm policies at the node dimension. Collection monitoring metrics support creating alarm policies at the Collection dimension.</div>
