---
title: "ApplySmsTemplate"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-applysmstemplate"
---

Use the ApplySmsTemplate API to apply for a text message template. It's recommended you use SDK to call the ApplySmsTemplate API.

<span id="Request"></span>
## Request

**HTTP method**: POST

**URL**: `https://sms.byteplusapi.com?Action=ApplySmsTemplate&Version=2021-01-11&area=overseas`

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
|Action |string |Yes |ApplySmsTemplate |The name of this API. |
|Version |string |Yes |2021\-01\-11 |The version of this API. |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Example of value** |**Description** |
|---|---|---|---|---|
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |
|area |string |Yes |overseas |The countries or regions of the message group: overseas. It means countries or regions outside Mainland China. |
|channelType |string |Yes |I18N_OTP |The enabled message type, including:<br><br><br>* I18N_OTP: International one\-time password message.<br><br>* I18N_MKT: International marketing message. |
|name |string |Yes |cx_test |The template name. |
|content |string |Yes |Your verification code is$ |The template content. |
|desc |string |No |This template is used to send verification codes. |The description of your template. |
|shortUrlConfig |shortUrlConfig |No |None |Configure it when you need a short URL. |
|shortUrlConfig.isEnabled |string |No |0 |The configuration switch. 0 means disabled, and 1 means enabled. |
|shortUrlConfig.isNeedClickDetails |string |No |0 |Whether to configure a static or dynamic link. 0 means static link, and 1 means dynamic link. |


**Example of request payload**

```json
{
"subAccount":"6df864b1",
    "area":"overseas",
    "name":"template_test",
    "channelType":"I18N_OTP",
    "desc":"This template is used to send verification codes",
    "content":"Your verification code is ${code}"
    }
```


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

```json
  "ResponseMetadata":{
        "RequestId":"2022090818181501017423503804ECB4B8",
        "Action":"ApplySmsTemplate",
        "Version":"2021-01-11",
        "Service":"volcSMS",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "applyId":"169000",
        "templateId":"ST_712d9312",
        "name":"template_test",
        "content":"Your verification code is ${code}",
        "status":1,
        "reason":"",
        "createdTime":1662632296,
        "channelType":"I18N_OTP"
    }
}
```


<span id="Error messages"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Message** |**Description** |**Solution** |
|---|---|---|---|
|1999 |None |A system error occurs. |Contact technical support team for help. |
|1007 |template check failed, req:%+v, msg:%s |The template's format is wrong. |Double check your template's format. |
|1001 |None |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
