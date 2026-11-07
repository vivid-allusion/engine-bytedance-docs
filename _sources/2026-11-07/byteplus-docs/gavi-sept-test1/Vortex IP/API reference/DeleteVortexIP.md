---
title: "DeleteVortexIP"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/DeleteVortexIP"
---

Call the DeleteVortexIP interface to delete a Vortex IP instance.

<span id="rB4fGEDZ"></span>
## Instructions

Subscription Vortex IP instances can only be deleted after they are suspended due to expiration.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteVortexIP |The action that you want to perform. Value: DeleteVortexIP. |
|Version |String |Yes |2020\-04\-01 |API version. The current version is 2020\-04\-01. |
|VortexId |String |Yes |vt\-bp1o94dp5i6ea\*\*\*\* |ID of a Vortex IP.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) API to query the ID of the Vortex IP. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |Request ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=DeleteVortexIP&Version=2020-04-01&VortexId=vt-bp1o94dp5i6ea**** HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteVortexIP",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
    },
    "Result":{
         "RequestId": "2021062415303301022514515207C4****"
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/gavi-sept-test1/Public_error_codes).


|HttpCode |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidBillingType.Malformed |The specified BillingType is malformed. |The specified BillingType format is invalid. |
|400 |InvalidVortexIP.InvalidStatus |The specified VortexIP is not in the correct status for the request. |The specified Vortex IP cannot respond to this request due to its status. |
|404 |InvalidVortexIP.NotFound |The specified Vortex IP does not exist. |The specified Vortex IP does not exist. |
|412 |InvalidVortexIP.InvalidBillingType |The specified VortexIP is not in the correct BillingType for the request. |The specified Vortex IP cannot respond to this request due to its billing method.<br><br> |
