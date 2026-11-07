---
title: "Celeborn FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Celeborn_FAQs"
---

<span id="3c72ad90"></span>
## How can shuffle performance be viewed when Spark jobs use Celeborn?

On the Spark UI shuffle stage page, you can check the metrics shown in the figure below. By considering shuffle write size and shuffle write time together, you can get a clear picture of end\-to\-end shuffle performance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4502838670e843b6bf191f85028f5bcc~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44b5b7a22a8c420c963031ee9af677f5~tplv-goo7wpa0wc-image.image) </span>

<span id="3abf96bf"></span>
## What causes long shuffle write time when the shuffle data volume is not large?

This is usually because Celeborn has reached a performance bottleneck. There are many possible reasons. You can check whether disk IOPS or disk bandwidth has reached its limit, and whether there are many nodes in Celeborn with prolonged PausePushData durations. Refer to the following monitoring metrics:

&nbsp;

<span id="81f384b0"></span>
### What causes excessive or prolonged PausePushData occurrences on Celeborn worker nodes?

If disk performance has not reached its bottleneck, you can appropriately increase the worker off\-heap memory based on node specifications and workload, or adjust the pause threshold:

```Plain
CELEBORN_WORKER_OFFHEAP_MEMORY=xxx
```


```Plain
celeborn.worker.directMemoryRatioToPauseReceive=xxx
```


<span id="2daab15a"></span>
### How can shuffle fetch failures be reduced?

If large jobs frequently encounter shuffle fetch failures, you can consider enabling Celeborn's multi\-replica feature when disk capacity is sufficient. Spark jobs can add the following parameters to enable it:

```Plain
--conf spark.celeborn.client.push.replicate.enabled=true
```
