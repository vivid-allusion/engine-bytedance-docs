---
title: "DeleteSmsTemplate"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-deletesmstemplate_1"
---

Use the DeleteSmsTemplate OpenAPI to delete the specific template or template order

<span id="3fd47f9d"></span>
## Request

**HTTP method**: DELETE

**URL**: https://sms.byteplusapi.com/sms/openapi/sms_template

**Header parameters**


|**Parameter** |**Value** |**Description** |**Required** |
|---|---|---|---|
|Authorization |Basic base64 (username:password). For example: Basic NzQ2VIBlxxxxxXXXXXXXXXXXXXXGF6dDlZSG4xSml6Vjc3NzY= |Find the username and password information on the **Service Settings of Admin Settings** page in the SMS console |Yes |


**Request body parameters**


|**Parameter** |**Type** |**Required** |**Example of value** |**Description** |
|---|---|---|---|---|
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |
|id |string |Yes |169\*\*\* |The apply ID of the template. NOTE: not the template ID |
|isOrder |bool |Yes |true |Whether the template is under approval. |


**Example of request payload**

```JSON
{ 
    "subAccount":"7a76864c", 
    "id":"2092", 
    "isOrder":true
}
```


<span id="3084e4ef"></span>
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
|Result |string |The result in response.The result returns only when no error occurs. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240112071030C8A055F87A80690CCD26",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": "BOE"
    },
    "Result": ""
}
```


<span id="32445816"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Message** |**Description** |**Solution** |
|---|---|---|---|
|1999 |None |A system error occurs. |Contact the technical support team for help. |
|1005 |Status is not reviewing. |The template has been approved when you want to close the application ticket. |Contact the technical support team for help. |
|1006 |Not existed. |The ID of the template that you want to delete does not exist. |Double check your template's ID. |
|1001 |None |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
