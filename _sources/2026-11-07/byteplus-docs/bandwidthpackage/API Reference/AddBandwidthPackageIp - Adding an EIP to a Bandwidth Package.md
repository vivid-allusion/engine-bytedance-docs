---
title: "AddBandwidthPackageIp - Adding an EIP to a Bandwidth Package"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/AddBandwidthPackageIp"
---

Call the AddBandwidthPackageIp API to add an elastic IP address (EIP) or an IPv6 Internet bandwidth to a Bandwidth Package.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

To add an EIP or an IPv6 Internet bandwidth to a Bandwidth Package, the following conditions must be met:


* Both have the same ISP.

* Both have the same protection type.

* Both are in the same region.

* The billing method of the EIP or the IPv6 Internet bandwidth must be Pay\-as\-you\-go.


After you add the EIP or the IPv6 Internet bandwidth to a Bandwidth Package, its original maximum bandwidth becomes invalid, and it will share the total bandwidth of the Bandwidth Package. For billing changes, see [EIP/IPv6 Internet bandwidth billing changes](https://docs.byteplus.com/en/docs/bandwidthpackage/Billing-overview#.5YWs572RSVAvSVB2NuWFrOe9keW4puWuveS-p-iuoei0ueWPmOWMlg==).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddBandwidthPackageIp&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|6iqY31">必选</span> `Example: AddBandwidthPackageIp`

The action that you want to perform. Value: **AddBandwidthPackageIp**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|JUXsQW">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**BandwidthPackageId ** <span data-label="purple">String </span><span data-api-tag="require|clHR0V">必选</span> `Example: bwp-2zeo05qre24nhrqpy****`

The ID of the Bandwidth Package.

You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the Bandwidth Package ID.



**AllocationId ** <span data-label="purple">String </span><span data-api-tag="require|9PAaXi">必选</span> `Example: eip-sadase23123****`

The ID of the EIP or the IPv6 Internet bandwidth to be added to the Bandwidth Package instance.

You can call [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) or [DescribeIpv6AddressBandwidths](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6AddressBandwidths) to query the ID of the EIP or the IPv6 Internet bandwidth.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=AddBandwidthPackageIp&Version=2020-04-01&BandwidthPackageId=bwp-2zeo05qre24nhrqpy****&AllocationId=eip-sadase23123**** HTTP/1.1
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
        "Action": "AddBandwidthPackageIp",
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
|400 |InvalidBandwidthPackage.InvalidStatus |The specified bandwidth package is not in the correct status for the request. The specified bandwidth package is in freeze. |The specified Bandwidth Package is in a status that cannot respond to this request. The current Bandwidth Package is frozen. |
|400 |InvalidBillingType.Malformed |The specified billing type of EIP is malformed. |The specified billing method is invalid. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being processed by another request. Try again later. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. The specified elastic ip is in freeze. |The specified EIP or Virtual Private Cloud (VPC) cannot respond to this request due to its status. The current EIP is frozen. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. |The specified EIP is in a status that cannot respond to this request. |
|400 |InvalidIpv6.InUse |The specified IPv6 address bandwidth is being operated by another request. |The specified IPv6 Internet bandwidth is being processed by another request. Try again later. |
|400 |InvalidProtocol.Mismatch |The protocol of the bandwidth package does not match with the EIP. |The protocol type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the bandwidth package does not match with the EIP. |The specified egress of the Bandwidth Package does not match that of the EIP. |
|400 |MissingParameter |The request is missing a required parameter. |This request is missing a required parameter. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the EIP number of that you can add to bandwidth package. |You have reached the maximum of EIPs that you can add to a Bandwidth Package. |
|403 |Forbidden |You are not authorized to perform operations on the specified EIP. The specified EIP is a service\-managed EIP. |No permission to manage the specified EIP. The specified EIP is managed by cloud products. |
|403 |Forbidden |You are not authorized to perform operations on the specified bandwidth package. Because of SecurityProtectionTypesInconsistent. |No permission to perform actions on the specified Bandwidth Package. The protection type of the specified EIP is inconsistent with that of the Bandwidth Package. |
|403 |Forbidden |You are not authorized to perform operations on the specified bandwidth package. The ISP of EIP and bandwidth package is not same. |The ISP of EIP is inconsistent with that of the Bandwidth Package. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|409 |InvalidEip.Conflict |The specified EIP conflicts with that of another EIP in your bandwidth package. |The specified EIP is already added to a Bandwidth Package. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
