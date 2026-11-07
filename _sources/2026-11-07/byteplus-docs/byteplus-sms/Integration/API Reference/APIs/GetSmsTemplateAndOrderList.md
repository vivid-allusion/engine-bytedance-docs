---
title: "GetSmsTemplateAndOrderList"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-getsmstemplateandorderlist"
---

Use the GetSmsTemplateAndOrderList API to get all the templates' information. It's recommended you use SDK to call the GetSmsTemplateAndOrderList API.

<span id="Request"></span>
## Request

**HTTP method**: GET

**Base URL**: `https://sms.byteplusapi.com?Action=ApplySmsTemplate&Version=2021-01-11&area=overseas`

**Header parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|AccessKey |string |Yes |AKLTNzEzY2\*\*\*\* |The access key ID of your BytePlus account. Click [here](https://console.byteplus.com/iam/keymanage) to obtain it. |
|SecretKey |string |Yes |RGTLuSHvnYxn\*\*\*\* |The secret access key ID of your BytePlus account. Click [here](https://console.byteplus.com/iam/keymanage) to obtain it. |
|ServiceName |string |Yes |volcSMS |The SMS service name. |
|Region |string |Yes |ap\-singapore\-1 |The service region name. |
|Content\-Type |string |Yes |application/json;charset=utf\-8 |The structured format of the request body. The Content\-Type of SMS service is `application/json; charset=utf-8`. |


**Query parameters**


|**Parameter** |**Type** |**Required** |**Value** |**Description** |
|---|---|---|---|---|
|Action |string |Yes |GetSmsTemplateAndOrderList |The name of this API. |
|Version |string |Yes |2021\-01\-11 |The version of this API. |
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |
|area |string |Yes |overseas |The countries or regions of the message group:<br><br><br>* overseas: Countries or regions outside Mainland China<br><br>* all: All the countries |
|templateId |string |No |ST_712\*\*\*\* |The template ID. |
|name |string |No |test |The template name. |
|channelType |string |No |I18N_OTP |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message<br><br>* I18N_MKT: International marketing message |
|content |string |No |Your verification code is $ |The template content. |


**Request example**

`https://sms.byteplusapi.com??Action=GetSmsTemplateAndOrderList&Version=2021-01-11&area=overseas&subAccount=19cb0b72`

<span id="Response"></span>
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
|Result |string |The result in response.<br><br>**Note**: The result returns only when no error occurs. |
|Result.list |[]SmsTemplateInfo |The template list. |
|Result.id |string |The `applyId` in the response result of `ApplySmsTemplate`. |
|Result.templateId |string |The template ID. |
|Result.channelType |string |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|Result.name |string |The template's name. |
|Result.content |string |The template's content. |
|Result.status |int |The approval status. 1: In progress; 2: Failed; 3: Passed; 4: Closed, which means you have deleted the template; 5: Exempted, which means your template is exempted from the approval. |
|Result.isOrder |bool |Whether the template is under approval. |
|Result.reason |string |The reason for the approval. |
|Result.createdTime |int |Time when the message group was created. |
|Result.shortUrlConfig |shortUrlConfig |The configuration for short links. Only marketing messages have this parameter. |
|Result.isEnabled |string |The configuration switch. 0 means disabled, and 1 means enabled. |
|Result.rawUrl |string |The original long link of the short link. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```json
 "ResponseMetadata":{
        "RequestId":"202209081707130102080361061D370281",
        "Action":"GetSmsTemplateAndOrderList",
        "Version":"2021-01-11",
        "Service":"volcSMS",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "list":[
            {
                "id":"59510",
                "templateId":"ST_6ed69cd9",
                "name":"template_test_1",
                "content":"Your verification code is ${code}",
                "status":3,
                "reason":"",
                "createdTime":1652167628,
                "channelType":"I18N_NTC",
                "isOrder":true,
                "shortUrlConfig":{
                    "isEnabled":"0"
                }
            },
            {
                "id":"55040",
                "templateId":"ST_6df45f41",
                "name":"template_test_2",
                "content":"Hi! Check your order status here: https://shortcm.xyz/order",
                "status":3,
                "reason":"",
                "createdTime":1648135626,
                "channelType":"I18N_MKT",
                "isOrder":false,
                "shortUrlConfig":{
                    "isEnabled":"1",
                    "rawUrl":"https://docs.byteplus.com/byteplus-sms/docs"
                }
            }
        ]
    }
}
```


<span id="Error messages"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Message** |**Description** |**Solution** |
|---|---|---|---|
|1999 |None |A system error occurs. |Contact technical support team for help. |
|1015 |exceed qps limit. |The request exceeds the API's QPS limit. |Contact technical support team for help. |
|1001 |None |Incorrect values for parameters. |Refer to the Request section and use the correct values for parameters. |
