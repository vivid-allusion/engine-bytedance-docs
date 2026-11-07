---
title: "Configure a retry policy"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Configuring_a_retry_policy"
---

The API gateway supports configuring a retry policy for routes; you can specify retry conditions to automatically retry failed requests. For example: failure to connect to the backend service, or retrying the request when a specified HTTP status code is returned.

<span id="vILF4Zys"></span>
## Background information

The API gateway allows you to configure retry conditions for different protocols. The specific conditions and description are shown in the following table.


|**Protocol** |**Reset conditions** |**Condition description** |
|---|---|---|
|HTTP |5xx |The backend service returns a `5xx` status code, or the connection is disconnected, reset, or a read timeout occurs. |
||reset |Disconnection, reset, and read timeout events occur. |
||connect\-failure |Failed to connect to the backend Service. A request error occurred. |
||refused\-stream |The backend Service uses the `REFUSED_STREAM` error code to reset the stream. |
||retriable\-status\-codes |The HTTP status code returned by the backend service matches the retry status code specified by the user. |
|gRPC |cancelled |The gRPC status code in the response header of the backend service is `cancelled`. |
||deadline\-exceeded |The gRPC status code in the backend service response header is `deadline-exceeded`. |
||internal |The gRPC status code in the response header of the backend service is `internal`. |
||resource\-exhausted |The gRPC status code in the response header of the backend service is `resource-exhausted`. |
||unavailable |The gRPC status code in the backend service response header is `unavailable`. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The route has been created. For details, refer to [add route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. Select **Route Management \> Route List** in the left navigation bar.

4. In the routing list, select the target route and click **Edit** under the **Actions** column.

5. On the edit route page, in the **Advanced configuration** region, check **Retry**, then check **Enable** that appears after retry, and configure the retry conditions.

   
   |Parameter |Description |
   |---|---|
   |Specify scenario |Configure retry conditions or status codes:<br><br><br>* **Retry condition**: Select system preset retry conditions from the dropdown menu. Preset retry conditions are provided for both HTTP and gRPC protocols.<br><br>* **Status code**: Configure HTTP status codes that require retry, for example, the `403` status code.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Retry condition</strong> and <strong>Status code</strong> have an <strong>or</strong> relationship, meaning that if a request matches either one, the request will be automatically retried.</div><br> |
   |Request retry |Configure the number of request retries and the time for a single retry. |
   

6. Click **Confirm**.


<span id="3nmRVd3w"></span>
## Result validation

After configuration is complete, you can use the API gateway to access the backend Service. When an access request meets the **retry conditions** or **status codes**, the system will automatically retry according to the configuration.
