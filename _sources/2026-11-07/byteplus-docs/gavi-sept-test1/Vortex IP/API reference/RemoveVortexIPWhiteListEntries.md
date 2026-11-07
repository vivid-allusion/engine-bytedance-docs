---
title: "RemoveVortexIPWhiteListEntries"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/RemoveVortexIPWhiteListEntries"
---

Call the RemoveVortexIPWhiteListEntries interface to delete internet mode VortexIP allowlist entries.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter Name |Type  |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes   |DescribeAutoRouteRules |The action that you want to perform. Value: DescribeAutoRouteRules. |
|Version |String |Yes   |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|VortexId |String |Yes   |vt\-bp1o94dp5i6ea\*\*\*\* |Vortex IP's ID.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) interface to query the Vortex IP's ID. |
|WhiteListEntries.N |String |Yes   |WhiteListEntries.1=10.XX.XX.0/24&WhiteListEntries.2=10.XX.XX.0/24 |The source CIDR block of the allowlist entries, only CIDR addresses are supported.<br><br><br>* Argument \- N: indicates the serial number of the allowlist entry, with a value range of 1～20.<br><br>* Only supports passing in IPv4 entries.<br><br>* Separate IP entries with ampersands ( & ). |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |


<span id=".6K-35rGC56S65L6L"></span>
## Request Examples

```Plain Text
GET /?Action=RemoveVortexIPWhiteListEntries&Version=2020-04-01&VortexId=vt-bp1o94dp5i6ea****&WhiteListEntries.1=10.XX.XX.0/24&WhiteListEntries.2=10.XX.XX.0/24 HTTP/1.1
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
        "Action": "RemoveVortexIPWhiteListEntries",
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
## Error Codes


|HttpCode |Error codes |Error Message |Description |
|---|---|---|---|
|400 |InvalidCIDR.Malformed |The specified CIDR is malformed. |The format of the specified CIDR is invalid. |
||InvalidCidr.Conflict |The specified Cidr are repeated. |The specified Cidr is duplicate. |
||InvalidVortexIP.InvalidAccessType |The specified VortexIP AccessType does not support the operation. |The specified VortexIP access type cannot fulfill this request. |
||InvalidVortexIP.InvalidStatus |The specified VortexIP is not in the correct status for the request. |The specified VortexIP is in a status that cannot respond to the request. |
||LimitExceeded.WhiteListEntryNumber |You've reached the limit on the number of WhiteListEntries that you can operate. |The resource limit for actions has been reached. |
||MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'WhiteListEntries'. |A required parameter is missing in the request. Please ensure all necessary arguments, such as WhiteListEntries, are provided when initiating the request. |
|404 |InvalidCidr.NotFound |The specified Cidr does not exist. |The specified Cidr does not exist. |
||InvalidVortexIP.NotFound |The specified VortexIP does not exist. |The specified VortexIP does not exist. |
