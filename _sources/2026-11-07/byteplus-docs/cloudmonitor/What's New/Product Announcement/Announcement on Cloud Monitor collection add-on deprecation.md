---
title: "Announcement on Cloud Monitor collection add-on deprecation"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Cloud_Monitor_Collection_Component_Decommissioning_Notice"
---

VKE will stop providing the metrics\-collector add\-on for Cloud Monitor on October 9, 2025 (UTC+8). The add\-on installed in existing container clusters also becomes unavailable. To make sure that you can monitor container metrics as expected, use [basic container observability](https://docs.byteplus.com/en/docs/vke/Monitoring-overview) to install prometheus\-agent for metric collection. The basic container observability feature is more powerful, which achieves collection, monitoring, and alerting for metrics of clusters, basic resources, and applications.


* For details on supported container observability metrics, see [VKE metrics](https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Vital-Kubernetes-Engine).

* If you use alert rules for VKE in Cloud Monitor, you need to manually configure the corresponding alerts in VMP. For details, see [Best practices for switching alert configuration from Cloud Monitor to VMP](https://docs.byteplus.com/en/docs/vke/Best_practices_for_switching_alert_configuration_from_Cloud_Monitor_to_VMP).
