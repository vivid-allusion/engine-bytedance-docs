---
title: "DescribeImageSharePermission - Queries image sharing information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeImageSharePermission"
---

Call the DescribeImageSharePermission operation to query all accounts to whom a custom image is shared.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeImageSharePermission&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|bnFwyP">必选</span> `Sample value: DescribeImageSharePermission`

The action that you want to perform. Value: DescribeImageSharePermission.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|KdPMmL">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ImageId** <span data-label="purple">string</span> <span data-api-tag="require|TMtqJu">必选</span> `Sample value: image-ebgy1og99tfct0gw****`

The image ID. You can call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) operation and configure the `Visibility=private` parameter to query and obtain the ID of the custom image.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 15`

The number of entries per page.


* Default value: 15.

* Value range: 1 to 100.



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Accounts** <span data-label="purple">object[]</span> `Sample value: --`

The information of one or more accounts to which the image is shared.


**AccountId** <span data-label="purple">string</span> `Sample value: 210005****`

The account ID.




**ImageId** <span data-label="purple">string</span> `Sample value: image-4431h3l7hl31a0******`

The image ID.



**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The pagination token returned by this call. If this value is empty, the current page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeImageSharePermission&Version=2020-04-01&ImageId=image-ebgy1og99tfct0gw**** HTTP/1.1
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
        "Action": "DescribeImageSharePermission",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken":"bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******",
        "ImageId": "image-ebgy1og99tfct0gw****",
        "Accounts": [
            {
                "AccountId": "210005****"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|404 |InvalidImage.NotFound |The specified image does not exist. |The specified image does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
