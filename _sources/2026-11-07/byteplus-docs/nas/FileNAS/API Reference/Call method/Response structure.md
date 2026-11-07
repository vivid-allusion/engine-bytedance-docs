---
title: "Response structure"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Response-structure"
---

This topic introduces the response structure used by PFS.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="tip">When the HTTP status code is 200, the API request is successful.</div>


* <div data-tips="true" data-tips-type="tip">When the HTTP status code is not 200, the API request fails. Detailed failure information is returned in JSON format.</div>



<span id="4f1f068b"></span>
## Response examples


* **Response results for a successful request**


```JSON
{
        "ResponseMetadata" : {
          "RequestId": "52ece640-60ba-4cf9-bf34-302fb45e****",
          "Action": "CreateFileSystem",
          "Version": "2022-01-01",
          "Service": "FileNAS",
          "Region": "ap-southeast-1"
          },
        "Result":{
        "OrderNo":"Order724371858305511****",
        "FileSystemId": "enas-ap8d820ea7****"
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="tip">ResponseMetadata and its internal fields, including RequestId, Action, Version, Service, and Region, are fixed fields that will always be returned as long as an API request is initiated, regardless of whether the request is successful or not.</div>


* <div data-tips="true" data-tips-type="tip">RequestId is a unique identifier for an API request. In case of API exceptions, you can contact technical support and provide this ID for troubleshooting.</div>


* <div data-tips="true" data-tips-type="tip">Result is a fixed field. The content of this field varies depending on the product. This field will not be returned if the request fails.</div>


* <div data-tips="true" data-tips-type="tip">Apart from the fixed fields, the remaining fields are defined by specific APIs. Refer to the respective API documentation for the returned fields of each API.</div>


* **Response results for a failed request**


```JSON
{
   "ResponseMetadata" : {
        "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7ed****",
        "Action": "CreateFileSystem",
          "Version": "2022-01-01",
          "Service": "FileNAS",
          "Region": "ap-southeast-1",
          "Error": {
            "Code": "Failed",
            "Message": "The request processing has failed due to some unknown error, exception or failure.", 
        }
   }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="tip">A failed request will always have an Error field, which contains the Code and Message fields.</div>


   * <div data-tips="true" data-tips-type="tip">Code is the specific error code. Use the code to find the corresponding cause of the error and solutions in the list of common error codes and the error codes specific to this API.</div>


   * <div data-tips="true" data-tips-type="tip">Message provides the specific reason for the error. This text may change over time as the service is updated and improved.</div>


* <div data-tips="true" data-tips-type="tip">The Result field is not returned in case of a failed request.</div>
