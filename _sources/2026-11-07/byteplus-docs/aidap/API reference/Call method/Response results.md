---
title: "Response results"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Response_results"
---

This topic introduces the API response results information of the AI Native Database Platform.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An HTTP status code of 200 indicates that the API request succeeded.</div>


* <div data-tips="true" data-tips-type="tip">Any HTTP status code other than 200 indicates that the API request failed. The specific failure message is returned in JSON format.</div>



<span id=".6L-U5Zue57uT5p6c56S65L6L"></span>
## Response results sample


* **Response results returned when a request call succeeds**

   ```Plain Text
   {
       "ResponseMetadata" : {
             "RequestId": "52ece640-60ba-4cf9-bf34-302fb45eef4f",
             "Action": "DescribeRegions",
             "Version": "2018-01-01",
             "Service": "aidap",
             "Region": "cn-beijing"
         },
       "Result": { /* 具体业务的返回信息 */
             "Regions":[
                { 
                 "RegionId": "cn-beijing", 
                 "RegionName": "华北 2（北京）"
                }
             ] 
       }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">ResponseMetadata and its internal RequestId, Action, Version, Service, and Region are fixed fields. They will be returned as long as an API request is initiated, whether the request succeeds or not.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">RequestId is a unique identifier for an API request. If an API encounters an Abnormal state, you can <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support and provide this ID to help locate the issue.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Result is a fixed field whose content is defined by different products. The Result field is not returned when the request call fails.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In addition to the fixed fields, the rest are fields defined by the specific API. For the fields returned by different APIs, refer to the specific definitions in the API documentation.   </div>
   

* **Result returned when the request call fails**

   ```Plain Text
   {
      "ResponseMetadata" : {
           "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7eddfbe",
           "Action": "ListRegions",
           "Version": "2018-01-01",
           "Service": "aidap",
           "Region": "cn-beijing",
           "Error": {
               "Code": "Failed",
               "Message": "The request processing has failed due to some unknown error, exception or failure."
           }
      }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Error field will definitely appear when the request call fails. The Error field contains the Code and Message fields, where:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Code indicates the specific error code. You can first find the reason and solution in the public error code and the error code list corresponding to the current interface, based on the error code.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Message will give the specific reason for the error. This text may change with business development or experience optimization.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Result field is not returned when the request call fails.   </div>
