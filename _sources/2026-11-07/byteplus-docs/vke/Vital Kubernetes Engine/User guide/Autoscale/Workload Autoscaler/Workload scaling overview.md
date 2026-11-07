---
title: "Workload scaling overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-Workload-Autoscaler-works"
---

Workload scaling refers to the modification of the scheduling capacity of a workload by adding the number of application workload replicas. This topic describes the workload scaling solutions and principles in VKE clusters.

<span id=".5pa55qGI5LuL57uN"></span>
## Solution introduction

VKE supports the workload scaling solutions described in the following table.


|Solution name |HPA |CronHPA |IHPA |
|---|---|---|---|
|Solution overview |[Horizontal Pod Autoscaler](https://kubernetes.io/zh-cn/docs/tasks/run-application/horizontal-pod-autoscale/) |CronHPA functions as a preset task, which can execute specified scaling rules at specified times. This automatically scales out or scales in computing resources to meet business requirements and control costs. |Intelligent Horizontal Pod Autoscaler (IHPA) is provided by the internal AI algorithm team of the BytePlus cloud\-native team based on the time series prediction algorithm. IHPA can generate resource profiles and time\-based resource views of workload replicas and resources (such as CPU and memory utilization) based on historical and predicted workload data. IHPA accurately adjusts the number of workload replicas to promptly respond to changes in business workloads based on data. |
|Scaling criteria |* Resource metrics such as CPU, memory, GPU, and network<br><br>* Custom metrics |The time period, such as specific time points each hour, each day, each week, or each month. |* Performs prediction and learning based on resource metrics such as CPU and memory, and generates resource views that reflect changes over time.<br><br>* Automatically scales resources based on resource views. |
|Application scenarios |HPA is suitable for online services that include a large number of pods and require frequent scaling to handle traffic fluctuations, such as e\-commerce services, online education, and financial services. |CronHPA is suitable for services that have fixed traffic patterns and scenarios where you need to run applications at a scheduled time. |IHPA can automatically identify the pattern of workload fluctuations and predict resource demand based on historical metric data to implement predictive scaling, which reduces the impact of native HPA scaling delay on business operations. |
|Related documentation |* [Achieving autoscaling by using CPU and memory metrics](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler)<br><br>* [Achieving autoscaling by using GPU and network metrics](https://docs.byteplus.com/en/docs/vke/Using-GPU-metrics-for-autoscaling)<br><br>* [Achieving autoscaling by using custom metrics](https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling) |[Creating CronHPA](https://docs.byteplus.com/en/docs/vke/Creating-a-CronHPA) |* [IHPA overview](https://docs.byteplus.com/en/docs/vke/Intelligent_Horizontal_Pod_Autoscaler_overview)<br><br>* [Creating IHPA](https://docs.byteplus.com/en/docs/vke/Create_an_Intelligent_Horizontal_Pod_Autoscaler) |


<span id=".5oqA5pyv5Y6f55CG"></span>
## Technical principles

<span id=".5oyH5qCH5Ly457yp"></span>
### HPA

The Horizontal Pod Autoscaler (HPA) is used in Kubernetes clusters for automatically scaling Pods horizontally. It dynamically adjusts the number of Pods in workloads such as Deployments and ReplicaSets based on metrics like CPU and memory utilization, GPU and GPU memory usage, and network throughput.

A HPA is implemented as a Kubernetes API resource and a controller. The behavior of the controller is determined by resources. The controller periodically obtains metrics such as CPU and memory utilization, GPU and GPU video memory utilization, and network throughput, and compares the obtained metric values with the target values to make corresponding adjustments to the number of replicas in Replication Controllers or Deployments.

HPA is implemented as a control loop, and the loop cycle is specified by the `--horizontal-pod-autoscaler-sync-period` flag in the controller manager.

The process in each cycle is as follows:


* The controller manager queries the user\-defined **expected metrics** of resources in HPA.

* In addition, the controller manager obtains the **current resource metrics** of each pod based on the resource metrics API (with the metrics server being its implementation).

* The HPA calculates the scaling proportion based on the **current metric** and the **expected metric**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The formula is as follows: <strong>Expected number of replicas = ceil [Current number of replicas × (Current metric/Expected metric)]</strong>. Here, ceil refers to rounding up the value to the nearest integer.   </div>
   

   For example:

   * Assuming the current CPU metric is `200` millicores and the expected metric is `100` millicores, since `200.0/100.0 = 2.0`, the replica count will double.

   * Assuming the current CPU metric is `50` millicores and the expected metric is `100` millicores, since `50.0/100.0 = 0.5`, the replica count will halve.

   * If the calculated scaling proportion is close to 1, specifically when `|scaling ratio - 1.0| <= tolerance value` based on the Kubernetes HPA calculation method, the scaling operation will not be performed. The default tolerance value in the community edition is 0.1, which is the globally set value of the `--horizontal-pod-autoscaler-tolerance` parameter.


HPA can be configured with one or multiple target metrics. When configured with a single target metric, the desired number of replicas is calculated by summing the current metric values of all Pods, dividing by the target value, and rounding up. For example, consider a Deployment with 3 Pods whose CPU usage is 70%, 50%, and 90% respectively. If the HPA target CPU utilization is set to 50%, the desired number of replicas is calculated as (70 + 50 + 90) / 50 = 4.2, which rounds up to 5.

If you configure multiple expected metrics, calculate the expected number of replicas for each one. Use the maximum value as the final expected number of replicas.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">HPA does not apply to objects that cannot be scaled, such as DaemonSets.</div>


<span id=".5a6a5pe25Ly457yp"></span>
### CronHPA

The Cron Horizontal Pod Autoscaler (CronHPA) functions as a preset task, which can execute specified scaling rules at specified times. This automatically scales out or scales in computing resources to meet business requirements and control costs.

CronHPA is suitable for scenarios where workloads change regularly over time, such as flash sales in e\-commerce. The flash sales in e\-commerce start at a fixed time point. In this case, you can use the CronHPA feature to automatically scale out workloads during specified time periods to ensure that the whole system runs as expected.

<span id=".aHBhLeWSjC1jcm9uaHBhLeWFvOWuueaAp-ivtOaYjg=="></span>
## Description of HPA and CronHPA compatibility

The YAML definition for CronHPA is as follows:

```yaml
apiVersion: vke.volcengine.com/v1alpha1
kind: CronHPA
metadata:
  name: nginx-cronhpa
  namespace: default
spec:
  crons:
  - schedule: CRON_TZ=Asia/Shanghai 1 1 * * *
    target: 1
  scaleTargetRef:
    kind: HorizontalPodAutoscaler
    name: nginx-hpa
  scaleWorkloadRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx
status: {}
```


Based on the preceding definition of CronHPA, you can discover that:


* CronHPA knows the values of `minReplicas`, `maxReplicas`, and `desiredReplicas` in HPA.

* CronHPA knows the current value of `Relicas` that corresponds to `scaleTargetRef` in HPA.

* CronHPA adjusts the number of workload replicas by preferentially adjusting HPA.

* CronHPA compares the desired and current replica counts and takes the larger value. It then determines if scale\-in or scale\-out is needed, and whether to adjust HPA's upper limit.

* CronHPA determines whether to modify the lower limit of HPA by comparing the desired number of replicas and the configured number of replicas for HPA and taking the lower value.


Therefore, CronHPA is compatible with HPA in the following rules:


|HPA (min/max) |CronHPA |Workload replica |Scaling result |Description of compatibility rules |
|---|---|---|---|---|
|1/10 |5 |5 |* HPA (min/max): 1/10<br><br>* Workload replicas: 5 |When the target replica count in CronHPA equals the current count, you don't need to modify HPA's maximum/minimum replica counts or the current application replica count. |
|1/10 |4 |5 |* HPA (min/max): 1/10<br><br>* Workload replicas: 5 |When the target number of replicas in CronHPA is less than the current number of replicas, retain the current number of replicas. |
|1/10 |6 |5 |* HPA (min/max): 6/10<br><br>* Workload replicas: 6 |When the target replica count in CronHPA is higher than the current replica count, keep the CronHPA target count. If the target replica count exceeds the HPA minimum replicas (minReplicas), update the HPA minReplicas. |
|5/10 |4 |5 |* HPA (min/max): 4/10<br><br>* Workload replicas: 5 |When the target number of replicas in CronHPA is less than the current number of replicas, retain the current number of application replicas. When the target number of replicas in CronHPA is less than the minimum number of HPA replicas (minReplicas), modify the minimum number of HPA replicas. |
|5/10 |11 |5 |* HPA (min/max): 11/11<br><br>* Workload replicas: 11 |When the target replica count in CronHPA exceeds the current count, retain that target number. When the target replica count in CronHPA exceeds HPA's maxReplicas, adjust HPA's maximum replicas. |
