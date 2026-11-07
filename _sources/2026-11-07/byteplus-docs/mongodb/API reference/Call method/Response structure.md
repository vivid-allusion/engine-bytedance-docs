---
title: "Response structure"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/response-structure"
---

This topic introduces the response structure used by Document Database for MongoDB.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An HTTP status code of 200 indicates that the interface request succeeded.</div>


* <div data-tips="true" data-tips-type="tip">All non\-200 HTTP status codes indicate that the interface request failed. The specific failure message is returned in JSON format.</div>



<span id=".6L-U5Zue57uT5p6c56S65L6L"></span>
## Response examples


* **Response results for successful request**

   ```json
   {
       "ResponseMetadata" : {
             "RequestId": "202202091517470102040490790603E341",
             "Action": "DescribeRegions",
             "Version": "2022-01-01",
             "Service": "mongodb",
             "Region": "cn-beijing",
         }
       "Result": { /* Response from the specific service */
             "Regions":[
                { 
                 "RegionId": "cn-beijing", 
                 "RegionName": "China (Beijing)"
                },
             ] 
       }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">ResponseMetadata and its internal RequestId, Action, Version, Service, and Region are fixed fields. They will be returned as long as an API request is initiated, whether the request succeeds or not.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">RequestId is the unique identifier of an API request. If an anomaly occurs with the API, <a href="https://console.byteplus.com/workorder/create/">submit ticket</a> for technical support by providing the ID to locate the problem.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Result is a fixed field whose content is defined by different products. This field will not be returned if the request fails.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In addition to the fixed fields, the rest are fields defined by the specific API. For the fields returned by different APIs, refer to the specific definitions in the API documentation.   </div>
   

* **Response results for failed request**

   ```json
   {
      "ResponseMetadata" : {
           "RequestId": "202202091526190102100291611503CEA0",
           "Action": "DescribeRegions",
           "Version": "2022-01-01",
           "Service": "mongodb",
           "Region": "cn-beijing",
           "Error": {
               "Code": "Failed",
               "Message": "The request processing has failed due to some unknown error, exception or failure.", 
           }
      }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Error field will definitely appear when the request call fails. The Error field contains the Code and Message fields, where:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Code indicates the specific error code. You can first find the reason and solution in the public error code and the error code list corresponding to the current interface, based on the error code.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Message will give the specific reason for the error. This text may change with business development or experience optimization.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Result field is not returned when the request call fails.   </div>
