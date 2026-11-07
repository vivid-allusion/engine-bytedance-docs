---
title: "Monitoring"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/FAQs-about-monitoring"
---

<span id=".5L2_55So5LqR55uR5o6n5Yqf6IO977yM5piv5ZCm6Ieq5Yqo5Lya5Zyo5LqR5pyN5Yqh5Zmo5LiK6Z2i5a6J6KOFYWdlbnTvvJ8="></span>
## If I use Cloud Monitor, will an agent be automatically installed on the ECS instance?

The platform provides basic monitoring features for CPU, memory, disk, and network by default. To have a deeper understanding of the resource running status, you can install an agent process on an instance to collect metric data of the operating system.

For the method of installing the add\-on, see [Installing the monitoring add-on](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent).

<span id="932018d0"></span>
## Can Cloud Monitor monitor the GPU status of GPU ECS instances?

Yes.

<span id="d2f2e4a6"></span>
## How long is the monitoring data retained? Can I specify the retention duration?

You cannot specify the retention duration currently. The metric data storage duration varies based on different cloud products. It can be 30 days, 60 days, or 90 days. For more details, see [Cloud product monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

In the console, you can query up to 15 days of data at a time. To query data within a longer period, query data multiple times.

<span id="1dc59a35"></span>
## What do in\-band monitoring data and out\-of\-band monitoring data mean in ECS instances?


* **In\-band monitoring data**: System monitoring data, with the monitoring collector deployed in ECS instances, which is used to collect metrics directly within the operating system of the ECS instances.

* **Out\-of\-band monitoring data**: Infrastructure monitoring data, with the monitoring collector deployed outside ECS instances, which is used to collect metrics by using virtual software on the host.


To distinguish between in\-band and out\-of\-band metrics, you only need to view whether the name of a metric contains the word **out\-of\-band**. For example, out\-of\-band CPU utilization is an out\-of\-band metric.

<span id="def764da"></span>
## Is there a delay in CDN and DCDN monitoring data?

A data delay of about 7 minutes exists. This is because CDN and DCDN data must be collected from edge nodes and aggregated to the central system, and the data is collected at the minute level.
