---
title: "Probe management"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Probe_management"
---

Probe management provides full lifecycle management for data collection probes in the observability system, including installing probes, viewing probe details, modifying configuration, upgrading, monitoring status, and more. These management operations ensure the stability, reliability, and trustworthiness of observability data in large\-scale distributed systems. This topic describes how to install and manage probes.

<span id="IsGSjewG"></span>
## Background

<span id="qXm00wyv"></span>
### Glossary


|Term |Description |
|---|---|
|Add\-on |A component that manages probes and acts as a controller. It is primarily used to deliver configurations to probes and is typically deployed as a Deployment in container environments. For example, the` apmplus-opentelemetry-collector `component in a VKE cluster is primarily used to deliver configurations to and manage the `o11yagent-apm-otel-collector `probe. |
|Probe |An independent component embedded in a target system to collect data. It continuously collects metrics, logs, traces, and other data without changing business logic and reports data to a monitoring storage backend. For example, the `o11yagent-apm-otel-collector` probe in server\-side applications collects metrics, logs, traces, and other data from the corresponding application and reports the data in batches to Server\-side Monitoring. |


<span id="E9dTOvEE"></span>
### Metric descriptions

The following table describes the metrics displayed on the monitoring dashboards for probes and probe instances:


|Metric |Description |
|---|---|
|CPU |The CPU usage of a probe or probe instance. This metric can be used to evaluate collector load, identify traffic spikes, and prevent computing bottlenecks caused by overload. |
|Mem |The memory usage of a probe or probe instance, which reflects the memory overhead of observability data buffers and parsing and processing logic. |
|OTEL Receiver Bytes |The number of bytes of raw data received per second by a probe or probe instance. This metric can be used to measure the total volume of data pushed from upstream services to the probe and detect sudden spikes in business instrumentation reporting. |
|OTEL Receiver Request Count |The number of reporting requests received per second by a probe or probe instance. This metric primarily reflects the request frequency of business reporting and can be used to determine whether the reporting frequency is abnormal on the business side. |
|Flush Bytes |The total outbound traffic (in bytes per second) that a probe or probe instance pushes in batches to the observability storage backend after aggregation and compression. |
|Flush Count |The number of batch reports per second by a probe or probe instance. This metric indicates the frequency of network calls that the probe makes to push data to the backend. A higher Flush Count indicates that the probe divides data into smaller batches, causing greater network request overhead. |


<span id="EWClPsdd"></span>
## Prerequisites


* Before installing a third\-party cloud container probe or host probe, ensure that you have obtained the BytePlus account AK/SK information with `APMPlusServerDataExportRolePolicy` permission, which is used to authorize the third\-party cloud for probe installation and data reporting. 

* Before installing a third\-party cloud container probe, obtain the cluster name information for the container cluster in the third\-party cloud.

* Currently, host probes can be installed only on Linux hosts running CentOS 7 series or later.

* When you use the VPC access method during probe installation, ensure network connectivity between the resources to be collected and the Observability Platform.


<span id="5Itl3lxj"></span>
## Install probes


<Tabs>
<Tab zoneid="unERP8msBU" title="BytePlus VKE probes">
<TabTitle>BytePlus VKE probes</TabTitle>

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select ** Integration center \-\> Probe Management**.

3. Click **Install probe** in the upper\-right corner, and select **BytePlus VKE ** on the Container probe tab.

4. Select the target region and complete cross\-service authorization to ensure that the Observability Platform can properly obtain VKE cluster and add\-on installation information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Cross\-service authorization needs to be configured only once. If cross\-service authorization has not been completed, follow the on\-screen instructions for configuration.   </div>
   

5. Select the target cluster to install the probe.

   * If the cluster does not have a probe installed, click **Install with one\-click** to install the latest version of the add\-on and container probe.

   * If the cluster already has a probe installed, reinstallation is not required. Additionally, click **Configuration** to navigate to the container cluster add\-on management page. On this page, you can configure deployment information for the probe instance. Click **Uninstall** to quickly uninstall the add\-on and container probe.


</Tab>
<Tab zoneid="XwP6Ty3twS" title="Third-party cloud container probes">
<TabTitle>Third-party cloud container probes</TabTitle>

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select ** Integration center \-\> Probe Management**.

