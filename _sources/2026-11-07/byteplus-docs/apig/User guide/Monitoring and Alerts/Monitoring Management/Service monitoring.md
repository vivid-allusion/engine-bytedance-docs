---
title: "Service monitoring"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Service_Monitoring"
---

API gateway connects to [Vital Managed Service for Prometheus (VMP) ](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus), offering the capability to monitor API gateway service\-level performance metrics. For specific monitoring metrics information, please refer to [Monitoring Metric](https://docs.byteplus.com/en/docs/apig/Monitoring_metrics). This article introduces how to view the monitoring data of the service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The VMP service has been activated, and a VMP workspace has been created. Please refer to [Creating a workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* An APIG instance has been created, and it has been bound to a VMP workspace. For details, please refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Changing the bindings is not supported after binding a VMP workspace.</div>


* <div data-tips="true" data-tips-type="danger">All monitoring data of the current APIG instance will be collected and stored under the workspace bound to you. Deleting the workspace may lead to permanent loss of monitoring data for the gateway, please proceed with caution.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. Select **Route management \> Service list (Domain name)**  from the left navigation bar. In the service list, click on the target service name to enter the service Overview page.

4. Click **Monitoring** to switch to the **Monitoring** tab.

5. Set the query time range to view various monitoring metrics of the current service. Supports viewing up to the past 30 days of monitoring data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have bound a specific <strong>domain name</strong> in <strong>Domain Management</strong>, you can select the domain name from the drop\-down box to view Monitoring info.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have bound a wildcard domain in <strong>Domain Management</strong>, you can <strong>enter</strong> a specific domain name in the drop\-down box to view Monitoring info.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, a wildcard domain name <code>*.abc.com</code> is bound in domain management. At this time, the Service actually matches a very wide range of domain names, and any <code>{content}.abc.com</code> will be matched. If you need to find the monitoring information of one of the domain names, you can directly enter the domain name, such as `test.abc.com`, and the matching and filter can be completed.   </div>
