---
title: "View cluster status"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Cluster_status"
---

This document describes the possible states that may occur during the lifecycle of a Volcano Engine E\-MapReduce (EMR) cluster, as well as how to handle abnormal states.


|Cluster status |Note |
|---|---|
|Initializing |The cluster is being created and initialized. Please wait patiently. |
|Initialization failedFailed |The cluster failed to initialize for some reason. Please recreate the cluster. |
|Running |The cluster is running. You can submit and run jobs. |
|Pending payment |The cluster is awaiting payment after order confirmation. |
|Shut down |The cluster has expired and is in the shutdown period. Please renew promptly, otherwise the cluster will be automatically released. |
|Releasing |The cluster is being released. Please wait patiently. |
|Recovering |The cluster is being restored for use after timely renewal during the shutdown period. Please wait patiently. |
|Released |The cluster has been successfully released and can no longer be used. |
