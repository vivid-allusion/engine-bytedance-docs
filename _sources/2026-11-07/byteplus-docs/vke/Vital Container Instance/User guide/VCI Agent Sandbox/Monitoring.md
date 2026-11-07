---
title: "Monitoring"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring"
---

This topic mainly describes the metrics supported by the sandbox in VCI Agent Sandbox.

<span id="R9xnhPmk"></span>
## Metrics

The sandbox instances in VCI Agent Sandbox provide related performance metrics through VCI monitoring capabilities. For detailed descriptions, see [VCI monitoring](https://docs.byteplus.com/en/docs/vke/VCI-Monitoring).

<span id="UQtw7pKK"></span>
## Supported metrics


|**Category** |**Metric** |**Metric description** |**Type** |**Tag** |**Value** |
|---|---|---|---|---|---|
|**Workqueue** |workqueue_depth |The number of pending tasks in the current workqueue. |Gauge |name |* containerimagecommit<br><br>* sandbox<br><br>* sandboxclaim<br><br>* sandboxsnapshot<br><br>* sandboxwarmpool |
||workqueue_queue_duration_seconds |The period of time a task waits in the queue to be processed. |Histogram |name |* containerimagecommit<br><br>* sandbox<br><br>* sandboxclaim<br><br>* sandboxsnapshot<br><br>* sandboxwarmpool |
||workqueue_work_duration_seconds |The time from retrieving a task from the queue to completing processing. |Histogram |name |* containerimagecommit<br><br>* sandbox<br><br>* sandboxclaim<br><br>* sandboxsnapshot<br><br>* sandboxwarmpool |
||workqueue_adds_total |The total number of events processed by the workqueue. |Counter |name |* containerimagecommit<br><br>* sandbox<br><br>* sandboxclaim<br><br>* sandboxsnapshot<br><br>* sandboxwarmpool |
|**Resource usage (Controller)**  |process_resident_memory_bytes |The resident memory usage of the Controller process. |Gauge |\- |No |
||process_cpu_seconds_total |The total CPU time consumed by the Controller process. |Counter |\- |No |
||go_goroutines |The number of Goroutines. |Gauge |\- |No |
|**VKE API call** |transport_request_duration_in_seconds_count |The total number of requests sent to the underlying VKE API. |Counter |action, status_code |Specific called VKE API |
||transport_request_duration_in_seconds_bucket |The distribution of response latencies for VKE API calls. |Histogram |action, status_code |Specific called VKE API |
|**Sandbox business metrics (Business)**  |sandbox_transition_latency_seconds_bucket |The latency of sandbox lifecycle transitions (start and stop). |Histogram |transition_type |* Start<br><br>* ShutDown |
||sandbox_snapshot_completion_latency_seconds_bucket |The period of time taken to complete snapshot creation. |Histogram |\- |No |
||container_image_commit_completion_latency_seconds_bucket |The period of time taken to complete the image commit. |Histogram |\- |No |
||sandbox_snapshot_long_running_count |The number of times that the duration of snapshot reconciliation exceeded 15 minutes. |Counter |namespace |No |
