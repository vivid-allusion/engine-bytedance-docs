---
title: "Integrating server-side applications from third-party clouds"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Integrating_server-side_applications_from_third-party_clouds"
---

In addition to integrating server\-side applications in VKE, the integration center provides multi\-cloud integration capabilities, allowing server\-side applications in third\-party cloud environments to be integrated into Server\-side Monitoring for management. This topic uses a Go application in a Tencent Cloud container cluster as an example to describe how to integrate a server\-side application from a third\-party cloud environment into Server\-side Monitoring.

<span id="nNJzJMRT"></span>
## Prerequisites

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For workload configuration in different third\-party cloud environments and methods for obtaining key information such as cluster_id, refer to the official documentation of the corresponding cloud vendor.</div>



* Make sure that public network access is enabled for the cluster in the third\-party cloud environment to ensure normal configuration delivery during the multi\-cloud integration process.

* Pod labels or annotations have been configured in the workload of the application to be integrated for easier application filtering.


<span id="tIwneMFz"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Integration Center currently supports server\-side applications of the Go, Java, Node.js, and Python types. Except for the default Pod filtering rules, all other integration steps are identical. This topic uses a Go application as an example.</div>


* <div data-tips="true" data-tips-type="default">The methods for connecting to a container cluster and restarting workloads may vary across different third\-party cloud environments. Refer to the official documentation of the respective cloud vendor for details.</div>



<span id="HH4BUOkw"></span>
### Step 1: Install the probe

Configure the key parameters and obtain the probe installation command, then connect to the third\-party cloud container cluster and execute the probe installation command to install the probe. For details, see the installation instructions for third\-party cloud container probes in the [Probe management](https://docs.byteplus.com/en/docs/Observability_Platform/Probe_management) section.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After the probe is successfully installed, wait 3 to 5 minutes before monitoring data can be collected normally.</div>


<span id="wjdvAAzM"></span>
### Step 2: Configure the integration task


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select ** Integration Center \-\> Integration marketplace**.

3. In the **Backend Application** category, click **Go**.

4. On the **Third\-party cloud** tab, configure integration parameters as needed and then click **Create integration task**.

   
   |Parameter |Description |
   |---|---|
   |Cloud vendor |Select the cloud provider to which the application belongs. Currently, Tencent Cloud, Huawei Cloud, Alibaba Cloud, AWS, and self\-built Kubernetes are supported. |
   |Region |Select the region to which the application belongs after being connected to Server\-side Monitoring. |
   |Access protocol type |Select the protocol type used to connect the application to Server\-side Monitoring. Currently, OpenTelemetry is supported. |
   |workspace |Select the workspace to which the application belongs after being connected to Server\-side Monitoring. |
   |Cluster |Select the container cluster where the application to be integrated is running. |
   

5. Configure the integration task parameters and click **Confirm**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The parameter configuration requirements for third\-party cloud integration tasks are identical to those for VKE integration tasks. For detailed configuration instructions, see: <a href="https://docs.byteplus.com/en/docs/Observability_Platform/Integrating_server-side_applications_in_VKE">Integrating server\-side applications in VKE</a>.   </div>
   

6. After completing the integration task configuration, go to the source platform's container cluster and restart the corresponding workload for the configuration to take effect for data collection.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The redeployment operation restarts all Pods managed by the Deployment. We recommend performing this operation during off\-peak hours.   </div>
   

<span id="k3t2JYA3"></span>
## Validate results

After the workload is redeployed, go to the [Server-side Monitoring](https://console.byteplus.com/observe/apmplus-server) console. On the Services page, search for the service by container name and check the data reporting status. **Normal** indicates that data was reported successfully recently.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">By default, the service name is the same as the container name defined in the workload.</div>


<span id="5uk1eIcO"></span>
## What to do next


* After an integration task is created, you can go to the Integration management page to view and manage the task. For details, see[ Integration management](https://docs.byteplus.com/en/docs/Observability_Platform/Integration_management).

* After an integration task is created, you can go to the probe management page to view the probe and probe details. For details, see [Probe management](https://docs.byteplus.com/en/docs/Observability_Platform/Probe_management).
