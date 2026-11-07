---
title: "How do I fix common HTTP error codes?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Common-HTTP-error-codes-occur"
---

Requests may encounter HTTP error codes other than 2xx or 3xx, for example, 502, 503, 413, and 499. View logs to determine whether the error was returned by the Ingress Controller. If the error was returned by the Ingress Controller, follow the instructions below to fix it:


|**HTTP status code** |**Cause analysis** |**Solution** |
|---|---|---|
|413 |The request size exceeds the maximum limit. |Increase the value of `proxy-body-size` in the ingress\-nginx\-controller ConfigMap (the default value is 20M). |
|499 |The client disconnected prematurely for some reason, which may not be a component or back\-end service issue. |* If a small number of 499 errors occur, it may be normal depending on the business scenario and can be ignored.<br><br>* If a large number of 499 errors occur, check whether the back\-end service processing time and front\-end request timeout meet expectations. |
|502 |The Ingress Controller cannot connect to the backend properly. |* Check whether the back\-end service load is normal. If the load is too high, try scaling out the back\-end service.<br><br>* By default, the Ingress Controller uses HTTP/1.1 and persistent connections to access back\-end services. Ensure the idle timeout for back\-end long connections is longer than the default 900\-second timeout of the Ingress Controller.<br><br>* Check whether the back\-end service port configuration is correct and whether it can be manually accessed in the Controller Pod. |
|503 |The Ingress Controller fails to find a back\-end pod, or none of the pods is accessible. |* View the solutions to HTTP 502 errors.<br><br>* Check back\-end service readiness and configure a reasonable health check.<br><br>* Check whether the back\-end service configuration is correct and whether an endpoint exists. |
