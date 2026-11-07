---
title: "Metrics Reference"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4"
---

BytePlus CDN metrics provide key data points for monitoring service performance and analyzing traffic patterns. This document serves as a comprehensive reference, explaining the definition and calculation methods for all available metrics. It covers two main categories: [user request metrics](https://docs.byteplus.com/en/docs/18/20645#user-request-metrics), which track interactions between end\-users and the CDN, and [origin request metrics](https://docs.byteplus.com/en/docs/18/20645#origin-request-metrics), which monitor traffic between the CDN and your origin server.

The following definitions apply to the statistical methods for these metrics:


* Specified statistical time period: Indicates the statistical time period between the start time (`StartTime`) and end time (`EndTime`) you specify.

* Actual statistical time period: The actual time period as determined by the start time (`StartTime`), end time (`EndTime`), and time granularity (`Interval`) you specify. Metric data are calculated based on the actual statistical time period.

* Time interval: The time granularity (`Interval`) divides the actual statistical time into a series of time intervals.

* Breakdown data: A series of metric data points calculated by the CDN for each time interval. Breakdown data is used to show data trend within the actual statistical time period.

* Aggregate data: Refers to an aggregate data obtained by the CDN after aggregating the metric data of all time intervals. Aggregate data is used to show the data overview within the actual statistical time period.


For detailed descriptions of these definitions, see [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/Jbrkn1).

<span id="user-request-metrics"></span>
## User Request Metrics

<span id="data-transferred-by-users-to-cdn-traffic"></span>
### Data transferred by users to CDN (Traffic)

<span id="definition"></span>
#### Definition

This metric indicates the amount of data transferred by users to the CDN, which is the sum of the header size and body size of user requests, measured in bytes.

This metric accounts for user requests that meet the following conditions:


* The request method is neither GET nor HEAD.


<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data indicate the amount of traffic for each time interval.


* The traffic for a single time interval = the sum of data transferred by users to the CDN within that time interval.


<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data indicates the total amount of traffic during the actual statistical time period.

<span id="data-transferred-by-cdn-to-users-traffic"></span>
### Data transferred by CDN to users (Traffic)

This metric indicates the amount of data transferred by the CDN to users, which is the sum of the response header size and response body size, measured in bytes.

 &nbsp;

This metric accounts for user requests that meet the following conditions:


* The request method is neither GET nor HEAD.


<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data indicate the amount of traffic for each time interval.


* The traffic for a single time interval = the sum of traffic consumed by all CDN responses within that time interval.


<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data indicate the total traffic during the actual statistical time period.

<span id="data-transferred-by-users-to-cdn-bandwidth"></span>
### Data transferred by users to CDN (Bandwidth)

<span id="definition"></span>
#### Definition

Indicates the bandwidth calculated based on the amount of data transferred by the user to the CDN, measured in bps. Bandwidth is calculated based on the data volume and duration.

This metric is for user requests that meet the following conditions:


* The request method is neither GET nor HEAD.


<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data indicate the bandwidth for each time interval. According to the specified statistical time granularity, there are two methods to calculate bandwidth:


* If the time granularity is 1 minute or 5 minutes, the bandwidth for a single time interval is calculated as follows:

   * ((Data transmitted by users to CDN) \* 8) / (Duration of the time interval)

* If the time granularity is 1 hour or 1 day, the bandwidth calculation for a single time interval is as follows:

   1. Use the above calculation formula to calculate a series of bandwidth for the interval at 5\-minute granularity.

   2. Calculate the maximum of these bandwidth values, which is the peak bandwidth.


<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data indicate the peak bandwidth during the actual statistical period across all intervals. The method to calculate aggregate data is as follows:


1. Based on the specified time granularity, calculate the bandwidth for each interval within the period. The calculation method for bandwidth in each interval is the same as that for breakdown data.

2. Calculate the maximum of these bandwidth values.


<span id="7d5b0c46"></span>
#### Peak Bandwidth Time

Indicates the start time of the time interval in which the bandwidth peak occurred.

<span id="data-transferred-by-cdn-to-users-bandwidth"></span>
### Data transferred by CDN to users (Bandwidth)

Indicates the bandwidth calculated based on the amount of data transferred by the CDN to users, measured in bps. Bandwidth is calculated based on the data volume and duration.

<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data indicate the bandwidth for each time interval. Depending on the specified time granularity, there are two methods to calculate bandwidth:


* If the time granularity is 1 minute or 5 minutes, then the bandwidth calculation for a single time interval is as follows:

   * ((Data transferred by CDN to users) \* 8) / (Duration of the time interval)

* If the time granularity is 1 hour or 1 day, then the bandwidth calculation for a single time interval is as follows:

   1. Use the formula above to calculate a series of bandwidth values for the time interval at a 5\-minute granularity.

   2. Calculate the maximum of these bandwidth values, which is the peak bandwidth.


<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data indicate the peak bandwidth across all time intervals during the actual statistical time period. The calculation method for aggregate data is as follows:


1. Based on the specified time granularity, calculate the bandwidth for each interval within that period. The calculation method for bandwidth in each interval is the same as that for breakdown data.

2. Calculate the maximum value among these bandwidth values.


<span id="peak-bandwidth-time"></span>
#### Peak Bandwidth Time

Indicates the start time of the time interval in which the peak bandwidth was observed.

<span id="requests"></span>
### Requests

<span id="definition"></span>
#### Definition

This metric counts the total number of user requests received by the CDN.


* Number of user requests = dynamic requests + static requests + Requests with a 405 status code from CDN responses


<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data indicate the number of requests for each time interval.


* Number of requests for a single time interval = Number of requests received by CDN in that time interval.


<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data indicate the total number of requests during the actual statistical time period.

<span id="dynamic-requests"></span>
### Dynamic Requests

The definition and statistical method for this metric are similar to those for the main Requests metric. However, the metric data only account for user requests that meet all of the following conditions:


* The request method is neither GET nor HEAD.

* The response status code from the CDN is not 405. A 405 code indicates that the request method is not allowed by the CDN.


<span id="static-requests"></span>
### Static Requests

The definition and statistical method for this metric are similar to user requests. However, the metric data only account for user requests that meet all of the following conditions:


* The request method is either GET or HEAD.

* The response status code from the CDN is not 405.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, for WebSocket requests, the data for this metric is inaccurate. When querying data for this metric, please filter out the WebSocket protocol.</div>


<span id="request-qps"></span>
### Request QPS

<span id="definition"></span>
#### Definition

This metric refers to the QPS for all user requests received by the CDN.

<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data show the request QPS for each time interval. Based on the specified statistical time granularity, there are two methods to calculate request QPS:


* If the time granularity is 1 minute or 5 minutes, the request QPS calculation for a single time interval is as follows:

   * (Number of requests in the time interval) / (Length of the time interval)

* If the time granularity is 1 hour or 1 day, the request QPS calculation for a single time interval is as follows:

   1. At a 5\-minute time granularity, calculate a series of QPS using the formula above for the time interval.

   2. Calculate the peak of these QPS values, which is the QPS peak.


<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data indicate the peak of request QPS during the entire actual statistical time across all intervals. The method to calculate aggregate data is as follows:


1. Based on the specified time granularity, calculate the request QPS for each interval during that time. The calculation method for QPS in each time interval is the same as that for breakdown data.

2. Determine the peak from these request QPS values.


<span id="status-codes"></span>
### Status Codes

<span id="definition"></span>
#### Definition

In CDN's responses to user requests, this metric refers to the number of status codes in the following categories:


* The number of all status codes.

* The number of 2xx status codes and the number of each status code in this category.

* The number of 3xx status codes and the number of each status code in this category.

* The number of 4xx status codes and the number of each status code in this category.

* The number of 5xx status codes and the number of each status code in this category.


<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data indicate the number of status codes in each time interval for each category.

<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data represents the total number of status codes for each category during the actual statistical time period.

<span id="request-response-time"></span>
### Request Response Time

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, for WebSocket requests, the data for this metric is inaccurate. When querying data for this metric, please filter out the WebSocket protocol.</div>


<span id="definition"></span>
#### Definition

This metric represents the average time CDN takes to respond to user requests, measured in milliseconds (ms).

For a user request, the response time is the time span between the following two time points:


* The first byte of the response transferred from CDN to the user.

* The last byte of the response completely transferred by CDN.


Note: This metric is calculated on the CDN side.

When CDN finishes transmitting the last byte of the response, this time point is recorded as the response completion time for that request.

<span id="breakdown-data"></span>
#### Breakdown Data

The breakdown data represents the average response time within each time interval. This metric data is calculated based on requests for which CDN completed responses within each time interval.


* The response time for a single time interval = (Total time spent by CDN to respond to all user requests) / (Number of requests)


<span id="aggregate-data"></span>
#### Aggregate Data

The aggregate data indicates the average response time within the actual statistical time period. The calculation for the aggregate data is as follows:


* (Total response time of all requests within the actual statistical time period) / (Number of requests within the actual statistical time period)


<span id="average-data-transfer-rate"></span>
### Average Data Transfer Rate

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, for WebSocket requests, the data for this metric is inaccurate. When querying data for this metric, please filter out the WebSocket protocol.</div>


<span id="definition"></span>
#### Definition

This metric represents the average data transfer rate of CDN when responding to all user requests, measured in Bps. It is calculated for user requests with a **2xx response status code**.

It is important to note that the metric data is calculated on the CDN side.

When the CDN finishes transferring the last byte of a response, that point in time is recorded as the response completion time for the request. When the CDN calculates the data transfer rate for a time interval, the calculation includes all requests whose response completion time falls within that time interval.

<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data represents the average speed within each time interval, calculated for requests to which the CDN completed a response within that time interval.


* Average speed for a single time interval = (Sum of data transfer speeds for all requests in the time interval) / (Number of requests in the time interval)

   * Data transfer speed for a single request = (Amount of data transferred by the CDN for the request) / (Time taken by the CDN to respond to the request)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When calculating download speed, the CDN excludes requests with a response time of less than 1 millisecond to avoid data deviation.</div>


<span id="aggregate-data"></span>
#### Aggregate Data

Aggregate data indicates the average speed over the actual statistical period. The calculation method is as follows:


* (Sum of data transfer speeds for all requests within the actual statistical period) / (Number of requests within the actual statistical period)


<span id="traffic-hit-rate-for-user-requests-traffic-hitrate"></span>
### Traffic Hit Rate for User Requests (traffic_hitrate)

<span id="definition"></span>
#### Definition

The traffic hit rate is calculated based on the following traffic volumes:


* The amount of data transferred by the CDN to users.

* The amount of data transferred by the origin to the CDN.


The traffic hit rate is displayed in numerical form. For example, 0.9999 represents 99.99%.

<span id="breakdown-data"></span>
#### Breakdown Data

Breakdown data indicate the traffic hit rate for each time interval.


* Traffic hit rate for a single time interval = (Data transferred by the CDN to users in this time interval \- Data transferred by the origin to the CDN in this time interval ) / (Data transferred by the CDN to users in this time interval)


<span id="aggregate-data"></span>
#### Aggregate Data

The aggregate data indicates the traffic hit rate within the actual statistical time period. The calculation for the aggregate data is as follows:


* (Data transferred by the CDN to users within the actual statistical time period \- Data transferred by the origin to the CDN within the actual statistical time period) / (Data transferred by the CDN to users within the actual statistical time period)


<span id="origin-request-metrics"></span>
## Origin Request Metrics

For origin requests, breakdown data and aggregate data are calculated in the same manner as [User Request Metrics](https://docs.byteplus.com/en/docs/18/20645#user-request-metrics). The table below just lists descriptions for these metrics.


|Metric |Description |
|---|---|
|Data transferred from Origin to CDN (Traffic) |Indicates the amount of data transferred from the origin to the CDN, measured in bytes. The amount of data is calculated based on the origin responses received by the CDN, and is the sum of the response header size and the response body size. |
|Data transferred from CDN to Origin (Traffic) |Indicates the amount of data transferred by the CDN to the origin, measured in byte. The amount of data is the sum of the size of the request header and the size of the request body in origin requests. |
|Data transferred from Origin to CDN (Bandwidth) |Indicates the bandwidth calculated based on the amount of data transferred from the origin to the CDN, measured in bps. |
|Data transferred from CDN to Origin (Bandwidth) |Indicates the bandwidth calculated based on the amount of data transferred by the CDN to the origin, measured in bps. |
|Origin Requests |Indicates the count of origin requests. |
|Origin Request QPS |Indicates the QPS for origin requests. |
|Status Codes |Indicates the number of status codes in the following categories in origin responses received by the CDN:<br><br><br>* The number of all status codes.<br><br>* The number of 2xx status codes and the number of each status code in that category.<br><br>* The number of 3xx status codes and the number of each status code in that category.<br><br>* The number of 4xx status codes and the number of each status code in that category.<br><br>* The number of 5xx status codes and the number of each status code in that category. |
|Origin Request Response Time |Indicates the average time CDN takes to receive responses from the origin, measured in milliseconds (ms). For an origin request, the response time is the time span between the following two time points:<br><br><br>* CDN receives the first byte of the origin response.<br><br>* CDN receives the last byte of the origin response.<br><br><br>The time at which the CDN receives the last byte of the origin's response is recorded as the completion time for that origin request. |
