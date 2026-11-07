---
title: "Getting Started"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
section: "Document"
source: "https://docs.byteplus.com/en/docs/vmp/Quick-start"
---

This topic describes the basic procedure for using VMP to help you get started quickly.

<span id=".5L2_55So5rWB56iL"></span>
## Usage Process

The usage process of VMP is shown in the following figure.


1. Create a  root user and enable access to the VMP console.

2. Create a VMP workspace.

   VMP provides you with multiple types of workspaces, which you can select based on your actual needs. For details, please refer to [Workspace Types](https://docs.byteplus.com/en/docs/vmp/workspaces-types) and [Create Workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

3. Product & business access.

   VMP integrates well with the open\-source ecosystem and supports cloud\-native monitoring, along with various SDKs and Exporters provided by the open\-source community. It supports monitoring various cloud services, middleware, and custom applications through collector add\-ons, managed collectors, and other methods. For details, see [Integration overview](https://docs.byteplus.com/en/docs/vmp/Monitoring-overview).

4. View metrics.

   If you need to view specific metrics of a monitored object, you can quickly query and display metric data by using the Explore feature. For more details, please refer to [Metric Query](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

5. Monitoring dashboard.

   The system has built\-in common monitoring dashboards. Self\-built Grafana is also supported, and you can integrate metric data from Vital Managed Service for Prometheus into Grafana to achieve the goals of metric query and self\-built metric dashboards.

   * Preset dashboards: Preset VKE cluster dashboards for clusters, nodes, Pods, and GPUs. This helps you easily view common monitoring information for clusters. For details, see [Dashboard overview](https://docs.byteplus.com/en/docs/vmp/Dashboard-overview).

   * Deploy your own Grafana. For details, see [Deploying Grafana in a VKE cluster and integrating it with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster) and [Deploying Grafana on an ECS instance and integrating it with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace?lang=en).

   You can configure alerts in the system by specifying the monitoring metrics, thresholds, and alarm levels of the alert, and receive alert notifications through various methods such as email, Generic Webhook, and Feishu bot.

   * [Configuring alerts](https://docs.byteplus.com/en/docs/vmp/Alerting_overview?lang=en)

   * [Receiving alerting notifications through emails](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email)

   * [Receiving alert information by custom Larkbot](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-Lark)

   * [Receiving alert information by Feishu application robot](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot)

   * [Receiving alert information by DingTalk](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-DingTalk)

   * [Receiving alert information by WeCom](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Wecom)

   * [Receiving alerting notifications through phone calls](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone)
