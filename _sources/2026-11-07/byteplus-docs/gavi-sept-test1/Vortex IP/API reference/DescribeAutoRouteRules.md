---
title: "DescribeAutoRouteRules"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeAutoRouteRules"
---

Call the DescribeAutoRouteRules interface to query all supported intelligent routing domain names.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter Name |Type  |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes   |DescribeAutoRouteRules |The action that you want to perform. Value: DescribeAutoRouteRules. |
|Version |String |Yes   |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |
|AutoRouteRules |Array |["youtube"] |The intelligent routing domain name supported by VortexIP. |


<span id=".6K-35rGC56S65L6L"></span>
## Request Examples

```Plain Text
GET /?Action=DescribeAutoRouteRules&Version=2020-04-01 HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeAutoRouteRules",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "AutoRouteRules":
                   [
                   "youtube"
                     ]
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Codes

For more information on common error codes, refer to [Common Error Codes](https://docs.byteplus.com/en/docs/gavi-sept-test1/Public_error_codes).
