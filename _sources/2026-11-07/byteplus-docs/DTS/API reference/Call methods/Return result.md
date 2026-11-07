---
title: "Return result"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/response_results"
---

This topic introduces the API return result information of Database Transmission Service (DTS).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An HTTP status code of 200 indicates that the interface request succeeded.</div>


* <div data-tips="true" data-tips-type="tip">All non\-200 HTTP status codes indicate that the interface request failed. The specific failure message is returned in JSON format.</div>


* **Return result of the successful request call**

   ```Plain Text
   {
       "ResponseMetadata": {
           "RequestId": "20230320102619F78568E65FC7880F296B",
           "Action": "StartTransmissionTask",
           "Version": "2022-10-01",
           "Service": "dts",
           "Region": "cn-beijing"
       },
       "Result": null
   }
   ```
   


The parameter information returned by the request call is as follows:


* ResponseMetadata and its internal RequestId, Action, Version, Service, and Region are fixed fields. They will be returned as long as an API request is initiated, whether the request succeeds or not.

* RequestId is the unique identifier of an API request. If an anomaly occurs with the API, you can [submit a ticket](https://console.byteplus.com/workorder/create) for technical support by providing the ID to locate the problem.

* Result is a fixed field, and the content of this field may vary depending on the product. Refer to the actual return. This field will not be returned when the request call fails.

* In addition to the fixed fields, the rest are fields defined by the specific API. For the fields returned by different APIs, refer to the specific definitions in the API documentation.

* **Return result of the failed request call**

   ```Plain Text
   {
       "ResponseMetadata": {
           "RequestId": "2023032010312552E6F4178AA5850F712E",
           "Action": "ModifyTransmissionTask",
           "Version": "2022-10-01",
           "Service": "dts",
           "Region": "cn-beijing",
           "Error": {
               "CodeN": 100008,
               "Code": "InvalidActionOrVersion",
               "Message": "Could not find operation ModifyTransmissionTask for version 2022-10-01"
           }
       }
   }
   ```
   

* The error field will definitely appear when the request call fails. The error field contains the code and message fields, where:

   * Code indicates the specific error code. You can first find the reason and solution in the public error code and the error code list corresponding to the current interface, based on the error code.

   * Message will give the specific reason for the error. This text may change with business development or experience optimization.

* The Result field is not returned when the request call fails.
