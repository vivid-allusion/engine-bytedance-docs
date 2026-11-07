---
title: "How to handle \"503 Service unavailable\" response?"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/How_to_handle_503_Service_unavailable_response"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When calling the API Gateway Service, a `503 Service unavailable` error is returned, and the Response Body contains `upstream connect error or disconnect/reset before headers. reset reason: connection failure`。

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


|Cause analysis |Solutions |
|---|---|
|Network link issue |Please confirm that the network link is clear. |
|Backend service itself is abnormal |Please check the status of your backend service.<br><br><br>* Service status is abnormal: Please handle the backend service business logic on your own.<br><br>* Service status is normal: Please confirm whether the backend service associated with the API Gateway has been deleted.<br><br>   * The associated backend service has been deleted: please log in to the [API Gateway console](https://console.byteplus.com/veapig), modify the backend service associated with the API Gateway route, and configure it to an accessible backend service.<br><br>   * The associated backend service has not been deleted: please [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000170). |
|response_flags=UF |When viewing the access log, the display response_flags=UF indicates that the connection to the upstream Upstream can not be made.<br><br><br>* The backend IP can not be pinged within the gateway. Please set the Security groups.<br><br>   For details, refer to [Creating an Elastic Compute Service type upstream](https://docs.byteplus.com/en/docs/apig/Elastic_Compute_Service_type_Upstream) and [Creating a Vital Kubernetes Engine type upstream](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream).<br><br>* The Security groups are set, and the gateway cannot ping the backend IP, indicating that the upstream host, which has been taken offline, has not been removed from the Upstream.<br><br>   * ECS type Upstream: After the ECS is offline or deleted, the gateway ECS type Upstream is not synchronously updated. Please update the ECS Upstream promptly.<br><br>   * K8s type Upstream: the gateway\-controller sync failed. Please investigate whether the gateway\-controller has crashed and promptly restore the gateway\-controller.<br><br>* The Security groups are set, the backend IP can be pinged within the gateway, but telnet to the Upstream host port failed, indicating that the port of the Upstream host is incorrect.<br><br>   Please modify the port of the Upstream host to the correct port. |
|response_flags=UC |Viewing the access log shows response_flags=UC, indicating that during the gateway's forwarding request, the backend terminated the TCP connection from the gateway to the backend.<br><br><br>* Indicates that the gateway's UpstreamIdleTimeout is greater than the backend's idleTimeout. After the backend configuration's idletimeout expires, it sends a FIN to turn off the connection with the gateway, and the gateway side forwards the request reusing this connection.<br><br>   Please adjust the gateway UpstreamIdleTimeout to be less than the backend idleTimeout. |
|response_flags=UH |Viewing the access log shows response_flags=UH, indicating that the backend Upstream does not have a healthy IP.<br><br>Please check whether the k8s Service has available Endpoints. |
