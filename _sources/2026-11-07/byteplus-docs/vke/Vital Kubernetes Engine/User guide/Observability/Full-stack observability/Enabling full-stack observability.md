---
title: "Enabling full-stack observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Network-and-application-observability"
---

Full\-stack observability provides a metric collection method without code modification by using eBPF, which achieves metric and trace monitoring for cluster networks, applications, and services. This topic describes how to configure the full\-stack observability feature.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* TLS has been activated. To activate this service, log in to the [TLS console](https://console.byteplus.com/tls) and activate the service based on the on\-screen prompts.

* A **log project** has been created in TLS. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects)

* APMPlus has been activated. To activate this service, log in to the [APMPlus console](https://console.byteplus.com/apmplus/console/overview) and activate the service based on the on\-screen prompts.


<span id=".5q2l6aqk5LiA77ya5byA5ZCv6KeC5rWL"></span>
## Enabling observability

<span id="OES0lDCX"></span>
### Step 1: Enable observability


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, find the target cluster and click its name.

3. In the left navigation bar of the cluster management page, click **Observability settings** and click the **Full\-stack observability** tab.

4. In the **Network and application observability** section, click **Enable**, and configure network and application observability.

   1. **Prometheus workspace**: This section displays the VMP workspace already associated with the cluster. For details, see [Operation and maintenance configuration](https://docs.byteplus.com/en/docs/vke/Operation-and-maintenance-configuration). Click the workspace name to change the workspace in the pop\-up dialog box.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you change the VMP workspace, the workspace associated with the cluster will change. Proceed with caution.      </div>
      

   2. **Enable status check for VKE observability**: Check whether cloud\-native observability is enabled in the cluster. If this feature is not enabled, you need to enable cloud\-native observability first. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<span id=".5q2l6aqk5LqM77ya6YWN572u5o6i6ZKI"></span>
### Step 2: Configure the probe


1. **Configure Microscope Agent probe**: Click **Configuration parameters** to configure the Microscope Agent probe.

2. Specify the parameters of the probe, such as the specifications and the number of replicas.

   
   |Parameters |Description |
   |---|---|
   |Built\-in parameters |The system provides multiple preset parameters to help you quickly specify the parameters of the probe, including **Small instance type**, **Medium instance type**, **Large instance type**, and **Blank configuration**. If you select Built\-in parameters, the system automatically fills in the parameter configurations that correspond to the probe. |
   |Microscope Agent |Configure the resource requirements of the Microscope Agent add\-on, including the CPU request, CPU upper limit, memory request, and memory upper limit. |
   |OTel Collector |Configure the resource requirements and autoscaling configurations for the OTel Collector add\-on, including the CPU request, CPU upper limit, memory request, and memory upper limit.<br><br><br>* **Resource**: Configure the resource requirements of the OTel Collector add\-on, including the CPU request, CPU upper limit, memory request, and memory upper limit.<br><br>* **Autoscaler**: Configure the autoscaling settings for the OTel Collector add\-on, including the minimum number of instances, maximum number of instances, CPU utilization, and memory utilization. |
   |Microscope Operator |Configure the resource requirements of the Microscope Operator add\-on, including the CPU request, CPU upper limit, memory request, memory upper limit, and the initial number of instances. |
   

1. After you specify the parameters of the probe, click **Next: Check before deploy**. The system will automatically check whether the probe can be installed with the current cluster resource utilization. When cluster resources are insufficient, you need to first scale out the cluster.

4. Click **Submit** to complete the probe configuration.


<span id=".5q2l6aqk5LiJ77ya6YWN572u6KeC5rWL6IyD5Zu0"></span>
### Step 3: Configure the observability scope


1. In the workload list, select the workloads for which you want to enable network and application observability.

2. Click **Select label** to filter workloads by label or annotation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can use multiple labels or annotations to filter workloads. Multiple labels and annotations are in an <strong>AND</strong> relationship.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can directly click and select the corresponding label or annotation in the <strong>Label</strong> column or <strong>Annotation</strong> column of the workload list.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After configuration is complete, newly deployed workloads in the cluster will not be automatically added to the observability scope. You can also perform manual configuration.   </div>
   

3. After all configurations are complete, click **Enable** to enable network and application observability and install the managed probe.


<span id=".6YeH6ZuG6YWN572u"></span>
## Configuring collection

<span id=".6YWN572u6YeH6ZuG5oyH5qCH"></span>
### Configuring metric collection

After network and application observability is enabled, you can configure metric collection and select the network and application metrics that you need to collect.


1. In the left navigation bar of the cluster management page, click **Observability settings** and click the **Full\-stack observability** tab.

2. Find the **Network and application observability** section and click **Edit settings**. Click the **Metric** tab, and click **Edit** to configure eBPF metrics.


3. After configuration is complete, click **Confirm** to complete the metric configuration.

<span id=".6YWN572u5pWw5o2u6ZO-6Lev6YeH6ZuG"></span>
### Configuring trace data collection


1. In the left navigation bar of the cluster management page, click **Observability settings**.

2. Find the **Network and application observability** section and click **Edit settings**. Click the **Chain** tab. You can collect data traces by using APMPlus or TLS.

   
   |Parameters |Description |
   |---|---|
   |Storage settings |Configure the storage service used after trace data collection. **APMPlus** or **TLS** is supported. |
   |**Dependency check** |The system will automatically check whether the data collection storage service (APMPlus or TLS) is authorized for use and enabled. If the service fails to pass the check, check whether you have activated the storage service. |
   |**Configuring collection** ||
   |Project |If you set the **Storage settings** parameter to **TLS**, select a project from the drop\-down list. Project management is a resource management method. For details, see [Project overview](https://docs.byteplus.com/en/docs/6649/189152). |
   |Log project |If you set the **Storage settings** parameter to **TLS**, select a log project from the drop\-down list. |
   |Application protocol |Select the application protocol to enable trace collection. HTTP, HTTPS, DNS, gRPC, and Redis are supported. |
   |Slow request threshold |Configure the slow request threshold for different protocols. |
   

3. After configuration is complete, click **Confirm** to complete the trace data collection configuration.


<span id=".5o6i6ZKI6L-Q57u0"></span>
## Performing operation and maintenance on probes

After installing the probe, you can monitor, maintain, and restart it.

<span id=".5o6i6ZKI55uR5o6n"></span>
### Monitoring probes


1. In the left navigation bar of the cluster management page, click **Observability settings**.

2. Find the **Network and application observability** section and click **Edit settings**. Click the **Probe** tab to view the running status and resource usage of the Microscope\-agent and Otel Collector probes.


<span id=".6YeN5ZCv5o6i6ZKI"></span>
### Restarting probes

Click **Restart** in the **Actions** column to restart the specified probe.

<span id=".5p-l55yL5oyH5qCH5ZKM5ouT5omR"></span>
## Viewing metrics and topologies


* To view network and performance metrics, see [Resource retrieval](https://docs.byteplus.com/en/docs/vke/Resource-explore).

* To view resource topologies, see [Resource topologies](https://docs.byteplus.com/en/docs/vke/Cluster-topology).
