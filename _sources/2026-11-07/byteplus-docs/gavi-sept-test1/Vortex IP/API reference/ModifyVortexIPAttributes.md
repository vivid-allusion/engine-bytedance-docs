---
title: "ModifyVortexIPAttributes"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/ModifyVortexIPAttributes"
---

Call ModifyVortexIPAttributes to modify the name, description, password, and maximum bandwidth for a Vortex IP.

<span id="sb4ct8ND"></span>
## **Instructions**


* If you do not configure the following optional parameters, their current values remain unchanged.

* Subscription Vortex IP instances do not support modifying maximum bandwidth.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |ModifyVortexIPAttributes |The action that you want to perform. Value: ModifyVortexIPAttributes. |
|Version |String |Yes |2020\-04\-01 |API version. The current version is 2020\-04\-01. |
|VortexId |String |Yes |vt\-bp1o94dp5i6ea\*\*\*\* |ID of a Vortex IP.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) API to query the ID of the Vortex IP. |
|VortexName |String |No |VortexIP\-1 |Name of the Vortex IP instance.<br><br><br>* Must be 1 to 128 characters.<br><br>* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-). |
|AutoRouteRules.N |String |No |AutoRouteRules.1=youtube |Domain name of the Vortex IP smart routing.<br><br>You can call the [DescribeAutoRouteRules](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeAutoRouteRules) API to query the collection of domains that support smart routing.<br><br><br>* N represents the sequence number of a smart route. Currently, only one valid value (1). |
|Bandwidth |Integer |No |10 |Maximum bandwidth of Vortex IP. Unit: Mbps. Valid range: 20 to 2000. |
|Description |String |No |This is a VortexIP |Description of Vortex IP.<br><br><br>* Must be 0 to 255 characters.<br><br>* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。). |
|Password |String |No |K29e!s0#57@%<br><br> |Authentication password of Vortex IP.<br><br><br>* Must be 12 to 30 characters.<br><br>* Must not start with “/” or “$6$”. Must include at least three of the following four elements:<br><br>   * Uppercase letters (A\-Z);<br><br>   * Lowercase letters (a\-z);<br><br>   * Numbers (0\-9);<br><br>   * Symbols. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |Request ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=ModifyVortexIPAttributes&Version=2020-04-01&VortexId=vt-bp1o94dp5i6ea****&VortexName=VortexIP-1 HTTP/1.1
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
        "Action": "ModifyVortexIPAttributes",
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
|400 |InvalidAutoRouteRule.Conflict |The auto route rules are duplicate. |The specified AutoRouteRules is duplicated. |
|400 |InvalidBandwidth.Malformed |The specified Bandwidth is malformed. |The format of specified Bandwidth is invalid. |
|400 |InvalidBillingType.Malformed |The specified BillingType is malformed. |The specified BillingType format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format of specified Description is invalid. |
|400 |InvalidPassword.Malformed |The specified Password is malformed. |The specified Password format is invalid. |
|400 |InvalidVortexIP.InvalidStatus |The specified VortexIP is not in the correct status for the request. |The specified Vortex IP cannot respond to this request due to its status. |
|400 |InvalidVortexIP.UnSupportAction |The specified VortexIP does not support the operation. |The specified VortexIP does not support the current operation. |
|400 |InvalidVortexName.Malformed |The specified VortexName is malformed. |The format of specified VortexName is invalid. |
|404 |InvalidVortexIP.NotFound |The specified Vortex IP does not exist. |The specified Vortex IP does not exist. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
