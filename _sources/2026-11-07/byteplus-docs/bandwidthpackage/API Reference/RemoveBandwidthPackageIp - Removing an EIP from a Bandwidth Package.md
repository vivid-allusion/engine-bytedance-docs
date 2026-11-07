---
title: "RemoveBandwidthPackageIp - Removing an EIP from a Bandwidth Package"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/RemoveBandwidthPackageIp"
---

Call the RemoveBandwidthPackageIp API to remove an elastic IP address (EIP) or an IPv6 Internet bandwidth from a Bandwidth Package.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The EIP's original maximum bandwidth is restored.

* The EIP's original metering method is restored, and billing starts immediately.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When an EIP that was originally applied for via the Bandwidth Package console is removed from the package, it defaults to <a href="https://docs.byteplus.com/en/docs/eip/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5">Pay\-by\-data\-transfer</a> metering with a bandwidth cap of 100 Mbps.​</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RemoveBandwidthPackageIp&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|niuvB6">必选</span> `Example: RemoveBandwidthPackageIp`

The action that you want to perform. Value: **RemoveBandwidthPackageIp**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|klcPgv">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**BandwidthPackageId ** <span data-label="purple">String </span><span data-api-tag="require|FlTffL">必选</span> `Example: bwp-2zeo05qre24nhrqpy****`

ID of the Bandwidth Package.

You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the Bandwidth Package ID.



**AllocationId** <span data-label="purple">String</span> <span data-api-tag="require|x5JT3Z">必选</span> `Example: eip-sadase23123****`

ID of the EIP or IPv6 Internet bandwidth to be removed from the Bandwidth Package.

You can call [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) or [DescribeIpv6AddressBandwidths](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6AddressBandwidths) to query the ID of the EIP or the IPv6 Internet bandwidth.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=RemoveBandwidthPackageIp&Version=2020-04-01&BandwidthPackageId=bwp-2zeo05qre24nhrqpy****&AllocationId=eip-sadase23123**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "RemoveBandwidthPackageIp",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being processed by another request. Try again later. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. |The specified EIP is in a status that cannot respond to this request. |
|400 |InvalidEip.Malformed |The specified EIP is malformed.The specified EIP not exist in the bandwidth package. |The specified EIP is not associated with the specified Bandwidth Package. |
|400 |InvalidIpv6.InUse |The specified IPv6 address bandwidth is being operated by another request. |The specified IPv6 Internet bandwidth is being operated by another request. Please try again later. |
|400 |MissingParameter |The request is missing a required parameter. |This request is missing a required parameter. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the EIP number of that you can add to bandwidth package. |You have reached the maximum of EIPs that you can add to a Bandwidth Package. |
|403 |Forbidden |You are not authorized to perform operations on the specified EIP. The specified EIP is a service\-managed EIP. |No permission to manage the specified EIP. The specified EIP is managed by cloud products. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
