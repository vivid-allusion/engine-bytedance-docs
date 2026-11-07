---
title: "Autoscaling overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Autoscaling-overview"
---

The autoscaling feature is widely used in cloud computing resource services. Typical scenarios include online workloads, large\-scale computing and training tasks, GPU\-accelerated deep learning tasks, model inference and model training tasks that use shared GPUs, and regular and periodical workload changes. Cluster autoscaling comprises two dimensions:


* Resource layer elasticity: refers to node autoscaling. When a cluster's capacity planning cannot meet its scheduling capacity, scale out resources to replenish capacity. Options include Elastic Compute Service (ECS) or Vital Container Instance (VCI) resources.

* Scheduling layer elasticity: refers to workload autoscaling. The scheduling capacity of a workload is modified by adding application workload replicas. For example, Horizontal Pod Autoscaler (HPA) is a typical elastic add\-on running on the scheduling layer. It adjusts the number of application replicas, changing the scheduling capacity occupied by the workload. This achieves scheduling layer elasticity.


The following table describes the autoscaling feature supported by both the resource layer and the scheduling layer in VKE clusters.


|Solution name |Solution introduction |Related documentation |
|---|---|---|
|Cluster Autoscaler |Cluster nodes are automatically scaled based on the pod scheduling status and resource usage through [Cluster Autoscaler (CA)](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler) or Karpenter. This ensures that the basic resources of clusters can meet business requirements. |* [Configuring node autoscaling based on CA](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler)<br><br>* [Configuring node instant autoscaling based on Karpenter](https://docs.byteplus.com/en/docs/vke/Configure_node_instant_autoscaler_Karpenter) |
|Workload autoscaling |HPA: a metric\-based workload autoscaler that automatically scales pods in a workload based on pod metrics such as pod CPU utilization, memory utilization, GPU video memory utilization, and network throughput.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">HPA can also perform autoscaling based on custom metrics.</div><br> |* [Achieving autoscaling by using CPU and memory metrics](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler)<br><br>* [Achieving autoscaling by using GPU and network metrics](https://docs.byteplus.com/en/docs/vke/Using-GPU-metrics-for-autoscaling)<br><br>* [Achieving autoscaling by using custom metrics](https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling) |
||CronHPA: automatically scales workloads at specified time points, which is suitable for scenarios where application resource utilization changes cyclically. |[Creating CronHPA](https://docs.byteplus.com/en/docs/vke/Creating-a-CronHPA) |
||IHPA: By using historical and predicted workload data, IHPA generates resource profiles and time\-based resource views of workload replicas and resources (such as CPU and memory utilization). IHPA accurately adjusts the number of workload replicas to promptly respond to changes in business workloads based on data. |[Creating IHPA](https://docs.byteplus.com/en/docs/vke/Create_an_Intelligent_Horizontal_Pod_Autoscaler) |
