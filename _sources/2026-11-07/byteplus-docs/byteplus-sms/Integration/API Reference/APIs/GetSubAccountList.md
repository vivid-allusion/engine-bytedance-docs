---
title: "GetSubAccountList"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-getsubaccountlist"
---

Use the GetSubAccountList API to query the name, ID, and creation time of a message group. It's recommended you use SDK to call the GetSubAccountList API.

<span id="Request"></span>
## Request

**HTTP method**: GET

**URL**: `https://sms.byteplusapi.com?Action=GetSubAccountList&Version=2021-01-11`

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
|Action |string |Yes |GetSubAccountList |The name of this API. |
|Version |string |Yes |2021\-01\-11 |The version of this API. |
|subAccount |string |Yes |A123\*\*\*\* |The message group ID. |
|subAccountName |string |No |Test_message_group |The message group name. |
|pageIndex |int |No |1 |Set the page index of the list. The default number is 1. |
|pageSize |int |No |20 |Set the page size of the list. The default number is 1,000. |


**Request example**

`https://sms.byteplusapi.com?Action=GetSubAccountList&Version=2021-01-11&subAccountName=Test_message_group`

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
|Result |Result |The result in response. The result returns only when no error occurs. |
|Result.List |Array |The list of the name, ID, and creation time of a message group. |
|Result.List.subAccountName |string |Name of the message group. |
|Result.List.subAccountId |string |ID of the message group. |
|Result.List.createdTime |int64 |Time when the message group was created. |
|Error |Error |The error messages. For details, refer to the Error messages section. |
|Error.Code |string |The codes of error messages. |
|Error.Message |string |The description of the error messages. |


**Example of response payload**

```json
{
    "ResponseMetadata": {
        "RequestId": "a8e0788d-334e-49fc-92e8-61b7878c9735",
        "Action": "GetSubAccountList",
        "Version": "2021-01-11",
        "Service": "volcSMS",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "list":[
            {
                "subAccountName":"MKT_group_1",
                "subAccountId":"6e54b***",
                "createdTime":1649799715
            }
        ],
        "total":1
    }

```


<span id="Error messages"></span>
## Error messages

If you encounter error messages in response body, refer to the following table for details and solutions. For BytePlus common error codes, refer to [Common error codes](https://docs.byteplus.com/byteplus-platform/reference/common-error-codes).


|**Code** |**Description** |**Solution** |
|---|---|---|
|1999 |A system error occurs. |Contact technical support team for help. |
|1001 |Incorrect values for parameters. |Refer to the **Request** section and use the correct values for parameters. |
