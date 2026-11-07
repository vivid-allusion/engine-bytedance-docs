---
title: "Instance monitoring"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Instance_Monitoring"
---

API gateway connects to [Vital Managed Service for Prometheus (VMP) ](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus), providing the ability to monitor performance metrics at the APIG instance level. For specific monitoring metrics, please refer to [Monitoring Metrics](https://docs.byteplus.com/en/docs/apig/Monitoring_metrics). This article explains how to view monitoring information of an instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The VMP service is activated, and a VMP workspace has been created. For detailed operations, please refer to [Creating a workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* An APIG instance has been created, and it has been bound to a VMP workspace. For detailed operations, please refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">After binding to a VMP workspace, changes are not supported.</div>


* <div data-tips="true" data-tips-type="danger">All monitoring data under the current APIG instance will be collected and stored in your bound VMP workspace. Deleting a workspace may lead to permanent loss of monitoring data for the gateway, please proceed with caution.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left **navigation bar**, click on the target instance name and enter the Overview page.

4. Click **Monitoring** to switch to the **Monitoring** tab.

5. Set the query time range to view the current instance's monitoring metrics. Supports viewing up to the past 30 days of monitoring data.
