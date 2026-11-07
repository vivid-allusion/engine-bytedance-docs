---
title: "AddVortexIPWhiteListEntries"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/AddVortexIPWhiteListEntries"
---

Invoke AddVortexIPWhiteListEntries Interface to add internet mode VortexIP allowlist entries.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter Name |Type  |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes   |DescribeAutoRouteRules |The action that you want to perform. Value: DescribeAutoRouteRules. |
|Version |String |Yes   |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|VortexId |String |Yes   |vt\-bp1o94dp5i6ea\*\*\*\* |The ID of the Vortex IP.<br><br>You can call the [DescribeVortexIPs](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeVortexIPs) interface to query the ID of Vortex IP. |
|WhiteListEntries.N.Cidr |String |Yes   |WhiteListEntries.1.Cidr=10.XX.XX.0/24&WhiteListEntries.2.Cidr=10.XX.XX.0/24 |The source address CIDR block for the allowlist entry; only CIDR addresses are supported.<br><br><br>* Argument \- N: represents the serial number of the allowlist entry, with a value range of 1～20.<br><br>* Only supports passing in IPv4 entries.<br><br>* Separate IP entries with ampersands ( & ). |
|WhiteListEntries.N.Description |String |No  |WhiteListEntries.1.Description=This is WhiteListEntries01.&WhiteListEntries.2.Description=This is WhiteListEntries02. |The Description of the allowlist entry.<br><br><br>* Argument \- N: Represents the sequence number of the allowlist entry, value range: 1–20.<br><br>* Separate IP entries with ampersands ( & ). |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |


<span id=".6K-35rGC56S65L6L"></span>
## Request Examples

```Plain Text
GET /?Action=AddVortexIPWhiteListEntries&Version=2020-04-01&VortexId=vt-bp1o94dp5i6ea****&WhiteListEntries.1.Cidr=10.XX.XX.0/24&WhiteListEntries.2.Cidr=10.XX.XX.0/24 HTTP/1.1
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
        "Action": "AddVortexIPWhiteListEntries",
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


|HttpCode |Error codes |Error Message |Description |
|---|---|---|---|
|400 |InvalidCIDR.Malformed |The specified CIDR is malformed. |The format of the specified CIDR is invalid. |
||InvalidCidr.Conflict |The specified Cidr are repeated. |The specified Cidr are repeated. |
||InvalidCidr.Conflict |The specified Cidr already exists. |The specified Cidr already exists. |
||InvalidDescription.Malformed |The specified Description is malformed. |The format of the specified Description is invalid. |
||InvalidVortexIP.InvalidAccessType |The specified VortexIP AccessType does not support the operation. |The specified VortexIP access type cannot respond to this request. |
||InvalidVortexIP.InvalidStatus |The specified VortexIP is not in the correct status for the request. |The specified VortexIP status cannot respond to the request. |
||LimitExceeded.WhiteListEntryNumber |You've reached the limit on the number of WhiteListEntries that you can operate. |You have reached the maximum number of operable resources. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have the permission to perform operations on the specified service. |
|404 |InvalidVortexIP.NotFound |The specified VortexIP does not exist. |The specified VortexIP does not exist. |
