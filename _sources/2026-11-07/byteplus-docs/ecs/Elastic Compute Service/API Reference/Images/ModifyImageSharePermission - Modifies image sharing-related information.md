---
title: "ModifyImageSharePermission - Modifies image sharing-related information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyImageSharePermission"
---

Call the ModifyImageSharePermission operation to manage permissions for image sharing.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

For prerequisites and precautions for calling this operation, refer to [Precautions](https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image#.5rOo5oSP5LqL6aG5).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyImageSharePermission&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|DiYAWF">必选</span> `Sample value: ModifyImageSharePermission`

The action that you want to perform. Value: ModifyImageSharePermission.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|PZVtEm">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**AddAccounts.N** <span data-label="purple">string[]</span> `Optional` `Sample value: AddAccounts.1=210005****&AddAccounts.2=210007****`

The accounts with which you want to share the image. Up to 50 accounts are supported.


* Parameter \- N: specifies the sequence number of the account.

* Separate accounts with `&`.



**ImageId** <span data-label="purple">string</span> <span data-api-tag="require|U05bRt">必选</span> `Sample value: image-ebgy1og99tfct0gw****`

The image ID. You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and configure the `Visibility=private` parameter to query and obtain the ID of the custom image.



**RemoveAccounts.N** <span data-label="purple">string[]</span> `Optional` `Sample value: RemoveAccounts.1=210000****&RemoveAccounts.2=210000****`

Removes the accounts with which the image is shared.


* Parameter \- N: specifies the sequence number of the account.

* Separate accounts with `&`.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyImageSharePermission&Version=2020-04-01&ImageId=image-ebgy1og99tfct0gw****&AddAccounts.1=210005**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "ModifyImageSharePermission",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidAccount.Malformed |The specified Account is malformed. |The specified account is invalid. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidImageSharePermissionForRemove.UnSupported |The specified image share permission cannot be used for remove. |The specified image sharing relationship cannot be deleted. Please remove it on the Resource Sharing platform. |
|400 |InvalidImageStatus |The specified image is not in the correct status for the request. |The current status of the image does not support this operation. |
|400 |LimitExceeded.MaximumShareImageAccount |You've reached the limit on the number of account that you can share. |The number of accounts with which the image is shared exceeds the limit. |
|400 |MissingParameter.AddAccountsAndRemoveAccounts |The required parameter AddAccountsAndRemoveAccounts is not supplied. |Neither of the parameters AddAccounts nor RemoveAccounts is provided. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
