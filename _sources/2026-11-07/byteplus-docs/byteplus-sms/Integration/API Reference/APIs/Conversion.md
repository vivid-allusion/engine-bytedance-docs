---
title: "Conversion"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-conversion"
---

Use the Conversion API to report successful conversions by uploading the MessageIDs of SMS messages that have achieved their intended goals, such as link clicks, purchases, or OTP verifications. With MessageIDs, BytePlus can accurately calculate the conversion rate for SMS.

<span id="e6279095"></span>
## Request

**HTTP Method**: POST

**URL**:


* http://sms.byteplusapi.com/sms/conversion

* https://sms.byteplusapi.com/sms/conversion


**Header parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|ServiceName |string |Yes |volcSMS |The SMS service name. |
|Region |string |Yes |ap\-singapore\-1 |The service region name. |
|Content\-Type |string |Yes |application/json;charset=utf\-8 |The structured format of the request body. The Content\-Type of SMS service is application/json; charset=utf\-8. |


**Query parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|Action |string |Yes |Conversion |The name of this API. |
|Version |string |Yes |2020\-01\-01 |The version of this API. |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Example of value** |**Description** |
|---|---|---|---|---|
|MessageIDs |string |Yes |["b69aeb31\-1e8b\-48c9\-ba5f\-160b761a2eb0","b34779e3\-78a6\-4ed9\-9074\-84a3f30b4fc0"] |The `MessageID` parameter returned from `sendSMS`, `SendBatchSms`, or `SendSmsVerifyCode` via HTTP, with a length limit of 1\-100. SMPP placeholders are supported. |


**Request example**

```JSON
{
    "MessageIDs":[
        "b69aeb31-1e8b-48c9-ba5f-160b761a2eb0",
        "b34779e3-78a6-4ed9-9074-84a3f30b4fc0"
    ]
}
```


<span id="10c928c4"></span>
## Response

**Response parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |ResponseMetadata |The parameter values in your request headers. |
|ResponseMetadata.RequestId |string |ID number of the request. |
|ResponseMetadata.Action |string |The HTTP method of the request. |
|ResponseMetadata.Version |string |The version of the request. |
|ResponseMetadata.Service |string |The service requested. |
|ResponseMetadata.Region |string |The region requested. |
|Result |Result |The result in the response. The result returns only when no error occurs. |
|Error |Error |The error messages. For details, refer to the Error messages section. |


**Example of successful response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "021668604596455fdbddc0200ff00060a925dd300000730a34a8e",
        "Action": "Conversion",
        "Version": "2020-01-01",
        "Service": "volcSMS",
        "Region": "ap-singapore-1"
    },
    "Result": ""
}
```


**Example of failed response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "021668604278414fdbddc0200ff00060a925dd300000730b15ce0",
        "Action": "Conversion",
        "Version": "2020-01-01",
        "Service": "volcSMS",
        "Region": "ap-singapore-1",
        "Error": {
            "Code": "ZJ10200",
            "Message": "The length of MessageIDs should be between 1 and 100"
        }
    }
}
```


<span id="a1e0a55f"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Message** |**Description** |
|---|---|---|
|RE:0000 |Authentication failed |Please check if the parameters are used correctly or refer to the authentication processing in the SDK. |
|RE:0001 |SMS service not activated |Please check if the current AccessKey has already activated SMS service. If the SMS service has been activated, please refer to the SMS service documentation to call the interface. |
|RE:0002 |Account shutdown |Please contact BytePlus customer service for confirmation. |
|RE:0003 |Subaccount not existing |Please fill in the correct SMS Account, which is the message group ID. |
|RE:0004 |Signature error |Please confirm if the signature exists under the corresponding SMS account, or log in to the SMS service console to check if the signature has been approved on the SMS signature page. |
|RE:0005 |Template error |Please check if the template exists under the corresponding SMS account, or log in to the SMS service console to check if the template has been approved on the SMS template page. |
|RE:0006 |Phone number format error |Please pass in the correct format for the parameter PhoneNumbers. |
|RE:0007 |IP verification error |The IP whitelist has been activated. Please contact BytePlus customer service to confirm if the current IP has been whitelisted. |
|RE:0008 |OpenAPI authentication error |Please check if the parameters are used correctly or refer to the authentication processing in the SDK. |
|RE:0009 |Request parameters error |Please check if the parameters are correct according to the interface documentation. |
|RE:0010 |Account charge overdue |Please log in to the expense center of the console to check if the balance is sufficient. |
|RE:0011 |Unsupport area |Please distribute or apply for SMS distribution within the allowed regions. |
|RE:0012 |Unsupport send type |Please log in to the console, click Edit in the message group list, and check if the allowed message types are checked. |
|RE:0013 |Sending volume exceeds threshold |Please check the upper limit setting for sending messages on the console. |
|RE:0014 |Decryption failed |Decryption failed, please check the encryption configuration on the console. |
|RE:0500 |Unknown interaction error |Please try calling the interface again. |
