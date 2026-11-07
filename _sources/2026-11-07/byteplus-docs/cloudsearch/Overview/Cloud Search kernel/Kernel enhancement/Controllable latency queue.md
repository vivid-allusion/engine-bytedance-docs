---
title: "Controllable latency queue"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Controllable_latency_queue"
---

<span id="4b2cfb05"></span>
## Problem phenomenon

In a certain business scenario, the instance's daily processing capacity is around 1100 QPS, with CPU utilization at approximately 50%.

When request volume surges to 1500 QPS, latency spikes from 150ms to near\-total timeouts within minutes, causing request queuing, 100% CPU utilization, and complete service degradation.<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acbb506b2c9e4361b1b1bfe6bd0793e8~tplv-goo7wpa0wc-image.image) </span>

When request volume increases from 1100 QPS to 1500 QPS (a 40%~50% QPS growth, or less), why don't latency and CPU utilization rise proportionally, but instead approach a near crash? Under ideal conditions, requests within the instance's original processing capacity should succeed, with only additional requests failing. Why do nearly all requests fail?

<span id="167849ee"></span>
## Problem analysis

The key contributing factors are **internal queue backlog** and **excessive thread contention** within the instance.

Example:

If the processing capacity is 1300 QPS but the incoming requests total 1500 QPS, then 200 requests accumulate each second.

The instance's default queue size is 1000. In this example, the queue becomes saturated within 5 seconds. At this point, the instance scales threads up to CPU core\*1.5 (upper limit) to process queries, which causes CPU utilization spikes.

High CPU load, numerous threads, and thread contention collectively result in per\-request latency spikes (multiple times higher than usual), further degrading overall cluster throughput.

<span id="3446a5ff"></span>
## Solutions

For requests dequeued from the instance's internal queue, search\-related requests will be aborted if their queuing time exceeds the threshold (default: 10s) instead of being executed.

Here are the reasons for the decisions above:


* The upstream process has already timed out.

   For example, the processing time for a daily request is 200ms, but under 100% CPU utilization, the request time increases to 1s. Processing the entire queue requests will take approximately more than 20 minutes, rendering further operations non\-viable.

* To facilitate rapid cluster recovery.

   A 20+ minute queue recovery time is generally unacceptable for many businesses. In such cases, a full instance restart becomes the only viable quick recovery option, despite its significant operational overhead. Dropping timed\-out requests from the queue constitutes the optimal recovery strategy.


Support dynamic updates to the timeout in the search queue. The command is as follows:

```Plain
PUT _cluster/settings
{
    "persistent": {
        "thread_pool.search.queue_wait_timeout":"30s"
    }
}
```


<span id="17fe90ee"></span>
## FAQs

[Submit a ticket](https://console.byteplus.com/workorder/create/?step=1) if you encounter unresolved issues when performing updates to controllable latency queue time\-out parameters.
