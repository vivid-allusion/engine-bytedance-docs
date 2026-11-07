---
title: "Observability"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Observability"
---

AI Native BaaS for Supabase (hereinafter referred to as “BytePlus Supabase”) provides independent observability monitoring pages for five core modules: Data API, Auth, Edge Functions, Storage, and Realtime. You can view key metrics such as request volume, error rate, response time, and user activity for each module in the console to help you understand your application's operational status and end\-user behavior in real time.

<span id="GMTFaBli"></span>
## Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="2oFIMnSc"></span>
## Precautions

Starting from August 20, 2026, the Report page will officially upgrade to Observability, providing richer monitoring capabilities.

<span id="viNh5hQ9"></span>
## Procedure

<span id="qFGQElN0"></span>
### Enter the observability page


1. Click **Observability** in the left navigation bar.

2. Select the module to view in the **GENERAL** or **PRODUCT** section:

   * **GENERAL**

      * **Overview**: provides a service health overview.

      * **Query performance**: offers SQL statement\-level performance analysis information.

      * **API gateway**: displays aggregated monitoring data for all requests passing through the API gateway.

   * **PRODUCT**

      * **Data API**: view request metrics for accessing the database via Data API (PostgREST).

      * **Auth**: check usage, error, and performance metrics related to user authentication.

      * **Edge functions**: view the number of calls, status codes, and execution durations of edge functions.

      * **Storage**: view object storage request volume, error rate, and response time consumption.

      * **Realtime**: view real\-time communication service request metrics.


<span id="FLSqHtBl"></span>
### Select time range

At the top of each monitoring page, you can set the data display time range using the time selector, supporting recent 10 minutes, recent 30 minutes, recent 60 minutes, recent 3 hours, recent 24 hours, recent 7 days, recent 14 days, recent 28 days, and other common options. Charts automatically adjust time granularity based on the selected range.

<span id="1nGWf55k"></span>
### Add filter condition

Only **API Gateway**, **Data API, Storage**, **Realtime**, and **Auth API Gateway** monitoring pages support adding filter conditions. Click the  **+ Add filter** button to filter monitoring data by attributes within the current time range and accurately locate target requests or responses. Filter conditions consist of the following three parts:


* **Attribute filter**: select filter dimension, supporting the following attributes:

   * `request.path`: request path

   * `request.method`: Request method

   * `request.search`: request query parameters

   * `request.headers.x_client_info`: client info request header

   * `request.headers.user_agent`: User\-Agent request header

   * `response.status_code`: response status code

* **Comparison**: supports is (exact match) and matches (regex match).

* **Value**: input the target value for filtering (string type).


Click the **Add filter** button to apply after configuration. Multiple filter conditions can be added, with conditions combined by intersection.

&nbsp;

<span id="11YSemf6"></span>
### Refresh data

Click the refresh button at the top of the page to manually fetch the latest monitoring data.

<span id="Pac1uAMs"></span>
## Monitoring metrics

<span id="NmjjP6UI"></span>
### Overview

The Overview page, located under the **GENERAL** group in the left navigation of Observability, provides an overview of Service Health. The page displays request trends for the following six services as thumbnails within the selected time range:


* API Gateway

* PostgREST

* Auth

* Edge Functions

* Storage

* Realtime


Click the arrow at the top right of each service thumbnail to jump to the detailed monitoring page of the corresponding module. The top right of the page supports selecting the time range (Last 60 minutes, Last 24 hours, and Last 7 days) and manual Refresh.

<span id="27gOo6dN"></span>
### Query Performance

The Query Performance page is located under the **GENERAL** group in the left navigation of Observability and actually embeds the contents of the Advisors \> Query Performance page.

The top of the page displays the following three summary metrics:


* **Slow Queries**: the number of slow SQL queries identified in the current analysis report.

* **Cache Hit Rate**: the percentage of database cache hits.

* **Avg. Rows Per Call**: average rows returned per call.


The main page is a performance analysis table at the SQL statement level, including the following columns: Query (SQL statement), Time consumed (time consumption), Count (execution count), Max time (maximum time consumption), Mean time (average time consumption), Min time (minimum time consumption), Rows processed (rows processed), Cache hit rate (cache hit rate), Role (execution role).

The table supports searching by query content and filtering by Roles. Click a SQL statement to view details; the top right corner of the page provides the **Enable Index Advisor** button to activate the index recommendation feature.

