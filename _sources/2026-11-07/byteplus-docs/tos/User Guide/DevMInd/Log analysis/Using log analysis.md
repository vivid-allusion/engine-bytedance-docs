---
title: "Using log analysis"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Using-log-analysis"
---

This topic explains how to use the log analysis feature, including how to enable and disable it.

<span id="lq3b11OM"></span>
## Enabling log analysis

You can enable log analysis for a bucket using one of the following methods:


<Tabs>
<Tab zoneid="Z2IYzvny3G" title="From DevMind">
<TabTitle>From DevMind</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the **DevMind** page, click **Log analysis** in the left navigation pane.

4. Click **Kanban configuration**, and locate the bucket you want to manage on this page.

5. Turn the switch on in the **log analysis** column of the bucket.

6. In the **Enable log analysis** dialog box, click **Open**.


</Tab>
<Tab zoneid="vMrQdKPckE" title="When creating a bucket">
<TabTitle>When creating a bucket</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. Then, in the upper\-left corner of the displayed page, click **Create bucket**.

3. On the **Create bucket** page, expand **Advanced settings**, and turn on the **Log analysis** switch.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on other parameters when creating a bucket, see <a href="https://docs.byteplus.com/docs/tos/docs-create-a-bucket">Creating buckets</a>.   </div>
   


</Tab>
<Tab zoneid="JDTrfEZNpG" title="For an existing bucket">
<TabTitle>For an existing bucket</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, click **Logging**. Then, on the **Log analysis** tab, click **Edit**.

6. Turn on the switch and click **Select**.


</Tab>
</Tabs>


<span id="yApny1Ec"></span>
## Disabling log analysis

You can disable log analysis for a bucket using one of the following methods:


<Tabs>
<Tab zoneid="bdgD7zuPHi" title="From DevMind">
<TabTitle>From DevMind</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **DevMind**.

3. On the **DevMind** page, click **Log analysis** in the left navigation pane.

4. Click **Kanban configuration**, and locate the bucket you want to manage on this page.

5. Turn the switch off in the **log analysis** column of the bucket. Log analysis is disabled for this bucket when the switch turns gray.


</Tab>
<Tab zoneid="mEsOQa8d15" title="From the bucket details page">
<TabTitle>From the bucket details page</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, click **Logging**. Then, on the **Log analysis** tab, click **Disable associated logging**.

6. In the box that appears, click **Disable**.


</Tab>
<Tab zoneid="BTOdGnHFs2" title="Related operations">
<TabTitle>Related operations</TabTitle>

Disabling log analysis will not automatically delete the associated Torch Log Service (TLS) topic. To avoid continued log\-related charges, delete the topic in the TLS console first.

When you proceed to disable log analysis on the **Logging** page, a box will appear with the project and topic IDs corresponding to the bucket. You can use these IDs to locate and delete the topic associated with the bucket. For instructions, see [Topics](https://docs.byteplus.com/en/docs/tls/Managing_topics#.5Yig6Zmk5pel5b-X5Li76aKY) and [Delete a project](https://docs.byteplus.com/en/docs/tls/Managing_projects#.5Yig6Zmk5pel5b-X6aG555uu).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<span id="4byltLIz"></span>
### <div data-tips="true" data-tips-type="warning">Since all buckets in the same region share one topic, deleting a bucket's topic will also delete the historical log records of other buckets in that region. For more information, see <a href="https://docs.byteplus.com/docs/tos/Why-cant-the-logging-function-be-used">Why does deleting a bucket's topic cause other buckets' log functions to stop working?</a></div>



</Tab>
</Tabs>


<span id="ORsH1I0f"></span>
## Setting the log retention period


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, click **Logging**. Then, on the **Log analysis** tab, click **Set log retention time**.

6. In the box that appears, specify the days and click **Set**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The data retention period can be set anywhere from one day to 3,650 days.   </div>