3. Click **Install probe** in the upper\-right corner, and select **Third\-party cloud** on the Container probe tab.

4. Select the target region and configure parameters as needed. The installation command for the third\-party cloud container probe will be generated.

   
   |Parameter |Description |
   |---|---|
   |Integration methods |The method for a third\-party cloud application to access Server\-side Monitoring. You can select VPC access or public network access based on network connectivity and security requirements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To use VPC access, ensure the resources you want to collect are network\-connected to the Observability Platform.</div><br> |
   |Cloud provider type |The cloud provider to which the application belongs. Currently, Tencent Cloud, Huawei Cloud, Alibaba Cloud, AWS, and self\-built Kubernetes are supported. |
   |Cluster name |The name of the container cluster in the third\-party cloud where the probe will be installed. |
   |Workload type |The workload type used when you deploy the probe as a container. You can select Deployment, DaemonSet, or StatefulSet as needed.<br><br><br>* **Deployment**: Deploys probe instances via a stateless workload and supports elastic scaling of multiple replicas. This type is suitable for stateless, centralized collection scenarios, for example, APM, trace, and cluster\-level metric aggregation.<br><br>* **DaemonSet**: Deploys probe instances via a DaemonSet. This type is suitable for node logs, host monitoring, container metrics, and profiling scenarios.<br><br>* **StatefulSet**: Deploys probe instances via a stateful workload. This type is suitable for Prometheus collection scenarios. |
   |Access Key |The AK information of the BytePlus account, together with the SK information, is used to authorize the third\-party cloud for probe installation and data reporting. |
   |Secret Key |The SK information corresponding to the BytePlus account AK. |
   



&nbsp;

5. Connect to the third\-party cloud container cluster via kubectl and execute the installation command to install the probe. After the probe is successfully installed, wait 3 to 5 minutes before monitoring data can be collected normally.

   * Execute the `kubectl get pods -n o11yagent-monitor` command to view the installed probe processes. If the probe STATUS is ONLINE, the installation succeeds.

   * To uninstall an installed probe, execute the `helm uninstall o11yagent-operator -n o11yagent-monitor` command.


</Tab>
<Tab zoneid="Hp0d4AwoFF" title="Host probes">
<TabTitle>Host probes</TabTitle>

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select ** Integration center \-\> Probe Management**.

3. Click ** Install probe** in the upper\-right corner.

4. Select the target region and configure parameters as needed. The installation command for the host probe will be generated.

   
   |Parameter |Description |
   |---|---|
   |Operating system |Select the operating system of the host where the probe will be installed. Currently, Linux is supported. |
   |Cloud vendor |Select the cloud provider to which the host belongs. Currently, BytePlus, Tencent Cloud, Huawei Cloud, and self\-built hosts are supported. |
   |Integration methods |The method for the host to access Server\-side Monitoring. You can select VPC access or public network access based on network connectivity and security requirements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To use VPC access, ensure the resources you want to collect are network\-connected to the Observability Platform.</div><br> |
   |workspace |The workspace for host access to Server\-side Monitoring.<br><br>Workspaces are a data management and isolation method provided by Server\-side Monitoring. Each workspace has independent data reporting credentials and can centrally manage traces, logs, and metrics for different application ownership scenarios. |
   |Access Key |The AK information of the BytePlus account, together with the SK information, is used to authorize the third\-party cloud for probe installation and data reporting. |
   |Secret Key |The SK information corresponding to the BytePlus account AK. |
   

5. Log in to the host and execute the installation command to install the probe. After the probe is successfully installed, wait 3 to 5 minutes before monitoring data can be collected normally.

   * Execute the` o11yagentctl ps `command to view the installed probe processes. If the probe STATUS is ONLINE, the installation succeeds.

   * To uninstall an installed probe, execute the `wget -qO- https://o11yagent-registry-cn.tos-cn.ivolces.com/scripts/o11yagentd/latest/o11yagentd.sh | bash -s -- uninstall --service o11yagent_cloud` command.


</Tab>
</Tabs>


<span id="0f3W0QKt"></span>
## Manage probes