This report is generated based on the pg_stat_statements table and the pg_stat_statements extension. Click **Reset report** to reset the analysis data (recommended to reset after completing query optimization). Source supports switching between Primary Database or Replica.

<span id="9FuEO5qC"></span>
### API Gateway

The API Gateway page displays aggregated monitoring data for all requests passing through the API gateway, including the following metric modules:


|**Metric** |**Decscription** |
|---|---|
|Total Requests |display the total number of requests within the selected time range, along with average tps (average transactions per second) and peak tps (peak transactions per second); also display the ranking of request paths and http method request counts in a list, click to expand and view details. |
|Response Errors |Display the trend of the number of response Errors within the selected time range. |
|Response Speed |Display the trend of response time consumption within the selected time range and the average response time ranking of each request path. |


The page supports clicking  **+ Add filter** to add filter conditions. The filter parameters are the same as Data API, Storage, and Realtime. Refer to the "adding filter conditions" section for details. The top right corner of the page supports selecting time ranges and manual refresh.

The API Gateway page also supports filtering by **request type**. You can select specific request types to view from the dropdown menu in the top left corner of the page, with the following options supported:


* **All Requests**: shows all requests.

* **Data API (PostgREST)** : shows only database API requests initiated via PostgREST.

* **Auth**: shows only requests related to the Auth service.

* **Storage**: shows only requests related to the Storage service.

* **Realtime**: shows only requests related to the Realtime service.

* **GraphQL (pg_graphql)** : shows only GraphQL requests.


<span id="svoxOmkM"></span>
### Data API

Data API monitoring page displays requests to the Database via the PostgREST interface, including the following metrics:


|**Metric** |**Decscription** |
|---|---|
|Tables Without RLS Policies |Number of tables with rls enabled but no policy configured, refreshes every 30 seconds. |
|Total Requests |Show the total number of Data API requests within the selected time range and present their distribution in a bar chart by time bucket. Also show Average TPS (transactions per second) and Peak TPS. The table below lists the number of calls for each request by method, HTTP status code, and path. |
|Response Errors |Display the number and hourly distribution of error requests within the selected time range to help you quickly locate abnormal interfaces. |
|Response Speed |Show the average response time of Data API requests within the selected time range (milliseconds), displayed as a bar chart showing time consumption changes for each time bucket. The table below lists the average time consumption by request path to help identify slow requests. |


<span id="gvweE1bK"></span>
### Auth

Auth monitoring page displays the operation and performance data of the user authentication module, divided into the following parts.

<span id="lChlnLBc"></span>
#### Usage

Usage metrics are shown in the table below.


|**Metric** |**Decscription** |
|---|---|
|Registered Users Total |Displays the total registered users as of now and the trend over time. This data is directly queried from the database, unaffected by log retention periods. |
|Trailing Auth Active Days |Display the range of consecutive days users perform auth activities as a distribution chart to help you understand user retention. |
|Auth Daily Active Users |Displays the daily unique active users (DAU) authenticated, counted by UTC calendar day. |
|Auth Daily Active Users (%) |Displays the percentage of daily active users relative to the total cumulative registered users, calculated as: number of daily active users ÷ total cumulative registered users as of the day × 100%. |
|Active Users |Show the trend of deduplicated active users with valid user identities within the selected time range. |
|Sign In Attempts by Type |Display the number of login requests categorized by login methods, such as Password login, Token refresh, and third\-party login. |
|Sign Ups |Display the number and trend of successful registrations within the selected time range. |
|Password Reset Requests |Show the number of password reset requests within the selected time range. |


Usage metrics support filtering by login method. The supported login providers are shown in the table below.


|**Type** |**Provider** |
|---|---|
|Email / phone |Email, Phone, Magic Link, Email Change |
|social account |Google, Apple, GitHub, GitLab, Facebook, Twitter, Discord, Kakao, LinkedIn, LinkedIn OIDC, Twitch, Spotify, Snapchat、Notion、Figma、Zoom、Slack OIDC、WorkOS |
|Enterprise / SSO |Azure, SAML, SSO/SAML, Keycloak |
|Multi\-factor authentication |TOTP (time\-based one\-time password), Recovery (recovery code) |


<span id="xErTbc1G"></span>
#### Monitoring


|**Metric** |**Decscription** |
|---|---|
|API Gateway Auth Errors |Show the number and trend over time of Auth requests returning error status codes through the API gateway, filterable by status code or error type. |


Monitoring indicators support filtering by status code. Status code consists of the following two parts:


