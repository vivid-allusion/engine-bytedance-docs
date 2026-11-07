---
title: "GetSmsTemplateAndOrderDetail"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-getsmstemplateandorderdetail"
---

Use the GetSmsTemplateAndOrderDetail OpenAPI to query the information of a specific template or template order

<span id="f6397325"></span>
## Request

**HTTP method**: GET

**URL**: https://sms.byteplusapi.com/sms/openapi/sms_template_and_order

**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Authorization |Basic base64 (username:password). For example: Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY= |Find the username and password information on the **Service Settings of Admin Settings** page in the SMS console |Yes |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |
|templateId |string |Yes |ST_712\*\*\*\* |The template ID. |


**Example of request payload**

```JSON
{
    "subAccount" : "108c6df6",
    "templateId" : "ST_7a0ae33e"
}
```


<span id="8ce048b8"></span>
## Response

**Response parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |ResponseMetadata |The parameter values in your request headers. |
|ResponseMetadata.RequestId |string |ID number of the request. |
|ResponseMetadata.Action |string |Empty string |
|ResponseMetadata.Version |string |Empty string |
|ResponseMetadata.Service |string |Empty string |
|ResponseMetadata.Region |string |Region info, ignored |
|Result |Result |The result in response. The result returns only when no error occurs. |
|Result.id |string |The applyId in the response result of ApplySmsTemplate. |
|Result.templateId |string |The template ID. |
|Result.channelType |string |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|Result.name |string |The template's name. |
|Result.content |string |The template's content. |
|Result.status |int |The approval status. 1: In progress; 2: Failed; 3: Passed; 4: Closed, which means you have deleted the template; 5: Exempted, which means your template is exempted from the approval. |
|Result.isOrder |bool |Whether the template is under approval. |
|Result.reason |string |The reason for the approval. |
|Result.createdTime |int |Time when the message group was created. |
|Result.shortUrlConfig |shortUrlConfig |The configuration for short links. Only marketing messages have this parameter. |
|Result.shortUrlConfig.isEnabled |string |The configuration switch. 0 means disabled, and 1 means enabled. |
|Result.shortUrlConfig.rawUrl |string |The original long link of the short link. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024011207282514804EDC307DD60DF365",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": "BOE"
    },
    "Result": {
        "id": "2088",
        "templateId": "ST_7a4f584e",
        "name": "111",
        "content": "1111",
        "status": 1,
        "reason": "",
        "createdTime": 1703757071,
        "channelType": "I18N_MKT",
        "channelTypeName": "International marketing message",
        "isOrder": true,
        "openId": "",
        "shortUrlConfig": {
            "isEnabled": "",
            "belong": "",
            "token": "",
            "type": "",
            "rawUrl": "",
            "expiration": "",
            "ua_check_strategy": ""
        },
        "signature": "",
        "theme": "",
        "desc": "",
        "carrierStatus": {},
        "approveTime": 0,
        "expireTime": 0,
        "restValidDays": 0
    }
}
```


<span id="d68b47bd"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Description** |**Solution** |
|---|---|---|
|1999 |A system error occurs. |Contact the technical support team for help. |
|1001 |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
