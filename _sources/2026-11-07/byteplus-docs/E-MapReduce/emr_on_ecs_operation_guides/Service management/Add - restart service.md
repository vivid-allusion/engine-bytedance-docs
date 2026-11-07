---
title: "Add/restart service"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs-add_or_restart_services"
---

Volcano Engine E\-MapReduce (EMR) allows you to add services that were not selected for installation during cluster creation after the cluster has been successfully created. You can also manage services in an existing cluster, including configuring service parameters, starting, stopping, or restarting services. This document describes how to add services and restart services in the EMR console.

<span id="_1-使用前提"></span>
# Prerequisites

An EMR cluster type has been created. See [Create clusters](https://docs.byteplus.com/docs/E-MapReduce/ecs_create_a_cluster_3190_and_later) for details.

<span id="d0d78f70"></span>
# Service addition entry

When creating an EMR cluster, mandatory services are installed by default. Optional services can be added and installed after the cluster creation is complete.


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the left navigation bar, click **Resources \> on ECS \> cluster name** to enter the specific cluster details page.

3. On the cluster details page, click the **Service list**tab to go to the cluster service list page.

4. Click the **Add service** button in the upper right corner of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c1d3044868b48808d5e0df3559b3eb9~tplv-goo7wpa0wc-image.image) </span>


<span id="2b2ea1f5"></span>
# Configure services and custom deployment

<span id="52b059b2"></span>
## Limits

To use the **Custom deployment** feature when **adding services**, pay attention to the restrictions in **Set deployment topology**:


* **Custom deployment**Only clusters with **service high availability** enabled are supported.

* **Custom deployment**Due to restrictions on the number of nodes, node groups, and service roles, if the conditions are not met, the page options will be grayed out and cannot be adjusted.


<span id="7fd6962d"></span>
## Procedure

Go to the **Add service** page, select the services you want to add, and choose whether to enable them at the **Custom deployment** button in the lower left corner:


* When disabled, services will be automatically deployed according to the default rules.

* When enabled, you can configure the deployment topology of service components. Click **Set deployment topology,**  to enter the service topology configuration page, where you can select the target node group for component deployment. The right side displays **Selected configuration plan**.


After completing the configuration, click the **Confirm** button. Wait for the component installation to complete. When the component service status is **Normal**, the component addition is complete.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The available services vary by cluster type and version .</div>


<span id="8be2b687"></span>
## Related operations

After services are added, to further adjust the deployment topology of service components, use the **service scaling** feature. For details, see [Service scaling](https://docs.byteplus.com/docs/E-MapReduce/Service_scaling).

<span id="_3-重启服务"></span>
# Restart services

For component services that have already been created, if a service is abnormal or its parameters have been modified, you need to restart the corresponding service to restore normal operation or apply the modified configuration parameters. You can restart services in the corresponding component service page.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When restarting a service, running tasks will be automatically closed. Please confirm the status of tasks and data in advance to avoid data anomalies.</div>



1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the left navigation pane, click Resources \> Cluster list \> Cluster name to access the details page for the specific cluster.

3. On the cluster details page, click the Service managementtab to go to the cluster service list page.

4. On the service list page, click the specific **service name** to enter the component service page. You can restart services using either of the following two methods:

   * Click the **Service operation** **Restart** button to open the restart settings window:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5652818c6a354b3b8c1e879abf0ef8cd~tplv-goo7wpa0wc-image.image) </span>

      * Execution range: Select the execution machines for restarting the service based on the actual scenario.

      * Restart method: Choose the restart method for the current service.

      * Operation notes: Enter the note information for the restart operation, specify the reason for the restart to facilitate tracking subsequent operations. The note content is limited to 1–200 characters.

      * Click the Confirm button. The platform will automatically restart the components on the corresponding host. Wait for the service to finish restarting.

   * You can also go to the Service management tab, and on the right side of the specific component name, click the Restart button in the Operation column **to restart the component.** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/429f4739c3c64d37952baa719b365b08~tplv-goo7wpa0wc-image.image) </span>


<span id="0df27eaf"></span>
# Restart after modifying service parameters

After modifying service parameters, the interface will prompt you to restart the service to apply the changes. At this point, you can click the corresponding restart service prompt link, select the restart method, and optionally enable the Rolling restart switch.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the HDFS, YARN, Presto, and Spark components support this feature.</div>



|Restart method |Restart note |
|---|---|
|Restart |Follow the standard restart process. You can choose whether to enable the Rolling restart switch. If enabled, this restart will not stop the entire service component. EMR will restart service components one by one in a certain order. The overall restart time is longer than a direct restart, but not all services will be stopped. |
|Force restart |Forced restart will immediately restart the target process. Performing cleanup will not save data. It is not recommended to perform this operation on normally running service processes.<br><br>You can choose whether to enable the Rolling restart switch. If enabled, this restart will not stop the entire service component. EMR will restart service components one by one in a certain order. The overall restart time is longer than a direct restart, but not all services will be stopped. |
|Restart by yourself |If you determine that the modified parameter configuration has already taken effect, or you have manually restarted the service component, you can choose to perform a manual restart. After confirmation, you will need to manage the configuration activation yourself. |
