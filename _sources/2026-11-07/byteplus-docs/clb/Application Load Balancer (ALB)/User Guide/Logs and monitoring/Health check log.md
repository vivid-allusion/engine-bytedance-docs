---
title: "Health check log"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Health-check-logs"
---

Enabling the health check log delivery feature sends instance health check logs to Torch Log Service (TLS), allowing direct search and analysis of log entries based on TLS. This helps you quickly access, view, and analyze logs to troubleshoot health check issues.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ALB delivers health check logs only when the backend server's health check status changes.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin

You have activated the TLS log service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ALB does not charge for log delivery; you only pay the TLS fee.</div>


<span id=".5byA5ZCv5YGl5bq35qOA5p-l5pel5b-X5oqV6YCS"></span>
## Enable health check log delivery


1. Log in to the BytePlus [Application Load Balancer console](https://console.byteplus.com/alb).

2. Click **Instance management** in the left navigation pane to enter the **Instance management** page.

3. On the **Instance management** page, click the instance to configure.

4. On the **Instance details** tab, in the **Log delivery \> Health check log** section, click **Edit configuration**.

5. Enable **Health check log** and select **log project** and **log topic** according to your business needs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you first activate the health check log delivery/access log analysis feature, you need to authorize the TLS service for your service role <a href="https://console-stable.volcanicengine.com/iam/rolemanage/ServiceRoleForAlb/">ServiceRoleForAlb</a> to proceed with delivery operations.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deleting the service role will invalidate cross\-service authorization, causing logs from all instances with access logging enabled to fail delivery. Proceed with caution.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no log project or log topic is available, you can create them before selecting.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Logs from one instance can only be delivered to one specified log topic, but one log topic can receive logs from different instances.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended that you deliver access logs and health check logs to different log projects or log topics for easy management and to avoid inconsistencies in retrieval fields.   </div>
   

6. After confirming that the configuration information is correct, click **Confirm** to complete enabling health check log delivery.


<span id=".5YWz6Zet5YGl5bq35qOA5p-l5pel5b-X5oqV6YCS"></span>
## Disable health check log delivery


* The health check log delivery can be stopped at any time. In the **Log Delivery \> Health Check Log** module, click **Edit Configuration** to disable **Health Check Log**.

* After stopping log delivery, delivered logs will remain in TLS. The retention period depends on TLS configuration for the log topic.

* When enabling health check log delivery again, you must reselect the log project and log topic.


<span id=".5a2X5q616Kej6YeK"></span>
## Field Description


|Field |Explanation |Example |
|---|---|---|
|instanceId |albid |alb\-2fem89fq7du685oxruwmh\*\*\*\* |
|origin |ALB private IP address: listen PORT. |192.168.2.128:80 |
|destination |rsIP:Port。 |192.168.3.114:80 |
|protocol |Health check protocol used |HTTP |
|result |Result, specifically including: succeeded, failed. |succeeded |
|cause |Causes, including unexpected and unresponsive. |unexpected |
|domain |Forwarding rules domain name |www.test.com |
|url |Forwarding rules URL |/index |
