---
title: "Alert configuration overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_alerts"
---

VKE provides comprehensive cluster monitoring and alert capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). The capabilities cover typical scenarios such as the control plane, nodes, networks, workloads, and AI training tasks. This topic describes configuration methods, alert levels, and configuration recommendations for cluster alerts in production environments.

<span id="1OU8vL2s"></span>
## Configuration method

VMP provides various preset alert rule templates. You can use these templates to quickly create alert rule groups. You can also customize alert rules based on PromQL statements according to your business needs, or export preset template YAML files, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. The following table describes the definitions and applicable scenarios of each configuration method.


|Configuration method |Application scenarios |References |
|---|---|---|
|Using preset templates |The system provides preset alert rule templates for common scenarios, such as initial setup and quick establishment of a cluster alert baseline.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For detailed information about preset VKE alert templates, see <a href="https://docs.byteplus.com/en/docs/vke/Preset_alert_templates">Preset alert templates</a>.</div><br> |[Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_through_preset_templates) |
|Configure alerts through custom templates |* You need to modify the default threshold or duration in a centralized manner.<br><br>* You need to delete rules that do not apply to the current cluster.<br><br>* You need to supplement specific business labels, routing policies, and variable scopes.<br><br>* You need to reuse standardized alert solutions for multiple clusters or environments. |[Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en) |
|Custom alert rules |* Monitor specific namespaces, business Pods, key APIs, or tenants.<br><br>* Define metrics such as the latency, error rate, and saturation based on your business SLIs/SLOs.<br><br>* Incorporate internal SOPs, on\-call tiers, and dedicated notification routing. |[Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en) |


<span id="BSWkKe5l"></span>
## **Alert levels**

VMP alert templates define different alert levels. We recommend mapping these alert levels to your on\-call or escalation policy based on your business scenario.


|Alert levels |Description |
|---|---|
|P0 |High\-priority faults. They typically indicate that a component is unavailable, a severe error has occurred, or immediate action is strongly recommended. |
|P1 |Critical anomalies. They typically indicate a significant performance drop, an increase in error rate, or that key resources are approaching their limits. |
|P2 |General alerts. They are typically used for risk reminders, identifying abnormal trends, or early warnings. |


<span id="MUXvd1ud"></span>
## Configuration recommendations


* **General clusters for production environments**: We recommend enabling the templates for VKE control plane components, VKE workloads, VKE nodes, VKE DNS services, VKE CNI components, VKE CSI components, and VKE Ingress\-Nginx to cover the cluster's core components, nodes, and network.

* **GPU/RDMA training clusters**: In addition to the general templates, enable VKE AI training tasks and VKE AIOps service templates. This focuses on monitoring GPU utilization, RDMA link quality, and training task exceptions.

* **General suggestions for alert management**:

   * Send notifications through different channels by environment (such as development, pre\-release, and production environments).

   * Configure escalation notifications for P0 alerts via phone calls, SMS, or IM.

   * Regularly export the YAML files of templates for version archiving and optimize thresholds and durations based on actual alert noise.
