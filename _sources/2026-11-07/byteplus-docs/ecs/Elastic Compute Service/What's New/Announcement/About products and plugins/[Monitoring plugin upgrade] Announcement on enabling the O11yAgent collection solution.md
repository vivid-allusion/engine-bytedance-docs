---
title: "[Monitoring plugin upgrade] Announcement on enabling the O11yAgent collection solution"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Monitoring_plugin_upgrade_Announcement_on_enabling_the_O11yAgent_collection_solution"
---

Dear BytePlus users,to enhance the efficiency and flexibility of monitoring data collection, BytePlus will fully adopt O11yAgent as the standard collection plugin for ECS instances to replace cloud\-monitor\-agent. We sincerely recommend that you upgrade to O11yAgent.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After this, the old collection plugin cloud\-monitor\-agent will only be maintained for existing scenarios and will not be added with new monitoring metrics.</div>


<span id="31zgn3D3"></span>
## Applicable scenarios

If you have any of the following requirements, we strongly recommend that you immediately install or upgrade to theO11yAgent collection plugin.


* You need long\-term monitoring and monitoring metric observation capability that supports sustainable iteration.

* You need to visually manage the monitoring plugin to achieve one\-click deployment and status monitoring.

* You need more monitoring metrics to increase O&M granularity, such as the metrics of "Total number of processes" and "GPU decoder usage".


<span id="eQx6qNSi"></span>
## Comparison of new and old plugins


|Plugin |Plugin name |Scope |Differences |
|---|---|---|---|
|New plugin |O11yAgent |* [Infrastructure/operating system monitoring](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data)<br><br>* [Process monitoring](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics)<br><br>* [GPU/RDMA monitoring](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) |* The plugin is a new\-generation observability data collection plugin that fully covers all monitoring metrics of cloud\-monitor\-agent. Additionally, it adds more monitoring metrics to meet your needs for higher monitoring granularity.<br><br>* The plugin provides white\-screen installation/upgrade interfaces, one\-click deployment and status monitoring, and user\-friendliness.<br><br>* It will be the default collection plugin for new ECS instances, and new monitoring metrics will only be added based on the O11yAgent plugin. |
|Old plugin |cloud\-monitor\-agent |* [TCP link monitoring](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data)<br><br>* [Infrastructure/operating system monitoring](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data)<br><br>* [Process monitoring](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics)<br><br>* [GPU/RDMA monitoring](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) |* It is currently the default collection plugin for ECS instances.<br><br>* The plugin does not provide a white\-screen operation interface and the operation is more complex than O11yAgent.<br><br>* Subsequently, the legacy plugin cloud\-monitor\-agent will only be maintained for existing scenarios, and no new monitoring metrics will be added. |


<span id="c5M0hyLE"></span>
## Impact on you

The O11yAgent collection pluginsupports all monitoring metrics of the cloud\-monitor\-agent collection plugin. The upgrade is simple, does not affect operations of your existing services, and does not require reconfiguration of alert rules. O11yAgent has more advantages than the cloud\-monitor\-agent plugin. For more information, see [Comparison of new and old plugins](https://docs.byteplus.com/en/docs/ecs/Monitoring_plugin_upgrade_Announcement_on_enabling_the_O11yAgent_collection_solution?lang=zh&TagIDs=2,288,70,69#eQx6qNSi).

If you have any questions or need assistance, please contact your account manager.

<span id="Ud5knpcb"></span>
## Installation/upgrade descriptions of collection plugin

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you install the collection plugin on an ECS instance, make sure that the instance has the cloud assistant Agent installed. Otherwise, the installation will fail and the <code>CloudAssistantNotInstalled</code> prompt message will appear. <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">Learn more</a>.</div>



|ECS instances |Recommended installation method |Installation/upgrade descriptions |
|---|---|---|
|Newly purchased ECS instances |Automatic installation |After you enable "[the newly purchased ECS instances automatically install the collection plug-in](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console#b6d8de5f)" in the Cloud Monitor console, the newly purchased ECS instances will be automatically installed with the O11yAgent collection plugin. |
|Existing ECS instances<br><br> |Global installation/upgrade |* For information about white\-screen installation or upgrade, refer to the [Globally install collection plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console#d851fa25) and [Globally upgrade collection plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console#be30c520).<br><br>* For information about script installation or upgrade, refer to the [Black-screen installation of plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_manually#.6buR5bGP5a6J6KOF5o-S5Lu2). |
