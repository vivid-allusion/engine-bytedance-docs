---
title: "GetSmsTemplateAndOrderList"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-getsmstemplateandorderlist_1"
---

Use the GetSmsTemplateAndOrderList OpenAPI to get all the templates' information.

<span id="49e40e52"></span>
## Request

**HTTP method**: GET

**URL**: https://sms.byteplusapi.com/sms/openapi/sms_template_and_order_list

**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Authorization |Basic base64 (username:password). For example: Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY= |Find the username and password information on the **Service Settings of Admin Settings** page in the SMS console |Yes |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |
|templateId |string |No |ST_712\*\*\*\* |The template ID. |
|name |string |No |test |The template name. |
|channelType |string |No |I18N_OTP |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message<br><br>* I18N_MKT: International marketing message |
|content |string |No |Your verification code is $ |The template content. |


**Example of request payload**

```JSON
{
    "subAccount" : "108c6df6"
}
```


<span id="10303f9e"></span>
## Response

**Response parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|ResponseMetadata |ResponseMetadata |The parameter values in your request headers. |
|ResponseMetadata.RequestId |string |ID number of the request. |
|ResponseMetadata.Action |string |Empty string |
|ResponseMetadata.Version |string |Empty string |
|ResponseMetadata.Service |string |Empty string |
|ResponseMetadata.Region |string |The region requested. |
|Result |string |The result in response.<br><br>**Note**: The result returns only when no error occurs. |
|Result.list |Array |The template list. |
|Result.list.id |string |The applyId in the response result of ApplySmsTemplate. |
|Result.list.templateId |string |The template ID. |
|Result.list.channelType |string |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|Result.list.name |string |The template's name. |
|Result.list.content |string |The template's content. |
|Result.list.status |int |The approval status. 1: In progress; 2: Failed; 3: Passed; 4: Closed, which means you have deleted the template; 5: Exempted, which means your template is exempted from the approval. |
|Result.list.isOrder |bool |Whether the template is under approval. |
|Result.list.reason |string |The reason for the approval. |
|Result.list.createdTime |int |Time when the message group was created. |
|Result.list.shortUrlConfig |shortUrlConfig |The configuration for short links. Only marketing messages have this parameter. |
|Result.list.shortUrlConfig.isEnabled |string |The configuration switch. 0 means disabled, and 1 means enabled. |
|Result.list.shortUrlConfig.rawUrl |string |The original long link of the short link. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240112065234DFF25597FF89980B0AAA",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": "BOE"
    },
    "Result": {
        "list": [
            {
                "id": "92",
                "templateId": "ST_7a22fd28",
                "name": "testTemplate",
                "content": "${value}",
                "status": 3,
                "reason": "",
                "createdTime": 1702974278,
                "channelType": "I18N_MKT",
                "channelTypeName": "International marketing message",
                "isOrder": false,
                "openId": "",
                "shortUrlConfig": {
                    "isEnabled": "0",
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
        ],
        "total": 1
    }
}
```


<span id="f09baae9"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Message** |**Description** |**Solution** |
|---|---|---|---|
|1999 |None |A system error occurs. |Contact the technical support team for help. |
|1015 |exceed qps limit. |The request exceeds the API's QPS limit. |Contact the technical support team for help. |
|1001 |None |Incorrect values for parameters. |Refer to the Request section and use the correct values for parameters. |
