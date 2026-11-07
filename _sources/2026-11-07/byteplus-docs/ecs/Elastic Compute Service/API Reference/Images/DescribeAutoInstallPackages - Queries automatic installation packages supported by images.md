---
title: "DescribeAutoInstallPackages - Queries automatic installation packages supported by images and instance type families"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeAutoInstallPackages"
---

Call the DescribeAutoInstallPackages API to query the automatic installation packages supported for the specified image and instance type family.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeAutoInstallPackages&groupName=%E9%95%9C%E5%83%8F&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|dIKLU6">必选</span> `Sample value: DescribeAutoInstallPackages`

The action that you want to perform. Value: DescribeAutoInstallPackages.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|QgT44K">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ImageId** <span data-label="purple">string</span> <span data-api-tag="require|HEm2S2">必选</span> `Sample value: image-3tksv4n6ay3vj0*****`

The image ID. To obtain it, call the [DescribeImages](https://docs.byteplus.com/en/docs/ecs/DescribeImages) API.



**InstanceTypeFamily** <span data-label="purple">string</span> <span data-api-tag="require|lvunRb">必选</span> `Sample value: ecs.g3i`

The instance type family.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Packages** <span data-label="purple">object[]</span> `Sample value: --`

The automatic installation packages supported by images.


**Items** <span data-label="purple">object[]</span> `Sample value: --`

The information about the automatic installation package.


**Bin** <span data-label="purple">string</span> `Sample value: CUDA`

The name of the automatic installation package.



**Version** <span data-label="purple">string</span> `Sample value: 11.4.1`

The version of the automatic installation package.




**PackgeId** <span data-label="purple">string</span> `Sample value: pkg-3tksv4n*****`

The ID of the automatic installation package.



**ScriptId** <span data-label="purple">string</span> `Sample value: script-3tksv4n*****`

The ID of the automatic installation script.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeAutoInstallPackages&Version=2020-04-01&ImageId=image-3tksv4n6ay3vj0***** HTTP/1.1
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
        "Action": "DescribeAutoInstallPackages",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "Packages": [
            {
              "Items": [
                {
                  "Bin": "CUDA",
                  "Version": "11.4.1"
                }
              ],
              "PackgeId": "pkg-3tksv4n*****",
              "ScriptId": "script-3tksv4n*****"
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
|400 |MissingParameter.ImageId |The required parameter ImageId is not supplied. |The image ID cannot be empty. |
|400 |MissingParameter.InstanceTypeFamily |The required parameter InstanceTypeFamily is not supplied. |The InstanceTypeFamily parameter cannot be left empty. |
