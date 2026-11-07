---
title: "DeleteSmsTemplate"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-deletesmstemplate"
---

Use the DeleteSmsTemplate API to delete text message templates. It's recommended you use SDK to call the DeleteSmsTemplate API.

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
|id |string |Yes |169\*\*\* |The template ID. |
|isOrder |bool |Yes |true |Whether the template is under approval. |


**Example of request payload**

```json
{
    "subAccount":"A123****",
    "id":"169***",
    "isOrder":false
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
|Result |string |The result in response.The result returns only when no error occurs. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```json
{
    "ResponseMetadata":{
        "RequestId":"2022090818314901017423503804EDB6DB",
        "Action":"DeleteSmsTemplate",
        "Version":"2021-01-11",
        "Service":"volcSMS",
        "Region":"ap-singapore-1"
    },
    "Result":""
}
```


<span id="Error messages"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Message** |**Description** |**Solution** |
|---|---|---|---|
|1999 |None |A system error occurs. |Contact technical support team for help. |
|1005 |Status is not reviewing. |The template has been approved when you want to close the application ticket. |Contact technical support team for help. |
|1006 |Not existed. |The ID of the template that you want to delete does not exist. |Double check your template's ID. |
|1001 |None |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
