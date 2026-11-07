---
title: "Data insight"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Data-insight"
---

<span id="YQeIut8Y"></span>
## Overview

Data Insight leverages the query and analysis capabilities of Torch Log Service (TLS) to analyze log data that ALB delivers to TLS. It covers comprehensive analysis dimensions, including real\-time metrics, access characteristics, and global monitoring, supporting scenarios such as daily O&M, business analysis, and capacity planning.


|**Module** |**Core capability** |**Typical application scenarios** |
|---|---|---|
|**Second\-level metric monitoring** |Real\-time monitoring of core metrics such as QPS, latency, error rate, and request traffic, with comparison between access latency and upstream latency |Real\-time O&M, troubleshooting, and performance bottleneck identification |
|**Access overview analysis** |Analyzes PV/UV period\-over\-period and year\-over\-year, user geographical distribution, terminal types, and popular domains |Business growth assessment, deployment planning, and operational strategy formulation |
|**Monitoring Center** |Displays instance status across multiple dimensions including availability, performance, and errors, with P50/P90/P99 latency metrics |SLA evaluation, error classification and troubleshooting, and global operational status awareness |


<span id="pGDIobz6"></span>
## Authorize data insight


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation tree, select **Data Insight**.

4. Click **Configure access**.

   * ALB Cross\-Service Authorization: Click **Authorize now** next to ALB Cross\-Service Authorization. You will be redirected to the ALB authorization page. Click **Authorize now**.

   * TLS Cross\-Service Authorization: Click **Authorize now** next to TLS Cross\-Service Authorization. You will be redirected to the ALB authorization page. Click **Authorize now**.

5. Click **Enable now** to complete the action.


<span id="zQy473bF"></span>
## Enable/Disable log collection

Store the metrics of the ALB instance in TLS, and directly perform retrieval, chart\-based visual analysis, and more.


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation tree, select **Data Insight**.

4. On the **ALB** ** second\-level metric monitoring** tab, click **Configure access** on the right.

   * Single operation:

      * Turn on: click **Enable** to the right of the target ALB instance to complete the action.

      * Turn off: click **Disable** to the right of the target ALB instance to complete the action.

   * Batch operation:

      * Turn on: Select multiple ALB instances and click **Batch enable** to complete the action.

      * Turn off: Select multiple ALB instances and click **Batch disable** to complete the action.


<span id="wxS6xCMU"></span>
## View data insight


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation tree, select **Data Insight**.

   * ALB Second\-Level Metric Monitoring: On the **ALB Dashboard \> ALB Second\-Level Metric Monitoring** tab, filter and view ALB metric data for 5 minutes, 15 minutes, 1 hour, 6 hours, 1 day, or a custom time range as needed.

      
      |**Metric name** |**Notes** |
      |---|---|
      |QPS |Requests per second (QPS), reflecting the current business traffic scale |
      |Access latency |Client\-to\-ALB request processing latency |
      |Upstream latency |ALB\-to\-backend forwarding latency |
      |Request traffic |Inbound request traffic volume |
      |Response body traffic |Outbound response body traffic volume |
      |Success rate |Successful request ratio (percentage of requests without 4xx/5xx errors) |
      |Status code 3xx |Number of requests with 3xx status codes returned by ALB |
      |Error status code |Total number of requests with 4xx/5xx error status codes returned by ALB |
      |Status code 2xx |Number of requests with 2xx status codes returned by ALB |
      |Upstream 3xx status code |Number of 3xx responses returned by the backend service |
      |Upstream error status codes |Total number of 4xx/5xx errors returned by the backend service |
      |Upstream 2xx status code |Number of 2xx responses returned by the backend service |
      

   * ALB Access Overview: On the **ALB Dashboard \> ALB Access Overview** tab, filter and view ALB access data for 1 hour, 6 hours, 1 day, 7 days, 30 days, or a custom time range as needed.

      
      |**Metric name** |**Notes** |
      |---|---|
      |PV comparison versus yesterday |Current\-period PV vs. same period yesterday |
      |PV comparison versus last week |Current\-period PV vs. same period last week |
      |UV comparison versus yesterday |Current\-period UV vs. same period yesterday |
      |UV comparison versus last week |Current\-period UV vs. same period last week |
      |PV distribution by province |PV distribution by province |
      |PV distribution by country |PV distribution by country |
      |UV distribution by province |UV distribution by province |
      |UV distribution by country |UV distribution by country |
      |Today's page views (PV) |Total cumulative PV for the current day |
      |PV over the last 7 days |Total cumulative PV over the last 7 days |
      |UV today |Cumulative unique visitors for the current day |
      |Unique visitors (UV) over the last 7 days |Cumulative unique visitors over the last 7 days |
      |Top 10 provinces by access volume |Top 10 provinces by access volume |
      |Top 10 cities by access count |Ranking of the Top 10 cities by access volume |
      |Top 10 UserAgents by access count |Ranking of the Top 10 client types by access volume |
      |Top 10 hosts by access volume |Top 10 domains by access volume |
      

   * ALB Monitoring Center: On the **ALB Dashboard \> ALB Monitoring Center** tab, filter and view ALB access data for 1 hour, 6 hours, 1 day, 7 days, 30 days, or a custom time range as needed.

      
      |**Metric name** |**Notes** |
      |---|---|
      |Access PV |Total PV within the period |
      |Request success rate |Successful request ratio |
      |Number of 4xx requests |Number of requests returning 4xx client errors |
      |Number of 499 requests |Number of requests returning 499 status codes (client actively disconnected) |
      |Average latency |Average request processing latency |
      |Number of 404 requests |Number of requests returning 404 status codes |
      |Number of 5xx requests |Number of requests returning 5xx server errors |
      |Number of 504 requests |Number of requests returning 504 gateway timeout errors |
      |PV |PV trend chart over time |
      |Status code distribution |Trend of the distribution proportion of various status codes |
      |Traffic |Inbound/outbound traffic trends |
      |Access failure rate |Trend of the request failure rate |
      |Average latency |Average latency trend |
      |P50 latency |50th percentile latency (median latency) |
      |P90 latency |90th percentile latency |
      |P99 latency |99th percentile latency (tail latency) |
      |Top request host |Top hosts by access volume |
      |Top request URL |Top URLs by access volume |
      |Top request backend |Top backends by access volume |
      

&nbsp;


&nbsp;
