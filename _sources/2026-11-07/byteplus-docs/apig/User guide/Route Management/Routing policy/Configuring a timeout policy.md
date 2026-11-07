---
title: "Configuring a timeout policy"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Configuring_a_timeout_policy"
---

The API gateway supports enabling response timeout feature for routes and configuring the timeout duration. You can configure the maximum time to wait for a response result as needed. If the API gateway does not receive a response from the backend service within the specified time, the gateway will return a response with an HTTP status code of `504`.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A route has been created. For details refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **Route Management \> Route List**.

4. In the route list, select the target route and click **Edit ** in the **Actions** column.

5. In the advanced **configuration** area of the edit route page, check the **Enable** box after **timeout**, and set the timeout duration.

   
   |Parameter |Description |
   |---|---|
   |Timeout |After the API gateway forwards the request to the backend service, it waits for the backend service to respond to the request until the upper time limit.<br><br><br>* Enable: A specific timeout duration needs to be configured.<br><br>* Disable: No timeout limit. |
   

6. Click **Confirm** to complete the configuration.


<span id="3rJuUdE3"></span>
## Result validation

After configuring, you can use the API gateway to access the backend Service and verify whether the configured timeout is effective.
