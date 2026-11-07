---
title: "IHPA overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Intelligent_Horizontal_Pod_Autoscaler_overview"
---

Intelligent Horizontal Pod Autoscaler (IHPA) performs workload scaling based on data and provides fine\-grained management of the number of resource replicas. This effectively addresses the latency issue in resource scaling performed by traditional HPA based on a fixed schedule during sudden traffic spikes. HPA performs replica scaling on a scheduled basis.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta·Apply for Trial</strong></a>]: This feature is currently at the beta stage. Submit an application if you need to use it.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Traditional workload autoscalers in Kubernetes clusters mainly consist of Horizontal Pod Autoscaler (HPA) and Cron Horizontal Pod Autoscaler (CronHPA). The following table describes the drawbacks and limitations of both approaches.


|Autoscaling method |Main drawback |
|---|---|
|HPA |The number of replicas is adjusted based on changes in workload metrics, which indicates that scaling is always triggered after service changes. This means service availability risks arise when the values of metrics spike. |
|CronHPA |* You need to manually specify the scaling time and the number of replicas for each workload. When a large number of workloads exist, the cost and complexity are high.<br><br>* CronHPA cannot automatically detect business changes. Therefore, you also need to perform manual adjustment, which lacks flexibility. |


<span id=".5pm66IO95Ly457yp"></span>
## IHPA

<span id=".5qC45b-D6IO95Yqb"></span>
### Core capabilities

To address the pain points of HPA and CronHPA, the BytePlus cloud\-native team integrates the time series prediction algorithm provided by the internal AI algorithm team to provide the O&M\-free Intelligent Horizontal Pod Autoscaler (IHPA) feature that can perform scale\-out in advance based on prediction results. By using historical and predicted workload data, IHPA generates resource profiles and time\-based resource views of workload replicas and resources (such as CPU and memory utilization). IHPA accurately adjusts the number of workload replicas to promptly respond to changes in business workloads based on data.

<span id=".5bqU55So5Zy65pmv"></span>
### Application scenarios

IHPA applies to the following scenarios:


* **Resource scaling latency during sudden business traffic spikes**: Scaling is triggered based on actual business resource usage. Before the replica scaling is complete, there is a delay before business traffic can be handled, causing pending business requests.

* **Resource waste or insufficiency when specifying the number of workload replicas based on workload peaks and troughs**: Frequent manual intervention is required when the business exhibits periodical resource usage fluctuation. This means you have to manually scale replicas based on changes in business traffic, which is not only labor\-intensive but also risks resource waste or insufficiency.
