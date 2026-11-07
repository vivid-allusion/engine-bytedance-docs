---
title: "ModifyBandwidthPackageEipBandwidth - Modifying independent bandwidth for an EIP"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/ModifyBandwidthPackageEipBandwidth"
---

Call the ModifyBandwidthPackageEipBandwidth API to configure dedicated bandwidth for an elastic IP address (EIP) within a Bandwidth Package. This sets an independent bandwidth cap for the EIP, limiting the maximum bandwidth it can consume from the Bandwidth Package.​

<span id=".5L2_55So6K-05piO"></span>
## Notes


* The EIP is already added to a Bandwidth Package.

* After the EIP is removed from the Bandwidth Package, the independent bandwidth configured for it within the package is removed.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBandwidthPackageEipBandwidth&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|WT60AQ">必选</span> `Example: ModifyBandwidthPackageEipBandwidth`

The action that you want to perform. Value: **ModifyBandwidthPackageEipBandwidth**.



**Version** <span data-label="purple"> String </span> <span data-api-tag="require|sBvpvI">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**AllocationId** <span data-label="purple"> String </span> <span data-api-tag="require|r_OWp6">必选</span> `Example: eip-2ze7ujxscd****`

The ID of the elastic IP address (EIP). You can call the [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) API to query the EIP ID.



**Bandwidth ** <span data-label="purple"> Integer </span><span data-api-tag="require|ni18XA">必选</span> `Example: 200`

The bandwidth cap that the EIP can consume from the Bandwidth Package.​

You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the bandwidth cap of the Bandwidth Package.

Value range: 1 \- Maximum bandwidth of Bandwidth Package.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyBandwidthPackageEipBandwidth&Version=2020-04-01&AllocationId=eip-2ze7ujxscd****&Bandwidth=200 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifyBandwidthPackageEipBandwidth",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed. |The specified bandwidth is invalid. |
|400 |InvalidBandwidthPackage.InvalidStatus |The specified bandwidth package is not in the correct status for the request. The specified bandwidth package is in freeze. |The specified Bandwidth Package is in a status that cannot respond to this request. The current Bandwidth Package is frozen. |
|400 |InvalidBwpStatus.NotSupport |The status of the specified bandwidth package does not support independent bandwidth. |The specified bandwidth package does not support enabling independent bandwidth due to its status. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being processed by another request. Try again later. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. The specified elastic ip is in freeze. |The specified EIP or Virtual Private Cloud (VPC) cannot respond to this request due to its status. The current EIP is frozen. |
|400 |InvalidEip.Malformed |The specified EIP is malformed.The specified EIP not exist in the bandwidth package. |The specified EIP is not associated with the specified Bandwidth Package. |
|400 |InvalidEip.NotSupport |IPv6 EIP does not support this operation. |IPv6 EIP does not support this action. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|403 |Forbidden |You are not authorized to perform operations on creating independent bandwidth EIP. |No permission to create an EIP with independent bandwidth. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
