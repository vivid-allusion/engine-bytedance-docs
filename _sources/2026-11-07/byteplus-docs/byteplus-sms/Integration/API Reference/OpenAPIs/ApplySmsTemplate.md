---
title: "ApplySmsTemplate"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-applysmstemplate_1"
---

Use the ApplySmsTemplate OpenAPI to apply for a text message template

<span id="1b483800"></span>
## Request

**HTTP method**: POST

**URL**: https://sms.byteplusapi.com/sms/openapi/sms_template

**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Authorization |Basic base64 (username:password). For example: Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY= |Find the username and password information on the **Service Settings of Admin Settings** page in the SMS console |Yes |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Example of value** |**Description** |
|---|---|---|---|---|
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |
|channelType |string |Yes |I18N_OTP |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|name |string |Yes |cx_test |The template name. |
|content |string |Yes |Your verification code is$ |The template content. |
|desc |string |No |This template is used to send verification codes. |The description of your template. |
|shortUrlConfig |shortUrlConfig |No |None |Configure it when you need a short URL. |
|shortUrlConfig.isEnabled |string |No |0 |The configuration switch. 0 means disabled, and 1 means enabled. |
|shortUrlConfig.isNeedClickDetails |string |No |0 |Whether to configure a static or dynamic link. 0 means static link, and 1 means dynamic link. |


**Example of request payload**

```JSON
{ 
    "subAccount":"7a76864c", 
    "name":"template_test_123", 
    "channelType":"I18N_OTP", 
    "desc":"This template is used to send verification codes", 
    "content":"Your verification code is ${code}" 
}
```


<span id="2ea2c87c"></span>
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
|Result |Result |The result in response.The result returns only when no error occurs. |
|Result.applyId |string |The ID number of the applied template. |
|Result.templateId |string |The template ID. |
|Result.channelType |string |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|Result.name |string |The name of the template. |
|Result.content |string |The content of template. |
|Result.status |int |The approval status.<br><br><br>* 1: In progress;<br><br>* 2: Failed;<br><br>* 3: Passed;<br><br>* 4: Closed, which means you have deleted the template;<br><br>* 5: Exempted, which means your template is exempted from the approval. |
|Result.createdTime |int |Time when the message group was created. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202401120705127BB899FEAD4E8B0BD130",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": "BOE"
    },
    "Result": {
        "applyId": "2106",
        "templateId": "ST_7a984b2a",
        "openId": "",
        "name": "template_test_123",
        "content": "Your verification code is ${code}",
        "status": 1,
        "reason": "",
        "createdTime": 1705043113,
        "channelType": "I18N_OTP",
        "channelTypeName": ""
    }
}
```


<span id="f00a31a6"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Description** |**Solution** |
|---|---|---|
|1999 |A system error occurs. |Contact the technical support team for help. |
|1001 |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
