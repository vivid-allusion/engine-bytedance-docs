---
title: "Request response"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response"
---

The following sections use the `GetUser` API of the IAM service as an example. The sample responses of a successful request and a failed request are as follows:

<span id="899a7db6"></span>
## Success response

See the following example:

```json
{
    "ResponseMetadata": {
        "RequestId": "202112021830130102252430810768****",
        "Action": "GetUser",
        "Version": "2018-01-01",
        "Service": "iam"
    },
    "Result": {
        "User": {
            "CreateDate": "20210428T023119Z",
            "UpdateDate": "20211124T100123Z",
            "Status": "active",
            "AccountId": 20000*****,
            "UserName": "demo****",
            "Description": "",
            "DisplayName": "",
            "Email": "******",
            "EmailIsVerify": false,
            "MobilePhone": "******",
            "MobilePhoneIsVerify": false,
            "Trn": "trn:iam::20000*****:user/demo****"
        }
    }
}
```


When a request is processed successfully, the response contains `ResponseMetadata` and `Result`. The descriptions of related fields are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The returned value of <code>Result</code> depends on the function of the requested API operation.</div>



|**Field name** |**Description** |
|---|---|
|RequestID |The unique ID of the API request. |
|Action |The name of the requested API operation. |
|Version |The version of the requested API. |
|Service |The name of the requested service. |


<span id="59f4a3a1"></span>
## Error response

See the following example:

```json
{
    "ResponseMetadata": {
        "RequestId": "20211202183645010225243125026D****",
        "Action": "GetUser",
        "Version": "2018-01-01",
        "Service": "iam",
        "Region": "ap-singapore-1",
        "Error": {
            "CodeN": 100010,
            "Code": "SignatureDoesNotMatch",
            "Message": "The request signature we calculated does not match the signature you provided. Check your Secret Access Key and signing method. Consult the service documentation for details."
        }
    }
}
```


When a request fails to be processed, the response does not contain `Result`, but contains `Error` in `ResponseMetadata`. The descriptions of related fields are as follows:


|**Field name** |**Description** |
|---|---|
|Error |This field indicates that the API request has been failed. |
|CodeN |The ID of the error code (some APIs do not return CodeN). |
|Code |The description of the error. |
|Message |The description of the specific causes of an error. |
|RequestID |The unique ID of the API request. When a problem cannot be solved independently, you can contact our support team and provide the `RequestID` for troubleshooting. |