<Tabs>
<Tab zoneid="yTvKpcUUog" title="BytePlus VKE probes">
<TabTitle>BytePlus VKE probes</TabTitle>

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select **Integration center \-\> Probe management**, and then go to the **BytePlus VKE** tab under **Container probe**. Then, view the list of add\-ons associated with integration tasks.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Add\-ons in the same environment type have the same name and can be distinguished by the cluster they belong to.   </div>
   

   * **Upgrade an add\-on**: When a new version of an add\-on is released, a reminder icon will appear in the target add\-on row. Click **Upgradable** to upgrade to the latest version with one click.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The platform releases new versions of add\-ons periodically. We recommend that you upgrade regularly to access the latest features.      </div>
      

   * **Deployment configuration**: Find the target add\-on and click **Configuration** in the "Actions" column to modify its deployment settings, including deployment method, number of instances, CPU request/limit, and memory request/limit. For configuration recommendations, see [Recommended apmplus-opentelemetry-collector specifications](https://docs.byteplus.com/en/docs/apmplus/Usage_specification_recommendations_for_the_apmplus-opentelemetry-collector_component).

3. Click the name of the target add\-on. You can then view the probe(s) managed by the add\-on in the expanded section.

4. Click the name of the target probe to go to the details page of the corresponding workload and view more workload details.

5. Click **Details** in the "Actions" column to the right of the target probe to view probe details and the probe instance.

   
   |Section |Description |
   |---|---|
   |Cluster |The container cluster to which the current probe belongs. Click the cluster ID in the "Basic information" section to go to the cluster management page. |
   |Resource Configuration |The Request/Limit configuration of the current probe. Click **Edit** to modify the configuration.<br><br><br>* Request: The requested amounts of CPU and memory resources.<br><br>* Limit: The upper limits of CPU and memory resource usage. |
   |Probe Instance |Click the name of the target probe instance to go to the Pod details page corresponding to the instance and view more information. |
   ||Click **Metric** in the "Actions" column to the right of the target probe instance to view monitoring dashboards for the probe instance metrics. You can use this feature for performance analysis. For more information about metrics, see[ Metric descriptions](https://docs.byteplus.com/en/docs/314/115100#E9dTOvEE). |
   ||Click **Runtime Logs** in the "Actions" column to the right of the target probe instance to go to the log management page and view logs generated while the current probe instance is running. You can use this feature for fault analysis. |
   |Integration Task |The integration task associated with the current probe. Click the integration task name to go to the integration task configuration details page. For details, see[ Integration management](https://docs.byteplus.com/en/docs/Observability_Platform/Integration_management). |
   |Monitoring dashboard |The monitoring dashboards for metrics related to the current probe, which can be used for performance analysis. For more information about metrics, see[ Metric descriptions](https://docs.byteplus.com/en/docs/314/115100#E9dTOvEE). |
   |Runtime Logs |Go to the log page of the workload corresponding to the probe and view logs generated while the current probe is running. You can use this feature for fault analysis.<br><br> |
   





</Tab>
<Tab zoneid="cakrNvlML2" title="Third-party cloud container probes">
<TabTitle>Third-party cloud container probes</TabTitle>

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select **Integration center \> Probe management**, and then go to the **Third\-party cloud** tab under ** Container probe**. Then, view the list of probes for third\-party clouds.

3. Find the target probe and click **Upgrade** in the "Actions" column. The pop\-up window displays all available newer versions. After selecting a version, click **Confirm** to upgrade the probe to the target version.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Third\-party cloud environments cannot automatically detect new probe version releases. If you want to use the latest version, we recommend manually upgrading it by clicking "Upgrade" and regularly checking for new versions.   </div>
   

4. Click **Details** in the "Actions" column to the right of the target probe to view probe details and the probe instance. The details include basic information, probe instances, associated integration tasks, monitoring dashboard, and more.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The third\-party cloud environment probe details available are basically the same as those on the "BytePlus VKE" tab. For details, see the description in the BytePlus VKE probe section.   </div>
   


</Tab>
<Tab zoneid="I6fzPfdny2" title="Host probes">
<TabTitle>Host probes</TabTitle>

1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select ** Integration center \> Probe management**. On the **Host probe tab**, view the list of host probes.

3. Click **Details** in the "Actions" column to the right of the target probe to view probe details and the probe instance. The details include basic information, associated integration tasks, monitoring dashboard, and more.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The available host probe details are basically the same as those on the "BytePlus VKE" tab. For details, see the description in the BytePlus VKE probe section.   </div>
   


</Tab>
</Tabs>


&nbsp;
