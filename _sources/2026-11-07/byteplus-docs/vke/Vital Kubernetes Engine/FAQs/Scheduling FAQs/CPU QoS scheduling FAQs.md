---
title: "CPU QoS scheduling FAQs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CPU_QoS_scheduling_FAQs"
---

This topic describes frequently asked questions and solutions related to using CPU QoS.

### What is the relationship between CPU QoS and Kubernetes\-native QoS?

Kubernetes\-native QoS classifies resource guarantee tiers primarily based on a Pod's requests and limits. CPU QoS is a runtime CPU resource management capability used to further manage resource pools, CPU Burst, and pressure\-based eviction. CPU QoS and Kubernetes\-native QoS can be used together, but they are not equivalent. For more information related to native QoS, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/pods/pod-qos/).

### What is the relationship between CPU QoS and Pod CPU Burst?

CPU QoS is responsible for workload tiering and CPU service quality assurance, while Pod CPU Burst provides short\-term CPU elasticity when the node has spare computing capacity. Both can be enabled at the same time.

### How do I choose between shared_cores and reclaimed_cores?

shared_cores is suitable for regular online or latency\-sensitive applications. reclaimed_cores is suitable for offline, batch processing, retryable, or interruptible tasks.

### Does enabling CPU QoS require modifying application code?

No. CPU QoS takes effect on the node side. In most cases, you only need to add annotations to the workload and configure cluster\-level policies as needed.

### Does enabling CPU QoS guarantee reduced latency?

CPU QoS can reduce the impact of lower\-priority workloads competing for CPU on higher\-priority workloads. However, the actual effect still depends on the workload model, node resource utilization, Burst configuration, and eviction policies. We recommend evaluating the results by combining workload metrics with the platform's observability data.

### Will reclaimed_cores Pods always be evicted?

No. Whether a Pod is evicted depends on whether the enableSuppressionEviction switch is enabled, whether node pressure has persistently exceeded the threshold, and whether the Pod is within the scope of eviction.

### Why do Pods without QoS configuration also enter the shared pool?

The current default behavior is that Pods without `katalyst.kubewharf.io/qos_level` set are treated as shared_cores Pods. For more explicit resource governance, we recommend explicitly declaring the QoS type for critical workloads and offline tasks.

### What are the kernel requirements for enabling Overlap?

Overlap depends on CPU Idle and requires the node kernel to support the `cpu.idle` parameter. We recommend using images that support this feature, such as veLinux 2.0 (kernel 5.15/6.6). This feature cannot be enabled for kernels that do not support the `cpu.idl`e parameter, such as velinux1 5.10 and Ubuntu 20.04. For more information about node images, see [OS image overview](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).

You can check whether a node supports CPU Idle by performing the following steps:

1. Log in to the node where the Pod resides. For the login method, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Run the following command to check whether the node supports CPU Idle. Run the corresponding command based on your cgroup version.

   ```Bash
   #cgroup v1
   cat /sys/fs/cgroup/cpu/kubepods/cpu.idle
   #cgroup v2
   cat /sys/fs/cgroup/kubepods.slice/cpu.idle
   ```

### Will offline workloads affect online workloads after Overlap is enabled?

Overlap uses CPU Idle to ensure that online workloads take priority. katalyst\-agent sets `cpu.idle` to 1 for reclaimed_cores Pods, which lowers their scheduling priority:

* When a shared_cores Pod requires CPU, reclaimed_cores Pods yield their CPU resources within millisecond\-level latency.

* When a shared_cores Pod is idle, reclaimed_cores Pods can reuse that CPU capacity. This can be further combined with pressure\-based eviction policies to protect online workloads.

### Can I use In\-Place Pod Resize after enabling CPU Idle?

We recommend against using them together for the following reasons:

* When the cgroupDriver of kubelet is set to cgroupfs, In\-Place Pod Resize fails to update the `cpu.weight` or `cpu.shares` of Pods.

* When the cgroupDriver of kubelet is set to systemd, and the systemd version is earlier than 252, In\-Place Pod Resize fails to update the `cpu.weight` or `cpu.shares` of Pods.

* When the cgroupDriver of kubelet is set to systemd, and the systemd version is 252 or later, updating the `cpu.weight` or `cpu.shares` of Pods through In\-Place Pod Resize temporarily invalidates the CPU Idle of the Pods, affecting the scheduling priority of online applications.
