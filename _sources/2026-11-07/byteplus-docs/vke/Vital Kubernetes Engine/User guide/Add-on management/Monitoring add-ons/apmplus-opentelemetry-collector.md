---
title: "apmplus-opentelemetry-collector"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/apmplus-opentelemetry-collector-add-on"
---

The apmplus\-opentelemetry\-collector add\-on is an application performance monitoring add\-on, which collects OpenTelemetry data and Prometheus metrics, and sends them to the application performance monitoring service.

<span id="UoIeg0vF"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/apmplus/apmplus-opentelemetry-collector_component_release_notes).

<span id="VWvWf9ma"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Monitoring** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |OpenTelemetry Collector Configuration |Specify the number of OpenTelemetryCollector instances in the add\-on. For more details, see [Usage specification recommendations for the apmplus-opentelemetry-collector add-on](https://docs.byteplus.com/en/docs/apmplus/Usage_specification_recommendations_for_the_apmplus-opentelemetry-collector_component). |
   |PrometheusScraper configuration |Specify the number of PrometheusScraper instances in the add\-on. For more details, see [Usage specification recommendations for the apmplus-opentelemetry-collector add-on](https://docs.byteplus.com/en/docs/apmplus/Usage_specification_recommendations_for_the_apmplus-opentelemetry-collector_component). |
   

5. Click **Confirm** to finish configuration.


<span id="PfZQWNyQ"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="uH5cAzLe"></span>
## Related documentation


* [Application performance observability](https://docs.byteplus.com/en/docs/vke/Application_performance_observability)
