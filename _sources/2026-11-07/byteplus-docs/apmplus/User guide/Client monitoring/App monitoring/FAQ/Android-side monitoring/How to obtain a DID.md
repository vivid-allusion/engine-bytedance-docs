---
title: "How to obtain a DID"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_obtain_a_DID"
---

First, determine whether DID has already been defined by the business.

Android:


* If the business process has already been customized, use the custom DID configuration directly, that is, the value returned by `getDid()` during initialization.

* If there is no business customization: call the `ApmInsightAgent.getDid()` interface to obtain the internal default DID.


Harmony:


* If the business logic has already been customized, use the custom DID configuration directly, that is, the value returned by `getDeviceId()` during initialization.

* If the business has not customized HiLog log filtering for `device_id`, you can view the value of device_id included in the parameter of the reported URL.