* **Operator**: supports = equals, \>= greater than or equal to, <= less than or equal to, \> greater than, < less than, != not equal to.

* **Value**: enter the target status code (such as 200, 500, etc.).


<span id="XepcRkWL"></span>
#### Performance


|**Metric** |**Decscription** |
|---|---|
|Sign In Processing Time |Displays the processing time consumption of login requests, supporting viewing of average, maximum, and P50, P95, P99 percentiles. |
|Sign In Processing Time Percentiles |Presents the percentile distribution of login time consumption as a percentile graph to help you understand tail latency. |


<span id="nvEDHtfO"></span>
#### Auth API Gateway


|**Metric** |**Decscription** |
|---|---|
|Total Requests |Displays the total number of Auth requests through the API Gateway, average TPS, and peak TPS, supporting filtering by path, status code, and other dimensions. |
|Response Errors |Display the number and time distribution of Auth request errors. |
|Response Speed |Display the average response time consumption of Auth requests and the ranking of average time consumption for each path. |


<span id="yb5UuQq6"></span>
### Edge Functions

The Edge Functions monitoring page displays the invocation and execution status of edge functions. The top of the page supports filtering by function and status code.

The filter methods are as follows:


* **Function**: Search and select the target function name from the dropdown list, then click **Apply** to apply.

* **Status Code**: Set the filter conditions for response status codes, consisting of the following two items:

   * **Operator**: Supports = equals, \>= greater than or equal to, <= less than or equal to, \> greater than, < less than, != not equal to.

   * **Value**: Enter the target status code (such as 200, 500, etc.).


After setting, click **Apply** to apply or click **Clear** to clear filter conditions.


|**Metric** |**Decscription** |
|---|---|
|Total Edge Function Invocations |Displays the total number of calls and the time trend for all Edge Functions in the selected time range. |
|Edge Function Status Codes |Displays the distribution of request counts by HTTP status code to help you quickly identify abnormal function executions. |
|Edge Function Execution Time |Shows the execution time consumption of Edge Functions, supporting the view of time consumption data under different aggregation dimensions (average, P95, etc.). |


<span id="4fvSBz7q"></span>
### Storage

The Storage monitoring page displays the request status of Object Storage services.


|**Metric** |**Decscription** |
|---|---|
|Total Requests |Display the total number of Storage requests, average TPS, and peak TPS within the selected time range, and present the distribution of requests over time with a bar chart. The table below lists the number of calls for each request by method, status code, and path. |
|Response Errors |Displays the number and time trend of error requests in Storage. |
|Response Speed |Show the average response time consumption (ms) of Storage requests. The table below lists the average time consumption by request path. |


<span id="bFGru9lK"></span>
### Realtime

The Realtime monitoring page displays the request status processed by the real\-time communication service through the API gateway.


|**Metric** |**Decscription** |
|---|---|
|Total Requests |Displays the total number of Realtime service requests, average TPS, and peak TPS within the selected time range. |
|Response Errors |Show the number and time distribution of errors in realtime requests. |
|Response Speed |Show the change in average response time consumption for Realtime requests. |


<span id="7qoLyior"></span>
## Precautions


* Monitoring data refresh may be delayed; newly generated request data may take up to 24 hours to appear fully in the charts.

* Log\-based metrics (such as request count, error count, response time consumption) are limited by the log retention period. Logs are retained by default for 30 days; historical data beyond the retention period is not retrievable.

* Indicators based on real\-time database queries (such as the cumulative number of registered users and the number of tables without configured RLS policies) are not limited by the log retention period. However, related historical data cannot be restored after users are physically deleted.

* Average TPS and Peak TPS are calculated based on request data within the selected time range. The larger the time range, the longer the statistical period for the values.

* Monitoring data for each module is isolated by project. Data from different projects is not visible to each other.


<span id="h0Ur0ocM"></span>
## FAQs and troubleshooting

<span id="9JQNnBXs"></span>
### Why does the monitoring page show "No data to show"?

If your instance is newly created or there is no request traffic for the selected module within the selected time range, the page will display "No data to show". Confirm the instance has actual traffic and try expanding the time range. In addition, data refresh has delays. Newly generated request data may take up to 24 hours to display.

<span id="M3GoQ8Ef"></span>
### Why can I only view data from the recent 30 days?

Monitoring indicators based on logs are retained by default for 30 days. Contact technical support for data retention beyond the default period.
