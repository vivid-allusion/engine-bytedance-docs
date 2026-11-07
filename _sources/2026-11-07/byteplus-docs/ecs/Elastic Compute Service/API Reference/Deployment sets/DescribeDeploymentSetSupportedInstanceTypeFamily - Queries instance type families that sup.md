---
title: "DescribeDeploymentSetSupportedInstanceTypeFamily - Queries instance type families that support deployment sets"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSetSupportedInstanceTypeFamily"
---

Call the DescribeDeploymentSetSupportedInstanceTypeFamily operation to query the instance type families that support the deployment set feature.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

For more information about deployment sets, refer to [Deployment set overview](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeDeploymentSetSupportedInstanceTypeFamily&groupName=%E9%83%A8%E7%BD%B2%E9%9B%86&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|VVkUhD">必选</span> `Sample value: DescribeDeploymentSetSupportedInstanceTypeFamily`

The action that you want to perform. Value: DescribeDeploymentSetSupportedInstanceTypeFamily.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|34sLaZ">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DeploymentSetCreateInstanceTypeFamilies** <span data-label="purple">string[]</span> `Sample value: ["ecs.i2","ecs.g2i"]`

The instance type families that support creating instances by using the deployment set feature.



**DeploymentSetModifyInstanceTypeFamilies** <span data-label="purple">string[]</span> `Sample value: ["ecs.g2i","ecs.g1ie"]`

The instance type families that support modifying deployment sets.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeDeploymentSetSupportedInstanceTypeFamily&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"2021110417394001022514606307*****",
        "Action":"DescribeDeploymentSetSupportedInstanceTypeFamily",
        "Version":"2020-04-01",
        "Service":"ecs",
        "Region":"cn-beijing"
    },
    "Result":{
        "DeploymentSetCreateInstanceTypeFamilies":[
            "ecs.c1ie",
            "ecs.c2i",
            "ecs.c2a",
            "ecs.r1ie",
            "ecs.r2i",
            "ecs.r2a",
            "ecs.g1ie",
            "ecs.g2i",
            "ecs.g2a",
            "ecs.i2",
            "ecs.d2",
            "ecs.d1s",
            "ecs.hfg2",
            "ecs.hfc2",
            "ecs.hfr2",
            "ecs.ebmg2i",
            "ecs.ebmg2a",
            "ecs.ebmhfc2i",
            "ecs.ebmi2"
        ],
        "DeploymentSetModifyInstanceTypeFamilies":[
            "ecs.c1ie",
            "ecs.c2i",
            "ecs.c2a",
            "ecs.r1ie",
            "ecs.r2i",
            "ecs.r2a",
            "ecs.g1ie",
            "ecs.g2i",
            "ecs.g2a",
            "ecs.hfg2",
            "ecs.hfc2",
            "ecs.hfr2",
            "ecs.ebmg2i",
            "ecs.ebmg2a",
            "ecs.ebmhfc2i"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
