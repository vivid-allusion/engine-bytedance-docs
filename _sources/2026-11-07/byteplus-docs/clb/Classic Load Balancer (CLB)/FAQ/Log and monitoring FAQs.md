---
title: "Log and monitoring FAQs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Log-and-monitoring-faq"
---

* [Why does the monitoring data for the public CLB metric "Out/In Traffic" exceed the Internet bandwidth limit?](https://docs.byteplus.com/en/docs/42/11797#.5YWs572R6LSf6L295Z2H6KGh55uR5o6n5oyH5qCH4oCc5Ye65YWl5bim5a694oCd55qE55uR5o6n5pWw5o2u5Li65LuA5LmI6LaF5Ye65LqG5YWs572R5bim5a695LiK6ZmQ77yf)

* [Why do the number of active TCP connections on CLB differ from those on the backend server?](https://docs.byteplus.com/en/docs/42/11797#.5Li65LuA5LmI6LSf6L295Z2H6KGh55qEVENQ5rS76LeD6L-e5o6l5pWw5LiO5ZCO56uv5pyN5Yqh5Zmo5LiK55qE6L-e5o6l5pWw5LiN5LiA6Ie077yf)

* [How to quickly judge the response time of CLB through monitoring data?](https://docs.byteplus.com/en/docs/42/11797#.5aaC5L2V6YCa6L-H55uR5o6n5pWw5o2u5b-r6YCf5Yik5pat6LSf6L295Z2H6KGh55qE5ZON5bqU5pe26Ze077yf)

* [Why is there no log information after configuring the access log feature?](https://docs.byteplus.com/en/docs/42/11797#.6YWN572u6K6_6Zeu5pel5b-X5Yqf6IO95ZCO5Li65LuA5LmI5rKh5pyJ5pel5b-X5L-h5oGv77yf)

* [Why can't IAM users view monitoring data?](https://docs.byteplus.com/en/docs/42/11797#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf)

* [What impact do CLB's loss-related monitoring metrics (including lost connections, lost inbound and outbound packets, and lost inbound and outbound bandwidth) have on business?](https://docs.byteplus.com/en/docs/42/11797#.6LSf6L295Z2H6KGh55qE5Lii5aSx57G755uR5o6n5oyH5qCH77yI5YyF5ous5Lii5aSx6L-e5o6l5pWw44CB5Lii5aSx5Ye65YWl5YyF5pWw5ZKM5Lii5aSx5Ye65YWl5bim5a6977yJ5a-55Lia5Yqh5pyJ5LuA5LmI5b2x5ZON77yf)

* [Can historical monitoring data be viewed after unsubscribing from a CLB instance?](https://docs.byteplus.com/en/docs/42/11797#.Q0xC5a6e5L6L6YCA6K6i5ZCO5piv5ZCm5pSv5oyB5p-l55yL5Y6G5Y-y55uR5o6n5pWw5o2u77yf)

* [Why does the QPS metric for CLB monitoring show no data?](https://docs.byteplus.com/en/docs/42/11797#.Q0xC55qE55uR5o6n5oyH5qCHUVBT5Li65LuA5LmI5rKh5pyJ5pWw5o2u77yf)

* [What is the sampling interval for CloudMonitor collecting CLB monitoring data?](https://docs.byteplus.com/en/docs/42/11797#.5LqR55uR5o6n6YeH6ZuGQ0xC55uR5o6n5pWw5o2u55qE6YeH5qC36Ze06ZqU77yf)


<span id=".5YWs572R6LSf6L295Z2H6KGh55uR5o6n5oyH5qCH4oCc5Ye65YWl5bim5a694oCd55qE55uR5o6n5pWw5o2u5Li65LuA5LmI6LaF5Ye65LqG5YWs572R5bim5a695LiK6ZmQ77yf"></span>
## Why does the monitoring data for the public CLB metric "Out/In Traffic" exceed the internet bandwidth limit?

The monitoring data for the public CLB metric "Out/In Traffic" includes both internet and private network traffic, so it may exceed the internet bandwidth limit. The CLB instance specification defines the bandwidth for private network traffic. For detailed private network bandwidth limits of each specification, please refer to [Product specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

<span id=".5Li65LuA5LmI6LSf6L295Z2H6KGh55qEVENQ5rS76LeD6L-e5o6l5pWw5LiO5ZCO56uv5pyN5Yqh5Zmo5LiK55qE6L-e5o6l5pWw5LiN5LiA6Ie077yf"></span>
## Why is the number of active TCP connections on the CLB inconsistent with the number of connections on the backend server?

> The following assumes all access requests on the backend server come from CLB forwarding.


Since the layer 4 CLB directly passes through client requests by default, the active TCP connections on layer 4 listeners (TCP/UDP protocol) equal the number of connections on the backend server. If this CLB instance has only one layer 4 listener, the instance's active TCP connections also equal the number of connections on the backend server.

Because the layer 7 CLB establishes a connection with the client first, then connects to the backend server. Therefore, the active TCP connections of the layer 7 listener (HTTP/HTTPS protocol) and the layer 7 CLB instance may differ from the number of connections on the backend server.

<span id=".5aaC5L2V6YCa6L-H55uR5o6n5pWw5o2u5b-r6YCf5Yik5pat6LSf6L295Z2H6KGh55qE5ZON5bqU5pe26Ze077yf"></span>
## How to quickly judge the CLB response time through monitoring data?

The layer 7 CLB can view the average response time of an instance or listener through monitoring metrics or check the precise response time for each request in the access log.

<span id=".6YCa6L-H55uR5o6n5oyH5qCH5p-l55yLQ0xC5a6e5L6L55qE5bmz5Z2H5ZON5bqU5pe26Ze0"></span>
### View the average response time of the CLB instance via monitoring metrics


1. Log in to the [CLB Console](https://console.byteplus.com/clb/LoadBalancer).

2. Select the region of the target instance in the top menu bar.

3. Click the name of your target instance to enter the instance details page, and select the Monitoring tab.

4. Click the Instance tab to view the monitoring metrics of the instance, such as Average response time.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When multiple Layer 7 listeners exist under an instance, the instance's average response time equals the average of all Layer 7 listeners' average response times; if only one Layer 7 listener exists, the instance's average response time equals that listener's average response time.   </div>
   

<span id=".6YCa6L-H55uR5o6n5oyH5qCH5p-l55yL55uR5ZCs5Zmo55qE5bmz5Z2H5ZON5bqU5pe26Ze0"></span>
### View the average response time of the listener through monitoring metrics


1. Log in to the [CLB Console](https://console.byteplus.com/clb/LoadBalancer).

2. Select the region of the target instance in the top menu bar.

3. Click the name of your target instance to enter the instance details page, and select the Monitoring tab.

4. Click the Listener tab and select the target Layer 7 listener.

5. View the monitoring metric Average response time for the target listener.


<span id=".6YCa6L-H6K6_6Zeu5pel5b-X5p-l55yL5ZON5bqU5pe26Ze0"></span>
### Check the response time through access logs


1. See [getting access logs](https://docs.byteplus.com/en/docs/clb/Obtaining-access-logs#.5p-l55yL5pel5b-X5paH5Lu2) to obtain the log files of target instance.

2. Check the values of the fields shown in the table below in the log file to get the request response time.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the positions of each field in the log file, refer to <a href="https://docs.byteplus.com/en/docs/clb/Access-log-overview#MLdBptPB">log fields</a>.   </div>
   

   
   |Field name |Explanation |
   |---|---|
   |request_time |CLB response time, the total request processing time from receiving the first byte from the client to sending the last byte to the client. It includes the time for client request to CLB, CLB forwarding the request to the backend server, backend server responding to CLB, and CLB forwarding data to the client, measured in seconds. |
   |upstream_connect_time |Time for CLB to establish a TCP connection with the backend server, from starting connection to the backend server until sending the HTTP request, measured in seconds. |
   |upstream_header_time |Time consumed by CLB to receive HTTP headers from the backend server, that is, the time from establishing connection to the backend server until receiving the complete HTTP response headers from the backend server. The unit is seconds. |
   |upstream_response_time |Backend server response time: total time spent on the backend request, from starting connection to the backend server until receiving the full response from the backend server, measured in seconds. |
   


<span id=".6YWN572u6K6_6Zeu5pel5b-X5Yqf6IO95ZCO5Li65LuA5LmI5rKh5pyJ5pel5b-X5L-h5oGv77yf"></span>
## Why is there no log information after configuring the access log feature?


* Confirm whether CLB supports the access log feature.

   Currently, only CLBs with Layer 7 listeners (HTTP/HTTPS protocols) support the access log feature. If you only add four layers of listeners (UDP/TCP protocols) to the CLB you are viewing, access logs cannot be obtained.

* Confirm that the CLB is accessible and access requests exist.

   If the CLB is abnormal or no access requests reach the CLB, no access logs are generated after enabling access log configuration.


<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

If the IAM user is only authorized for CLB permissions and not authorized for CloudMonitor permissions, they cannot view CLB service monitoring data. Use the IAM user's main account to  to add system\-predefined CloudMonitor policy permissions to the IAM user based on actual needs.


|Policy name |Supported action |
|---|---|
|CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
|CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |


<span id=".6LSf6L295Z2H6KGh55qE5Lii5aSx57G755uR5o6n5oyH5qCH77yI5YyF5ous5Lii5aSx6L-e5o6l5pWw44CB5Lii5aSx5Ye65YWl5YyF5pWw5ZKM5Lii5aSx5Ye65YWl5bim5a6977yJ5a-55Lia5Yqh5pyJ5LuA5LmI5b2x5ZON77yf"></span>
## What impact do the CLB's loss\-related monitoring metrics (including lost connections, lost inbound/outbound packets, and lost inbound/outbound bandwidth) have on business?

The data source scenarios of CLB loss\-related monitoring metrics (including lost connections, lost inbound/outbound packets, and lost inbound/outbound bandwidth) and the impact of each scenario on business are as follows:


* Data loss caused by inbound or outbound traffic exceeding the CLB instance specification limits.

   At this time, the related business will be affected. You can [refer to changing the instance specification](https://docs.byteplus.com/en/docs/clb/CLB-instances-03) to upgrade the CLB instance specifications. For detailed information about instance types, see [Product Type and Specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no obvious traffic limit excess is shown in any monitoring metrics data, the inbound or outbound traffic exceeding the CLB instance type limits may be caused by burst traffic in seconds. In this case, it is recommended to switch the CLB instance to pay\-per\-CU billing, which costs less than changing the instance type. Pay\-as\-you\-go (Pay\-by\-CU) is currently in Beta stage. If you need a trial, please contact your account manager.   </div>
   

* Data loss caused by listener bandwidth limits.

   At this point, the related services may be affected. You can [modify the listener bandwidth limit](https://docs.byteplus.com/en/docs/clb/Editing-the-listener).

* Data loss caused by inbound access data lacking connection information, such as from network jitter or connection attempting non\-SYN initial packets.

   Related services may be affected. If exceptions occur, contact BytePlus technical support.


<span id=".Q0xC5a6e5L6L6YCA6K6i5ZCO5piv5ZCm5pSv5oyB5p-l55yL5Y6G5Y-y55uR5o6n5pWw5o2u77yf"></span>
## Can historical monitoring data be viewed after unsubscribing a CLB instance?

Unsupported. All resources related to the CLB instance are deleted upon unsubscribing and cannot be restored.

<span id=".Q0xC55qE55uR5o6n5oyH5qCHUVBT5Li65LuA5LmI5rKh5pyJ5pWw5o2u77yf"></span>
## Why is there no data for the CLB monitoring metric QPS?

The monitoring metric QPS is exclusive to Layer 7 listeners (HTTP, HTTPS protocols). Layer 4 listeners (TCP, UDP protocols) do not have this metric.

CLB supports viewing monitoring metrics separately for CLB instances and listeners. If you are viewing a Layer 4 listener or a CLB instance configured only with Layer 4 listeners, no data will appear for the QPS monitoring metric of the target CLB resource.

<span id=".5LqR55uR5o6n6YeH6ZuGQ0xC55uR5o6n5pWw5o2u55qE6YeH5qC36Ze06ZqU77yf"></span>
## What is the sampling interval for CloudMonitor to collect CLB monitoring data?

30 seconds. CloudMonitor collects CLB monitoring metrics every 30 seconds; this data represents the average value during that 30\-second period. For example, new connections are displayed in CloudMonitor as the average new connections per second over 30 seconds.
