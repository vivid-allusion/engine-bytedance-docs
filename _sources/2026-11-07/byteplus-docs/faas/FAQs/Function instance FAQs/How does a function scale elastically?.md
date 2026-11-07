---
title: "How does a function scale elastically?"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/How_does_a_function_scale_elastically"
---

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Event functions, web applications, tasks, and other function types do not support custom elastic scaling policies; only microservices applications support them. To configure elastic scaling policies for microservices applications, see <a href="https://docs.byteplus.com/en/docs/faas/Elastic_scaling">Auto\-scaling</a>.</div>


veFaaS automatically scales functions based on business traffic, dynamically adjusting the number of instances to match the request load.


* **Expand**: When business traffic increases, the system automatically creates new instances to handle requests.

* **Scale down**: After a request is executed, if an instance receives no new requests within one minute and its load is below the set threshold, the system automatically recycles the instance.

* **Billing**: Elastic instances do not incur compute charges when no requests are being executed.
