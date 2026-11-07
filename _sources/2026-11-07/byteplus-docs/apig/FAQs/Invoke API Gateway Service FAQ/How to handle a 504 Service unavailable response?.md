---
title: "How to handle a 504 Service unavailable response?"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/How_to_handle_a_504_Service_unavailable_response"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

when calling the API gateway service, a `504 Service unavailable` error occurs, with the response body content being `upstream connect error or disconnect/reset before headers. reset reason: connection failure`。

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


|Cause analysis |Solutions |
|---|---|
|Network link problem |Please confirm that the network link is smooth. |
|Backend service itself is abnormal |Please check the status of your backend service.<br><br><br>* Service status abnormal: please handle the backend service logic yourself.<br><br>* Service status normal: please confirm whether the associated backend service for the API gateway has been deleted.<br><br>   * Associated backend service is deleted: please log in to the [API Gateway console](https://console.byteplus.com/veapig), modify the associated backend Service for the API gateway route, and configure an accessible backend Service.<br><br>   * Associated backend Service is not deleted: please [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000170). |
|response_flags=UF |When viewing access logs, display response_flags=UF, indicating that the backend Upstream does not have a healthy IP.<br><br><br>* The backend Upstream exceeded the route's timeout and has not returned a response.<br><br>   istio Default timeout is set to 0, meaning it never times out. When you change the route timeout to a non\-zero value, this error occurs.<br><br>   Please increase the route's timeout.<br><br>* Please check whether the route's <settings\>timeout</settings\> setting is less than 15s. |
|response_flag=UT |If route.timeout is less than (num_retries+1)\*cluster.connect_timeout, although the log shows response_flag=UT, it may be a scenario with response_flags=UF. Please investigate and resolve one by one according to the scenario of response_flags=UF. Parameter description:<br><br><br>* route.timeout: default 15 seconds, includes all retry times.<br><br>* num_retries: number of retries after failure, default value is 2, num_retries+1=3, hence there will be a total of 3 requests.<br><br>* cluster.connect_timeout: The timeout for upstream connections, default is 5s. |
