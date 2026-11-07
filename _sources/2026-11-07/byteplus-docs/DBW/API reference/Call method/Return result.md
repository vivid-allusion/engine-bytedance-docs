---
title: "Return result"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/responses"
---

This topic describes the API return results of Database Workshop (DBW).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An HTTP status code of 200 indicates that the interface request succeeded.</div>


* <div data-tips="true" data-tips-type="tip">All non\-200 HTTP status codes indicate that the interface request failed. The specific failure message is returned in JSON format.</div>



<span id=".6L-U5Zue57uT5p6c56S65L6L"></span>
## Return result example


* **Return result of the successful request call**

   ```json
   {
       "ResponseMetadata" : {
           "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7eddfbe",
           "Action": "DataConnectInstance",
           "Version": "2018-01-01",
           "Service": "dbw",
           "Region": "cn-beijing"
       },
    
       "Result": {/* 具体业务的返回信息 */
             "SessionId" : "MTU3MTc4MTIwMjQ1OTc3NDk3Ni8xNTcxNzgxMjA0MzMwNDM4NjU2",
             "DatabaseName": "information_schema"
       }
   }
   ```
   


The parameter information returned by the request call is as follows:


* ResponseMetadata and its internal `RequestId`, `Action`, `Version`, `Service`, and `Region` are fixed fields. They will be returned as long as an API request is initiated, whether the request succeeds or not.

* RequestId is the unique identifier of an API request. If an anomaly occurs with the API, you can [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/) for technical support by providing the ID to locate the problem.

* Result is a fixed field, and the content of this field may vary depending on the product. Refer to the actual return. This field will not be returned when the request call fails.

* In addition to the fixed fields, the rest are fields defined by the specific API. For the fields returned by different APIs, refer to the specific definitions in the API documentation.

* **Return result of the failed request call**

   ```json
   {
       "ResponseMetadata": {
           "RequestId": "202210141739510101742551810409CE5E",
           "Action": "DataExecCommands",
           "Version": "2018-01-01",
           "Service": "dbw",
           "Region": "cn-beijing",
           "Error": {
               "Code": "ParamError",
               "Message": "The request processing has failed due to some unknown error, exception or failure."
           }
       },
       "Result": null
   }
   ```
   

* The `Error` field will definitely appear when the request call fails. The `Error` field contains the `Code` and `Message` fields, where:

   * `Code` indicates the specific error code. You can first find the reason and solution in the public error code and the error code list corresponding to the current interface, based on the error code.

   * `Message` will give the specific reason for the error. This text may change with business development or experience optimization.

* The `Result` field is not returned when the request call fails.
