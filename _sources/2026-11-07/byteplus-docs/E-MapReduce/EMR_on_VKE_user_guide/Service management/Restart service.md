---
title: "Restart service"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Restart_service"
---

The service restart feature allows you to manually perform a restart operation to quickly restore service operations when a service instance encounters an exception or when new configurations need to be applied. This feature primarily addresses issues such as unresponsive services or configuration updates not taking effect. This document mainly describes how to restart a service instance through the console or by calling the API (Application Programming Interface).

<span id="zp8PPDAbS3"></span>
## Feature overview

The service restart feature provides a manual operation that allows users to restart one or more service instances. This operation is used to handle unresponsive or hung services, or to force the application of new settings after updating configurations, ensuring service stability and the timely application of configurations.

<span id="EcaiZmWokL"></span>
### Use cases


* **Service hang recovery**: Applicable for scenarios where unresponsive service instances need to be quickly restored.

* **Configuration update**: Applicable for scenarios where the service needs to be restarted after modifying configurations to make the new settings take effect.


<span id="byvJ8xbvF9"></span>
### Important notes


* The restart operation will cause a brief service interruption. Perform this operation during off\-peak business hours.

* When restarting the service, running tasks will be automatically closed. Confirm the status of tasks and data in advance to avoid data anomalies.


<span id="DHn8JWz9cK"></span>
### Prerequisites


* A cluster has been created, and the cluster status is running.

* You have the "Manage" role permission for the cluster.


<span id="zMMxcGCqFs"></span>
## Procedure


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. In the left navigation pane, click **Resource Management \> on VKE \> Cluster Name** to enter the details page of the specific cluster.

3. On the cluster details page, click the Service listtab to enter the cluster service list page.

4. On the service list page, click the specific **service name** to enter the component service page. You can restart using either of the following methods:

   * **Method 1**: Click the Service operationsRestart button in to open the restart settings window:

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This operation will restart all components of the service.      </div>
      

&nbsp;

   * **Method 2**: On the **Service Management** tab, to the right of the component name, click the **Restart** button in the **Actions** column to restart the component.

&nbsp;


&nbsp;
