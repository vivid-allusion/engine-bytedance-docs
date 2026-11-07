---
title: "Monitoring FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Monitoring-FAQs"
---

<span id="uUbKHUcN"></span>
## Why do basic monitoring and operating system monitoring show different CPU usage values in instance metric monitoring?

This discrepancy arises because CPU usage in basic monitoring excludes CPU IoWait, whereas CPU usage in operating system monitoring includes it.

<span id=".5aaC5L2V5p-l55yL5a6e5L6L55qE5bim5a6955So6YeP77yf"></span>
## How to view the bandwidth usage of an instance?

You can go to the EIP console to view bandwidth usage. For more information, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/eip/Viewing-monitoring-data).

<span id=".5aaC5L2V5omp5a655a6e5L6L5bim5a6977yf"></span>
## How do I expand the bandwidth of an instance?

You can expand the instance bandwidth by modifying the bandwidth upper limit of the EIP. For more information, see [Modifying bandwidth upper limit](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth).

<span id=".5aaC5L2V5p-l55yL5a6e5L6L55qE56OB55uY55So6YeP77yf"></span>
## How to view the disk usage of an instance?

You can access the operating system monitoring page for the target instance to view disk usage. For more information, see [Viewing the monitoring data of instance](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-monitoring-data).

<span id="9DtWp9nH"></span>
## Why is the RDMA monitoring data empty when using the exclusive mode of the RDMA network interface for container training tasks?

It might be because `/var/lib/kubelet/pod-resources/kubelet.sock` does not exist, or the connection permission is lacking, causing the virtual machine layer to be unable to retrieve the corresponding RDMA network interface information, which results in monitoring failure.

&nbsp;
